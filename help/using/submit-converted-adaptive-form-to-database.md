---
title: Skicka de konverterade adaptiva formulären med ett JSON-schema till databasen
description: Skicka de konverterade adaptiva formulären med ett JSON-schema till databasen genom att skapa en formulärdatamodell och referera till den i ett AEM arbetsflöde.
solution: Experience Manager Forms
feature: Adaptive Forms
topic: Administration
topic-tags: forms
role: Admin, Developer
level: Beginner, Intermediate
exl-id: 5447b66f-9fac-476f-ab8a-9290bb1f9c0d
source-git-commit: c2392932d1e29876f7a11bd856e770b8f7ce3181
workflow-type: tm+mt
source-wordcount: '1506'
ht-degree: 0%

---

# Integrera anpassningsbara blanketter med databaser med hjälp av AEM arbetsflöde {#submit-forms-to-database-using-forms-portal}

Med tjänsten Automated forms conversion (AFCS) kan du konvertera ett icke-interaktivt PDF-formulär, ett Acro-formulär eller ett XFA-baserat PDF-formulär till en adaptiv form. När du startar konverteringsprocessen kan du generera ett anpassat formulär antingen med eller utan databindningar.

Om du väljer att generera ett adaptivt formulär utan databindningar kan du integrera det konverterade adaptiva formuläret med en formulärdatamodell, ett XML-schema eller ett JSON-schema efter konverteringen. För formulärdatamodellen måste du binda adaptiva formulärfält manuellt med formulärdatamodellen. Men om du genererar ett adaptivt formulär med databindningar associerar konverteringstjänsten automatiskt adaptiva formulär med ett JSON-schema och skapar en databindning mellan fälten som finns i det adaptiva formuläret och JSON-schemat. Sedan kan du integrera det anpassade formuläret med en valfri databas, fylla i data i formuläret och skicka det till databasen. När integreringen med databasen är klar kan du konfigurera fälten i det konverterade adaptiva formuläret så att de hämtar värden från databasen och fyller i adaptiva formulärfält i förväg.

I följande bild visas olika steg för att integrera ett konverterat adaptivt formulär med en databas:

![databasintegration](assets/integrate-adaptive-form-with-database.png)

I den här artikeln beskrivs de stegvisa instruktionerna för att köra alla dessa integrationssteg.

## Krav {#pre-requisites}

* Konfigurera en AEM 6.4- eller 6.5-författarinstans
* Installera [senaste Service Pack](https://helpx.adobe.com/experience-manager/aem-releases-updates.html) för AEM
* Senaste versionen av AEM Forms-tilläggspaketet
* Konfigurera [Tjänsten automated forms conversion](configure-service.md)
* Konfigurera en databas. Databasen som används i exempelimplementeringen är MySQL 5.6.24. Du kan emellertid integrera det konverterade adaptiva formuläret med valfri databas.

## Exempel på anpassningsbart formulär {#sample-adaptive-form}

Om du vill köra ett användningsexempel för att integrera konverterade adaptiva formulär med en databas med hjälp av ett AEM arbetsflöde hämtar du följande exempelfil i PDF.

Du kan hämta exempelformuläret Kontakta oss med:

[Hämta fil](assets/sample_contact_us_form.pdf)

Filen PDF fungerar som indata till tjänsten Automated forms conversion (AFCS). Tjänsten konverterar den här filen till ett anpassat formulär. I följande bild visas det exempel på hur du kontaktar oss i PDF-format.

![exempelformulär för låneansökan](assets/sample_contact_us_form.png)

## Installera filen mysql-connector-java-5.1.39-bin.jar {#install-mysql-connector-java-file}

Utför följande steg på alla författare- och publiceringsinstanser för att installera filen mysql-connector-java-5.1.39-bin.jar:

1. Navigera till `http://server:port/system/console/depfinder` och söka efter paketet com.mysql.jdbc.
1. I kolumnen Exporterad av kontrollerar du om paketet exporteras av något paket. Fortsätt om paketet inte exporteras av något paket.
1. Navigera till `http://server:port/system/console/bundles` och klicka **[!UICONTROL Install/Update]**.
1. Klicka **[!UICONTROL Choose File]** och bläddra till filen mysql-connector-java-5.1.39-bin.jar. Välj även **[!UICONTROL Start Bundle]** och **[!UICONTROL Refresh Packages]** kryssrutor.
1. Klicka **[!UICONTROL Install]** eller **[!UICONTROL Update]**. Starta om servern när du är klar.
1. (Endast Windows) Stäng av operativsystemets brandvägg.

## Förbered data för formulärmodellen {#prepare-data-for-form-model}

Med AEM Forms dataintegrering kan du konfigurera och ansluta till olika datakällor. När du har genererat ett anpassat formulär med konverteringsprocessen kan du definiera formulärmodellen baserat på en formulärdatamodell, XSD eller ett JSON-schema. Du kan använda en databas, Microsoft Dynamics eller någon annan tredjepartstjänst för att skapa en formulärdatamodell.

I den här självstudien används MySQL-databasen som källa för att skapa en formulärdatamodell. Skapa ett schema i databasen och lägg till **konturer** till schemat baserat på de fält som är tillgängliga i det adaptiva formuläret.

![Exempeldata mittSQL](assets/db_entries_sample_form.png)

Du kan använda följande DDL-programsats för att skapa **konturer** tabellen i databasen.

```sql
CREATE TABLE `contactus` (
   `name` varchar(45) NOT NULL,
   `email` varchar(45) NOT NULL,
   `phonenumber` varchar(10) DEFAULT NULL,
   `issuedesc` varchar(1000) DEFAULT NULL,
   PRIMARY KEY (`email`)
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

## Konfigurera anslutning mellan AEM och databas {#configure-connection-between-aem-instance-and-database}

Utför följande konfigurationssteg för att skapa en anslutning mellan AEM och MYSQL-databasen:

1. Gå till sidan AEM Web Console Configuration på `http://server:port/system/console/configMgr`.
1. Sök och klicka för att öppna **[!UICONTROL Apache Sling Connection Pooled DataSource]** i redigeringsläge i webbkonsolkonfigurationen. Ange värdena för egenskaperna enligt följande tabell:

   <table> 
    <tbody> 
    <tr> 
    <th><strong>Egenskap</strong></th> 
    <th><strong>Värde</strong></th> 
    </tr> 
    <tr> 
    <td><p>Datakällans namn</p></td> 
    <td><p>Ett datakällnamn för filtrering av drivrutiner från datakällpoolen.</p></td>
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

## Skapa formulärdatamodell {#create-form-data-model}

När du har konfigurerat MYSQL som datakälla skapar du en formulärdatamodell på följande sätt:

1. I AEM författarinstans går du till **[!UICONTROL Forms]** > **[!UICONTROL Data Integrations]**.

1. Tryck **[!UICONTROL Create]** > **[!UICONTROL Form Data Model]**.

1. I **[!UICONTROL Create Form Data Model]** guide, ange **workflow_submit** som namn på formulärdatamodellen. Tryck **[!UICONTROL Next]**.

1. Markera MYSQL-datakällan som du har konfigurerat i föregående avsnitt och tryck på **[!UICONTROL Create]**.

1. Tryck **[!UICONTROL Edit]** och utöka datakällan som visas i den vänstra rutan för att markera **konturer** bord, **[!UICONTROL get]** och **[!UICONTROL insert]** tjänster, och trycka **[!UICONTROL Add Selected]**.

   ![Exempeldata mittSQL](assets/fdm_details_workfdlow_submit.png)

1. Markera datamodellsobjektet i den högra rutan och tryck på **[!UICONTROL Edit Properties]**. Välj **[!UICONTROL get]** och **[!UICONTROL insert]** från **[!UICONTROL Read Service]** och **[!UICONTROL Write Service]** nedrullningsbara listor. Ange argument för tjänsten Read och tryck på **[!UICONTROL Done]**.

1. I **[!UICONTROL Services]** väljer du **[!UICONTROL get]** service och knacka **[!UICONTROL Edit Properties]**. Välj **[!UICONTROL Output Model Object]**, inaktivera **[!UICONTROL Return array]** växla och tryck **[!UICONTROL Done]**.

1. Välj **[!UICONTROL Insert]** service och knacka **[!UICONTROL Edit Properties]**. Välj **[!UICONTROL Input Model Object]** och knacka **[!UICONTROL Done]**.

1. Tryck **[!UICONTROL Save]** för att spara formulärdatamodellen.

Du kan hämta exempelformulärdatamodellen med:

[Hämta fil](assets/DownloadedFormsPackage_1497728018502500.zip)

## Generera anpassningsbara formulär med JSON-bindning {#generate-adaptive-forms-with-json-binding}

Använd [Automated forms conversion-tjänst (AFCS) som ska konverteras](convert-existing-forms-to-adaptive-forms.md) den [Kontakta oss](#sample-adaptive-form) till en anpassningsbar form med databindning. Se till att du inte väljer **[!UICONTROL Generate adaptive form(s) without data bindings]** när du genererar det anpassade formuläret.

![Adaptiv form med JSON-bindning](assets/generate_af_with_data_bindings.png)

Markera de konverterade **Kontakta oss** finns i **[!UICONTROL output]** mapp i **[!UICONTROL Forms & Documents]** och knacka **[!UICONTROL Edit]**. Tryck **[!UICONTROL Preview]**, ange värden i anpassade formulärfält och tryck **[!UICONTROL Submit]**.

Logga in på **crx-databas** och navigera till */content/forms/fp/admin/submit/data* för att visa de inskickade värdena i JSON-format. Följande är exempeldata i JSON-format när du skickar den konverterade **Kontakta oss** adaptiv form:

```json
{
  "afData": {
    "afUnboundData": {
      "data": {}
    },
    "afBoundData": {
      "data": {
        "name1": "Gloria",
        "email": "abc@xyz.com",
        "phone_number": "2346578965",
        "issue_description": "Test message"
      }
    },
    "afSubmissionInfo": {
      "computedMetaInfo": {},
      "stateOverrides": {},
      "signers": {},
      "afPath": "/content/dam/formsanddocuments/docs_conversion/output/sample_form_json",
      "afSubmissionTime": "20191204014007"
    }
  }
}
```

Du måste skapa en arbetsflödesmodell nu som kan bearbeta dessa data och skicka dem till MYSQL-databasen med den formulärdatamodell som du har skapat i de föregående avsnitten.

## Skapa en arbetsflödesmodell för att bearbeta JSON-data {#create-workflow-model}

Utför följande steg för att skapa en arbetsflödesmodell och skicka data i anpassade formulär till databasen:

1. Öppna konsolen Arbetsflödesmodeller. Standardwebbadressen är `https://server:port/libs/cq/workflow/admin/console/content/models.html/etc/workflow/models`.

1. Välj **[!UICONTROL Create]** sedan **[!UICONTROL Create Model]**. The **[!UICONTROL Add Workflow Model]** visas.

1. Ange **[!UICONTROL Title]** och **[!UICONTROL Name]** (valfritt). Till exempel: **workflow_json_submit**. Tryck **[!UICONTROL Done]** för att skapa modellen.

1. Välj arbetsflödesmodell och tryck på **[!UICONTROL Edit]** för att öppna modellen i redigeringsläge. Tryck på + och lägg till **[!UICONTROL Invoke Form Data Model Service]** steg till arbetsflödesmodellen.

1. Tryck på **[!UICONTROL Invoke Form Data Model Service]** steg och knacka ![Konfigurera](assets/configure_icon.png).

1. I **[!UICONTROL Form Data Model]** väljer du den formulärdatamodell som du har skapat i **[!UICONTROL Form Data Model path]** fält och markera **[!UICONTROL insert]** från **[!UICONTROL Service]** listruta.

1. I **[!UICONTROL Input for Service]** flik, välja **[!UICONTROL Provide input data using literal, variable, or a workflow metadata, and a JSON file]** i listrutan väljer **[!UICONTROL Map input fields from input JSON]** kryssruta, markera **[!UICONTROL Relative to payload]** och tillhandahåller **data.xml** som värdet för **[!UICONTROL Select input JSON document using]** fält.

1. I **[!UICONTROL Service Arguments]** anger du följande värden för formulärdatamodellens argument:

   ![Anropa datamodelltjänst för formulär](assets/invoke_form_data_model_service.png)

   Observera att formulärdatamodellsfälten, till exempel kontaktar punktnamn, mappas till **afData.afBoundData.data.name1**, som refererar till JSON-schemabindningarna för det skickade adaptiva formuläret.

## Konfigurera adaptiv formuläröverföring {#configure-adaptive-form-submission}

Utför följande steg för att skicka det adaptiva formuläret till arbetsflödesmodellen som du skapade i föregående avsnitt:

1. Välj det konverterade formuläret Kontakta oss som finns i **[!UICONTROL output]** mapp i **[!UICONTROL Forms & Documents]** och knacka **[!UICONTROL Edit]**.

1. Öppna adaptiva formuläregenskaper genom att trycka **[!UICONTROL Form Container]** och sedan knacka ![Konfigurera](assets/configure_icon.png).

1. I **[!UICONTROL Submission]** avsnitt, markera **[!UICONTROL Invoke an AEM workflow]** från **[!UICONTROL Submit Action]** väljer du arbetsflödesmodell som du skapade i föregående avsnitt och anger **data.xml** i **[!UICONTROL Data File Path]** fält.

1. Tryck ![Spara](assets/save_icon.png) för att spara egenskaperna.

1. Tryck **[!UICONTROL Preview]**, ange värden i anpassade formulärfält och tryck **[!UICONTROL Submit]**. De inskickade värdena visas nu i MYSQL-databastabellen i stället för **crx-databas**.

## Konfigurera anpassningsbara formulär för förifyllningsvärden från databasen

Utför följande steg för att konfigurera adaptiva formulär till förifyllda värden från MYSQL-databasen baserat på den primärnyckel som definieras i tabellen (i det här fallet e-post):

1. Tryck på **E-post** fält i det adaptiva formuläret och knacka ![Redigera regel](assets/edit-rules.png).

1. Tryck **[!UICONTROL Create]** och markera **[!UICONTROL is changed]** från **[!UICONTROL Select State]** nedrullningsbar lista i **[!UICONTROL When]** -avsnitt.

1. I **[!UICONTROL Then]** avsnitt, markera **[!UICONTROL Invoke Service]** och **get** som tjänst för formulärdatamodellen som du har skapat i ett tidigare avsnitt i den här artikeln.

1. Välj **E-post** i **[!UICONTROL Input]** och de tre övriga fälten i formulärdatamodellen, **Namn**, **Telefonnummer** och **Ärendebeskrivning** i **[!UICONTROL Output]** -avsnitt. Tryck **[!UICONTROL Done]** för att spara inställningarna.

   ![Konfigurera inställningar för e-postförifyllning](assets/email_prefill_settings.png)

   På grund av befintliga e-postposter i MYSQL-databasen kan du fylla i värdena för de tre övriga fälten i förväg **[!UICONTROL Preview]** det adaptiva formulärets läge. Om du till exempel anger aya.tan@xyz.com i **E-post** fält (baserat på befintliga data i [Förbered formulärdatamodell](#prepare-data-for-form-model) avsnitt i den här artikeln) och tabba ut från fältet, de övriga tre fälten, **Namn**, **Telefonnummer** och **Ärendebeskrivning** visas automatiskt i det anpassade formuläret.

Du kan hämta det konverterade adaptiva exempelformuläret med:

[Hämta fil](assets/DownloadedFormsPackage_1498226829041200.zip)
