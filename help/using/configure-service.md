---
title: Konfigurera den automatiserade konverteringstjänsten för formulär
description: Redo för AEM att använda tjänsten Automated forms conversion
solution: Experience Manager Forms
feature: Adaptive Forms
topic: Administration
topic-tags: forms
role: Admin, Developer, User
level: Beginner, Intermediate
exl-id: 8f21560f-157f-41cb-ba6f-12a4d6e18555
source-git-commit: e95b4ed35f27f920b26c05f3398529f825948f1f
workflow-type: tm+mt
source-wordcount: '2684'
ht-degree: 6%

---

# Konfigurera den automatiserade konverteringstjänsten för formulär {#about-this-help}

I den här hjälpen beskrivs hur en AEM kan konfigurera tjänsten Automated forms conversion för att automatisera konverteringen av PDF forms till adaptiva formulär. Den här hjälpen är till för IT-administratörer och AEM på din organisation. Informationen baseras på antagandet att alla som läser den här hjälpen känner till följande tekniker:

* Installera, konfigurera och administrera Adobe Experience Manager- och AEM-paket,

* Med Linux® och Microsoft® Windows®,

* Konfigurera SMTP-e-postservrar

<!--- >[!VIDEO](https://video.tv.adobe.com/v/29267/) 

**Watch the video or read the article to configure Automated Forms Conversion service** -->

## Onboarding{#onboarding}

Tjänsten är kostnadsfri för kunder med AEM 6.4 Forms och AEM 6.5 Forms On-Premise och företagskunder med Adobe-Managed Service. Du kan kontakta Adobes säljteam eller din Adobe-representant för att begära åtkomst till tjänsten. Tjänsten är också tillgänglig kostnadsfritt och föraktiverat för as a Cloud Service AEM Forms-kunder.

Adobe aktiverar åtkomst för organisationen och tillhandahåller behörigheter åt den person som utses till administratör i organisationen. Administratören kan ge åtkomst till AEM Forms-utvecklare (användare) i organisationen så att de kan ansluta till tjänsten.

## Förutsättningar {#prerequisites}

Du behöver följande för att kunna använda tjänsten Automated forms conversion:

* Tjänsten Automated forms conversion är aktiverad för din organisation
* Ett Adobe ID-konto med administratörsbehörighet för konverteringstjänsten
* En AEM 6.4-, AEM 6.5- eller AEM Forms as a Cloud Service-författarinstans med senaste AEM Service Pack eller senaste uppdateringar.
* En AEM användare (i din AEM instans) som är medlem i användargruppen formulär

## Konfigurera miljön {#setuptheservice}

Innan du använder tjänsten förbereder du AEM författarinstans för att ansluta till tjänsten som körs i Adobe Cloud. Utför följande steg i den listade sekvensen för att förbereda instansen för tjänsten:

1. [Ladda ned och installera AEM 6.4, AEM 6.5 eller AEM Forms as a Cloud Service](#aemquickstart)
1. [Hämta och installera det senaste AEM Service Pack](#servicepack)
1. [Hämta och installera det senaste AEM Forms-tilläggspaketet](#downloadaemformsaddon)
1. (valfritt) [Hämta och installera det senaste kopplingspaketet](#installConnectorPackage)
1. [Skapa egna teman och mallar](#referencepackage)

### Hämta och installera AEM 6.4 eller AEM 6.5 eller ombord på AEM Forms as a Cloud Service {#aemquickstart}


Tjänsten automated forms conversion körs AEM författarinstansen. Du måste AEM 6.4, AEM 6.5 eller AEM Forms as a Cloud Service för att kunna konfigurera en AEM författarinstans.

* Om du inte har AEM 6.4 eller AEM 6.5 kan du ladda ned det från nedanstående platser. När du har laddat ned AEM finns instruktioner om hur du konfigurerar en AEM författarinstans i [driftsätta och underhålla](https://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/deploy.html#defaultlocalinstall).:

   * Om du redan är AEM kan du hämta AEM 6.4 eller AEM 6.5 från [Adobe licenswebbplats](http://licensing.adobe.com).

   * Om du är Adobe partner ska du använda [Adobe Partner Training Program](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=82357Q) att begära AEM 6.4 eller AEM 6.5.

* Om du använder AEM Forms as a Cloud Service kan du läsa om [AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/setup-environment/setup-forms-cloud-service.html?lang=en#setup-environment) och [konfigurera en lokal utvecklingsmiljö](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/setup-environment/setup-local-development-environment.html?lang=en#setup-environment).

### (Endast för AEM 6.4 och AEM 6.5) Hämta och installera AEM senaste Service Pack {#servicepack}

Hämta och installera det senaste AEM Service Pack. Detaljerade instruktioner finns i [AEM 6.4 Service Pack versionsinformation](https://helpx.adobe.com/experience-manager/6-4/release-notes/sp-release-notes.html) eller [AEM 6.5 Service Pack versionsinformation](https://helpx.adobe.com/experience-manager/6-5/release-notes/sp-release-notes.html).

### (Endast för AEM 6.4 och AEM 6.5) Hämta och installera AEM Forms tilläggspaket  {#downloadaemformsaddon}

En AEM innehåller grundläggande formulärfunktioner. Konverteringstjänsten kräver AEM Forms alla funktioner. Ladda ned och installera AEM Forms-tilläggspaket för att utnyttja alla funktioner i AEM Forms. Paketet krävs för att konfigurera och köra konverteringstjänsten. Detaljerade anvisningar finns i [Installera och konfigurera datainhämtningsfunktioner.](https://helpx.adobe.com/experience-manager/6-5/forms/using/installing-configuring-aem-forms-osgi.html)

>[!NOTE]
> Kontrollera att du utför de obligatoriska konfigurationerna efter installationen när du har installerat tilläggspaketet.
>

<!-- ### (Optional) Download and install connector package  {#installConnectorPackage}

The connector package provides early access to the [Auto-detect logical sections](convert-existing-forms-to-adaptive-forms.md#run-the-conversion) features and improvements delivered in release AFC-2020.03.1. Do not install the package if you do not require feature and improvements delivered in AFC-2020.03.1.  You can [download the connector package from AEM Package Share](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/featurepack/AFCS-Connector-2020.03.1). -->


### Skapa egna teman och mallar {#referencepackage}

Om du börjar AEM 6.4 eller AEM 6.5 tum [produktionsläge](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/production-ready.html) (inget innehållets körningsläge) installeras inte referenspaketen. Referenspaketen innehåller exempelteman och mallar. Tjänsten Automated forms conversion kräver minst ett tema och en mall för att konvertera ett PDF-formulär till ett anpassningsbart formulär. Skapa ett eget tema och en egen mall [tjänstkonfiguration](#configure-the-cloud-service) om du vill använda egna mallar och teman innan du använder tjänsten.

Du kan även hämta och installera [AEM Forms Reference Assets](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) paket på din Author-instans. Det skapar vissa referensteman och mallar.

## Konfigurera tjänsten {#configure-the-service}

Innan du fortsätter att konfigurera tjänsten och ansluter din lokala instans till tjänsten som körs i Adobe Cloud, ska du lära dig mer om vilka profiler och behörigheter som krävs för att ansluta till tjänsten. Tjänsten använder två olika typer av profiler, administratörer och utvecklare:

* **Administratörer**: Administratörerna ansvarar för att hantera program och tjänster från Adobe för sin organisation. Administratörer ger utvecklare i sin organisation åtkomst till tjänsten Automated forms conversion som körs i Adobe Cloud. När en administratör har etablerats för en organisation får administratören ett e-postmeddelande med titeln **[!UICONTROL 'You now have administrator rights to manage Adobe software and services for your organization']**. Om du är administratör kontrollerar du att postlådan innehåller e-post med den tidigare nämnda titeln och fortsätter till [ge utvecklare av din organisation åtkomst](#adduseranddevs).

![E-postadress för administratörsåtkomst](assets/admin-console-adobe-io-access-grantedx75.png)

* **Utvecklare**: En utvecklare ansluter en lokal AEM Forms-författarinstans till Automated forms conversion-tjänsten som körs i Adobe Cloud. När en administratör ger en utvecklare behörighet att ansluta till Automated forms conversion-tjänsten skickas ett e-postmeddelande med titeln Du har nu utvecklaråtkomst för att hantera Adobe API-integreringar för din organisation till utvecklaren. Om du är utvecklare kan du kontrollera om din postlåda innehåller e-post med den tidigare nämnda titeln och fortsätta till [Koppla din lokala AEM till Automated forms conversion-tjänsten på Adobe Cloud.](#connectafcadobeio)

![E-postadress för utvecklaråtkomstbidrag](assets/email-developer-accessx94.png)

### (Endast för administratörer av AEM 6.4 och AEM 6.5) Bevilja åtkomst till utvecklare i din organisation {#adduseranddevs}

När Adobe har aktiverat åtkomst för din organisation och gett administratören de behörigheter som krävs kan administratören logga in på Admin Console (detaljerade instruktioner nedan), skapa en profil och lägga till utvecklare i profilen. Utvecklare kan ansluta en lokal instans av AEM Forms till tjänsten Automated forms conversion i Adobe Cloud.

Utvecklare är medlemmar i din organisation som har utsetts att köra konverteringstjänsten. Endast de utvecklare som läggs till i tjänstprofilen i Adobe Automated forms conversion har rätt att använda tjänsten Automated forms conversion. Följ stegen nedan för att skapa en profil och lägga till utvecklare i den. Minst en profil krävs för att ge utvecklare i organisationen nödvändig åtkomst:

1. Logga in på [Admin Console](https://adminconsole.adobe.com/). Använd **Adobe ID** av administratören som har tilldelats tjänsten Automated forms conversion för inloggning. Använd inte något annat ID eller Federated ID för att logga in.
1. Klicka på **[!UICONTROL Automated Forms Conversion]** alternativ.
1. Klicka **[!UICONTROL New Profile]** i **[!UICONTROL Products]** -fliken.
1. Ange **[!UICONTROL Name]**, **[!UICONTROL Display Name]** och **[!UICONTROL Description]** för profilen. Klicka på **[!UICONTROL Done]**. En profil skapas.

   ![Ange information för den nya profilen.](assets/create-new-profile-details.png)

1. Lägg till utvecklare i profilen. Så här lägger du till utvecklare:
   1. I [Admin Console](https://adminconsole.adobe.com/enterprise)navigera till fliken Översikt.
   1. Klicka **[!UICONTROL Assign Developers]** på det produktkort som krävs.
   1. Ange utvecklarnas e-postadress och eventuellt för- och efternamn.
   1. Välj produktprofiler. Tryck på **[!UICONTROL Save]**.

Upprepa stegen ovan för alla användare. Mer information om hur du lägger till utvecklare finns i [Hantera utvecklare](https://helpx.adobe.com/enterprise/using/manage-developers.html).

När en administratör lägger till utvecklare i profilen Adobe I/O meddelas utvecklarna via e-post. Efter att ha tagit emot e-postmeddelandet kan utvecklarna fortsätta med att [ansluta en lokal AEM Forms-instans med tjänsten Automated forms conversion i Adobe Cloud](#connectafcadobeio).

### (Endast för utvecklare) Anslut din lokala AEM Forms-instans till tjänsten Automated forms conversion i Adobe Cloud {#connectafcadobeio}

När en administratör har gett dig utvecklaråtkomst kan du ansluta din lokala AEM Forms-instans till tjänsten Automated forms conversion som körs i Adobe Cloud. Utför följande steg i den listade sekvensen för att ansluta din AEM Forms-instans till tjänsten:

* [Konfigurera e-postmeddelanden](configure-service.md#configureemailnotification)
* [Lägg till användare i gruppen för formuläranvändare](#adduserstousergroup)
* [Hämta offentliga certifikat](#obtainpubliccertificates)
* [Konfigurera tjänst-API:erna på Adobe Developer Console](#createintegration)
* [Konfigurera molntjänsten](configure-service.md#configure-the-cloud-service)

#### Konfigurera e-postmeddelande {#configureemailnotification}

Tjänsten Automated forms conversion använder Day CQ-e-posttjänsten för att skicka e-postmeddelanden. Dessa e-postmeddelanden innehåller information om lyckade eller misslyckade konverteringar. Om du väljer att inte få något meddelande hoppar du över dessa steg. Utför följande steg för att konfigurera Day CQ Mail Service:

* För AEM 6.4 Forms eller AEM 6.5 Forms:

   1. Gå till AEM konfigurationshanteraren på `http://localhost:4502/system/console/configMgr`
   1. Öppna Dag CQ Mail Service-konfigurationen. Ange ett värde för **[!UICONTROL SMTP server host name]**, **[!UICONTROL SMTP server port]** och **[!UICONTROL From address]** fält. Klicka på **[!UICONTROL Save]**.

      Du kan kontakta din e-postleverantör eller IT-administratör för att få information om värdnamn och port för SMTP-servern. Du kan använda valfri giltig e-postadress i formulärfältet. Exempel: notification@example.com eller donotreply@example.com.

   1. Öppna **[!UICONTROL Day CQ Link Externalizer]** konfiguration. I **[!UICONTROL Domains]** anger du det faktiska värdnamnet eller IP-adressen och portnumret för lokala instanser, författare och publiceringsinstanser. Klicka på **[!UICONTROL Save]**.

* För AEM Forms as a Cloud Service [logga en supportanmälan för att aktivera e-posttjänsten](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#sending-email).

#### Lägg till användare i gruppen för formuläranvändare {#adduserstousergroup}

Ange en e-postadress i profilen för den AEM användaren som ska köra tjänsten. Kontrollera att användaren är medlem i [formuläranvändare](https://experienceleague.adobe.com/docs/experience-manager-65/forms/manage-administer-aem-forms/forms-groups-privileges-tasks.html) grupp. E-post skickas till e-postadressen till den användare som kör konverteringen. Så här anger du en e-postadress för användaren och lägger till användare i formuläranvändargruppen:

1. Logga in på din AEM Forms-författarinstans som AEM. Använd dina lokala AEM för att logga in. Använd inte Adobe ID för att logga in. Tryck **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**.

1. Välj en användare som ska köra konverteringstjänsten och tryck på **[!UICONTROL Properties]**. Sidan Redigera användarinställningar öppnas.
1. Ange en e-postadress i dialogrutan **[!UICONTROL Email]** fält och knacka **[!UICONTROL Save]**. E-postmeddelandena skickas till den angivna e-postadressen när konverteringen har slutförts eller misslyckats.
1. Tryck på **Grupper** -fliken. På fliken Välj grupp skriver du och väljer **formuläranvändare** grupp. Tryck **Spara och stäng**. Användaren är nu medlem i gruppen för användare av formulär.

#### (Endast för AEM 6.4 och AEM 6.5) Skaffa offentliga certifikat {#obtainpubliccertificates}

Med ett offentligt certifikat kan du autentisera din profil på Adobe I/O.

1. Logga in på din AEM Forms-författarinstans. Navigera till **[!UICONTROL Tools]**> **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**. Tryck på **[!UICONTROL Create]**. The **[!UICONTROL Adobe IMS Technical Account Configuration]** visas.

   ![Sidan Konfiguration av Adobe IMS Technical Account](assets/adobe-ims-technical-account-configuration.png)

1. Välj **[!UICONTROL Automated Forms Conversion Service]** i molnlösningen.

1. Välj **[!UICONTROL Create new certificate]** och ange ett alias. Aliaset används som namn på dialogrutan. Tryck på **[!UICONTROL Create certificate]**. En dialogruta visas. Klicka på **[!UICONTROL OK]**. Certifikatet skapas.

1. Tryck **[!UICONTROL Download Public Key]** och spara *AEM-Adobe-IMS.crt* certifikatfil på din dator. Certifikatfilen används för [Konfigurera tjänst-API:erna på Adobe Developer Console](#createintegration). Tryck på **[!UICONTROL Next]**.

1. Ange följande:

   * Titel: Ange en titel.
   * Auktoriseringsserver: [https://ims-na1.adobelogin.com](https://ims-na1.adobelogin.com)\

   Lämna de andra fälten tomma (kommer senare). Håll sidan öppen.

   <!--
   Comment Type: draft

   <li> </li>
   -->

   <!--
   Comment Type: draft

   <li>Step text</li>
   -->

#### (Endast för AEM 6.4 och AEM 6.5) Konfigurera tjänst-API:erna på Adobe Developer Console {#createintegration}

Om du vill använda tjänsten Automated forms conversion skapar du ett projekt och lägger till API:t för automatisk Forms-konfigurationstjänst i projektet på Adobe Developer Console. Integreringen genererar API-nyckel, klienthemlighet, nyttolast (JWT).

1. Logga in på [https://console.adobe.io/](https://console.adobe.io/). Använd ditt Adobe ID-utvecklarkonto som administratören har konfigurerat för inloggning på Adobe I/O-konsolen.
1. Välj organisation i det övre högra hörnet. Kontakta administratören om du inte känner till din organisation.
1. Tryck på **[!UICONTROL Create new project]**. En skärm för att komma igång med ditt nya projekt visas. Tryck på **[!UICONTROL Add API]**. En skärm med en lista över alla API:er som är aktiverade för ditt konto visas.
1. Välj **[!UICONTROL Automated Forms Conversion service]** och trycka **[!UICONTROL Next]**. En skärm som konfigurerar API:t visas.
1. Välj [!UICONTROL Upload your public key] kan du ladda upp filen AEM-Adobe-IMS.crt som du laddat ned i [Hämta offentliga certifikat](#obtainpubliccertificates) och trycka **[!UICONTROL Next]**. Alternativet Skapa ett nytt tjänstkonto (JWT) visas. Tryck på **[!UICONTROL Next]**.
1. Välj en produktprofil och tryck **[!UICONTROL Save configured API]**. Markera profilen som skapades när [ge utvecklare av din organisation åtkomst](#adduseranddevs). Kontakta administratören om du inte vet vilken profil du ska välja.
1. Tryck **[!UICONTROL Service Account (JWT)]** om du vill visa API-nyckeln, klienthemligheten och annan information som krävs för att ansluta den lokala AEM till tjänsten Automated forms conversion. Informationen på sidan används för att skapa IMS-konfigurationer på den lokala datorn.

1. Öppna sidan IMS-konfiguration på den lokala instansen. Du lämnade den här sidan öppen i slutet av avsnittet [Hämta ett offentligt certifikat ](#obtainpubliccertificates).

   ![Ange titel, API-nyckel, klienthemlighet och nyttolast ](assets/ims-configuration-details.png)

1. På Adobe IMS Technical page anger du API Key och Client Secret. Använd de värden som anges på JWT (Service Account) på Adobe Developer konsolsida.

   >[!NOTE]
   >
   >
   >För nyttolast använder du koden som finns på fliken Generera JWT på JWT-sidan (Service Account) i Adobe Developer Console.

1. Tryck på **[!UICONTROL Save]**. IMS-konfigurationen skapas.

   >[!CAUTION]
   >
   >Skapa endast en IMS-konfiguration. Skapa inte fler än en IMS-konfiguration.

1. Välj IMS-konfigurationen och tryck på **[!UICONTROL Check Health]**. En dialogruta visas. Tryck på **[!UICONTROL Check]**. Meddelandet *Token har hämtats* visas när en anslutning har skapats.

   ![När anslutningen lyckades visas meddelandet om token som hämtats. ](assets/health-check.png)

   <br/> <br/>

#### Konfigurera Cloud Servicen {#configure-the-cloud-service}

Skapa en Cloud Service-konfiguration för att ansluta AEM till konverteringstjänsten. Du kan också ange en mall, ett tema och formulärfragment för en konvertering. Du kan skapa flera olika molntjänstkonfigurationer separat för varje formuläruppsättning. Du kan till exempel ha en separat konfiguration för säljavdelningsformulär och en separat konfiguration för kundsupportformulär. Så här skapar du en molntjänstkonfiguration:

1. Tryck på **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Tools]**> **[!UICONTROL Cloud Services]** > **[!UICONTROL Automate Forms Conversion Configuration]**.
1. Tryck på **[!UICONTROL Global]** mapp och tryck **[!UICONTROL Create]**. Sidan där du skapar konfigurationen för Automated forms conversion visas. Konfigurationen skapas i mappen Global. Du kan också skapa konfigurationen i en annan mapp som finns eller skapa en mapp för dina konfigurationer.

1. På **[!UICONTROL Create Automated Forms Conversion Configuration]** anger du ett värde för följande fält och trycker **[!UICONTROL Next]**.

   | Fält | Beskrivning |
   |--- |--- |
   | Titel | Unik rubrik för konfigurationen. Titeln visas i användargränssnittet som används för att starta konverteringen. |
   | Namn | Unikt namn för konfigurationen. Konfigurationen sparas i CRX-Repository med det angivna namnet. Namnet kan vara identiskt med titeln. |
   | Miniatyrplats | Platsen för miniatyrbilden för konfigurationen. |
   | Tjänst-URL | URL för tjänsten Automated forms conversion på Adobe Cloud. Använd `https://aemformsconversion.adobe.io/` URL. |
   | Mall | Standardmall som ska användas för konverterade formulär. Du kan alltid ange en annan mall innan du påbörjar konverteringen. En mall innehåller grundläggande struktur och ursprungligt innehåll för ett adaptivt formulär. Du kan välja en mall bland de färdiga mallarna. Du kan också skapa en anpassad mall. |
   | Tema | Standardtema som ska användas på konverterade formulär. Du kan alltid ange ett annat tema innan du påbörjar konverteringen.  Du kan klicka på ikonen för att välja ett tema som ingår i rutan. Du kan också skapa ett anpassat tema. |
   | Befintliga fragment | Placering av befintliga fragment, om sådana finns. |
   | Anpassad metamodell | Sökväg till .schema.json-filen för den anpassade metamodellen. Du kan skapa separata metamodeller för engelska, franska, tyska, spanska, italienska och portugisiska. |

1. I **[!UICONTROL Advanced]** -fliken i **[!UICONTROL Create Automated Forms Conversion Configuration]** page, specify value for the following field:

   <table>
   <thead>
   <tr>
   <th>Fält</th>
   <th>Beskrivning</th>
   </tr>
   </thead>
   <tbody>
   <tr>
   <td >Generera postdokument</td>
   <td>Välj alternativet att automatiskt generera arkivdokument för konverterade formulär. Alternativet är endast för XFA-baserade formulär (XDP och PDF forms). När du aktiverar alternativet kan du, när du har skickat in ett formulär, tillåta dina kunder att bevara en post, i utskrift eller i dokumentformat, med information som de har fyllt i formuläret för framtida referens. Detta kallas för ett urkunder.</td>
   </tr>
   <tr>
   <td>Aktivera analys</td>
   <td>(Endast för AEM 6.4 och AEM 6.5) Markera alternativet att aktivera Adobe Analytics för alla konverterade formulär. Kontrollera att Adobe Analytics är aktiverat för din AEM Forms-instans innan du använder alternativet.</td>
   </tr>
   </tbody>
   </table>

   * När källan är ett XFA-baserat formulär med tillägget .XDP, behåller DOR-utdatafilen XFA-layouten, annars använder konverteringstjänsten en mall som inte finns i rutan för att generera DOR för andra XFA-baserade formulär.
   * När ett XFA-formulär skickas sparas data från formuläret som ett XML-element eller ett attribut. Till exempel, `<Amount currency="USD"> 10.00 </Amount>`. Valutan sparas som ett attribut och valutabelopp, 10.00 sparas som ett element. Skicka data från ett anpassat formulär har inga attribut, utan bara element. När ett XFA-baserat formulär konverteras till ett adaptivt formulär innehåller de adaptiva data som skickas ett element för varje sådant attribut. Till exempel,

   ```css
      {
         "Type": "Principal",
   
         "Amount": "10.00",
   
         "currency": "USD"
      }
   ```

1. Tryck på **[!UICONTROL Create]**. Molnkonfigurationen har skapats. Din AEM Forms-instans är redo att börja konvertera äldre formulär till anpassningsbara formulär.
