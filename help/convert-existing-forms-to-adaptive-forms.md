---
title: 'Konvertera PDF-formulär till anpassningsbara formulär '
seo-title: 'Konvertera PDF-formulär till anpassningsbara formulär '
description: Kör tjänsten Automated forms conversion för att konvertera PDF forms till anpassningsbara formulär
seo-description: Kör tjänsten Automated forms conversion för att konvertera PDF forms till anpassningsbara formulär
uuid: 49fcd5c0-0e72-496d-9831-00f79d582f57
contentOwner: khsingh
topic-tags: forms
discoiquuid: 9358219c-6079-4552-92b9-b427a23811af
translation-type: tm+mt
source-git-commit: c4f0d07b38cdb6aa162a0b61abe12fe9d1677a8c
workflow-type: tm+mt
source-wordcount: '1487'
ht-degree: 8%

---


# Konvertera PDF-formulär till anpassningsbara formulär {#convert-print-forms-to-adaptive-forms}

Tjänsten AEM Forms Automated forms conversion, som drivs av Adobe Sensei, konverterar automatiskt PDF forms till enhetsvänliga och responsiva adaptiva formulär. Oavsett om du använder icke-interaktiv PDF forms, Acro Forms eller XFA-baserad PDF forms kan Automated forms conversion-tjänsten enkelt konvertera dessa formulär till anpassningsbara formulär. Mer information om funktioner, konverteringsarbetsflöde och introduktionsinformation finns i [tjänsten Automated forms conversion](introduction.md).

## Krav {#pre-requisites}

* [**Konfigurera konverteringstjänsten**](configure-service.md)

* **Förbered de  [](https://helpx.adobe.com/experience-manager/6-5/forms/using/template-editor.html) mallar som ska användas för konverterade formulär:** Om du använder en mall kan du använda enhetlig profilering för alla anpassade formulär. Tjänsten Automated forms conversion extraherar inte heller och använder inte sidhuvud och sidfot i PDF-källdokument. Du kan använda adaptiva formulärmallar för att ange sidhuvud och sidfot. Sidhuvud och sidfot som anges i mallen används i det adaptiva formuläret under konverteringen. När du skapar en mapp för mallarna väljer du alternativet **[!UICONTROL Browse configurations]** för alla.

* **Förbered  [](https://helpx.adobe.com/experience-manager/6-5/forms/using/themes.html) teman som ska användas för konverterade formulär:** Med ett tema kan du använda en konsekvent stil för alla anpassade former i organisationen.

* **(valfritt)** [**Konvertera PDF forms till Adobe Sign**](frequently-asked-questions.md)


## Starta konverteringsprocessen {#start-the-conversion-process}

När du har kopplat AEM till AEM Forms Conversion Service kan du konvertera PDF forms till adaptiva formulär. Följ de här stegen för att konvertera formulären:

* [Överför PDF forms till din AEM Forms-server](convert-existing-forms-to-adaptive-forms.md#upload-pdf-forms-to-your-aem-forms-server)
* [Kör konverteringen](convert-existing-forms-to-adaptive-forms.md#run-the-conversion)
* [Granska och korrigera konverterade formulär](review-correct-ui-edited.md)

### Överför PDF forms till din AEM Forms-server {#upload-pdf-forms-to-your-aem-forms-server}

Konverteringstjänsten konverterar PDF forms som finns i din AEM Forms-instans till adaptiva formulär. Du kan överföra alla PDF forms samtidigt eller i faser efter behov. Tänk på följande innan du laddar upp formulären:

* Behåll antalet formulär i en mapp under 15 och behåll det totala antalet sidor i en mapp under 50.
* Behåll mappstorleken mindre än 10 MB. Behåll inte formulär i en undermapp.
* Behåll antalet sidor i ett formulär under 15.
* Överför inte skyddade formulär. Tjänsten konverterar inte lösenordsskyddade och skyddade formulär.
* Ladda inte upp källformulär med blanksteg i filnamnet. Ta bort utrymmet från filnamnet innan du överför formulären.
* Ladda inte upp [PDF-portfolios](https://helpx.adobe.com/acrobat/using/overview-pdf-portfolios.html). Tjänsten konverterar inte en PDF-Portfolio till ett anpassningsbart formulär.
* Läs avsnitten [Kända fel](known-issues.md) och [God praxis och överväganden](styles-and-pattern-considerations-and-best-practices.md) och gör föreslagna formulärändringar.

Utför följande steg för att överföra formulären som ska konverteras till en mapp på din AEM Forms-instans:

1. Logga in på AEM Forms-instansen.

1. Tryck på **[!UICONTROL Adobe Experience Manager]** ![](assets/adobeexperiencemanager.png) > **[!UICONTROL Navigation]** ![](assets/compass.png) > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.
1. Tryck på **[!UICONTROL Create]**> **[!UICONTROL Folder]**. Ange **Rubrik** och **Namn** för mappen. Tryck på **[!UICONTROL Create]**. En mapp skapas.
1. Tryck för att öppna den nyligen skapade mappen.
1. Tryck på **[!UICONTROL Create]**> **[!UICONTROL File Upload]**. Markera formulären som ska överföras, klicka på **[!UICONTROL Open]** och klicka på **[!UICONTROL Upload]**. Formulären överförs.

### Kör konverteringen {#run-the-conversion}

När du har överfört formulären och konfigurerat tjänsten utför du följande steg för att starta konverteringen:

1. Tryck på **[!UICONTROL Adobe Experience Manager]** ![Dialogrutan Konverteringsinställningar](assets/adobeexperiencemanager.png) > **[!UICONTROL Navigation]** ![](assets/compass.png) > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]** på din AEM Forms-instans.
1. Markera ett formulär eller den mapp som innehåller PDF forms (formulär som ska konverteras) och tryck på **[!UICONTROL Start Automated Conversion]**. Dialogrutan **[!UICONTROL Conversion Settings]** visas.

   ![Ange konfigurationer](assets/conversion-settings-dialog.png)

1. På fliken **[!UICONTROL Basic]** i dialogrutan Konverteringsinställningar:

   * **[!UICONTROL Select a cloud configuration]**. När du väljer en konfiguration har standardmallen och -temat redan angetts. Om det behövs kan du ange en annan mall eller ett tema.
   * Ange en plats där du vill spara genererade adaptiva formulär och motsvarande schema. Du kan använda standardsökvägar eller ange anpassade sökvägar.
   * Använd alternativet **Generera adaptiva formulär utan bindningar till datamodell** för att välja om du vill generera ett adaptivt formulär med eller utan bindningar till datamodellen.
Om du inte väljer det här alternativet associerar konverteringstjänsten automatiskt de adaptiva formulären med ett JSON-schema och skapar en databindning mellan fälten som är tillgängliga i det adaptiva formuläret och JSON-schemat. Fältet **[!UICONTROL Save generated data model schema at]** visar standardplatsen för att spara det genererade JSON-schemat. Du kan också anpassa platsen för att spara det genererade schemat.
Om du väljer det här alternativet genererar konverteringstjänsten ett adaptivt formulär utan bindningar till datamodellen. När konverteringen är klar kan du koppla ett adaptivt formulär till en formulärdatamodell, ett XML-schema eller ett JSON-schema. Mer information finns i [Skapa ett anpassningsbart formulär](https://helpx.adobe.com/experience-manager/6-5/forms/using/creating-adaptive-form.html).

   <!--
   Comment Type: draft

   <note type="note">
   <p>The XDP or XFA-based PDF form is not used to generate the Document of Record. The conversion service auto-generates the Document of Record only if you enable the Tools &gt; Cloud Services &gt; Automated Forms Conversion Configuration &gt; <strong>&lt;Properties of selected configuration&gt; &gt;</strong> Advanced &gt; Generate Document of Record option.</p>
   <p> </p>
   </note>
   -->

1. På fliken **[!UICONTROL Additional]** i dialogrutan Konverteringsinställningar
   * Välj alternativet **[!UICONTROL Extract fragment from adaptive forms]** om du vill tillåta konverteringstjänsten att identifiera, extrahera och hämta formulärfragment för konverterade formulär. När du väljer alternativet **[!UICONTROL Extract fragment from adaptive forms]** aktiveras alternativen för att ange sökvägar för att spara extraherade formulärfragment och motsvarande formulärfragmentscheman.
   * Ange platsen för **[!UICONTROL existing adaptive form fragments]** om du har några befintliga JSON-schemabaserade och schemamindre anpassningsbara formulärfragment och du tänker använda dessa fragment i automatiskt genererade anpassningsbara formulär. Konverteringstjänsten matchar tillgängliga JSON-schemabaserade och schemamindre adaptiva formulärfragment med indata-PDF forms (endast icke-interaktiv PDF forms). Om det finns en matchning används det matchande adaptiva formulärfragmentet i motsvarande adaptiva formulär.

   >[!NOTE]
   >
   >
   > * Du kan bara använda alternativen **[!UICONTROL  Extract Fragment]** eller **[!UICONTROL Use existing adaptive form fragments]** åt gången. Du kan inte använda båda alternativen samtidigt.
   > * Du kan bara använda alternativet **[!UICONTROL Use existing adaptive form fragments]** med icke-interaktiv PDF forms. Andra formulärtyper stöds inte ännu.
   > * Du kan bara använda obundna fragment eller fragment som är bundna till ett JSON-schema med den automatiserade konverteringstjänsten. Använd inte XFA-fragment. XFA-fragment stöds inte.


   * Välj alternativet **[!UICONTROL Auto-detect multi-column layout of input forms]** om du vill behålla layouten för källformuläret för stora skärmar som stationära och bärbara datorer. Alternativet är användbart när du vill bevara layouten med flera kolumner för källformulär. Om en PDF-källfil till exempel har en layout med två kolumner, genererar tjänsten ett anpassat utdataformulär med en layout med två kolumner för stora skärmar och en layout med en kolumn för små skärmar som mobiltelefoner. Funktionen har några kända problem med datakällans schemastruktur. Mer information finns i artikeln [Kända fel](known-issues.md).
   * Som standard skapar tjänsten en separat toppnivåpanel för varje sida i ett PDF-formulär. Nu kan du använda alternativet **[!UICONTROL Auto-detect logical sections]** för att inte skapa paneler på sidnivå (sidnummerbaserade paneler) och bara skapa logiska paneler. Det enar också fälten som inte tillhör något avsnitt med föregående logiska avsnitt och fält i ett logisk avsnitt spritt över två angränsande sidor i ett enda logiskt avsnitt. Till exempel, om vissa fält i ett logiskt avsnitt finns i slutet av sidan ett och vissa är i början av sidan två, enas alla sådana fält i ett enda logiskt avsnitt.

      >[!NOTE]
      > Du behöver kopplingspaketet 1.1.38 eller senare för att kunna använda funktionen **[!UICONTROL Auto-detect logical sections]**.



1. Tryck på **[!UICONTROL Start Conversion]**. Konverteringen har startats. Konverteringsförloppet visas i mappen eller formuläret tills konverteringen pågår. Meddelandet ersätts av ett annat statusmeddelande (Konverterad, Delvis konverterad eller Konvertering misslyckades) när konverteringen är klar. När konverteringen är klar skickas även ett e-postmeddelande med status på den konfigurerade e-postadressen:

   * Vid en lyckad konvertering hämtas det konverterade adaptiva formuläret och det relaterade schemat till den sökväg som anges på fliken **[!UICONTROL Basic]** i konverteringsdialogrutan. Formulärfragment och motsvarande schema hämtas bara om alternativet Extrahera fragment är markerat innan konverteringen startas.
   * Vid en misslyckad konvertering visas **[!UICONTROL Conversion Failed]**-meddelandet om alla indataformulär inte kan konverteras eller om **[!UICONTROL Partially Failed]**-meddelandet visas när endast ett fåtal av alla indataformulär inte kan konverteras. Ett statusmeddelande skickas på den [konfigurerade e-postadressen](configure-service.md#configureemailnotification) och ett fel loggas i filen error.log.

   Om du konverterar ett XFA-baserat PDF-formulär till ett adaptivt formulär kopplar konverteringstjänsten automatiskt PDF-formuläret till det konverterade adaptiva formuläret som dokumentmall. Efter konverteringen kan du öppna de adaptiva formuläregenskaperna för att visa mallen för postdokument i **[!UICONTROL Document of Record Template Configuration]**-avsnittet på fliken **[!UICONTROL Form Model]**. </br>

   Konverteringstjänsten överför automatiskt PDF-formuläret till det konverterade adaptiva formuläret som dokumentmall endast om du aktiverar alternativet **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Automated Forms Conversion Configuration]** > **[!UICONTROL Properties of selected configuration]** > **[!UICONTROL Advanced]** > **[!UICONTROL Generate Document of Record]**.

   <!--
   Comment Type: draft

   <note type="note">
   <p>By default, the adaptive form produces a JSON schema instead of XML schema on submission. JSON schema of a converted adaptive form is complaint with XML schema of an XFA-based form. You can use the <a href="https://sling.apache.org/apidocs/sling5/org/apache/sling/commons/json/xml/XML.html#toString">org.apache.sling.commons.json.xml API</a> to convert a JSON schema to XML schema. You can also use the following sample code for conversion:</p>
   <p><code class="code">import org.apache.sling.commons.json.JSONException;
   <discoiqbr /> import org.apache.sling.commons.json.JSONObject;
   <discoiqbr /> import org.apache.sling.commons.json.xml.XML;
   <discoiqbr />
   <discoiqbr /> public class ConversionUtils {
   <discoiqbr />
   <discoiqbr /> public static String jsonToXML(String jsonString) throws JSONException {
   <discoiqbr /> //https://sling.apache.org/apidocs/sling5/org/apache/sling/commons/json/xml/XML.html#toString(java.lang.Object)
   <discoiqbr /> //jar - http://maven.ibiblio.org/maven2/org/apache/sling/org.apache.sling.commons.json/2.0.18/
   <discoiqbr /> //Note: Need to extract boundData part before converting to XML
   <discoiqbr /> return XML.toString(new JSONObject(jsonString));
   <discoiqbr /> }
   <discoiqbr /> }</code><br /> </p>
   </note>
   -->

   >[!NOTE]
   >
   >Om konverteringen tar mer än 60 minuter och PDF-formuläret fortfarande inte konverteras till ett anpassat formulär skapar du en mapp i AEM Forms-instansen, överför PDF-formuläret till den nya mappen och startar om konverteringen.

## Granska och korrigera de konverterade formulären {#review-and-correct-the-converted-forms}

Real world forms has complex data capture requirements. När den automatiska konverteringen är klar kan man granska konverteringskvaliteten på blanketten och göra nödvändiga uppdateringar i den. AEM Forms tillhandahåller en [granskning och korrigering av](review-correct-ui-edited.md)-redigerare för att göra nödvändiga ändringar. Det gör att du kan förbättra den automatiska identifieringen av formulärfält och konvertera identifierade fält från en typ till en annan. Du kan till exempel identifiera layout med två kolumner i ett formulär och ändra ett fält som automatiskt identifieras som en alternativknapp till flera alternativfält.
