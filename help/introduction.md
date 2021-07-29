---
title: Introduktion
description: Påskynda konverteringen av utskriftsformulär till anpassningsbara formulär
exl-id: edabeac8-cd66-48ca-a99f-9643a1c184cf
source-git-commit: fed54ea64e19c77868e8e58e29e909cf4447f696
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 65%

---

# Introduktion {#introduction-to-automated-forms-conversion-service}

Den automatiserade konverteringstjänsten för formulär hjälper till att påskynda digitisering och modernisering av upplevelsen av datainhämtning genom automatiserad konvertering av PDF-formulär till anpassningsbara formulär. Tjänsten, som drivs av Adobe Sensei, konverterar automatiskt PDF-formulären till anpassningsbara formulär som är smidiga för enheten, lättanvända och HTML5-baserade. Tjänsten drar nytta av de befintliga investeringarna i PDF-formulär och XFA och tillämpar även lämpliga valideringar, styling och layout för anpassningsbara formulärfält under konverteringen. Tjänsten hjälper till med att:

* Spara den manuella arbetskraft som krävs för att konvertera utskriftsformulär till anpassningsbara formulär
* Tillämpa mönster och lämpliga valideringar under konverteringen
* Generera dokument över dataposter under konverteringen
* Gruppera vanliga fält i återanvändbara formulärfragment
* Aktiverar Adobe Analytics under konverteringen

![Det är enkelt. Du ger oss källformulären och överlåter allt till oss. Vi erbjuder vackra, anpassningsbara formulär. Du kan alltid finslipa resultatet. ](assets/pdf-to-adaptive-form-gitx50.gif)

## Onboarding {#onboarding}

Tjänsten är kostnadsfri för kunder med AEM 6.4 Forms och AEM 6.5 Forms On-Premise och företagskunder med Adobe-Managed Service. Du kan kontakta Adobes säljteam eller din Adobe-representant för att begära åtkomst till tjänsten. Tjänsten är också tillgänglig kostnadsfritt och föraktiverat för AEM Forms som Cloud Service.

Adobe aktiverar åtkomst för organisationen och tillhandahåller behörigheter åt den person som utses till administratör i organisationen. Administratören kan ge åtkomst till AEM Forms-utvecklare (användare) i organisationen så att de kan ansluta till tjänsten. Mer information finns i [Konfigurera den automatiserade konverteringstjänsten för formulär](configure-service.md).

## PDF forms och språk som stöds {#supported-languages-and-pdf-forms}

Tjänsten stöder icke-interaktiva PDF-formulär, formulär som är skapade med Adobe Acrobat, kända som AcroForms, och XFA-baserade formulär som är skapade med AEM Forms eller Adobe LiveCycle.

Tjänsten stöder även Adobe Sign-aktiverade PDF forms. Om PDF-källformuläret har Adobe Sign-texttaggar, bevarar tjänsten all Adobe Sign-relaterad information under konverteringen och associerar signerarinformationen som finns i PDF-källfilen med motsvarande adaptiva formulärfält. Funktionen är bara tillgänglig för AcroForms.

Tjänsten kan konvertera engelska, franska, tyska och spanska blanketter till anpassningsbara blanketter. Du kan också översätta de genererade anpassningsbara formulären till ett annat språk med [AEM översättningsarbetsflöde](https://helpx.adobe.com/experience-manager/6-5/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.html).

## Konverteringsarbetsflöde  {#conversion-workflow}

Den automatiserade konverteringstjänsten för formulär körs på Adobe-molnet. Du ansluter AEM-instansen till tjänsten, laddar upp formulär till AEM-instansen och startar konverteringen. Hela konverteringsprocessen listas nedan:

![Arbetsflöde](assets/conversion-workflow.png)

### 1. Konfigurera miljön {#set-up-the-environment}

Den automatiserade konverteringstjänsten för formulär körs på Adobe-molnet. [Konfigurera Adobe I/O-konto för organisationen och anslut din lokala AEM-instans](configure-service.md) till konverteringstjänsten som körs på Adobe-molnet.

### 2. Konvertera PDF-formulär till anpassningsbara formulär {#use-the-conversion-service}

När AEM Forms-miljön har konfigurerats [laddar du upp PDF-formulär](convert-existing-forms-to-adaptive-forms.md) till AEM-instansen och [startar konverteringen](convert-existing-forms-to-adaptive-forms.md#run-the-conversion) för att konvertera PDF-formulären till anpassningsbara formulär. Tänk på följande innan du laddar upp formulären:

* Ladda inte upp skyddade formulär. Tjänsten konverterar inte lösenordsskyddade och krypterade formulär.
* Överför inte skannade, färgade, icke-engelska och ifyllda formulär. Sådana formulär stöds inte.
* Ladda inte upp PDF-formulär med mellanslag i filnamnet.
* Ladda inte upp [PDF-portfolios](https://helpx.adobe.com/acrobat/using/overview-pdf-portfolios.html). Tjänsten konverterar inte en PDF-Portfolio till ett anpassningsbart formulär.
* Gör de föreslagna ändringarna i PDF-formulären som beskrivs i artikeln [Rekommenderad praxis och saker att tänka på](styles-and-pattern-considerations-and-best-practices.md).
* Läs artikeln [Kända fel](known-issues.md) för att undvika fallgropar.

### 3. Granska konverterade formulär {#review-converted-forms}

Real world forms can have complex data capture requirements in field layout, naming, or implicit ideas which may not be correctly capture by AI/ML based detection logic. När den automatiserade konverteringen är klar kan du använda [redigeraren för granskning och korrigering](review-correct-ui-edited.md) för att granska det konverterade formuläret och göra nödvändiga uppdateringar och generera förbättrade utdata som stämmer bättre överens med önskat resultat. När du har gjort nödvändiga ändringar skickar du in formuläret för konvertering igen.

Hur lång tid det tar att automatisera konverteringen beror på olika faktorer, t.ex. storleken på indataformuläret, formulärets komplexitet, lånet i tjänstens behandlingskö. Användaren meddelas regelbundet om förloppet via statusindikatorn i mappen/filen. När konverteringen är klar skickas också en avisering via e-post till den konfigurerade e-postadressen.
