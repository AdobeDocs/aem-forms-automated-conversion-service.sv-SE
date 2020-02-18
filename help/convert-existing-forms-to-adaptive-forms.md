---
title: 'Konvertera PDF-formulär till anpassningsbara formulär '
seo-title: 'Konvertera PDF-formulär till anpassningsbara formulär '
description: Kör tjänsten Automatiserad formulärkonvertering för att konvertera PDF-formulär till anpassningsbara formulär
seo-description: Kör tjänsten Automatiserad formulärkonvertering för att konvertera PDF-formulär till anpassningsbara formulär
uuid: 49fcd5c0-0e72-496d-9831-00f79d582f57
contentOwner: khsingh
topic-tags: forms
discoiquuid: 9358219c-6079-4552-92b9-b427a23811af
translation-type: tm+mt
source-git-commit: bbf39e3bae55654f92a50f52a22cee5da938236d

---


#  Konvertera PDF-formulär till anpassningsbara formulär {#convert-print-forms-to-adaptive-forms}

Tjänsten AEM Forms Automated Forms Conversion, som drivs av Adobe Sensei, konverterar automatiskt dina PDF-formulär till enhetsvänliga och responsiva anpassningsbara formulär. Vare sig du använder icke-interaktiva PDF-formulär, Acro-formulär eller XFA-baserade PDF-formulär kan tjänsten Automated Forms Conversion enkelt konvertera dessa formulär till anpassningsbara formulär. Mer information om funktioner, konverteringsarbetsflöde och introduktionsinformation finns i [tjänsten Automated Forms Conversion](introduction.md) .

## Krav {#pre-requisites}

* [**Konfigurera konverteringstjänsten **](configure-service.md)

* **[Förbered](https://helpx.adobe.com/experience-manager/6-5/forms/using/template-editor.html)mallarna** som ska användas i konverterade formulär: Om du använder en mall kan du använda en enhetlig profilering för alla anpassade formulär. Tjänsten Automated Forms Conversion extraherar och använder inte heller sidhuvud och sidfot i PDF-källdokument. Du kan använda adaptiva formulärmallar för att ange sidhuvud och sidfot. Sidhuvud och sidfot som anges i mallen används i anpassningsbara formulär under konverteringen.

* **[Förbered](https://helpx.adobe.com/experience-manager/6-5/forms/using/themes.html)teman** som ska användas i konverterade formulär: Om du använder ett tema kan du använda en konsekvent stil på alla anpassade former i din organisation.

## Starta konverteringsprocessen {#start-the-conversion-process}

När du har anslutit din AEM-instans till AEM Forms Conversion Service kan du konvertera dina PDF-formulär till anpassningsbara formulär. Följ de här stegen för att konvertera formulären:

* [Överföra PDF-formulär till din AEM Forms-server](convert-existing-forms-to-adaptive-forms.md#upload-pdf-forms-to-your-aem-forms-server)
* [Kör konverteringen](convert-existing-forms-to-adaptive-forms.md#run-the-conversion)
* [Granska och korrigera konverterade formulär](review-correct-ui-edited.md)

### Överföra PDF-formulär till din AEM Forms-server {#upload-pdf-forms-to-your-aem-forms-server}

Konverteringstjänsten konverterar PDF-formulär som finns i AEM Forms-instansen till adaptiva formulär. Du kan överföra alla PDF-formulär samtidigt eller i faser efter behov. Innan du överför formulären bör du tänka på följande:

* Behåll antalet formulär i en mapp under 15 och behåll det totala antalet sidor i en mapp under 50.
* Behåll mappstorleken mindre än 10 MB. Behåll inte formulär i en undermapp.
* Behåll antalet sidor i ett formulär under 15.
* Överför inte skyddade formulär. Tjänsten konverterar inte lösenordsskyddade och skyddade formulär.
* Ladda inte upp källformulär med blanksteg i filnamnet. Ta bort utrymmet från filnamnet innan du överför formulären.
* Överför inte [PDF-portföljer](https://helpx.adobe.com/acrobat/using/overview-pdf-portfolios.html). Tjänsten konverterar inte en PDF-portfölj till adaptiva formulär.
* Läs avsnitten [Kända fel](known-issues.md) och [Bästa praxis och överväganden](styles-and-pattern-considerations-and-best-practices.md) och gör föreslagna ändringar i formulär.

Utför följande steg för att överföra formulären som ska konverteras till en mapp på din AEM Forms-instans:

1. Logga in på AEM Forms-instansen.

1. Tryck **[!UICONTROL Adobe Experience Manager]** > ![](assets/adobeexperiencemanager.png) **[!UICONTROL Navigation]** > ![](assets/compass.png) > **[!UICONTROL Forms]** **[!UICONTROL Forms & Documents]**.
1. Tryck **[!UICONTROL Create]**> **[!UICONTROL Folder]**. Ange **mappens namn** och **namn** . Tryck **[!UICONTROL Create]**. En mapp skapas.
1. Tryck för att öppna den nyligen skapade mappen.
1. Tryck **[!UICONTROL Create]**> **[!UICONTROL File Upload]**. Markera formulären som ska överföras, klicka **[!UICONTROL Open]** och klicka på **[!UICONTROL Upload]**. Formulären överförs.

### Kör konverteringen {#run-the-conversion}

När du har överfört formulären och konfigurerat tjänsten utför du följande steg för att starta konverteringen:

1. I din AEM Forms-instans trycker du på **[!UICONTROL Adobe Experience Manager]** dialogrutan ![Konverteringsinställningar >](assets/adobeexperiencemanager.png) **[!UICONTROL Navigation]** > ![](assets/compass.png) > **[!UICONTROL Forms]** **[!UICONTROL Forms & Documents]**.
1. Välj ett formulär eller den mapp som innehåller PDF-formulär (formulär som ska konverteras) och tryck på **[!UICONTROL Start Automated Conversion]**. Dialogrutan **[!UICONTROL Conversion Settings]** visas.

   ![Ange konfigurationer](assets/conversion-settings-dialog.png)

1. På fliken **[!UICONTROL Basic]** i dialogrutan Konverteringsinställningar:

   * **[!UICONTROL Select a cloud configuration]**. När du väljer en konfiguration har standardmallen och -temat redan angetts. Om det behövs kan du ange en annan mall eller ett tema.
   * Ange en plats där du vill spara genererade adaptiva formulär och motsvarande schema. Du kan använda standardsökvägar eller ange anpassade sökvägar.
   * Använd alternativet **Generera adaptiva formulär utan bindningar** till datamodell för att välja om du vill generera ett adaptivt formulär med eller utan bindningar till datamodellen.
Om du inte väljer det här alternativet associerar konverteringstjänsten automatiskt adaptiva formulär med ett JSON-schema och skapar en databindning mellan fälten som är tillgängliga i det adaptiva formuläret och JSON-schemat. I **[!UICONTROL Save generated data model schema at]** fältet visas standardplatsen där det genererade JSON-schemat ska sparas. Du kan också anpassa platsen för att spara det genererade schemat.
Om du väljer det här alternativet genererar konverteringstjänsten ett adaptivt formulär utan bindningar till datamodellen. När konverteringen är klar kan du koppla ett adaptivt formulär till en formulärdatamodell, ett XML-schema eller ett JSON-schema. Mer information finns i [Skapa ett anpassat formulär](https://helpx.adobe.com/experience-manager/6-5/forms/using/creating-adaptive-form.html).
   <!--
   Comment Type: draft

   <note type="note">
   <p>The XDP or XFA-based PDF form is not used to generate the Document of Record. The conversion service auto-generates the Document of Record only if you enable the Tools &gt; Cloud Services &gt; Automated Forms Conversion Configuration &gt; <strong>&lt;Properties of selected configuration&gt; &gt;</strong> Advanced &gt; Generate Document of Record option.</p>
   <p> </p>
   </note>
   -->

1. På fliken **[!UICONTROL Additional]** i dialogrutan Konverteringsinställningar
   * Välj alternativet om du vill att konverteringstjänsten ska kunna identifiera, extrahera och hämta formulärfragment för konverterade formulär. **[!UICONTROL Extract fragment from adaptive forms]** När du väljer **[!UICONTROL Extract fragment from adaptive forms]** alternativet aktiveras alternativen för att ange sökvägar för att spara extraherade formulärfragment och motsvarande formulärfragmentscheman.
   * Ange platsen för **[!UICONTROL existing adaptive form fragments]** om du har befintliga JSON-schemabaserade och schemamindre anpassningsbara formulärfragment och du planerar att använda dessa fragment i automatiskt genererade adaptiva formulär. Konverteringstjänsten matchar tillgängliga JSON-schemabaserade och schemamindre anpassningsbara formulärfragment med PDF-indataformulär (endast icke-interaktiva PDF-formulär). Om det finns en matchning används det matchande adaptiva formulärfragmentet i motsvarande adaptiva formulär.
   >[!NOTE]
   >
   >
   > * Du kan bara använda **[!UICONTROL  Extract Fragment]** eller **[!UICONTROL Use existing adaptive form fragments]** alternativ åt gången. Du kan inte använda båda alternativen samtidigt.
   > * Du kan bara använda alternativet **[!UICONTROL Use existing adaptive form fragments]** med icke-interaktiva PDF-formulär. Andra formulärtyper stöds inte ännu.
   > * Du kan bara använda obundna fragment eller fragment som är bundna till ett JSON-schema med den automatiserade konverteringstjänsten. Använd inte XFA-fragment. XFA-fragment stöds inte.


   * Välj alternativet **[!UICONTROL Auto-detect multi-column layout of input forms]** om du vill behålla layouten för källformuläret för stora skärmar som stationära och bärbara datorer. Alternativet är användbart när du vill bevara layouten med flera kolumner för källformulär. Om en PDF-källfil till exempel har en layout med två kolumner, genererar tjänsten ett anpassat utdataformulär med en layout med två kolumner för stora skärmar och en layout med en kolumn för små skärmar som mobiltelefoner. Funktionen har några kända problem med datakällans schemastruktur. Mer information finns i artikeln [Kända fel](known-issues.md) .



1. Tryck **[!UICONTROL Start Conversion]**. Konverteringen har startats. Konverteringsförloppet visas i mappen eller formuläret tills konverteringen pågår. Meddelandet ersätts av ett annat statusmeddelande (Konverterad, Delvis konverterad eller Konvertering misslyckades) när konverteringen är klar. När konverteringen är klar skickas även ett e-postmeddelande med status på den konfigurerade e-postadressen:

   * Vid en lyckad konvertering hämtas det konverterade adaptiva formuläret och det relaterade schemat till den sökväg som anges på fliken **[!UICONTROL Basic]** i konverteringsdialogrutan. Formulärfragment och motsvarande schema hämtas bara om alternativet Extrahera fragment är markerat innan konverteringen startas.
   * Vid en misslyckad konvertering visas **[!UICONTROL Conversion Failed]** ett meddelande om alla inmatningsformulär inte kan konverteras eller om **[!UICONTROL Partially Failed]** meddelandet visas när endast ett fåtal av alla inmatningsformulären inte kan konverteras. Ett statusmeddelande skickas till den [konfigurerade e-postadressen](configure-service.md#configureemailnotification) och ett fel loggas till filen error.log.
   Om du konverterar ett XFA-baserat PDF-formulär till ett adaptivt formulär kopplar konverteringstjänsten automatiskt PDF-formuläret till det konverterade adaptiva formuläret som dokumentmall. Efter konverteringen kan du öppna de adaptiva formuläregenskaperna och visa dokumentmallen under **[!UICONTROL Document of Record Template Configuration]** fliken **[!UICONTROL Form Model]** . </br>

   Konverteringstjänsten överför automatiskt PDF-formuläret till det konverterade adaptiva formuläret som dokumentmall endast om du aktiverar alternativet **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Automated Forms Conversion Configuration]** > **[!UICONTROL Properties of selected configuration]** > **[!UICONTROL Advanced]** > **[!UICONTROL Generate Document of Record]** .

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
   >Om konverteringsprocessen tar mer än 60 minuter och PDF-formuläret fortfarande inte konverteras till ett anpassat formulär skapar du en ny mapp på AEM Forms-instansen, överför PDF-formuläret till den nya mappen och startar om konverteringen.

## Granska och korrigera konverterade formulär {#review-and-correct-the-converted-forms}

Real world forms has complex data capture requirements. När den automatiska konverteringen är klar kan man granska konverteringskvaliteten på blanketten och göra nödvändiga uppdateringar i den. I AEM Forms finns en [recension och en korrekt](review-correct-ui-edited.md) redigerare som gör nödvändiga ändringar. Det gör att du kan förbättra den automatiska identifieringen av formulärfält och konvertera identifierade fält från en typ till en annan. Du kan till exempel identifiera layout med två kolumner i ett formulär och ändra ett fält som automatiskt identifieras som en alternativknapp till flera alternativfält.
