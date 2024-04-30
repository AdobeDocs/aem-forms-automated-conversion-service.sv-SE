---
title: Kända fel
description: Kända problem och begränsningar för tjänsten Automated forms conversion (AFCS)
solution: Experience Manager Forms
feature: Adaptive Forms
topic: Administration
topic-tags: introduction
role: Admin, Developer
level: Beginner, Intermediate
exl-id: 35f59e02-e38e-473a-94c8-123e0a85ac8e
source-git-commit: c2392932d1e29876f7a11bd856e770b8f7ce3181
workflow-type: tm+mt
source-wordcount: '789'
ht-degree: 0%

---

# Kända fel och begränsningar {#known-issues-limitations}

Innan du börjar använda tjänsten AEM Forms Automated forms conversion (AFCS) bör du läsa igenom följande kända problem och begränsningar:

## Kända fel {#known-issues}

* Mappen som innehåller formulär för konvertering får inte innehålla fler än 15 formulär och totalt 50 sidor. Källmappens storlek får inte överstiga 10 MB. Skapa inte undermappar i källmappen.
* Vissa formulärobjekt är lätt synliga för det mänskliga ögat men är [svårt att identifiera för tjänsten](styles-and-pattern-considerations-and-best-practices.md). Använd [Granska och korrigera redigerare](review-correct-ui-edited.md) för att identifiera och konvertera sådana formulärobjekt.
* Gransknings- och korrigeringsredigerare:

   * Har inte ångra-åtgärd. Med knappen Spara sparas ändringarna permanent.
   * Har inte stöd för repeterbara paneler för XFA-baserat formulär.
   * Om du ändrar en lista i en tabell med redigeraren Granska och Korrigera justeras inte radbredden automatiskt och texten kan flyttas till nästa rad i tabellen.
   * The **[!UICONTROL Auto-detect multi-column layout from input forms]** fungerar inte med gransknings- och korrigeringsredigerare samt formulärfragment.
   * Skriptsignatur som skapats med Gransknings- och Korrigeringsredigerare kan inte läsas in för publicerade adaptiva formulär.


* För XFA-baserade formulär:
   * Extrahering av fragment från ett XFA-baserat formulär stöds inte.
   * XFA-skript stöds inte. Skript för att automatiskt generera värden för en nedrullningsbar komponent.
   * Metamodellen fungerar inte för alternativgruppen
   * Alternativet för alternativgrupper med ett enda tecken identifieras inte
   * När källdokumentet är en dynamisk XFA-fil (.XDP) och den [definierar beteendet för XFA-egenskaper i ett adaptivt formulär](https://helpx.adobe.com/experience-manager/6-5/forms/using/xfa-api-supported-in-adaptive-form.html#supportedxfaelementsandtheirmappinginadaptiveformsbr)och egenskapen presence i källdokumentet inte respekteras. Ett fält i källdokumentet är t.ex. dolt och ett skript gör fältet synligt. Fältet förblir synligt i det anpassningsbara utdataformuläret.

* När du använder **Använd AcroForm som DoR (Document of Record) för genererade adaptiva formulär** kan du göra något av följande:

<table>
    <tr>
        <td>Bindning och data förloras för sammansatta textfält. Ett sammansatt textfält har flera textrutor justerade efter varandra. I ett AcroForm-formulär delas till exempel ett kreditkortsnummer upp i flera textrutor och varje textruta har en separat bindning. När AcroForm konverteras till adaptiv form har det konverterade adaptiva formuläret en enda bindning för alla textrutor. Du kan lösa det genom att ändra AcroForm-formuläret så att det använder en enda textruta för att ta emot kreditkortsnummer innan du konverterar ett AcroForm-formulär till ett anpassat formulär.</td>
        <td><img  src="assets/creditCard_Composite.png"/>                                                            </td>
    </tr>
    <tr>
        <td>Bindning och data förloras för sammansatta datumfält. Ett sammansatt datumfält består av tre olika fält. Ett födelsedatumfält i ett AcroForm delas till exempel upp i tre separata fält. Det adaptiva formuläret innehåller en datumväljarkomponent som är klar att användas. Om du vill använda datumväljarkomponenten i det adaptiva formuläret men behålla bindningen för AcroForm, innan du konverterar ett AcroForm till ett adaptivt formulär, ändrar du AcroForm så att ett enda datumfält används.</td>
        <td><img  src="assets/CompositeDateField.png"/></td>
    </tr>
    <tr>
        <td>Om kryssrutorna är större än den tillhörande texten, identifieras inte kryssrutorna och bindningen i AcroForm försvinner. Ändra AcroForm så att storleken på kryssrutorna blir mindre än den tillhörande texten.</td>
        <td><img  src="assets/large-text-box.png"/><br/><img  src="assets/small-text-box.png"/></td>
    </tr>
    <tr>
        <td>Om indatafälten inte är justerade mot motsvarande textfält, identifieras inte indatafältet.  </td>
        <td><img  src="assets/non-alingned-fields.png"/></td>
    </tr>
    <tr >
        <td>Tjänsten konverterar alla kryssrutor i ett AcroForm till separata urvalsgrupper. Separata urvalsgrupper skapas för att bevara bindningar med AcroForm. Sammanfoga inte urvalsgrupper i den anpassningsbara formen. Det kommer att leda till förlust av bindningar. Om du sammanfogar urvalsgrupperna konverterar du formuläret igen för att återta de förlorade bindningarna. </td>
        <td></td>
    </tr>
    <tr >
        <td>Gränser för vissa tabeller utökas från sidan i automatiskt genererat postdokument (DoR). </td>
        <td></td>
    </tr>
</table>

## Begränsningar {#limitations}

* PDF forms med komplex dynamisk layout, fält med prickad kontur eller fyllda fält stöds inte.
* Bilder och text i bilderna identifieras inte. Lägg till bilder manuellt i konverterade formulär.
* XDP-dokument för teckningar stöds inte.
* PDF forms som är större än 15 sidor stöds inte.
* Krypterade, lösenordsskyddade och skyddade dokument konverteras inte. Ta bort kryptering eller lösenord innan konverteringen körs.
* Komplexa tabeller som tabeller utan kanter, kapslade tabeller och tabeller med platshållarvärden stöds inte. Använd adaptiv formulärredigerare för att lägga till eller ändra komplexa tabeller efter konverteringen. Endast enkla tabeller med tomma fält, korrekta rubriker och tydliga gränser stöds.
* Tjänsten konverterar endast engelska, franska, tyska, spanska, italienska och portugisiska till anpassningsbara blanketter. Du kan översätta konverterade adaptiva formulär till ett annat språk med [Arbetsflöde för AEM](https://helpx.adobe.com/experience-manager/6-5/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.html).
* AEM 6.4 Forms stöder inte automatisk detektering av flerkolumnslayout för indataformulär.
* Information som kodats med PDF i källformat överförs inte till adaptiv form.
* Färger på PDF-källformen överförs inte till anpassningsbara formulärteman.
* Färgat PDF forms behandlas som gråskaleformulär och fält identifieras därefter.
