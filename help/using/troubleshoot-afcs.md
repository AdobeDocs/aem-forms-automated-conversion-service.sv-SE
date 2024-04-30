---
title: Felsök den automatiserade konverteringstjänsten för formulär (AFCS)
description: Vanliga AFCS-problem och deras lösningar
solution: Experience Manager Forms
feature: Adaptive Forms
topic: Administration
topic-tags: forms
role: Admin, Developer
level: Beginner, Intermediate
contentOwner: khsingh
exl-id: e8406ed9-37f5-4f26-be97-ad042f9ca57c
source-git-commit: c2392932d1e29876f7a11bd856e770b8f7ce3181
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 85%

---

# Felsök den automatiserade konverteringstjänsten för formulär (AFCS)

Dokumentet innehåller grundläggande felsökningssteg för vanliga fel.

<!--The article provides information on installation, configuration and administration issues that may arise in an Automated Forms Conversion Service production environment. -->

## Vanliga fel {#commonerrors}

| Fel | Exempel |
|--- |--- |
| **Felmeddelande** <br> Sidhuvudets åtkomsttoken är inte tillgängligt. <br><br> **Orsak** <br> En administratör har skapat flera IMS-konfigurationer, eller så kan IMS-konfigurationen inte nå AFCS-tjänsten på Adobe-molnet. <br><br>**Lösning** <br> Om det finns flera konfigurationer tar du bort samtliga konfigurationer och [skapar en ny konfiguration](configure-service.md#obtainpubliccertificates). <br> Om det endast finns en konfiguration använder du **hälsokontroll** för att [kontrollera anslutningen](configure-service.md#createintegrationoption). | ![Sidhuvudets åtkomsttoken är inte tillgängligt](assets/invalid-ims-configurations.png) |
| **Felmeddelande** <br> Det går inte att ansluta till tjänsten.  <br><br>**Orsak** <br> Felaktig tjänst-URL eller ingen tjänst-URL anges i molntjänsterna för tjänsten Automated forms conversion (AFCS). <br><br>**Upplösning** <br> Korrigera [Tjänst-URL](configure-service.md#configure-the-cloud-service) i Automated forms conversion Service (AFCS) Cloud-tjänster. | ![Det går inte att ansluta till tjänsten.](assets/wrong-service-url-configured.png) |
| **Felmeddelande** <br> Tjänsten kunde inte konvertera formuläret.  <br><br>**Orsak** <br> Problem med din nätverksanslutning, tjänsten är inte tillgänglig på grund av planerat underhåll eller avbrott på Adobe-molnet. <br><br>**Lösning** <br> Lös problemen med nätverksanslutningen och kontrollera tjänstens status på https://status.adobe.com/ för att se planerade eller oplanerade avbrott. | ![Det går inte att ansluta till tjänsten.](assets/conversion-failure.png) |
| **Felmeddelande** <br> Antalet sidor är fler än 15.  <br><br>**Orsak** <br> Källformuläret består av fler än 15 sidor.  <br><br>**Lösning** <br> Använd Adobe Acrobat för att dela formulär med fler än 15 sidor. Minska antalet sidor i ett formulär till färre än 15. | ![Det går inte att ansluta till tjänsten.](assets/number-of-pages.png) |
| **Felmeddelande** <br> Antalet filer är fler än 15.  <br><br>**Orsak** <br>  Mappen innehåller fler än 15 formulär. <br><br>**Lösning** <br> Minska antalet formulär i mappen till färre än eller lika med 15. Minska det totala antalet sidor i en mapp till färre än 50. Minska mappens storlek till mindre än 10 MB. Lägg inte formulär i en undermapp. Organisera källformulären i en grupp med 8–15 formulär. | ![Det går inte att ansluta till tjänsten.](assets/number-of-pages.png) |
| **Felmeddelande** <br> Källfilsformatet stöds inte.  <br><br>**Orsak** <br> Mappen som innehåller källformulär har vissa filer som inte stöds. <br><br>**Lösning** <br> Tjänsten stöder endast .xdp- och .pdf-filer. Ta bort samtliga filer med andra filnamnstillägg från mappen och kör konverteringen. | ![Det går inte att ansluta till tjänsten.](assets/unsupported-file-formats.png) |
| **Felmeddelande** <br> Inskannade formulär stöds inte.  <br><br>**Orsak** <br> PDF-formuläret innehåller endast inskannade bilder av formuläret och innehåller ingen innehållsstruktur. <br><br>**Lösning** <br> Tjänsten stöder inte konvertering av inskannade formulär eller en bild av ett formulär till ett anpassningsbart färdigt formulär. Du kan dock använda Adobe Acrobat för att konvertera bilden av ett formulär till ett PDF-formulär. Sedan kan du använda tjänsten för att konvertera PDF-formuläret till ett anpassningsbart formulär. Använd alltid en högkvalitativ bild av formuläret för konvertering i Acrobat. Det förbättrar kvaliteten på konverteringen. | ![Det går inte att ansluta till tjänsten.](assets/scanned-forms-error.png) |
| **Felmeddelande** <br> Krypterat PDF-formulär stöds inte.  <br><br>**Orsak** <br>Mappen innehåller krypterade PDF-formulär. <br><br>**Lösning** <br> Tjänsten stöder inte konvertering av ett krypterat PDF-formulär till ett anpassningsbart färdigt formulär. Ta bort krypteringen, ladda upp det icke-krypterade formuläret och kör omvandlingen. | ![Det går inte att ansluta till tjänsten.](assets/secured-pdf-form.png) |
| **Felmeddelande** <br> Det går inte att analysera metamodellen av JSON-schemat.  <br><br>**Orsak** <br> JSON-schemat som tillhandahålls tjänsten är inte korrekt formaterat, innehåller ogiltiga tecken eller använder ogiltig syntax för att mappa komponenter.  <br><br>**Lösning** <br> Kontrollera JSON-filens formatering. Du kan använda valfri JSON-verifierare online för att kontrollera schemats formatering och struktur. Mer information om metamodellens syntax finns i artikeln [Utöka standardmetamodellen](extending-the-default-meta-model.md). | ![Det går inte att ansluta till tjänsten.](assets/invalid-meta-model-schema.png) |
| **Fel (endast lokala miljöer)** <br> The **[!UICONTROL Source Language]** alternativet listar inte rätt språk för ett adaptivt formulär. <br><br>**Orsak** <br> Egenskapen jcr:language för det adaptiva formuläret har inte angetts korrekt.  <br><br>**Upplösning** <br> Open CRX-DE lite, navigera till `/content/forms/af/`öppnar du `jcr:content` och ange ett värde för noden på rätt språk. En lista över språk som stöds finns i [Lägg till lokaliseringsstöd för språk som inte stöds](https://experienceleague.adobe.com/docs/experience-manager-65/forms/manage-administer-aem-forms/supporting-new-language-localization.html#add-localization-support-for-non-supported-locales). | ![Det går inte att ansluta till tjänsten.](assets/aem-forms-translation-project-language-unavailable.png) |

<!--

<table>
<thead>
<tr>
<th>Error</th>
<th>Example</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>Error Message</strong> <p> The access token header is not available. </p><br><strong>Reason</strong> <br> An administrator has created multiple IMS configurations or IMS configuration is not able to reach AFCS service on Adobe Cloud. <br><br><strong>Resolution</strong> <br> If there are multiple configurations, delete all the configurations and <a href="configure-service.md#obtainpubliccertificates">create a new configuration</a>. <br> If there is a single configuration, use <strong> Health Check </strong> to <a href="configure-service.md#createintegrationoption">check connectivity</a>.</td>
<td><img alt="The access token header is not available" src="assets/invalid-ims-configuration.png" /></td>
</tr>
<tr>
<td><strong>Error Message</strong> <br> Unable to connect to the service.  <br><br><strong>Reason</strong> <br> Incorrect service URL or no service URL is mentioned in Automated Forms Conversion Service (AFCS) cloud services. <br><br><strong>Resolution</strong> <br> Correct <a href="configure-service.md#configure-the-cloud-service">Service URL</a> in Automated Forms Conversion Service (AFCS) Cloud services.</td>
<td><img alt="Unable to connect to the service." src="assets/wrong-endpoint-configured.png" /></td>
</tr>
<tr>
<td><strong>Error Message</strong> <br> The service failed to convert the form.  <br><br><strong>Reason</strong> <br> Network connectivity issues at your end, the service is down due to scheduled maintenance, or outage on Adobe Cloud. <br><br><strong>Resolution</strong> <br> Resolve network connectivity issues at your end and check the status of the service on <a href="https://status.adobe.com/">https://status.adobe.com/</a> for a planned or unplanned outage.</td>
<td><img alt="The service failed to convert the form." src="assets/service-failure.png" /></td>
</tr>
<tr>
<td><strong>Error Message</strong> <br> The number of pages is more than 15.  <br><br><strong>Reason</strong> <br> The source form is more than 15 pages long.  <br><br><strong>Resolution</strong> <br> Use Adobe Acrobat to split forms with more than 15 pages. Bring the number of pages in a form to less than 15.</td>
<td><img alt="The number of pages is more than 15." src="assets/number-of-pages.png" /></td>
</tr>
<tr>
<td><strong>Error Message</strong> <br> The number of files is more than 15.  <br><br><strong>Reason</strong> <br>  The folder contains more than 15 forms. <br><br><strong>Resolution</strong> <br> Bring the number of forms in a folder to less than or equal to 15. Bring the total number of pages in a folder less than 50. Bring the size of the folder to less than 10 MB. Do not keep forms in a sub-folder. Organize source forms into a batch of 8-15 forms.</td>
<td><img alt="The number of files is more than 15." src="assets/number-of-pages.png" /></td>
</tr>
<tr>
<td><strong>Error Message</strong> <br> The source file format is not supported.  <br><br><strong>Reason</strong> <br> The folder containing source forms have some unsupported files. <br><br><strong>Resolution</strong> <br> The service supports only .xdp and .pdf files. Remove files with any other extension from the folder and run the conversion.</td>
<td><img alt="The source file format is not supported." src="assets/unsupported-file-formats.png" /></td>
</tr>
<tr>
<td><strong>Error Message</strong> <br> Scanned forms are not supported.  <br><br><strong>Reason</strong> <br> The PDF form contains only scanned images of the form and contains no content structure. <br><br><strong>Resolution</strong> <br> The service does not support converting scanned forms or an image of a form to an adaptive out-of-the-box. However, you use Adobe Acrobat to convert the image of a form to a PDF Form. Then, use the service to convert the PDF Form to an adaptive form. Always use a high-quality image of the form for conversion in Acrobat. It improves the quality of the conversion.</td>
<td><img alt="Scanned forms are not supported." src="assets/scanned-forms-error.png" /></td>
</tr>
<tr>
<td><strong>Error Message</strong> <br> Encrypted PDF form is not supported.  <br><br><strong>Reason</strong> <br> The folder contains encrypted PDF forms. <br><br><strong>Resolution</strong> <br> The service does not support converting an encrypted PDF form to an adaptive form. Remove the encryption, upload the non-encrypted form, and run the conversion.</td>
<td><img alt="Encrypted PDF form is not supported." src="assets/secured-pdf-form.png" /></td>
</tr>
<tr>
<td><strong>Error Message</strong> <br> Unable to parse meta-model JSON schema.  <br><br><strong>Reason</strong> <br> The JSON schema supplied to the service is not properly formatted, contains invalid characters, or uses invalid syntax to map components.  <br><br><strong>Resolution</strong> <br> Check the formatting of the JSON file. You can use any online JSON validator to check the formatting and structure of the schema. See, <a href="extending-the-default-meta-model.md">Extend the default meta-model</a> article for information on meta-model syntax.</td>
<td><img alt="Unable to parse meta-model JSON schema" src="assets/invalid-meta-model-schema.png" /></td>
</tr>
</tbody>
</table>
-->
