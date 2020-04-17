---
title: 'Felsöka automatisk formulärkonverteringstjänst '
seo-title: 'Felsöka automatisk formulärkonverteringstjänst (AFCS) '
description: 'Vanliga AFCS-problem och deras lösningar '
seo-description: Vanliga AFCS-problem och deras lösningar
contentOwner: khsingh
topic-tags: forms
translation-type: tm+mt
source-git-commit: c413c5dc2da3a3e7e116b3355c63620f9dab17f8

---


# Felsöka automatisk formulärkonverteringstjänst

Dokumentet innehåller grundläggande felsökningssteg för vanliga fel.

<!--The article provides information on installation, configuration and administration issues that may arise in an Automated Forms Conversion Service production environment. -->

## Vanliga fel {#commonerrors}

| Fel | Exempel |
|--- |--- |
| **Felmeddelande** <br> Åtkomsttokenhuvudet är inte tillgängligt. <br><br> **Orsak** till att <br> en administratör har skapat flera IMS-konfigurationer eller att IMS-konfigurationen inte kan nå AFCS-tjänsten på Adobe Cloud. <br><br>**Upplösning **<br>Om det finns flera konfigurationer tar du bort alla konfigurationer och[skapar en ny konfiguration](configure-service.md#obtainpubliccertificates).<br>Om det finns en enda konfiguration använder du** Hälsokontroll **för att[kontrollera anslutningen](configure-service.md#createintegrationoption). | ![Åtkomsttokenhuvudet är inte tillgängligt](assets/invalid-ims-configurations.png) |
| **Felmeddelande** <br> Det gick inte att ansluta till tjänsten.  <br><br>**Orsak **<br>till felaktig tjänst-URL eller ingen tjänst-URL anges i molntjänsterna för automatisk formulärkonvertering.<br><br>**URL** för <br> tjänsten [Korrigera upplösning](configure-service.md#configure-the-cloud-service) i molntjänster för automatisk formulärkonvertering. | ![Det går inte att ansluta till tjänsten.](assets/wrong-service-url-configured.png) |
| **Felmeddelande** <br> Tjänsten kunde inte konvertera formuläret.  <br><br>**Orsak **till att<br>nätverksanslutningsproblem uppstår när du avslutar tjänsten på grund av planerat underhåll eller driftstopp i Adobe Cloud.<br><br>**Upplösning** <br> Lös problem med nätverksanslutningen när du är klar och kontrollera statusen för tjänsten på https://status.adobe.com/ för ett planerat eller oplanerat avbrott. | ![Det går inte att ansluta till tjänsten.](assets/conversion-failure.png) |
| **Felmeddelande** <br> Antalet sidor är fler än 15.  <br><br>**Orsak **till att<br>källformuläret är längre än 15 sidor.<br><br>**Upplösning** <br> Använd Adobe Acrobat för att dela upp formulär med mer än 15 sidor. Använd färre än 15 sidor i ett formulär. | ![Det går inte att ansluta till tjänsten.](assets/number-of-pages.png) |
| **Felmeddelande** <br> Antalet filer är fler än 15.  <br><br>**Orsak **<br>: Mappen innehåller fler än 15 formulär.<br><br>**Upplösning** Använd <br> 15 för att ställa in antalet formulär i en mapp. Det totala antalet sidor i en mapp är mindre än 50. Minska mappens storlek till mindre än 10 MB. Behåll inte formulär i en undermapp. Organisera källformulären i en batch på 8-15 formulär. | ![Det går inte att ansluta till tjänsten.](assets/number-of-pages.png) |
| **Felmeddelande** <br> Källfilformatet stöds inte.  <br><br>**Orsak **<br>: Mappen som innehåller källformulär har filer som inte stöds.<br><br>**Upplösning** <br> Tjänsten stöder bara .xdp- och .pdf-filer. Ta bort filer med andra tillägg från mappen och kör konverteringen. | ![Det går inte att ansluta till tjänsten.](assets/unsupported-file-formats.png) |
| **Felmeddelande**<br> för skannade formulär stöds inte.  <br><br>**Orsak **<br>: PDF-formuläret innehåller bara skannade bilder av formuläret och innehåller ingen innehållsstruktur.<br><br>**Upplösning** <br> Tjänsten stöder inte konvertering av skannade formulär eller en bild av ett formulär till ett anpassat, körklart formulär. Du kan dock använda Adobe Acrobat för att konvertera bilden av ett formulär till ett PDF-formulär. Använd sedan tjänsten för att konvertera PDF-formuläret till ett anpassat formulär. Använd alltid en högkvalitativ bild av formuläret för konvertering i Acrobat. Det förbättrar kvaliteten på konverteringen. | ![Det går inte att ansluta till tjänsten.](assets/scanned-forms-error.png) |
| **Felmeddelandets** krypterade PDF-formulär <br> stöds inte.  <br><br>**Orsak **:<br>Mappen innehåller krypterade PDF-formulär.<br><br>**Upplösning** <br> Tjänsten stöder inte konvertering av krypterade PDF-formulär till adaptiva formulär. Ta bort krypteringen, ladda upp det okrypterade formuläret och kör konverteringen. | ![Det går inte att ansluta till tjänsten.](assets/secured-pdf-form.png) |
| **Felmeddelande** <br> Det gick inte att parsa JSON-schema av metamodell.  <br><br>**Orsak **<br>till att JSON-schemat som tillhandahålls till tjänsten inte är korrekt formaterat, innehåller ogiltiga tecken eller använder ogiltig syntax för att mappa komponenter.<br><br>**Upplösning** Kontrollera <br> JSON-filens formatering. Du kan använda valfri JSON-validerare online för att kontrollera schemats formatering och struktur. Mer information om metamodellsyntax finns i [Utöka artikeln med metamodellen](extending-the-default-meta-model.md) som standard. | ![Det går inte att ansluta till tjänsten.](assets/invalid-meta-model-schema.png) |

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
<td><strong>Error Message</strong> <br> Unable to connect to the service.  <br><br><strong>Reason</strong> <br> Incorrect service URL or no service URL is mentioned in Automated Forms Conversion Service cloud services. <br><br><strong>Resolution</strong> <br> Correct <a href="configure-service.md#configure-the-cloud-service">Service URL</a> in Automated Forms Conversion Service Cloud services.</td>
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