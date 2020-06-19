---
title: Vanliga frågor
seo-title: Vanliga frågor
description: Vanliga frågor eller vanliga frågor
seo-description: vanliga frågor och svar om tjänsten Automatisk formulärkonvertering
uuid: 0f6dc39c-99b7-49a4-8e9e-ecc4a35110c0
topic-tags: introduction
discoiquuid: e17c2d2c-8300-4467-aa01-57365697939f
translation-type: tm+mt
source-git-commit: b1df14a331dc4aef7ce6383dec0091fa6db1fd7b
workflow-type: tm+mt
source-wordcount: '1685'
ht-degree: 5%

---


# Vanliga frågor{#frequently-asked-questions}

1. **Vilken version av AEM Forms stöder tjänsten Automated Forms Conversion?**
   <p>Tjänsten Automated Forms Conversion stöder AEM 6.4 Forms och AEM 6.5 Forms. Det fungerar med både AEM Forms på OSGi- och AEM-formulär på JEE. Du måste ha det senaste AEM Forms-tilläggspaketet ovanpå AEM-författarinstansen för att kunna använda tjänsten. For detailed instructions, see <a href="configure-service.md">Configure the Automated Forms Conversion</a> service.</p> 
    <br>

1. **Kan tjänsten installeras lokalt?**
   <p>Adobe utbildar AI- och ML-algoritmer i tjänsten Automated Forms Conversion med jämna mellanrum med nya data för att förbättra konverteringsnoggrannheten. De uppdaterade algoritmerna distribueras till konverteringstjänsten som körs på Adobe Cloud med regelbundna intervall. Tjänstens alla kunder drar nytta av de uppdaterade algoritmerna. Central driftsättning i molnet passar bäst för tjänsten Automated Forms Conversion för att kontinuerligt lära sig och leverera förbättringar till alla kunder.</p> 
    <p>Tjänsten konverterar tomma formulär till anpassningsbara formulär. Tjänsten stöder inte ifyllda formulär och extrahering av data från ifyllda formulär. Ta bort data från ifyllda formulär och ta bort eller tillåt egenutvecklad information från formulären innan formulären skickas till tjänsten för konvertering</p> <br>

1. **Stöder tjänsten alla format av PDF forms? Vilka språk stöds?**
   <p>Tjänsten kan konvertera icke-interaktiva PDF forms-, XFA-baserade XDP- och PDF forms samt AcroForms till adaptiva formulär. Tjänsten stöder inte skannade eller ifyllda formulär. Andra begränsningar finns i artikeln <a href="known-issues.md">Kända fel</a> .<br /> </p> 
    <p>Vi lägger regelbundet till stöd för andra källtyper. Se till att avsnittet <a href="introduction.md">PDF-formulär</a> som stöds finns med på bevakningslistan för att få en regelbunden uppdatering av nya funktioner och funktioner.</p>

   Tjänsten kan endast konvertera formulär på engelska till anpassningsbara formulär. Du kan översätta de genererade anpassningsbara formulären till ett annat språk med [AEM:s översättningsflöde.](https://helpx.adobe.com/experience-manager/6-5/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.html)</br> </br>

1. **Kan tjänsten producera en XDP istället för en adaptiv blankett?**
   <p>Tjänsten producerar inte XDP-utdata. Vi lägger regelbundet till funktioner och tjänster. Se till att de språk och PDF forms <a href="introduction.md">som</a> stöds finns med i din bevakningslista för en regelbunden uppdatering av nya funktioner.</p> <br>

1. **Vilken typ av genererat schema?**
   <p>Du kan använda tjänsten för att generera: </p>

   * ett anpassningsbart formulär som är bundet till ett JSON-schema och
   * ett anpassat formulär som inte är bundet till något schema <br><br>

1. **Kan tjänsten konvertera ett Microsoft Word-formulär till anpassningsbara formulär?**
   <p>Nej, tjänsten konverterar inte ett Microsoft Word-formulär till ett anpassat formulär. Du kan spara ett Microsoft Word-formulär till ett PDF-formulär och konvertera PDF-formuläret till ett anpassat formulär. Hela processen är </p> <br>

   1. Använd Adobe Acrobat för att [konvertera Word-dokument till en icke-interaktiv PDF](https://helpx.adobe.com/acrobat/how-to/create-pdf-files-word-excel-website.html).
   1. Använd Adobe Acrobat för att [konvertera PDF forms till ifyllbart PDF-formulär](https://helpx.adobe.com/acrobat/how-to/convert-word-excel-paper-pdf-forms.html).
   1. Använd Adobe Acrobat för att uppdatera och korrigera formulärfält manuellt.
   1. Spara PDF-formuläret. Nu kan du använda formuläret med konverteringstjänsten för att generera ett anpassat formulär. Du kan också använda formuläret som en dokumentmall.


1. **Kan tjänsten konvertera inskannade pappersblanketter och färglagda blanketter till anpassningsbara blanketter?**
   <p>Tjänsten kan konvertera PDF forms till anpassningsbara formulär. Tjänsten stöder inte skannade eller ifyllda formulär. Andra begränsningar finns i artikeln <a href="known-issues.md">Kända fel</a> .</p> <br>

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
   * PDF-källfilen innehåller en bild av formuläret i stället för det faktiska formuläret.
   * Tjänsten är felaktigt konfigurerad, tjänst-URL:en har inte angetts eller så är den angivna tjänst-URL:en felaktig. Kontrollera [tjänstkonfigurationen](configure-service.md#configure-the-cloud-service) på **[!UICONTROL AEM]** > **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Automated Forms Conversion configuration]**.
   * IMS-konfigurationen är inte korrekt konfigurerad. Utför en hälsokontroll av IMS-konfigurationen för att kontrollera att den fungerar som den ska. Så här kontrollerar du om IMS-konfigurationen är korrekt eller inte:
      1. Gå till `http://[servername]:[port]/libs/cq/adobeims-configuration/content/configurations.html`
      2. Välj konfigurationen. Klicka på **[!UICONTROL Check Health]** i sidhuvudet och klicka på **[!UICONTROL Check]**. Om det lyckas får du **[!UICONTROL Token retrieved successfully!]** ett meddelande. <br> <br>

1. **Påverkar användningen av anpassade teckensnitt konverteringen?**
   <p>När ett icke-interaktivt PDF-formulär konverteras till ett anpassningsbart formulär bäddas teckensnitten in i PDF-formuläret för att förbättra konverteringskvaliteten. Stödet för inbäddning av teckensnitt är begränsat till icke-interaktiva PDF forms. För att optimera konverteringen av AcroForm och XFA-baserad PDF forms används grundteckensnitt.</p> 
    <p>Endast formulär som är tillgängliga i den anpassade teckensnittskatalogen som finns i <strong>kundens katalog</strong> för teckensnittshanteraren i konfigurationen av tjänsten <strong></strong> CQ-DAM-Handler-Gibson är inbäddade i icke-interaktiva PDF-formulär.</p> 
    <p> </p> <br>

1. **Identifierar och använder tjänsten teckensnitt i käll-PDF i anpassningsbara formulär?**
   <p>Format och layout för ett responsivt HTML-formulär skiljer sig i allmänhet från ett PDF- eller pappersbaserat formulär. För att ge stöd för enhetlig layout och formatering i hela organisationen används <a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/themes.html">teman för att utforma ett formulär</a>. I konverteringstjänsten används de teckensnitt och teckensnittsformat som anges i det tema som används under konverteringen. Du kan ändra teckensnitt och teckensnittsformat för temat för att ge komponenterna i ett anpassat formulär ett distinkt utseende.</p> <br>

1. **Extraherar tjänsten automatiskt JavaScript från XDP-baserade formulär och tillämpar det på motsvarande adaptiva formulär?**
   <p>Tjänsten konverterar inte automatiskt skript av XFA-baserade formulär eller Acro-formulär till motsvarande anpassningsbara formulärregler. Du (formulärförfattare) kan använda <a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/rule-editor.html">regelredigeraren</a> för att lägga till interaktivitet i ett anpassat formulär.</p> <br>

1. **Vissa formulärobjekt konverteras inte korrekt till anpassningsbara formulärkomponenter. Hur löser jag problemet?**
   <p>Tjänsten Automated Forms Conversion har utbildats i en stor uppsättning formulär. Men AI/ML-baserade program begränsas av utbildningsdata och -mönster. Det kan finnas flera fälttyper, layouter, mönster och sammanhang som är märkbara för människans uppfattning, men som är svåra att hantera automatiskt. Tjänsten kanske inte kan identifiera sådana objekt eller kan identifiera dem felaktigt. Du kan använda redigeraren <a href="review-correct-ui-edited.md" target="_blank">Granska och korrigera</a> för att göra nödvändiga ändringar i den välbekanta pappersbaserade layouten i indataformuläret.</p> <br/>

1. **Vissa korrigeringar upprepas i alla formulär. Kan tjänsten identifiera och åtgärda alla sådana instanser i framtida konverteringar?**

   Tjänsten genomgående tränar på era formulär och mönster. Det lär sig nya mönster dagligen. Det är ännu inte dags att påbörja automatisk korrigering som upprepas i alla formulär. Håll ett öga på prereleaseformulär för att se om en sådan funktion finns tillgänglig. <br/><br/>

   Du kan använda en metamodell för att mappa formulärobjekten till valfri adaptiv formulärkomponent och förkonfigurera validering, regler, datamönster, hjälptext och hjälpmedelsegenskaper för komponenterna. Alla angivna egenskaper används under konverteringen. Du kan använda metamodell för att tillämpa gemensamma egenskaper på fält. Det kan hjälpa dig att minska antalet upprepade problem i olika formulär.<br/><br/>

1. **Vilka alternativ finns för formulär med känsliga data, som PII-information (Personal Identiable Information)?**
Tjänsten stöder endast tomma eller ofyllda formulär. Ladda inte upp ifyllda formulär eller formulär med personligt identifierbar information (PII). Du kan även ta bort förfyllda data och vit etikett-PII, konfidentiell och personlig information i källformulär. <br/>

1. **Var ska sidhuvud och sidfot placeras?**
   <p>Placera sidhuvud och sidfot i en anpassad formulärmall. Om PDF-källformuläret har sidhuvud och sidfot upptäcks och ersätts det identifierade sidhuvudet och sidfoten med sidhuvud och sidfot som är tillgängliga i en anpassningsbar formulärmall under konverteringen. Om det finns ett extra sidhuvud eller en extra sidfot i det adaptiva formuläret kan du använda redigeraren <a href="review-correct-ui-edited.md">Granska och korrigera</a> för att korrigera eller ta bort ett sådant sidhuvud eller en sådan sidfot.</p> <br />

1. **Hur mycket tid sparar tjänsten jämfört med den manuella processen att planera, skapa resurser (teman, mallar), skapa och publicera ett anpassat formulär?**
   <p>Hur lång tid det tar beror på storleken och komplexiteten i indataformulären och antalet förfrågningar. Tjänsten har för avsikt att avsevärt minska time to value genom att konvertera PDF forms till anpassningsbara formulär i mycket snabbare takt jämfört med den manuella konverteringen av formulär. </p> <br />

1. **Vad ska jag göra om jag råkar ut för ett fel relaterat till RSA-bibliotek? Felmeddelandet liknar det som anges nedan:** <br/>
   `*ERROR* [0:0:0:0:0:0:0:1 [1565757652491] POST /content/dam/formsanddocuments/demo004.affBatchProcessor.html HTTP/1.1] org.apache.sling.engine.impl.SlingRequestProcessorImpl service: Uncaught Throwable java.lang.NoClassDefFoundError: Could not initialize class com.rsa.cryptoj.o.dl at com.rsa.jsafe.JSAFE_SecureRandom.getInstance(Unknown Source) at com.adobe.internal.pdfm.util.Util.appendRandomNumberToPrefix(Util.java: 169) [com.adobe.aemfd.adobe-aemfd-assembler:6.0.34] at com.adobe.internal.pdfm.logging.JobLog.&amp;lt;init&amp;gt;(JobLog.java:126) [com.adobe.aemfd.adobe-aemfd-assembler:6.0.34]` <br>
Ovannämnda fel inträffar när startdelegering inte har konfigurerats för RSA/BouncyCastle-bibliotek. Utför följande steg för att lösa problemet:
   <p> </p>

   1. Stoppa AEM-instansen. Navigate to the `[AEM installation directory]\crx-quickstart\conf\` folder. Öppna filen sling.properties för redigering. Om du använder `[AEM installation directory]\crx-quickstart\bin\start.bat` för att starta en AEM-instans redigerar du sling.properties som finns på `[AEM_root]\crx-quickstart\`.
   1. Lägg till följande egenskaper i filen sling.properties:<br/> `sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*`<br />  `sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider=org.bouncycastle.*`<br /> `sling.bootdelegation.xerces=org.apache.xerces.*`
   1. Spara och stäng filen. <br/>
   1. Starta AEM-instansen.<br/>
   <br/>

1. **Hur ändrar man automatiskt gemener och versaler i text i anpassningsbara formulär?**
   <p>Du kan använda adaptiva varianter från teman eller stilredigerare för att ändra skiftläget för ett fält med adaptiv form. Du kan till exempel öppna temaredigeraren och ange värdet för egenskapen Case för all text i formuläret till versaler, gemener eller camelCase. Du kan också använda alternativet CSS-åsidosättning i temaredigeraren för att skapa olika typer av format.</p>