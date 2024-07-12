---
title: Skicka adaptiva blanketter till databasen med Forms Portal
description: Utöka standardmetamodellen för att lägga till mönster, valideringar och enheter som är specifika för din organisation och tillämpa konfigurationer på anpassningsbara formulärfält när du kör tjänsten Automated forms conversion (AFCS).
uuid: f98b4cca-f0a3-4db8-aef2-39b8ae462628
topic-tags: forms
discoiquuid: cad72699-4a4b-4c52-88a5-217298490a7c
source-git-commit: c2392932d1e29876f7a11bd856e770b8f7ce3181
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 0%

---


# Integrera adaptiva blanketter med databaser med Forms Portal {#submit-forms-to-database-using-forms-portal}

Med tjänsten Automated forms conversion (AFCS) kan du konvertera ett icke-interaktivt PDF-formulär, ett Acro-formulär eller ett XFA-baserat PDF-formulär till en adaptiv form. När du startar konverteringsprocessen kan du generera ett anpassat formulär antingen med eller utan databindningar.

Om du väljer att generera ett adaptivt formulär utan databindningar kan du integrera det konverterade adaptiva formuläret med en formulärdatamodell, ett XML-schema eller ett JSON-schema efter konverteringen. Men om du genererar ett adaptivt formulär med databindningar associerar konverteringstjänsten automatiskt de adaptiva formulären med ett JSON-schema och skapar en databindning mellan fälten som finns i det adaptiva formuläret och JSON-schemat. Sedan kan du integrera det anpassade formuläret med en valfri databas, fylla i data i formuläret och skicka det till databasen med hjälp av Forms Portal.

Följande bild visar olika steg i integreringen av ett konverterat adaptivt formulär i en databas med hjälp av Forms Portal:

![databasintegrering](assets/database_integration.gif)

I den här artikeln beskrivs de stegvisa instruktionerna för att köra alla dessa integrationssteg.

Exemplet, som behandlas i den här artikeln, är en referensimplementering av anpassade data- och metadatatjänster för att integrera en Forms Portal-sida med en databas. Databasen som används i exempelimplementeringen är MySQL 5.6.24. Du kan emellertid integrera Forms Portal-sidor med valfri databas.

## Krav {#pre-requisites}

* Konfigurera en AEM 6.4- eller 6.5-författarinstans
* Installera [senaste Service Pack](https://helpx.adobe.com/experience-manager/aem-releases-updates.html) för din AEM
* Senaste versionen av AEM Forms-tilläggspaketet
* Konfigurera tjänsten [Automated forms conversion (AFCS)](configure-service.md)
* Konfigurera en databas. Databasen som används i exempelimplementeringen är MySQL 5.6.24. Du kan emellertid integrera det konverterade adaptiva formuläret med valfri databas.

## Konfigurera anslutning mellan AEM och databas {#set-up-connection-aem-instance-database}

En anslutning mellan en AEM och en MYSQL-databas skapas:

* [Installera ett MYSQL-kopplingspaket](#install-mysql-connector-java-file)

* [Skapa schema och tabeller i databasen](#create-schema-and-tables-in-database)

* [Konfigurerar anslutningsinställningar](#configure-connection-between-aem-instance-and-database)

* [Konfigurera och konfigurera exempelpaketet för integrering med Forms Portal](#set-up-and-configure-sample)

### Installera filen mysql-connector-java-5.1.39-bin.jar {#install-mysql-connector-java-file}

Utför följande steg på alla författare- och publiceringsinstanser för att installera filen mysql-connector-java-5.1.39-bin.jar:

1. Gå till http://[server]:[port]/system/console/depfinder och sök efter paketet com.mysql.jdbc.
1. I kolumnen Exporterad av kontrollerar du om paketet exporteras av något paket. Fortsätt om paketet inte exporteras av något paket.
1. Gå till http://[server]:[port]/system/console/bundles och klicka på **[!UICONTROL Install/Update]**.
1. Klicka på **[!UICONTROL Choose File]** och bläddra till filen mysql-connector-java-5.1.39-bin.jar. Markera även kryssrutorna **[!UICONTROL Start Bundle]** och **[!UICONTROL Refresh Packages]**.
1. Klicka på **[!UICONTROL Install]** eller **[!UICONTROL Update]**. Starta om servern när du är klar.
1. (Endast Windows) Stäng av operativsystemets brandvägg.

### Skapa schema och tabeller i databasen {#create-schema-and-tables-in-database}

Utför följande steg för att skapa schema och tabeller i databasen:

1. Skapa ett schema i databasen med följande SQL-sats:

   ```sql
   CREATE SCHEMA `formsportal` ;
   ```

   där **formsportal** refererar till schemats namn.

1. Skapa en **data**-tabell i databasschemat med följande SQL-sats:

   ```sql
    CREATE TABLE `data` (
        `owner` varchar(255) DEFAULT NULL,
        `data` longblob,
        `metadataId` varchar(45) DEFAULT NULL,
        `id` varchar(45) NOT NULL,
        PRIMARY KEY (`id`)
        ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

1. Skapa en **metadata**-tabell i databasschemat med följande SQL-sats:

   ```sql
   CREATE TABLE `metadata` (
       `formPath` varchar(1000) DEFAULT NULL,
       `formType` varchar(100) DEFAULT NULL,
       `description` text,
       `formName` varchar(255) DEFAULT NULL,
       `owner` varchar(255) DEFAULT NULL,
       `enableAnonymousSave` varchar(45) DEFAULT NULL,
       `renderPath` varchar(1000) DEFAULT NULL,
       `nodeType` varchar(45) DEFAULT NULL,
       `charset` varchar(45) DEFAULT NULL,
       `userdataID` varchar(45) DEFAULT NULL,
       `status` varchar(45) DEFAULT NULL,
       `formmodel` varchar(45) DEFAULT NULL,
       `markedForDeletion` varchar(45) DEFAULT NULL,
       `showDorClass` varchar(255) DEFAULT NULL,
       `sling:resourceType` varchar(1000) DEFAULT NULL,
       `attachmentList` longtext,
       `draftID` varchar(45) DEFAULT NULL,
       `submitID` varchar(45) DEFAULT NULL,
       `id` varchar(60) NOT NULL,
       `profile` varchar(255) DEFAULT NULL,
       `submitUrl` varchar(1000) DEFAULT NULL,
       `xdpRef` varchar(1000) DEFAULT NULL,
       `agreementId` varchar(255) DEFAULT NULL,
       `nextSigners` varchar(255) DEFAULT NULL,
       `eSignStatus` varchar(45) DEFAULT NULL,
       `pendingSignID` varchar(45) DEFAULT NULL,
       `agreementDataId` varchar(255) DEFAULT NULL,
       `enablePortalSubmit` varchar(45) DEFAULT NULL,
       `submitType` varchar(45) DEFAULT NULL,
       `dataType` varchar(45) DEFAULT NULL,
       `jcr:lastModified` varchar(45) DEFAULT NULL,
       PRIMARY KEY (`id`),
       UNIQUE KEY `ID_UNIQUE` (`id`)
       ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

1. Skapa en **ytterligare metadatatabell** i databasschemat med följande SQL-sats:

   ```sql
   CREATE TABLE `additionalmetadatatable` (
       `value` text,
       `key` varchar(255) NOT NULL,
       `id` varchar(60) NOT NULL,
       PRIMARY KEY (`id`,`key`),
       CONSTRAINT ‘additionalmetadatatable_fk’ FOREIGN KEY (`id`) REFERENCES `metadata` (`id`) ON DELETE CASCADE
       ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

1. Skapa en **kommentarbar**-tabell i databasschemat med följande SQL-sats:

   ```sql
   CREATE TABLE `commenttable` (
       `commentId` varchar(255) DEFAULT NULL,
       `comment` text DEFAULT NULL,
       `ID` varchar(255) DEFAULT NULL,
       `commentowner` varchar(255) DEFAULT NULL,
       `time` varchar(255) DEFAULT NULL);
   ```

### Konfigurera anslutning mellan AEM och databas {#configure-connection-between-aem-instance-and-database}

Utför följande konfigurationssteg för att skapa en anslutning mellan AEM och MYSQL-databasen:

1. Gå till AEM webbkonsolkonfigurationssida på *http://[host]:[port]/system/console/configMgr*.
1. Klicka för att öppna **[!UICONTROL Forms Portal Draft and Submission Configuration]** i redigeringsläge.
1. Ange värdena för egenskaperna enligt följande tabell:

   <table> 
    <tbody> 
    <tr> 
    <th><strong>Egenskap</strong></th> 
    <th><strong>Beskrivning</strong></th>
    <th><strong>Värde</strong></th> 
    </tr> 
    <tr> 
    <td><p>Forms Portal Draft Data Service</p></td> 
    <td><p>Identifierare för datatjänsten för utkast</p></td>
    <td><p>formsportal.sampledataservice</p></td> 
    </tr>
    <tr> 
    <td><p>Forms Portal Draft Metadata Service</p></td> 
    <td><p>Identifierare för metadatatjänsten för utkast</p></td>
    <td><p>formsportal.samplemetadataservice</p></td> 
    </tr>
    <tr> 
    <td><p>Forms Portal Submit Data Service</p></td> 
    <td><p>Identifierare för Skicka datatjänst</p></td>
    <td><p>formsportal.sampledataservice</p></td> 
    </tr>
    <tr> 
    <td><p>Forms Portal Submit Metadata Service</p></td> 
    <td><p>Identifierare för tjänsten Skicka metadata</p></td>
    <td><p>formsportal.samplemetadataservice</p></td> 
    </tr>
    <tr> 
    <td><p>Datatjänst för Forms Portal som väntar på signering</p></td> 
    <td><p>Identifierare för datatjänsten för väntande signering</p></td>
    <td><p>formsportal.sampledataservice</p></td> 
    </tr>
    <tr> 
    <td><p>Metadatatjänst för Forms Portal som väntar på signering</p></td> 
    <td><p>Identifierare för metadatatjänsten för väntande signering</p></td>
    <td><p>formsportal.samplemetadataservice</p></td> 
    </tr>
    </tbody> 
    </table>
1. Låt andra konfigurationer vara som de är och klicka på **[!UICONTROL Save]**.
1. Sök och klicka för att öppna **[!UICONTROL Apache Sling Connection Pooled DataSource]** i redigeringsläge i webbkonsolkonfigurationen. Ange värdena för egenskaperna enligt följande tabell:

   <table> 
    <tbody> 
    <tr> 
    <th><strong>Egenskap</strong></th> 
    <th><strong>Värde</strong></th> 
    </tr> 
    <tr> 
    <td><p>Datakällans namn</p></td> 
    <td><p>Ett datakällnamn för filtrering av drivrutiner från datakällpoolen. I exempelimplementeringen används FormsPortal som datakällnamn.</p></td>
    </tr>
    <tr> 
    <td><p>JDBC-drivrutinsklass</p></td> 
    <td><p>com.mysql.jdbc.Driver</p></td>
    </tr>
    <tr> 
    <td><p>URI för JDBC-anslutning</p></td> 
    <td><p>jdbc:mysql://[värd]:[port]/[schemanamn]</p></td>
    </tr>
    <tr> 
    <td><p>Användarnamn</p></td> 
    <td><p>Ett användarnamn för att autentisera och utföra åtgärder på databastabeller</p></td>
    </tr>
    <tr> 
    <td><p>Lösenord</p></td> 
    <td><p>Lösenord som är kopplat till användarnamnet</p></td>
    </tr>
    <tr> 
    <td><p>Transaktionsisolering</p></td> 
    <td><p>READ_COMMTED</p></td>
    </tr>
    <tr> 
    <td><p>Maximalt antal aktiva anslutningar</p></td> 
    <td><p>1000</p></td>
    </tr>
    <tr> 
    <td><p>Maximalt antal inaktiva anslutningar</p></td> 
    <td><p>100</p></td>
    </tr>
    <tr> 
    <td><p>Minsta antal inaktiva anslutningar</p></td> 
    <td><p>10</p></td>
    </tr>
    <tr> 
    <td><p>Inledande storlek</p></td> 
    <td><p>10</p></td>
    </tr>
    <tr> 
    <td><p>Max. väntan</p></td> 
    <td><p>100000</p></td>
    </tr>
     <tr> 
    <td><p>Testa om Borgen</p></td> 
    <td><p>Markerad</p></td>
    </tr>
     <tr> 
    <td><p>Testa vid inaktivitet</p></td> 
    <td><p>Markerad</p></td>
    </tr>
     <tr> 
    <td><p>Valideringsfråga</p></td> 
    <td><p>Exempelvärden är SELECT 1(mysql), välj 1 från dual(oracle), SELECT 1(MS Sql Server) (validationQuery)</p></td>
    </tr>
     <tr> 
    <td><p>Timeout för verifieringsfråga</p></td> 
    <td><p>10000</p></td>
    </tr>
    </tbody> 
    </table>

### Konfigurera och konfigurera exemplet {#set-up-and-configure-sample}

Utför följande steg på alla författare- och publiceringsinstanser för att installera och konfigurera exemplet:

1. Hämta följande **aem-fp-db-integration-sample-pkg-6.1.2.zip** -paket till filsystemet.

[Hämta fil](assets/aem-fp-db-integration-sample-pkg-6.1.2.zip)

1. Gå till AEM på *http://[host]:[port]/crx/packmgr/*.
1. Klicka på **[!UICONTROL Upload Package]**.
1. Bläddra till paketet **aem-fp-db-integration-sample-pkg-6.1.2.zip** och klicka på **[!UICONTROL OK]**.
1. Klicka på **[!UICONTROL Install]** bredvid paketet för att installera paketet.

## Konfigurera det konverterade adaptiva formuläret för integrering med Forms Portal {#configure-converted-adaptive-form-for-forms-portal-integration}

Utför följande steg för att aktivera adaptiv formulärinlämning på Forms Portal-sidan:
1. [Kör konverteringen](convert-existing-forms-to-adaptive-forms.md#start-the-conversion-process) för att konvertera ett källformulär till ett anpassat formulär.
1. Öppna det adaptiva formuläret i redigeringsläge.
1. Tryck på formulärbehållaren och välj Konfigurera ![Anpassa formulär](assets/configure-adaptive-form.png).
1. I avsnittet **[!UICONTROL Submission]** väljer du **[!UICONTROL Forms Portal Submit Action]** i listrutan **[!UICONTROL Submit Action]**.
1. Tryck på ![Spara mallprincip](assets/edit_template_done.png) för att spara inställningarna.

## Skapa och konfigurera Forms Portal-sidan {#create-configure-forms-portal-page}

Så här skapar du en Forms Portal-sida och konfigurerar den så att du kan skicka adaptiva formulär på den här sidan:

1. Logga in på AEM författarinstans och tryck på **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Sites]**.
1. Välj den plats där du vill spara den nya Forms Portal-sidan och tryck på **[!UICONTROL Create]** > **[!UICONTROL Page]**.
1. Välj sidans mall, tryck på **[!UICONTROL Next]**, ange en rubrik för sidan och tryck på **[!UICONTROL Create]**.
1. Tryck på **[!UICONTROL Edit]** för att konfigurera sidan.
1. I sidhuvudet trycker du på ![Redigera mall](assets/edit_template_sites.png) > **[!UICONTROL Edit Template]** för att öppna sidans mall.
1. Tryck på Layoutbehållare och tryck på ![Redigera mallprincip](assets/edit_template_policy.png). Aktivera alternativen **[!UICONTROL Document Services]** och **[!UICONTROL Document Services Predicates]** på fliken **[!UICONTROL Allowed Components]** och tryck sedan på ![Spara mallprofil](assets/edit_template_done.png).
1. Infoga komponenten **[!UICONTROL Search & Lister]** på sidan. Därför listas alla befintliga adaptiva formulär som finns i AEM på sidan.
1. Infoga komponenten **[!UICONTROL Drafts & Submissions]** på sidan. Två flikar, **[!UICONTROL Draft Forms]** och **[!UICONTROL Submitted Forms]**, visas på Forms Portal-sidan. På fliken **[!UICONTROL Draft Forms]** visas även det konverterade adaptiva formuläret som genererats med stegen som beskrivs i [Konfigurera det konverterade adaptiva formuläret för integrering med Forms Portal](#configure-converted-adaptive-form-for-forms-portal-integration)

1. Tryck på **[!UICONTROL Preview]**, tryck på det konverterade adaptiva formuläret, ange värden för adaptiva formulärfält och skicka det. De värden som du anger för adaptiva formulärfält skickas till den integrerade databasen.
