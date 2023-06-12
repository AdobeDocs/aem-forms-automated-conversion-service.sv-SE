---
title: Vanliga frågor
seo-title: Frequently asked questions
description: Vanliga frågor eller vanliga frågor
seo-description: frequently asked questions for Automated Forms Conversion Service
uuid: 0f6dc39c-99b7-49a4-8e9e-ecc4a35110c0
topic-tags: introduction
discoiquuid: e17c2d2c-8300-4467-aa01-57365697939f
exl-id: 3a29f8d4-8ea0-49eb-bfe0-0eab5f0c52c7
source-git-commit: 298d6c0641d7b416edb5b2bcd5fec0232f01f4c7
workflow-type: tm+mt
source-wordcount: '1799'
ht-degree: 4%

---

# Vanliga frågor{#frequently-asked-questions}

1. **Vilken version av AEM Forms stöder Automated forms conversion?**
   <p>automated forms conversion har stöd för AEM 6.4 Forms och AEM 6.5 Forms. Det fungerar med både AEM Forms på OSGi- och AEM-formulär på JEE. Du behöver det senaste AEM Forms-tilläggspaketet AEM författarinstansen för att kunna använda tjänsten. Detaljerade anvisningar finns i <a href="configure-service.md">Konfigurera Automated forms conversion</a> service.</p> 
    <br>

1. **Kan tjänsten installeras lokalt?**
   <p>Adobe utbildar AI- och ML-algoritmer för Automated forms conversion-trafik regelbundet med nya data för att förbättra konverteringsnoggrannheten. De uppdaterade algoritmerna distribueras till konverteringstjänsten som körs på Adobe Cloud med regelbundna intervall. Tjänstens alla kunder drar nytta av de uppdaterade algoritmerna. Därför är en central driftsättning i molnet bäst lämpad för att Automated forms conversion ska kunna lära sig mer och leverera förbättringar till alla kunder.</p> 
    <p>Tjänsten konverterar tomma formulär till anpassningsbara formulär. Tjänsten stöder inte ifyllda formulär och extrahering av data från ifyllda formulär. Ta bort data från ifyllda formulär och ta bort eller tillåtslista företagsspecifik information från formulären innan du skickar dem till tjänsten för konvertering</p> <br>

1. **Stöder tjänsten alla format av PDF forms? Vilka språk stöds?**
   <p>Tjänsten kan konvertera icke-interaktiva PDF forms-, XFA-baserade XDP- och PDF forms samt AcroForms till adaptiva formulär. Tjänsten stöder inte skannade eller ifyllda formulär. Andra begränsningar finns i <a href="known-issues.md">kända problem</a> artikel.<br /> </p> 
    <p>Vi lägger regelbundet till stöd för andra källtyper. Behåll <a href="introduction.md">supportedPDF-formulär</a> om du vill få en regelbunden uppdatering om nya funktioner och funktioner.</p>

   Tjänsten kan endast konvertera engelska, franska, tyska, spanska, italienska och portugisiska blanketter till anpassningsbara blanketter. Du kan översätta de genererade anpassningsbara formulären till ett annat språk med [AEM:s översättningsflöde.](https://helpx.adobe.com/experience-manager/6-5/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.html)</br> </br>

1. **Kan tjänsten producera en XDP istället för en adaptiv blankett?**
   <p>Tjänsten producerar inte XDP-utdata. Vi lägger regelbundet till funktioner och tjänster. Behåll <a href="introduction.md">språk och PDF forms som stöds</a> om du vill få en regelbunden uppdatering om nya funktioner och funktioner.</p> <br>

1. **Vilken typ av genererat schema?**
   <p>Du kan använda tjänsten för att generera: </p>

   * ett anpassningsbart formulär som är bundet till ett JSON-schema och
   * ett anpassat formulär som inte är bundet till något schema <br><br>

1. **Kan tjänsten konvertera ett Microsoft Word-formulär till anpassningsbara formulär?**
   <p>Nej, tjänsten konverterar inte ett Microsoft Word-formulär till ett anpassat formulär. Du kan spara ett Microsoft Word-formulär i PDF och konvertera PDF-formuläret till ett anpassat formulär. Hela processen är </p> <br>

   1. Använd Adobe Acrobat för att [konvertera Word-dokument till en icke-interaktiv PDF](https://helpx.adobe.com/acrobat/how-to/create-pdf-files-word-excel-website.html).
   1. Använd Adobe Acrobat för att [konvertera det producerade PDF forms till ifyllbart PDF-formulär](https://helpx.adobe.com/acrobat/how-to/convert-word-excel-paper-pdf-forms.html).
   1. Använd Adobe Acrobat för att uppdatera och korrigera formulärfält manuellt.
   1. Spara formuläret PDF. Nu kan du använda formuläret med konverteringstjänsten för att generera ett anpassat formulär. Du kan också använda formuläret som en dokumentmall.


1. **Kan tjänsten konvertera inskannade pappersblanketter och färglagda blanketter till anpassningsbara blanketter?**
   <p>Tjänsten kan konvertera PDF forms i färg till adaptiva formulär. Tjänsten stöder inte skannade eller ifyllda formulär. Andra begränsningar finns i <a href="known-issues.md">kända problem</a> artikel.</p> <br>

1. **Kan tjänsten konvertera ett skannat formulär eller endast en bild av ett formulär till ett anpassat formulär?**
   <p>Tjänsten stöder inte konvertering av skannade formulär eller en bild av ett formulär till ett anpassat, körklart formulär. Du kan dock använda Adobe Acrobat för att konvertera bilden av ett formulär till ett PDF-formulär. Sedan kan du använda tjänsten för att konvertera PDF-formuläret till ett anpassningsbart formulär. Använd alltid en högkvalitativ bild av formuläret för konvertering i Acrobat. Det förbättrar kvaliteten på konverteringen.</p> <br>

1. **Vissa XDP-baserade formulär använder formulärfragment, var ska dessa formulärfragment överföras?**
   <p class="MsoNormal">Överför formulärfragment till konverteringsmappen och bevara den ursprungliga mappstrukturen. Den bevarar relativa sökvägar som används i XDP-baserade formulär och formulärfragment.</p> <br>

1. **Stöder tjänsten schemabundna XDP-formulär? Om jag har en XDP bunden till ett schema, måste jag bädda in schema till XDP?**
   <p>Ja, tjänsten stöder schemabundna XDP-formulär och kräver att schemat bäddas in i XDP-källformuläret. När du konverterar ett schemabundet XDP-formulär genererar tjänsten ett JSON-schema. JSON-schemat påminner strukturellt om XSD-schemat för XDP-källformulär.</p> <br>

1. **Tjänsten kunde inte konvertera formulär. Vad är orsaken och hur löser man problemet?**
De vanligaste orsakerna till att konverteringen misslyckas är:</p>
   * Skyddat PDF forms tillhandahålls för konverteringen. Använd inte lösenordsskyddad eller skyddad PDF forms för konvertering.
   * Internetanslutningen avbryts. Kontrollera att du är ansluten till Internet under konverteringen.
   * PDF har en bild av formuläret i stället för själva formuläret.
   * Tjänsten är felaktigt konfigurerad, tjänst-URL:en har inte angetts eller så är den angivna tjänst-URL:en felaktig. Kontrollera [tjänstkonfiguration](configure-service.md#configure-the-cloud-service) på **[!UICONTROL AEM]** > **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Automated Forms Conversion configuration]**.
   * IMS-konfigurationen är inte korrekt konfigurerad. Utför en hälsokontroll av IMS-konfigurationen för att kontrollera att den fungerar som den ska. Så här kontrollerar du om IMS-konfigurationen är korrekt eller inte:
      1. Gå till `http://[servername]:[port]/libs/cq/adobeims-configuration/content/configurations.html`
      2. Välj konfigurationen. Klicka på **[!UICONTROL Check Health]** från sidhuvudet och klicka **[!UICONTROL Check]**. Om det lyckas får du **[!UICONTROL Token retrieved successfully!]** meddelande. <br> <br>

1. **Påverkar användningen av anpassade teckensnitt konverteringen?**
   <p>När ett icke-interaktivt PDF-formulär konverteras till ett adaptivt formulär bäddas teckensnitten in i PDF-formuläret för att förbättra konverteringskvaliteten. Stödet för inbäddning av teckensnitt är begränsat till icke-interaktiva PDF forms. För att optimera konverteringen av AcroForm och XFA-baserad PDF forms används grundteckensnitt.</p> 
    <p>Endast formulär finns i katalogen med anpassade teckensnitt i listan <strong>Katalog för kundteckensnitt</strong> fält för <strong> CQ-DAM-Handler-Gibson Font Manager Service</strong> -konfigurationen är inbäddad i icke-interaktiv PDF-form.</p> 
    <p> </p> <br>

1. **Identifierar och använder tjänsten teckensnitt från PDF i källformat i anpassningsbara formulär?**
   <p>Format och layout för ett responsivt HTML-formulär skiljer sig i allmänhet från PDF eller pappersbaserade formulär. För enhetlig layout och enhetlig formatering i hela organisationen används anpassade blanketter <a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/themes.html">teman för att formatera ett formulär</a>. I konverteringstjänsten används de teckensnitt och teckensnittsformat som anges i det tema som används under konverteringen. Du kan ändra teckensnitt och teckensnittsformat för temat för att ge komponenterna i ett anpassat formulär ett distinkt utseende.</p> <br>

1. **Extraherar tjänsten automatiskt JavaScript från XDP-baserade formulär och tillämpar det på motsvarande adaptiva formulär?**
   <p>Tjänsten konverterar inte automatiskt skript av XFA-baserade formulär eller Acro Forms till motsvarande anpassningsbara formulärregler. Du (formulärförfattare) kan använda <a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/rule-editor.html">Regelredigerare</a> för att lägga till interaktivitet i ett anpassat formulär.</p> <br>

1. **Vissa formulärobjekt konverteras inte korrekt till anpassningsbara formulärkomponenter. Hur löser jag problemet?**
   <p>automated forms conversion är utbildad i ett stort antal blanketter. Men AI/ML-baserade program begränsas av utbildningsdata och -mönster. Det kan finnas flera fälttyper, layouter, mönster och sammanhang som är märkbara för människans uppfattning, men som är svåra att hantera automatiskt. Tjänsten kanske inte kan identifiera sådana objekt eller kan identifiera dem felaktigt. Du får använda <a href="review-correct-ui-edited.md" target="_blank">Granska och korrigera</a> redigerare för att göra nödvändiga ändringar i den välbekanta pappersblankettbaserade layouten i indataformuläret.</p> <br/>

1. **Vissa korrigeringar upprepas i alla formulär. Kan tjänsten identifiera och åtgärda alla sådana instanser i framtida konverteringar?**

   Tjänsten genomgående tränar på era formulär och mönster. Det lär sig nya mönster dagligen. Det är ännu inte dags att påbörja automatisk korrigering som upprepas i alla formulär. Håll ett öga på prereleaseformulär för att se om en sådan funktion finns tillgänglig. <br/><br/>

   Du kan använda en metamodell för att mappa formulärobjekten till valfri adaptiv formulärkomponent och förkonfigurera validering, regler, datamönster, hjälptext och hjälpmedelsegenskaper för komponenterna. Alla angivna egenskaper används under konverteringen. Du kan använda metamodell för att tillämpa gemensamma egenskaper på fält. Det kan hjälpa dig att minska antalet upprepade problem i olika formulär.<br/><br/>

1. **Vilka alternativ finns för formulär med känsliga data, som PII-information (Personal Identiable Information)?**
Tjänsten stöder endast tomma eller ofyllda formulär. Ladda inte upp ifyllda formulär eller formulär med personligt identifierbar information (PII). Du kan även ta bort förfyllda data, personligt identifierbar information, konfidentiell och företagsspecifik information i källformulär. <br/>

1. **Var ska sidhuvud och sidfot placeras?**
   <p>Placera sidhuvud och sidfot i en anpassad formulärmall. Om källformuläret PDF har sidhuvud och sidfot, upptäcks och ersätts det identifierade sidhuvudet och sidfoten med sidhuvud och sidfot som är tillgängliga i adaptiv formulärmall under konverteringen. Om det finns ett extra sidhuvud eller en extra sidfot i det anpassade formuläret kan du använda <a href="review-correct-ui-edited.md">Granska och korrigera</a> redigerare för att korrigera eller ta bort sådana sidhuvuden eller sidfötter.</p> <br />

1. **Hur mycket tid sparar tjänsten jämfört med den manuella processen att planera, skapa resurser (teman, mallar), skapa och publicera ett anpassat formulär?**
   <p>Hur lång tid det tar beror på storleken och komplexiteten i indataformulären och antalet förfrågningar. Tjänsten har för avsikt att avsevärt minska time to value genom att konvertera PDF forms till anpassningsbara formulär i mycket snabbare takt jämfört med den manuella konverteringsprocessen. </p> <br />

1. **Vad ska jag göra om jag råkar ut för ett fel relaterat till RSA-bibliotek? Felmeddelandet liknar det som anges nedan:** <br/>
   `*ERROR* [0:0:0:0:0:0:0:1 [1565757652491] POST /content/dam/formsanddocuments/demo004.affBatchProcessor.html HTTP/1.1] org.apache.sling.engine.impl.SlingRequestProcessorImpl service: Uncaught Throwable java.lang.NoClassDefFoundError: Could not initialize class com.rsa.cryptoj.o.dl at com.rsa.jsafe.JSAFE_SecureRandom.getInstance(Unknown Source) at com.adobe.internal.pdfm.util.Util.appendRandomNumberToPrefix(Util.java: 169) [com.adobe.aemfd.adobe-aemfd-assembler:6.0.34] at com.adobe.internal.pdfm.logging.JobLog.&amp;lt;init&amp;gt;(JobLog.java:126) [com.adobe.aemfd.adobe-aemfd-assembler:6.0.34]` <br>
Ovannämnda fel inträffar när startdelegering inte har konfigurerats för RSA/BouncyCastle-bibliotek. Utför följande steg för att lösa problemet:
   <p> </p>

   1. Stoppa AEM. Navigera till `[AEM installation directory]\crx-quickstart\conf\` mapp. Öppna filen sling.properties för redigering. Om du använder `[AEM installation directory]\crx-quickstart\bin\start.bat` om du vill starta en AEM ska du redigera sling.properties som finns på `[AEM_root]\crx-quickstart\`.
   1. Lägg till följande egenskaper i filen sling.properties:<br/> `sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*`<br />  `sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider=org.bouncycastle.*`<br /> `sling.bootdelegation.xerces=org.apache.xerces.*`
   1. Spara och stäng filen. <br/>
   1. Starta AEM.<br/>
   <br/>

1. **Hur ändrar man automatiskt gemener och versaler i text i anpassningsbara formulär?**
   <p>Du kan använda adaptiva varianter från teman eller stilredigerare för att ändra skiftläget för ett fält med adaptiv form. Du kan till exempel öppna temaredigeraren och ange värdet för egenskapen Case för all text i formuläret till versaler, gemener eller camelCase. Du kan också använda alternativet CSS-åsidosättning i temaredigeraren för att skapa olika typer av format.</p>

1. **Kan jag använda Adobe Sign texttaggar med Automated forms conversion?**
   <p> När du använder Automated forms conversion Service för att konvertera ett PDF-formulär till ett anpassningsbart formulär och PDF-formuläret har Adobe Sign-texttaggar, konverteras dessa taggar till motsvarande anpassningsbara formulärfält och signerarinformationen fylls i automatiskt.  Funktionen är endast tillgänglig för Acro Forms och adaptiva formulär har stöd för ett begränsat antal Adobe Sign-fält.</p>  </br>

1. **Hur skapar man ett Adobe Sign-aktiverat PDF-formulär?**
   </p>Så här skapar du ett Adobe Sign-aktiverat PDF-formulär:</p>

   Lägg till [Adobe Sign texttaggar](https://helpx.adobe.com/sign/using/text-tag.html) till fältnamn eller använda [Konvertera till Adobe Sign-formulär](https://helpx.adobe.com/sign/using/create-forms-with-acrobat.html) alternativ.
