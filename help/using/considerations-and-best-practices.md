---
title: Bästa praxis och överväganden
description: PUBLICERA INTE
seo-description: DO NOT PUBLISH
page-status-flag: never-activated
uuid: c2821264-39e2-44f8-b234-835c46f33fd5
topic-tags: introduction
discoiquuid: b786e40a-202e-4e17-a2f5-1f77c46538c2
privatebeta: true
index: false
source-git-commit: c2392932d1e29876f7a11bd856e770b8f7ce3181
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 3%

---


# Bästa praxis och överväganden {#do-not-publish-best-practices-and-considerations}

<!--
[DO NOT PUBLISH]
-->

AEM Forms tjänst för automatisk konvertering konverterar ett PDF-formulär till ett anpassningsbart formulär. Tjänsten använder artificiell intelligens och maskininlärningsalgoritmer för att förstå källformulärets layout och fält. Alla maskininlärningstjänster lär sig kontinuerligt av källdata och skapar bättre resultat vid varje förändring. Dessa tjänster lär sig av upplevelser som människor.

Automated forms conversion-tjänsten (AFCS) har utbildats på ett stort antal formulär. Den identifierar enkelt fält i ett källformulär och skapar anpassningsbara formulär. Det finns dock vissa fält och format i PDF forms som är lätta att se för det mänskliga ögat men svåra att förstå för tjänsten. Tjänsten kan tilldela vissa fält eller format andra än tillämpliga fälttyper eller paneler. Alla sådana fält- och formatmönster listas nedan.

Tjänsten börjar identifiera och tilldela rätt fält eller paneler till dessa mönster när den lär sig av källdata. Du kan använda [Granska och korrigera](review-correct-ui-edited.md) för att åtgärda sådana problem. Innan du börjar åtgärda problemen eller läser mer, bekanta dig med [adaptiva formulärkomponenter](https://helpx.adobe.com/experience-manager/6-5/forms/using/introduction-forms-authoring.html).

## Allmänt {#general}

<table border="1" cellpadding="1" cellspacing="0" style="border-collapse: separate; border-spacing: 0px;" width="100%"> 
 <tbody>
  <tr>
   <td width="30%">Kända mönster och upplösning</td> 
   <td width="70%">Exempel</td> 
  </tr>
   <td><p><strong>Mönster</strong></p> <p>Tjänsten konverterar inte ifyllt PDF forms till anpassningsbara formulär.</p> <p> </p> <p><strong>Upplösning</strong></p> <p>Använd tomma adaptiva formulär.</p> </td> 
   <td style="text-align: left;"><img src="assets/pre-filled-form.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>Mönster</strong></p> <p>Tjänsten kan inte identifiera text och fält i tätt format.</p> <p> </p> <p><strong>Upplösning</strong></p> <p>Öka bredden mellan text och fält i ett kompakt formulär innan konverteringen startar.</p> </td> 
   <td style="text-align: left;"><img src="assets/dense%20form.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>Mönster</strong></p> <p>Tjänsten stöder inte skannade formulär.</p> <p> </p> <p><strong>Upplösning</strong></p> <p>Använd inte skannade formulär. </p> </td> 
   <td><img src="assets/scanned-form.jpg" /></td> 
  </tr>
  <tr>
   <td><p><strong>Mönster</strong></p> <p>Tjänsten extraherar inte bilder och text i bilder. </p> <p> </p> <p><strong>Upplösning</strong></p> <p>Lägg till bilder eller text manuellt i konverterade formulär.</p> </td> 
   <td><img src="assets/image-in-adaptive-form.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>Mönster</strong></p> <p>Tabeller med prickade eller otydliga gränser och kanter konverteras inte.</p> <p><strong>Upplösning</strong></p> <p>Använd tabeller med tydliga gränser och ramar. stöds.</p> </td> 
   <td><img src="assets/border-less-tables.png" /></td> 
  </tr>
 </tbody>
</table>

## Urvalsgrupp  {#choice-group}

<table border="1" cellpadding="1" cellspacing="0" width="100%"> 
 <tbody>
  <tr>
   <td width="30%">Mönster</td> 
   <td width="70%">Exempel</td> 
  </tr>
  <tr>
   <td><p><strong>Mönster</strong></p> <p>Alternativ för alternativgrupper med andra former än rutor och cirklar konverteras inte till motsvarande adaptiva formulärkomponenter. </p> <p> </p> <p><strong>Upplösning</strong></p> <p>Ändra former för alternativ till ruta eller cirkel eller använd Gransknings- och korrigeringsredigeraren för att identifiera formerna.</p> </td> 
   <td><img src="assets/shaded-box-patterns.png" /> </td> 
  </tr>
 </tbody>
</table>

## Formulärfält {#form-fields}

<table border="1" cellpadding="1" cellspacing="0" width="100%"> 
 <tbody>
  <tr>
   <td width="30%">Mönster</td> 
   <td width="70%">Exempel</td> 
  </tr>
  <tr>
   <td width="25%"><p><strong>Mönster</strong></p> <p>Tjänsten identifierar inte fält utan tydliga gränser.</p> <p> </p> <p><strong>Upplösning</strong></p> <p>Använd Gransknings- och Korrigera-redigeraren för att identifiera sådana fält.</p> <p> </p> <p> </p> </td> 
   <td width="50%"><br /> <img src="assets/fields-without-clear-borders.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>Mönster</strong></p> <p>Tjänsten lämnar vissa formulärfält med beskrivningar längst ned eller till höger oidentifierade.</p> <p> </p> <p><strong>Upplösning</strong></p> <p>Använd gransknings- och korrigeringsredigeraren för att identifiera sådana fält</p> </td> 
   <td><br /> <img src="assets/forms-with-clear-borders-scale.png" /><br /> </td> 
  </tr>
  <tr>
   <td><p><strong>Mönster</strong></p> <p>Tjänsten sammanfogar eller tilldelar fel typ till vissa formulärfält som är placerade mycket nära varandra eller som inte har några tydliga kantlinjer. </p> <p> </p> <p><strong>Upplösning</strong></p> <p>Använd Gransknings- och Korrigera-redigeraren för att identifiera sådana fält.</p> </td> 
   <td><img src="assets/forms-with-fields-placed-nearby.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>Mönster</strong></p> <p>Tjänsten kan inte identifiera fält med långt borta bildtexter eller en prickad linje mellan bildtexten och inmatningsfältet.</p> <p> </p> <p><strong>Upplösning</strong></p> <p>Använd formulärfält med tydliga gränser eller använd Gransknings- och Korrigeringsredigerare för att åtgärda sådana problem.</p> </td> 
   <td><img src="assets/form-fields-with-far-away-captions.png" /></td> 
  </tr>
 </tbody>
</table>

## Listor {#lists}

<table border="1" cellpadding="1" cellspacing="0" width="100%"> 
 <tbody>
  <tr>
   <td width="30%">Mönster</td> 
   <td width="70%">Exempel</td> 
  </tr>
  <tr>
   <td><p><strong>Mönster</strong></p> <p>Listor som innehåller formulärfält sammanfogas eller konverteras inte till motsvarande adaptiva formulärkomponenter</p> <p><strong>Upplösning</strong></p> <p>Använd formulärfält med tydliga gränser eller använd Gransknings- och Korrigeringsredigerare för att åtgärda sådana problem.</p> </td> 
   <td><img src="assets/lists-with-fields.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>Mönster</strong></p> <p>Tjänsten kan lämna några kapslade listor oidentifierade</p> <p> </p> <p><strong>Upplösning</strong></p> <p>Använd Gransknings- och Korrigera-redigeraren för att åtgärda sådana problem.</p> </td> 
   <td><img src="assets/nested-lists.png" /> </td> 
  </tr>
  <tr>
   <td><p><strong>Mönster</strong></p> <p>Tjänsten sammanfogar vissa listor som innehåller urvalsgrupper med varandra</p> <p><strong>Upplösning</strong></p> <p>Använd Gransknings- och Korrigera-redigeraren för att åtgärda sådana problem.</p> </td> 
   <td><img src="assets/lists-containing-choice-groups.png" /> </td> 
  </tr>
 </tbody>
</table>

<!--
Comment Type: draft

<h3>Choice groups</h3>
-->

<!--
Comment Type: draft

<ul>
<li>Lists with form fields, nested lists, and nested choice groups are not supported.</li>
<li>Form fields with captions at bottom or right are not supported.</li>
<li>Form fiields without bordes are not supported.</li>
<li>Hidden form fields are not supported.</li>
<li>Button in PDF forms are not converted to adaptive form buttons.<br /> </li>
<li>Tables with clear explicit boundaries and borders are supported.</li>
<li>Fields with far away captions are not supported.<br /> </li>
<li>Choice groups with only box or circle shaped selectors are supported. </li>
</ul>
-->

