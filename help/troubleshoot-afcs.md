---
title: 'Felsöka automatisk formulärkonverteringstjänst '
seo-title: 'Felsöka automatisk formulärkonverteringstjänst (AFCS) '
description: 'Vanliga AFCS-problem och deras lösningar '
seo-description: Vanliga AFCS-problem och deras lösningar
contentOwner: khsingh
topic-tags: forms
translation-type: tm+mt
source-git-commit: 56e4696c0372223e0b27f1c313382a2a637b6db1

---


# Felsöka automatisk formulärkonverteringstjänst


<!--The article provides information on installation, configuration and administration issues that may arise in an Automated Forms Conversion Service production environment. --> The document  provides basic troubleshooting steps for common errors.

## Vanliga fel {#commonerrors}
<!--
|Error|Example|
|--- |--- |
|**Error Message** <br> The access token header is not available. <br><br>**Reason** <br> An administrator has created multiple IMS configurations or IMS configuration is not able to reach AFCS service on Adobe Cloud. <br><br>**Resolution** <br> If there are multiple configurations, delete all the configurations and [create a new configuration](configure-service.md#obtainpubliccertificates). <br> If there is a single configuration, use **[!UICONTROL Health Check]** to [check connectivity](configure-service.md#createintegrationoption).|![The access token header is not available](assets/invalid-ims-configuration.png)|
|**Error Message** <br> Unable to connect to the service.  <br><br>**Reason** <br> Incorrect service URL or no service URL is mentioned in Automated Forms Conversion Service cloud services. <br><br>**Resolution** <br> Correct [Service URL](configure-service.md#configure-the-cloud-service) in Automated Forms Conversion Service Cloud services.|![Unable to connect to the service.](assets/wrong-endpoint-configured.png)|
|**Error Message** <br> The service failed to convert the form.  <br><br>**Reason** <br> Network connectivity issues at your end, the service is down due to scheduled maintenance, or outage on Adobe Cloud. <br><br>**Resolution** <br> Resolve network connectivity issues at your end and check the status of the service on https://status.adobe.com/ for a planned or unplanned outage.|![Unable to connect to the service.](assets/service-failure.png)|
|**Error Message** <br> The number of pages is more than 15.  <br><br>**Reason** <br> The source form is more than 15 pages long.  <br><br>**Resolution** <br> Use Adobe Acrobat to split forms with more than 15 pages. Bring the number of pages in a form to less than 15. |![Unable to connect to the service.](assets/number-of-pages.png)|
|**Error Message** <br> The number of files is more than 15.  <br><br>**Reason** <br>  The folder contains more than 15 forms. <br><br>**Resolution** <br> Bring the number of forms in a folder to less than or equal to 15. Bring the total number of pages in a folder less than 50. Bring the size of the folder to less than 10 MB. Do not keep forms in a sub-folder. Organize source forms into a batch of 8-15 forms. |![Unable to connect to the service.](assets/number-of-pages.png)|
|**Error Message** <br> The source file format is not supported.  <br><br>**Reason** <br> The folder containing source forms have some unsupported files. <br><br>**Resolution** <br> The service supports only .xdp and .pdf files. Remove files with any other extension from the folder and run the conversion. |![Unable to connect to the service.](assets/unsupported-file-formats.png)|
|**Error Message** <br> Scanned forms are not supported.  <br><br>**Reason** <br> The PDF form contains only scanned images of the form and contains no content structure. <br><br>**Resolution** <br> The service does not support converting scanned forms or an image of a form to an adaptive out-of-the-box. However, you use Adobe Acrobat to convert the image of a form to a PDF Form. Then, use the service to convert the PDF Form to an adaptive form. Always use a high-quality image of the form for conversion in Acrobat. It improves the quality of the conversion. |![Unable to connect to the service.](assets/scanned-forms-error.png)|
|**Error Message** <br> Encrypted PDF form is not supported.  <br><br>**Reason** <br> The folder contains encrypted PDF forms. <br><br>**Resolution** <br> The service does not support converting an encrypted PDF form to an adaptive form. Remove the encryption, upload the non-encrypted form, and run the conversion. |![Unable to connect to the service.](assets/secured-pdf-form.png)|
|**Error Message** <br> Unable to parse meta-model JSON schema.  <br><br>**Reason** <br> The JSON schema supplied to the service is not properly formatted, contains invalid characters, or uses invalid syntax to map components.  <br><br>**Resolution** <br> Check the formatting of the JSON file. You can use any online JSON validator to check the formatting and structure of the schema. See, [Extend the default meta-model](extending-the-default-meta-model.md) article for information on meta-model syntax. |![Unable to connect to the service.](assets/invalid-meta-model-schema.png)| -->

<table>
<thead>
<tr>
<th>Fel</th>
<th>Exempel</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>Felmeddelande</strong> <br> Åtkomsttokenhuvudet är inte tillgängligt. <br><br><strong>Orsak</strong> till att <br> en administratör har skapat flera IMS-konfigurationer eller att IMS-konfigurationen inte kan nå AFCS-tjänsten på Adobe Cloud. <br><br><strong>Upplösning</strong> <br> Om det finns flera konfigurationer tar du bort alla konfigurationer och <a href="configure-service.md#obtainpubliccertificates">skapar en ny konfiguration</a>. <br> Om det finns en enda konfiguration använder du <strong>[!UICONTROL Health Check]</strong> för att <a href="configure-service.md#createintegrationoption">kontrollera anslutningen</a>.</td>
<td><img alt="Åtkomsttokenhuvudet är inte tillgängligt" src="assets/invalid-ims-configuration.png" /></td>
</tr>
<tr>
<td><strong>Felmeddelande</strong> <br> Det gick inte att ansluta till tjänsten.  <br><br><strong>Orsak</strong> <br> till felaktig tjänst-URL eller ingen tjänst-URL anges i molntjänsterna för automatisk formulärkonvertering. <br><br><strong>URL</strong> för <br> tjänsten <a href="configure-service.md#configure-the-cloud-service">Korrigera upplösning</a> i molntjänster för automatisk formulärkonvertering.</td>
<td><img alt="Det går inte att ansluta till tjänsten." src="assets/wrong-endpoint-configured.png" /></td>
</tr>
<tr>
<td><strong>Felmeddelande</strong> <br> Tjänsten kunde inte konvertera formuläret.  <br><br><strong>Orsak</strong> till att <br> nätverksanslutningsproblem uppstår när du avslutar tjänsten på grund av planerat underhåll eller driftstopp i Adobe Cloud. <br><br><strong>Upplösning</strong> Lös problem med nätverksanslutningen när du är klar och kontrollera tjänstens status på <br> https://status.adobe.com/ <a href="https://status.adobe.com/"></a> för ett planerat eller oplanerat avbrott.</td>
<td><img alt="Tjänsten kunde inte konvertera formuläret." src="assets/service-failure.png" /></td>
</tr>
<tr>
<td><strong>Felmeddelande</strong> <br> Antalet sidor är fler än 15.  <br><br><strong>Orsak</strong> till att <br> källformuläret är längre än 15 sidor.  <br><br><strong>Upplösning</strong> <br> Använd Adobe Acrobat för att dela upp formulär med mer än 15 sidor. Använd färre än 15 sidor i ett formulär.</td>
<td><img alt="Antalet sidor är fler än 15." src="assets/number-of-pages.png" /></td>
</tr>
<tr>
<td><strong>Felmeddelande</strong> <br> Antalet filer är fler än 15.  <br><br><strong>Orsak</strong> <br> : Mappen innehåller fler än 15 formulär. <br><br><strong>Upplösning</strong> Använd <br> 15 för att ställa in antalet formulär i en mapp. Det totala antalet sidor i en mapp är mindre än 50. Minska mappens storlek till mindre än 10 MB. Behåll inte formulär i en undermapp. Organisera källformulären i en batch på 8-15 formulär.</td>
<td><img alt="Antalet filer är fler än 15." src="assets/number-of-pages.png" /></td>
</tr>
<tr>
<td><strong>Felmeddelande</strong> <br> Källfilformatet stöds inte.  <br><br><strong>Orsak</strong> <br> : Mappen som innehåller källformulär har filer som inte stöds. <br><br><strong>Upplösning</strong> <br> Tjänsten stöder bara .xdp- och .pdf-filer. Ta bort filer med andra tillägg från mappen och kör konverteringen.</td>
<td><img alt="Källfilformatet stöds inte." src="assets/unsupported-file-formats.png" /></td>
</tr>
<tr>
<td><strong>Felmeddelande</strong><br> för skannade formulär stöds inte.  <br><br><strong>Orsak</strong> <br> : PDF-formuläret innehåller bara skannade bilder av formuläret och innehåller ingen innehållsstruktur. <br><br><strong>Upplösning</strong> <br> Tjänsten stöder inte konvertering av skannade formulär eller en bild av ett formulär till ett anpassat, körklart formulär. Du kan dock använda Adobe Acrobat för att konvertera bilden av ett formulär till ett PDF-formulär. Använd sedan tjänsten för att konvertera PDF-formuläret till ett anpassat formulär. Använd alltid en högkvalitativ bild av formuläret för konvertering i Acrobat. Det förbättrar kvaliteten på konverteringen.</td>
<td><img alt="Skannade formulär stöds inte." src="assets/scanned-forms-error.png" /></td>
</tr>
<tr>
<td><strong>Felmeddelandets</strong> krypterade PDF-formulär <br> stöds inte.  <br><br><strong>Orsak</strong> : <br> Mappen innehåller krypterade PDF-formulär. <br><br><strong>Upplösning</strong> <br> Tjänsten stöder inte konvertering av krypterade PDF-formulär till adaptiva formulär. Ta bort krypteringen, ladda upp det okrypterade formuläret och kör konverteringen.</td>
<td><img alt="Krypterat PDF-formulär stöds inte." src="assets/secured-pdf-form.png" /></td>
</tr>
<tr>
<td><strong>Felmeddelande</strong> <br> Det gick inte att parsa JSON-schema av metamodell.  <br><br><strong>Orsak</strong> <br> till att JSON-schemat som tillhandahålls till tjänsten inte är korrekt formaterat, innehåller ogiltiga tecken eller använder ogiltig syntax för att mappa komponenter.  <br><br><strong>Upplösning</strong> Kontrollera <br> JSON-filens formatering. Du kan använda valfri JSON-validerare online för att kontrollera schemats formatering och struktur. Mer information om metamodellsyntax finns i <a href="extending-the-default-meta-model.md">Utöka artikeln med metamodellen</a> som standard.</td>
<td><img alt="Det gick inte att parsa JSON-schemat för metamodellen" src="assets/invalid-meta-model-schema.png" /></td>
</tr>
</tbody>
</table>
