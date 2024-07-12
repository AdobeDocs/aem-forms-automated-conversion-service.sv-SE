---
title: Frågor och svar
description: Vanliga frågor eller vanliga frågor
solution: Experience Manager Forms
feature: Adaptive Forms
topic: Administration
topic-tags: introduction
role: Admin, Developer
level: Beginner, Intermediate
exl-id: 3a29f8d4-8ea0-49eb-bfe0-0eab5f0c52c7
source-git-commit: c2392932d1e29876f7a11bd856e770b8f7ce3181
workflow-type: tm+mt
source-wordcount: '1777'
ht-degree: 2%

---

# Frågor och svar{#frequently-asked-questions}

1. **Vilken version av AEM Forms stöder tjänsten Automated forms conversion (AFCS)?**
   <p>Tjänsten Automated forms conversion (AFCS) stöder AEM 6.4 Forms och AEM 6.5 Forms. Det fungerar med både AEM Forms på OSGi- och AEM-formulär på JEE. Du behöver det senaste AEM Forms-tilläggspaketet AEM författarinstansen för att kunna använda tjänsten. Mer information finns i <a href="configure-service.md">Konfigurera tjänsten Automated forms conversion</a>.</p> 
    <br>

1. **Kan tjänsten installeras lokalt?**
   <p>Adobe utbildar AI- och ML-algoritmer för Automated forms conversion service (AFCS) regelbundet med nya data för att förbättra konverteringsnoggrannheten. De uppdaterade algoritmerna distribueras till konverteringstjänsten som körs på Adobe Cloud med regelbundna intervall. Tjänstens alla kunder drar nytta av de uppdaterade algoritmerna. Därför är en central driftsättning i molnet bäst lämpad för tjänsten Automated forms conversion (AFCS) för att kontinuerligt lära sig och leverera förbättringar till alla kunder.</p> 
    <p>Tjänsten konverterar tomma formulär till anpassningsbara formulär. Tjänsten stöder inte ifyllda formulär och extrahering av data från ifyllda formulär. Ta bort data från ifyllda formulär och ta bort eller tillåtslista företagsspecifik information från formulären innan du skickar dem till tjänsten för konvertering</p> <br>

1. **Stöder tjänsten alla format för PDF forms? Vilka språk stöds?**
   <p>Tjänsten kan konvertera icke-interaktiva PDF forms-, XFA-baserade XDP- och PDF forms samt AcroForms till adaptiva formulär. Tjänsten stöder inte skannade eller ifyllda formulär. Andra begränsningar finns i artikeln <a href="known-issues.md">Kända fel</a>.<br />. </p> 
    <p>Vi lägger regelbundet till stöd för andra källtyper. Håll avsnittet <a href="introduction.md">supportedPDF-formulär</a> på bevakningslistan för att få en regelbunden uppdatering om nya funktioner och funktioner.</p>

   Tjänsten kan endast konvertera engelska, franska, tyska, spanska, italienska och portugisiska till anpassningsbara blanketter. Du kan översätta genererade adaptiva formulär till ett annat språk med hjälp av [AEM översättningsarbetsflöde.](https://helpx.adobe.com/experience-manager/6-5/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.html)</br> </br>

1. **Kan tjänsten producera en XDP i stället för ett adaptivt formulär?**
   <p>Tjänsten producerar inte XDP-utdata. Vi lägger regelbundet till funktioner och tjänster. Håll avsnittet <a href="introduction.md">Språk som stöds och PDF forms</a> på bevakningslistan för att få en regelbunden uppdatering av nya funktioner och funktioner.</p> <br>

1. **Vilken typ av genererat schema?**
   <p>Du kan använda tjänsten för att generera: </p>

   * ett anpassningsbart formulär som är bundet till ett JSON-schema och
   * ett anpassat formulär som inte är bundet till något schema <br><br>

1. **Kan tjänsten konvertera ett Microsoft Word-formulär till anpassningsbara formulär?**
   <p>Nej, tjänsten konverterar inte ett Microsoft Word-formulär till ett anpassat formulär. Du kan spara ett Microsoft Word-formulär i PDF och konvertera PDF-formuläret till ett anpassat formulär. Hela processen är </p> <br>

   1. Använd Adobe Acrobat för att [konvertera Word-dokument till ett icke-interaktivt PDF](https://helpx.adobe.com/acrobat/how-to/create-pdf-files-word-excel-website.html).
   1. Använd Adobe Acrobat för att [konvertera det producerade PDF forms till ifyllbart PDF-formulär](https://helpx.adobe.com/acrobat/how-to/convert-word-excel-paper-pdf-forms.html).
   1. Använd Adobe Acrobat för att uppdatera och korrigera formulärfält manuellt.
   1. Spara formuläret PDF. Nu kan du använda formuläret med konverteringstjänsten för att generera ett anpassat formulär. Du kan också använda formuläret som en dokumentmall.


1. **Kan tjänsten konvertera inskannade pappersformulär och färgade formulär till anpassningsbara formulär?**
   <p>Tjänsten kan konvertera PDF forms i färg till adaptiva formulär. Tjänsten stöder inte skannade eller ifyllda formulär. Andra begränsningar finns i artikeln <a href="known-issues.md">Kända fel</a>.</p> <br>

1. **Kan tjänsten konvertera ett skannat formulär eller endast en bild av ett formulär till ett anpassat formulär?**
   <p>Tjänsten stöder inte konvertering av skannade formulär eller en bild av ett formulär till ett anpassat formulär. Du kan dock använda Adobe Acrobat för att konvertera bilden av ett formulär till ett PDF-formulär. Sedan kan du använda tjänsten för att konvertera PDF-formuläret till ett anpassningsbart formulär. Använd alltid en högkvalitativ bild av formuläret för konvertering i Acrobat. Det förbättrar kvaliteten på konverteringen.</p> <br>

1. **Vissa XDP-baserade formulär använder formulärfragment, var ska dessa formulärfragment överföras?**
   <p class="MsoNormal">Överför formulärfragment till konverteringsmappen och bevara den ursprungliga mappstrukturen. Den bevarar relativa sökvägar som används i XDP-baserade formulär och formulärfragment.</p> <br>

1. **Stöder tjänsten schemabundna XDP-formulär? Om jag har en XDP bunden till ett schema, behöver jag bädda in schema till XDP?**
   <p>Ja, tjänsten stöder schemabundna XDP-formulär och kräver att schemat bäddas in i XDP-källformuläret. När du konverterar ett schemabundet XDP-formulär genererar tjänsten ett JSON-schema. JSON-schemat påminner strukturellt om XSD-schemat för XDP-källformulär.</p> <br>

1. **Tjänsten kunde inte konvertera formulär. Vad är orsaken och hur löser man problemet?**
De vanligaste orsakerna till att konverteringen misslyckas är:</p>
   * Skyddat PDF forms tillhandahålls för konverteringen. Använd inte lösenordsskyddad eller skyddad PDF forms för konvertering.
   * Internetanslutningen avbryts. Kontrollera att du är ansluten till Internet under konverteringen.
   * Source PDF har en bild av formuläret i stället för själva formuläret.
   * Tjänsten är felaktigt konfigurerad, tjänst-URL:en har inte angetts eller så är den angivna tjänst-URL:en felaktig. Kontrollera [tjänstkonfigurationen](configure-service.md#configure-the-cloud-service) på **[!UICONTROL AEM]** > **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Automated Forms Conversion configuration]**.
   * IMS-konfigurationen är inte korrekt konfigurerad. Utför en hälsokontroll av IMS-konfigurationen för att kontrollera att den fungerar som den ska. Så här kontrollerar du om IMS-konfigurationen är korrekt eller inte:
      1. Gå till `http://[servername]:[port]/libs/cq/adobeims-configuration/content/configurations.html`
      2. Välj konfigurationen. Klicka på **[!UICONTROL Check Health]** i sidhuvudet och klicka på **[!UICONTROL Check]**. Om det lyckas får du **[!UICONTROL Token retrieved successfully!]**-meddelandet. <br> <br>

1. **Påverkar användningen av anpassade teckensnitt konverteringen?**
   <p>När ett icke-interaktivt PDF-formulär konverteras till ett adaptivt formulär bäddas teckensnitten in i PDF-formuläret för att förbättra konverteringskvaliteten. Stödet för inbäddning av teckensnitt är begränsat till icke-interaktiva PDF forms. För att optimera konverteringen av AcroForm och XFA-baserad PDF forms används grundteckensnitt.</p> 
    <p>Endast formulär som är tillgängliga i den anpassade teckensnittskatalogen som listas i fältet <strong>Kundteckensnittskatalog</strong> i konfigurationen <strong> CQ-DAM-Handler-Gibson Font Manager Service</strong> är inbäddade i icke-interaktiva PDF-formulär.</p> 
    <p> </p> <br>

1. **Identifierar och använder tjänsten teckensnitt från PDF i källformulär för anpassningsbara utdata?**
   <p>Format och layout för ett responsivt HTML-formulär skiljer sig i allmänhet från PDF eller pappersbaserade formulär. För att ge stöd för enhetlig layout och formatering i hela organisationen används <a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/themes.html">teman för att formatera ett formulär</a>. I konverteringstjänsten används de teckensnitt och teckensnittsformat som anges i det tema som används under konverteringen. Du kan ändra teckensnitt och teckensnittsformat för temat för att ge komponenterna i ett anpassat formulär ett distinkt utseende.</p> <br>

1. **Extraherar tjänsten automatiskt JavaScript från XDP-baserade formulär och använder den på motsvarande adaptiva formulär?**
   <p>Tjänsten konverterar inte automatiskt skript av XFA-baserade formulär eller Acro Forms till motsvarande anpassningsbara formulärregler. Du (formulärförfattare) kan använda <a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/rule-editor.html">regelredigeraren</a> för att lägga till interaktivitet i ett anpassat formulär.</p> <br>

1. **Vissa formulärobjekt konverteras inte korrekt till adaptiva formulärkomponenter. Hur löser jag problemet?**
   <p>Automated forms conversion-tjänsten (AFCS) har utbildats på ett stort antal formulär. Men AI/ML-baserade program begränsas av utbildningsdata och -mönster. Det kan finnas flera fälttyper, layouter, mönster och sammanhang som är märkbara för människans uppfattning, men som är svåra att hantera automatiskt. Tjänsten kanske inte kan identifiera sådana objekt eller kan identifiera dem felaktigt. Du kan använda redigeraren <a href="review-correct-ui-edited.md" target="_blank">Granska och korrigera</a> för att göra nödvändiga ändringar i det välbekanta pappersformuläret baserat på layouten i indataformuläret.</p> <br/>

1. **Vissa korrigeringar upprepas i alla formulär. Kan tjänsten identifiera och åtgärda alla sådana instanser i framtida konverteringar?**

   Tjänsten genomgående tränar på era formulär och mönster. Det lär sig nya mönster dagligen. Det är ännu inte dags att påbörja automatisk korrigering som upprepas i alla formulär. Håll ett öga på prereleaseformulär för att se om en sådan funktion finns tillgänglig. <br/><br/>

   Du kan använda en metamodell för att mappa formulärobjekten till valfri adaptiv formulärkomponent och förkonfigurera validering, regler, datamönster, hjälptext och hjälpmedelsegenskaper för komponenterna. Alla angivna egenskaper används under konverteringen. Du kan använda metamodell för att tillämpa gemensamma egenskaper på fält. Det kan hjälpa dig att minska antalet upprepade problem i olika formulär.<br/><br/>

1. **Vilka alternativ finns för formulär med känsliga data, som PII-information (personligt identifierbar information)?**
Tjänsten stöder endast tomma eller ofyllda formulär. Ladda inte upp ifyllda formulär eller formulär med personligt identifierbar information (PII). Du kan även ta bort förfyllda data, personligt identifierbar information, konfidentiell och företagsspecifik information i källformulär. <br/>

1. **Var ska sidhuvud och sidfot placeras?**
   <p>Placera sidhuvud och sidfot i en anpassad formulärmall. Om källformuläret PDF har sidhuvud och sidfot, upptäcks och ersätts det identifierade sidhuvudet och sidfoten med sidhuvud och sidfot som är tillgängliga i adaptiv formulärmall under konverteringen. Om det finns ett extra sidhuvud eller en extra sidfot i det adaptiva formuläret kan du använda redigeraren <a href="review-correct-ui-edited.md">Granska och korrigera</a> för att korrigera eller ta bort det.</p> <br />

1. **Hur mycket tid sparar tjänsten jämfört med den manuella processen att planera, skapa resurser (teman, mallar), skapa och publicera ett anpassat formulär?**
   <p>Hur lång tid det tar beror på storleken och komplexiteten i indataformulären och antalet förfrågningar. Tjänsten har för avsikt att avsevärt minska time to value genom att konvertera PDF forms till anpassningsbara formulär i mycket snabbare takt jämfört med den manuella konverteringen av formulär. </p> <br />

1. **Vad gör jag om jag råkar ut för ett fel som är relaterat till RSA-bibliotek? Felmeddelandet liknar meddelandet som anges nedan:** <br/>
   `*ERROR* [0:0:0:0:0:0:0:1 [1565757652491] POST /content/dam/formsanddocuments/demo004.affBatchProcessor.html HTTP/1.1] org.apache.sling.engine.impl.SlingRequestProcessorImpl service: Uncaught Throwable java.lang.NoClassDefFoundError: Could not initialize class com.rsa.cryptoj.o.dl at com.rsa.jsafe.JSAFE_SecureRandom.getInstance(Unknown Source) at com.adobe.internal.pdfm.util.Util.appendRandomNumberToPrefix(Util.java: 169) [com.adobe.aemfd.adobe-aemfd-assembler:6.0.34] at com.adobe.internal.pdfm.logging.JobLog.&amp;lt;init&amp;gt;(JobLog.java:126) [com.adobe.aemfd.adobe-aemfd-assembler:6.0.34]` <br>
Ovannämnda fel inträffar när startdelegering inte har konfigurerats för RSA/BouncyCastle-bibliotek. Utför följande steg för att lösa problemet:
   <p> </p>

   1. Stoppa AEM. Navigera till mappen `[AEM installation directory]\crx-quickstart\conf\`. Öppna filen sling.properties för redigering. Om du använder `[AEM installation directory]\crx-quickstart\bin\start.bat` för att starta en AEM ska du redigera sling.properties som finns på `[AEM_root]\crx-quickstart\`.
   1. Lägg till följande egenskaper i filen sling.properties:<br/> `sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*`<br />  `sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider=org.bouncycastle.*`<br /> `sling.bootdelegation.xerces=org.apache.xerces.*`
   1. Spara och stäng filen. <br/>
   1. Starta AEM.<br/>
   <br/>

1. **Hur ändrar jag automatiskt skiftläget för adaptiv formulärtext?**
   <p>Du kan använda adaptiva varianter från teman eller stilredigerare för att ändra skiftläget för ett fält med adaptiv form. Du kan till exempel öppna temaredigeraren och ange värdet för egenskapen Case för all text i formuläret till versaler, gemener eller camelCase. Du kan också använda alternativet CSS-åsidosättning i temaredigeraren för att skapa olika typer av format.</p>

1. **Kan jag använda Adobe Sign texttaggar med tjänsten Automated forms conversion (AFCS)?**
   <p> När du använder tjänsten Automated forms conversion (AFCS) för att konvertera ett PDF-formulär till ett anpassningsbart formulär och formuläret PDF har Adobe Sign-texttaggar, konverteras dessa taggar till motsvarande anpassningsbara formulärfält och signerarinformationen fylls i automatiskt.  Funktionen är endast tillgänglig för Acro Forms och adaptiva formulär har stöd för ett begränsat antal Adobe Sign-fält.</p>  </br>

1. **Hur skapar jag ett Adobe Sign-aktiverat PDF-formulär?**
   </p>Så här skapar du ett Adobe Sign-aktiverat PDF-formulär:</p>

   Lägg till [Adobe Sign-texttaggar](https://helpx.adobe.com/sign/using/text-tag.html) i fältnamn eller använd alternativet [Konvertera till Adobe Sign-formulär](https://helpx.adobe.com/sign/using/create-forms-with-acrobat.html) .
