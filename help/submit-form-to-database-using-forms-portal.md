---
title: Skicka adaptiva formulär till databasen med Forms Portal
description: Utöka standardmetamodellen för att lägga till mönster, valideringar och enheter som är specifika för din organisation och tillämpa konfigurationer på anpassningsbara formulärfält samtidigt som tjänsten Automated Forms Conversion körs.
uuid: f98b4cca-f0a3-4db8-aef2-39b8ae462628
topic-tags: forms
discoiquuid: cad72699-4a4b-4c52-88a5-217298490a7c
translation-type: tm+mt
source-git-commit: 040b0ddb489b5bdfd640a93b22cd7bc512a39aea

---


# Integrera adaptiva blanketter med databaser med Forms Portal {#submit-forms-to-database-using-forms-portal}

Med tjänsten Automated Forms Conversion kan du konvertera ett icke-interaktivt PDF-formulär, ett Acro-formulär eller ett XFA-baserat PDF-formulär till ett adaptivt formulär. När du startar konverteringsprocessen kan du generera ett anpassat formulär antingen med eller utan databindningar.

Om du väljer att generera ett adaptivt formulär utan databindningar kan du integrera det konverterade adaptiva formuläret med en formulärdatamodell, ett XML-schema eller ett JSON-schema efter konverteringen. Men om du genererar ett adaptivt formulär med databindningar associerar konverteringstjänsten automatiskt adaptiva formulär med ett JSON-schema och skapar en databindning mellan fälten som finns i det adaptiva formuläret och JSON-schemat. Sedan kan du integrera det anpassade formuläret med en valfri databas, fylla i data i formuläret och skicka det till databasen med Forms Portal.

I följande bild visas olika steg för att integrera ett konverterat adaptivt formulär med en databas med hjälp av Forms Portal:

![databasintegration](assets/database_integration.gif)

I den här artikeln beskrivs de stegvisa instruktionerna för att köra alla dessa integrationssteg.

Exemplet, som behandlas i den här artikeln, är en referensimplementering av anpassade data- och metadatatjänster för att integrera en formulärportalsida med en databas. Databasen som används i exempelimplementeringen är MySQL 5.6.24. Du kan emellertid integrera Forms Portal-sidor med valfri databas.

## Krav {#pre-requisites}

* AEM 6.5-författarinstans med senaste AEM 6.5 Service Pack
* Senaste versionen av AEM Forms-tilläggspaketet
* [Tjänsten Automatisk formulärkonvertering](configure-service.md)
* En databas att integrera med. Databasen som används i exempelimplementeringen är MySQL 5.6.24. Du kan emellertid integrera Forms Portal med valfri databas.

## Konfigurera anslutning mellan AEM-instans och databas {#set-up-connection-aem-instance-database}

En anslutning mellan en AEM-instans och en MYSQL-databas skapas:

* [Installera ett MYSQL-kopplingspaket](#install-mysql-connector-java-file)

* [Skapa schema och tabeller i databasen](#create-schema-and-tables-in-database)

* [Konfigurerar anslutningsinställningar](#configure-connection-between-aem-instance-and-database)

* [Konfigurera och konfigurera exempelpaketet för Forms Portal-integration](#set-up-and-configure-sample)

### Installera filen mysql-connector-java-5.1.39-bin.jar {#install-mysql-connector-java-file}

Utför följande steg på alla författare- och publiceringsinstanser för att installera filen mysql-connector-java-5.1.39-bin.jar:

1. Gå till http://[server]:[port]/system/console/depfinder och sök efter paketet com.mysql.jdbc.
1. I kolumnen Exporterad av kontrollerar du om paketet exporteras av något paket. Fortsätt om paketet inte exporteras av något paket.
1. Gå till http://[server]:[port]/system/console/bundles och klicka på **[!UICONTROL Install/Update]**.
1. Klicka **[!UICONTROL Choose File]** och bläddra till filen mysql-connector-java-5.1.39-bin.jar. Markera **[!UICONTROL Start Bundle]** och **[!UICONTROL Refresh Packages]** markera kryssrutor.
1. Klicka på **[!UICONTROL Install]** eller **[!UICONTROL Update]**. Starta om servern när du är klar.
1. (Endast Windows) Stäng av operativsystemets brandvägg.

### Skapa schema och tabeller i databasen {#create-schema-and-tables-in-database}

Utför följande steg för att skapa schema och tabeller i databasen:

1. Skapa ett schema i databasen med följande SQL-sats:

   ```sql
   CREATE SCHEMA `formsportal` ;
   ```

   där det **formella** ordet hänvisar till schemats namn.

1. Skapa en **datatabell** i databasschemat med följande SQL-sats:

   ```sql
    CREATE TABLE `data` (
        `owner` varchar(255) DEFAULT NULL,
        `data` longblob,
        `metadataId` varchar(45) DEFAULT NULL,
        `id` varchar(45) NOT NULL,
        PRIMARY KEY (`id`)
        ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

1. Skapa en **metadatatabell** i databasschemat med följande SQL-sats:

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

1. Skapa en **extra metadatatabell** i databasschemat med följande SQL-sats:

   ```sql
   CREATE TABLE `additionalmetadatatable` (
       `value` text,
       `key` varchar(255) NOT NULL,
       `id` varchar(60) NOT NULL,
       PRIMARY KEY (`id`,`key`),
       CONSTRAINT ‘additionalmetadatatable_fk’ FOREIGN KEY (`id`) REFERENCES `metadata` (`id`) ON DELETE CASCADE
       ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

1. Skapa en **kommentarbar** tabell i databasschemat med följande SQL-sats:

   ```sql
   CREATE TABLE `commenttable` (
       `commentId` varchar(255) DEFAULT NULL,
       `comment` text DEFAULT NULL,
       `ID` varchar(255) DEFAULT NULL,
       `commentowner` varchar(255) DEFAULT NULL,
       `time` varchar(255) DEFAULT NULL);
   ```

### Konfigurera anslutning mellan AEM-instans och databas {#configure-connection-between-aem-instance-and-database}

Utför följande konfigurationssteg för att skapa en anslutning mellan AEM-instansen och MYSQL-databasen:

1. Gå till konfigurationssidan för AEM Web Console på *http://[host]:[port]/system/console/configMgr*.
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
    <td><p>Utkastdatatjänst för formulärportal</p></td> 
    <td><p>Identifierare för datatjänsten för utkast</p></td>
    <td><p>formsportal.sampledataservice</p></td> 
    </tr>
    <tr> 
    <td><p>Form Portal Draft Metadata Service</p></td> 
    <td><p>Identifierare för metadatatjänsten för utkast</p></td>
    <td><p>formsportal.samplemetadataservice</p></td> 
    </tr>
    <tr> 
    <td><p>Skicka datatjänst för formulärportal</p></td> 
    <td><p>Identifierare för Skicka datatjänst</p></td>
    <td><p>formsportal.sampledataservice</p></td> 
    </tr>
    <tr> 
    <td><p>Skicka metadatatjänst för formulärportal</p></td> 
    <td><p>Identifierare för tjänsten Skicka metadata</p></td>
    <td><p>formsportal.samplemetadataservice</p></td> 
    </tr>
    <tr> 
    <td><p>Formulärportalen väntar på att signera datatjänst</p></td> 
    <td><p>Identifierare för datatjänsten för väntande signering</p></td>
    <td><p>formsportal.sampledataservice</p></td> 
    </tr>
    <tr> 
    <td><p>Formportalen väntar på metadatatjänst för signering</p></td> 
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
    <td><p>Testa om Born</p></td> 
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

1. Ladda ned följande paket **aem-fp-db-integration-sample-pkg-6.1.2.zip** till filsystemet.

   [Hämta fil](assets/aem-fp-db-integration-sample-pkg-6.1.2.zip)

1. Gå till AEM-pakethanteraren på *http://[host]:[port]/crx/packmgr/*.
1. Click **[!UICONTROL Upload Package]**.
1. Bläddra till paketet **aem-fp-db-integration-sample-pkg-6.1.2.zip** och klicka på **[!UICONTROL OK]**.
1. Klicka **[!UICONTROL Install]** bredvid paketet för att installera paketet.

## Konfigurera det konverterade adaptiva formuläret för integration med Forms Portal {#configure-converted-adaptive-form-for-forms-portal-integration}

Utför följande steg för att aktivera adaptiv formuläröverföring med hjälp av sidan Forms Portal:
1. [Kör konverteringen](convert-existing-forms-to-adaptive-forms.md#start-the-conversion-process) för att konvertera ett källformulär till ett anpassningsbart formulär.
1. Öppna det adaptiva formuläret i redigeringsläge.
1. Tryck på Formulärbehållare och välj Konfigurera ![anpassat formulär](assets/configure-adaptive-form.png).
1. I **[!UICONTROL Submission]** avsnittet väljer du **[!UICONTROL Forms Portal Submit Action]** i **[!UICONTROL Submit Action]** listrutan.
1. Tryck på ![Spara mallprofil](assets/edit_template_done.png) för att spara inställningarna.

## Skapa och konfigurera sidan Formulärportal {#create-configure-forms-portal-page}

Så här skapar du en formulärportalsida och konfigurerar den så att du kan skicka adaptiva formulär på den här sidan:

1. Logga in på AEM-författarinstansen och tryck **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Sites]**.
1. Välj den plats där du vill spara den nya formulärportalsidan och tryck på **[!UICONTROL Create]** > **[!UICONTROL Page]**.
1. Välj en mall för sidan, tryck **[!UICONTROL Next]** på, ange en rubrik för sidan och tryck på **[!UICONTROL Create]**.
1. Tryck **[!UICONTROL Edit]** för att konfigurera sidan.
1. I sidhuvudet trycker du på ![Redigera mall](assets/edit_template_sites.png) > **[!UICONTROL Edit Template]** för att öppna sidans mall.
1. Tryck på Layoutbehållare och tryck på ![Redigera mallprofil](assets/edit_template_policy.png). På **[!UICONTROL Allowed Components]** fliken aktiverar du alternativen **[!UICONTROL Document Services]** och **[!UICONTROL Document Services Predicates]** och trycker på ![Spara mallprofil](assets/edit_template_done.png).
1. Infoga **[!UICONTROL Search & Lister]** komponent på sidan. Därför listas alla befintliga adaptiva formulär som är tillgängliga på din AEM-instans på sidan.
1. Infoga **[!UICONTROL Drafts & Submissions]** komponent på sidan. Två flikar **[!UICONTROL Draft Forms]** och **[!UICONTROL Submitted Forms]** visas på sidan Formulärportal. På fliken **[!UICONTROL Draft Forms]** visas även det konverterade adaptiva formuläret som genererats med stegen som beskrivs i [Konfigurera det konverterade adaptiva formuläret för Forms Portal-integrering](#configure-converted-adaptive-form-for-forms-portal-integration)

1. Tryck **[!UICONTROL Preview]** på det konverterade adaptiva formuläret, ange värden för adaptiva formulärfält och skicka det. De värden som du anger för adaptiva formulärfält skickas till den integrerade databasen.