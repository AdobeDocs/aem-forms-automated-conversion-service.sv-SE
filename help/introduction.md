---
title: Introduktion
description: 'Snabba upp konverteringen av tryckta blanketter till anpassningsbara blanketter '
translation-type: tm+mt
source-git-commit: ef5789dabccc65dcf988b9424b435aa036017691

---


# Introduktion {#introduction-to-automated-forms-conversion-service}

Tjänsten Automated Forms Conversion snabbar upp digitaliseringen och moderniseringen av datainhämtningen genom automatiserad konvertering av PDF-formulär till anpassningsbara formulär. Tjänsten, som drivs av Adobe Sensei, konverterar automatiskt dina PDF-formulär till enhetsvänliga, responsiva och HTML5-baserade adaptiva formulär. Med hjälp av de befintliga investeringarna i PDF-formulär och XFA lägger tjänsten även till lämpliga valideringar, format och layout i anpassningsbara formulärfält under konverteringen. Tjänsten hjälper till att

* Spara manuell arbetsinsats som krävs för att konvertera tryckta formulär till anpassningsbara formulär
* Tillämpar mönster och lämpliga valideringar under konverteringen
* Generera dokument för post under konvertering
* Gruppera ofta förekommande fält i återanvändbara formulärfragment
* Aktiverar Adobe Analytics under konverteringen

![Det är enkelt. Du ger oss bara källformulären och låter oss ta hand om allt. Vi kommer att ge dig vackra, anpassningsbara formulär. Naturligtvis kommer du att njuta av resultatet som du är nöjd med. ](assets/pdf-to-adaptive-form-gitx50.gif)

## Onboarding {#onboarding}

Tjänsten är kostnadsfri för kunder som har AEM 6.5 Forms On-Premise och Adobe Managed Service Enterprise. Du kan kontakta Adobes säljteam eller din Adobe-representant för att få tillgång till tjänsten.

Adobe ger åtkomst till din organisation och ger de behörigheter som krävs till den person som är utsedd som administratör i din organisation. Administratören kan ge AEM Forms-utvecklare (användare) i organisationen åtkomst till tjänsten. Mer information finns i [Konfigurera tjänsten](configure-service.md) Automated Forms Conversion.

## PDF-formulär och -språk som stöds {#supported-languages-and-pdf-forms}

Tjänsten stöder icke-interaktiva PDF-formulär, formulär som skapats med Adobe Acrobat som kallas AcroForms och XFA-baserade formulär som skapats med AEM Forms eller Adobe LiveCycle.

Tjänsten kan endast konvertera engelska formulär till anpassningsbara formulär. Du kan översätta de genererade anpassningsbara formulären till ett annat språk med hjälp av arbetsflödet [för](https://helpx.adobe.com/experience-manager/6-5/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.html)AEM-översättning.

## Arbetsflöde för konvertering {#conversion-workflow}

Tjänsten Automated Forms Conversion körs i Adobe Cloud. Du ansluter din AEM-instans till tjänsten, överför formulär till din AEM-instans och påbörjar konverteringen. Den fullständiga konverteringsprocessen visas nedan:

![Arbetsflöde](assets/conversion-workflow.png)

### 1.Konfigurera miljön {#set-up-the-environment}

Tjänsten Automated Forms Conversion körs i Adobe Cloud. [Konfigurera ditt företags Adobe I/O-konto och anslut din lokala AEM-instans](configure-service.md) till den konverteringstjänst som körs i Adobe Cloud.

### 2. Konvertera PDF-formulär till anpassningsbara formulär {#use-the-conversion-service}

När AEM Forms-miljön har konfigurerats kan du konvertera PDF-formulär till adaptiva formulär, [överföra PDF-formulär](convert-existing-forms-to-adaptive-forms.md) till din AEM-instans och [starta konverteringen](convert-existing-forms-to-adaptive-forms.md#run-the-conversion). Innan du överför formulären bör du tänka på följande:

* Överför inte skyddade formulär. Tjänsten konverterar inte lösenordsskyddade och krypterade formulär.
* Överför inte skannade, färgade, icke-engelska och ifyllda formulär. Sådana formulär stöds inte.
* Ladda inte upp PDF-formulär med blanksteg i filnamnet.
* Överför inte [PDF-portföljer](https://helpx.adobe.com/acrobat/using/overview-pdf-portfolios.html). Tjänsten konverterar inte en PDF-portfölj till adaptiva formulär.
* Gör de föreslagna ändringarna i PDF-formulär som beskrivs i artikeln [Bästa praxis och överväganden](styles-and-pattern-considerations-and-best-practices.md) .
* Läs artikeln [Kända fel](known-issues.md) för att undvika fallgropar.

### 3. Granska konverterade formulär {#review-converted-forms}

Real world forms can have complex data capture requirements in field layout, naming or implicit ideas which may not be correctly capture taken by AI/ML based detection logic. När den automatiska konverteringen är klar kan du använda [Gransknings- och korrigeringsredigeraren](review-correct-ui-edited.md) för att granska konverterade formulär och göra nödvändiga uppdateringar och generera bättre resultat. Skicka formuläret igen för konverteringen när du har gjort nödvändiga ändringar.

Hur lång tid det tar att automatisera konverteringen beror på olika faktorer, till exempel storleken på indataformuläret, formulärets komplexitet, lånet i tjänstens behandlingskö. Användaren meddelas regelbundet via statusindikator för mapp/fil. När konverteringen är klar skickas även ett e-postmeddelande till den konfigurerade e-postadressen.
