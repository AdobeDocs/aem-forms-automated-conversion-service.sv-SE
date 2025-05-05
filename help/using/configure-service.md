---
title: Konfigurera tjänsten Automated Forms Conversion (AFCS)
description: Förbered AEM-instansen för att använda tjänsten Automated Forms Conversion (AFCS)
solution: Experience Manager Forms
feature: Adaptive Forms
topic: Administration
topic-tags: forms
role: Admin, Developer, User
level: Beginner, Intermediate
exl-id: 8f21560f-157f-41cb-ba6f-12a4d6e18555
source-git-commit: 54cd2cf2fdc4f9b420125e4c04c87bec1b7f368d
workflow-type: tm+mt
source-wordcount: '2366'
ht-degree: 2%

---

# Konfigurera tjänsten Automated Forms Conversion (AFCS) {#about-this-help}

I den här artikeln beskrivs hur en AEM-administratör kan konfigurera tjänsten Automated Forms Conversion (AFCS) för att automatisera konverteringen av sin PDF forms till Adaptive Forms. Den här artikeln är avsedd för IT-administratörer och AEM-administratörer på din organisation. Informationen baseras på antagandet att alla som läser den här artikeln känner till följande tekniker:

* Installera, konfigurera och administrera Adobe Experience Manager- och AEM-paket,

* Med Linux® och Microsoft® Windows®,

<!--- >[!VIDEO](https://video.tv.adobe.com/v/29267/) 

**Watch the video or read the article to configure Automated Forms Conversion service (AFCS)** -->

## Onboarding{#onboarding}

Tjänsten är kostnadsfri för kunder som har AEM 6.5 Forms On-Premise och företagskunder med Adobe Managed Service. Du kan kontakta Adobe säljteam eller din Adobe-representant för att få tillgång till tjänsten. Tjänsten är också tillgänglig kostnadsfritt och föraktiverat för kunder som har AEM Forms as a Cloud Service.

Adobe aktiverar åtkomst för organisationen och tillhandahåller behörigheter åt den person som utses till administratör i organisationen. Administratören kan ge AEM Forms-utvecklare (användare) i din organisation åtkomst till tjänsten.

## Förutsättningar {#prerequisites}

Du behöver följande för att kunna använda tjänsten Automated Forms Conversion Service (AFCS):

* Tjänsten Automated Forms Conversion (AFCS) är aktiverad för din organisation
* Ett Adobe ID-konto med administratörsbehörighet för konverteringstjänsten
* En AEM 6.5-version med den senaste versionen av AEM Service Pack eller AEM Forms as a Cloud Service som författare med de senaste uppdateringarna.
* En AEM-användare (i din AEM-instans) som är medlem i en formuläranvändargrupp

## Konfigurera miljön {#setuptheservice}

Innan du använder tjänsten förbereder du din AEM-författarinstans för att ansluta till tjänsten som körs i Adobe Cloud. Utför följande steg i den listade sekvensen för att förbereda instansen för tjänsten:

1. [Ladda ned och installera AEM 6.5 eller AEM Forms as a Cloud Service](#aemquickstart)
1. [(Endast för AEM 6.5) Hämta och installera den senaste AEM Service Pack](#servicepack)
1. [(Endast för AEM 6.5) Hämta och installera det senaste AEM Forms-tilläggspaketet](#downloadaemformsaddon)
1. [Skapa egna teman och mallar](#referencepackage)

### 1. Ladda ned och installera AEM 6.5 eller AEM Forms as a Cloud Service {#aemquickstart}


Tjänsten Automated Forms Conversion (AFCS) körs på AEM Author Instance. Du måste ha AEM 6.5 eller AEM Forms as a Cloud Service för att kunna konfigurera en AEM-författarinstans.

* Om du inte har AEM 6.5 installerat laddar du ned det från nedanstående platser. När du har hämtat AEM finns instruktioner om hur du konfigurerar en AEM-författarinstans i [Distribuera och underhålla](https://helpx.adobe.com/se/experience-manager/6-5/sites/deploying/using/deploy.html#defaultlocalinstall).:

   * Om du redan är AEM-kund hämtar du AEM 6.5 från [Adobe licenswebbplats](http://licensing.adobe.com).

   * Om du är Adobe partner kan du använda [Adobe Partner Training Program](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=82357Q) för att begära AEM 6.5.

* Om du använder AEM Forms as a Cloud Service kan du läsa mer i [AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/setup-environment/setup-forms-cloud-service.html?lang=sv-SE#setup-environment) och [konfigurera en lokal utvecklingsmiljö](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/setup-environment/setup-local-development-environment.html?lang=sv-SE#setup-environment).

### 2. (Endast för AEM 6.5) Hämta och installera AEM senaste Service Pack {#servicepack}

Hämta och installera den senaste versionen av AEM Service Pack. Mer information finns i [AEM 6.5 Service Pack versionsinformation](https://experienceleague.adobe.com/sv/docs/experience-manager-65/content/release-notes/release-notes).

### 3. (Endast för AEM 6.5) Hämta och installera AEM Forms-tilläggspaket  {#downloadaemformsaddon}

En AEM-instans innehåller grundläggande formulärfunktioner. Konverteringstjänsten kräver AEM Forms alla funktioner. Ladda ned och installera AEM Forms-tilläggspaket för att utnyttja alla funktioner i AEM Forms. Paketet krävs för att konfigurera och köra konverteringstjänsten. Detaljerade instruktioner finns i [Installera och konfigurera datainhämtningsfunktioner.](https://experienceleague.adobe.com/sv/docs/experience-manager-65/content/forms/install-aem-forms/osgi-installation/installing-configuring-aem-forms-osgi)
https://adminconsole.adobe.com/
>[!NOTE]
> Kontrollera att du utför de obligatoriska konfigurationerna efter installationen när du har installerat tilläggspaketet.
>

<!-- ### (Optional) Download and install connector package  {#installConnectorPackage}

The connector package provides early access to the [Auto-detect logical sections](convert-existing-forms-to-adaptive-forms.md#run-the-conversion) features and improvements delivered in release AFC-2020.03.1. Do not install the package if you do not require feature and improvements delivered in AFC-2020.03.1.  You can [download the connector package from AEM Package Share](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/featurepack/AFCS-Connector-2020.03.1). -->


### 4. Skapa egna teman och mallar {#referencepackage}

Referenspaketen innehåller exempelteman och mallar. Tjänsten Automated Forms Conversion (AFCS) kräver minst ett tema och en mall för att konvertera ett PDF-formulär till ett adaptivt formulär. Skapa ett eget tema och en egen mall och en [tjänstkonfiguration](#configure-the-cloud-service) för att använda anpassade mallar och teman innan du använder tjänsten.

Du kan också hämta och installera [AEM Forms Reference Assets](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) -paketet på din Author-instans. Det skapar vissa referensteman och mallar.

## Konfigurera åtkomst och behörigheter

Innan du fortsätter med att konfigurera tjänsten och ansluter instansen till tjänsten som körs i Adobe Cloud, ska du läsa om vilka profiler och behörigheter som krävs för att ansluta till tjänsten. Tjänsten använder två olika typer av profiler, administratörer och utvecklare:

* **Administratörer**: Administratörer ansvarar för att hantera Adobe-program och -tjänster för sin organisation. Administratörer ger utvecklare i sin organisation åtkomst till tjänsten Automated Forms Conversion (AFCS) som körs i Adobe Cloud. När en administratör har etablerats för en organisation får administratören ett e-postmeddelande med titeln **[!UICONTROL 'You now have administrator rights to manage Adobe software and services for your organization']**. Om du är administratör kontrollerar du om postlådan innehåller e-post med den tidigare nämnda titeln och fortsätter till [Ge utvecklare i din organisation åtkomst](#adduseranddevs).

![E-post för beviljande av administratörsåtkomst](assets/admin-console-adobe-io-access-grantedx75.png)

* **Utvecklare**: En utvecklare ansluter en AEM Forms-författarinstans till den automatiska formulärkonverteringstjänsten (AFCS) som körs i Adobe Cloud. När en administratör ger en utvecklare behörighet att ansluta till AFCS (Automated Forms Conversion Service) skickas ett e-postmeddelande med titeln Du har nu tillgång till utvecklaråtkomst för att hantera Adobe API-integreringar för din organisation till utvecklaren. Om du är utvecklare kan du kontrollera om din postlåda innehåller e-post med den tidigare nämnda titeln och fortsätta till [Anslut din lokala AEM-instans till tjänsten Automated Forms Conversion på Adobe Cloud.](#connectafcadobeio)

![E-post om beviljande av utvecklaråtkomst](assets/email-developer-accessx94.png)

### Ge utvecklare i organisationen åtkomst

När Adobe har aktiverat åtkomst för din organisation och gett administratören de behörigheter som krävs kan administratören logga in på Admin Console (detaljerade instruktioner nedan), skapa en profil och lägga till utvecklare i profilen. Utvecklare kan ansluta en instans av AEM Forms till tjänsten Automated Forms Conversion (AFCS) i Adobe Cloud.

Utvecklare är medlemmar i din organisation som har utsetts att köra konverteringstjänsten. Endast de utvecklare som har lagts till i en AFCS-profil (Adobe Automated Forms Conversion Service) har rätt att använda tjänsten Automated Forms Conversion (AFCS).
Följ stegen nedan för att skapa en profil och lägga till utvecklare i den. Minst en profil krävs för att ge utvecklare i organisationen nödvändig åtkomst:

1. Logga in på [Admin Console](https://adminconsole.adobe.com/). Använd **Adobe ID** av administratören som har etablerats för att använda tjänsten Automated Forms Conversion (AFCS) för inloggning.
1. Klicka på alternativet **[!UICONTROL Automated Forms Conversion]**.
1. Klicka på **[!UICONTROL New Profile]** på fliken **[!UICONTROL Products]**.
1. Ange **[!UICONTROL Name]**, **[!UICONTROL Display Name]** och **[!UICONTROL Description]** för profilen. Klicka på **[!UICONTROL Done]**. Skapa till exempel en profil som **AFC_Flamingo_Test_Dev**.

   ![Ange information för den nya profilen.](assets/create-new-profile-details.png)

1. Lägg till utvecklare i profilen. Så här lägger du till utvecklare:
   1. Gå till fliken Översikt i [Admin Console](https://adminconsole.adobe.com/enterprise).
   1. Klicka på **[!UICONTROL Assign Developers]** på önskat produktkort.
   1. Ange utvecklarnas e-postadress och eventuellt för- och efternamn.
   1. Välj produktprofiler. Klicka på **[!UICONTROL Save]**.

Upprepa stegen ovan för alla användare. Mer information om hur du lägger till utvecklare finns i [Hantera utvecklare](https://helpx.adobe.com/se/enterprise/using/manage-developers.html).

När en administratör har lagt till utvecklare i Adobe I/O-profilen meddelas utvecklarna via e-post (om den är konfigurerad).

<!--
### Configure email notification for local AEM Forms instance

Automated Forms Conversion service (AFCS) uses the Day CQ mail service to send email notifications. These email notifications contain information about successful or failed conversions. If you choose not receive notification, skip these steps. Perform the following steps to configure the Day CQ Mail Service:

* **For AEM 6.5 Forms**:

   1. Go to AEM configuration manager at `http://[server]:[port]/system/console/configMgr`
   2. Open the Day CQ Mail Service configuration. Specify a value for the **[!UICONTROL SMTP server host name]**, **[!UICONTROL SMTP server port]**, and **[!UICONTROL From address]** fields. Click **[!UICONTROL Save]**.

      You can contact your email service provider or IT administrator for information about host name and port of SMTP server. You can use any valid email address in the from field. For example, notification@example.com or donotreply@example.com.

   3. Open the **[!UICONTROL Day CQ Link Externalizer]** configuration. In the **[!UICONTROL Domains]** field, specify the actual host name or IP address and port number for local, author, and publish instances. Click **[!UICONTROL Save]**.

* For AEM Forms as a Cloud Service, [log a support ticket to enable the email service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=sv-SE#sending-email). -->

### Lägg till användare i gruppen för formuläranvändare {#adduserstousergroup}

Ange en e-postadress i profilen för den AEM-användare som ska köra tjänsten. Kontrollera att användaren är medlem i gruppen **forms-users**. E-post skickas till e-postadressen till den användare som kör konverteringen. Så här anger du en e-postadress för användaren och lägger till användare i formuläranvändargruppen:

1. Logga in som AEM-administratör på din AEM Forms-författarinstans. Använd dina lokala AEM-inloggningsuppgifter för att logga in.
1. Klicka på **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**.
1. Välj en användare som är utsedd att köra konverteringstjänsten och klicka på **[!UICONTROL Properties]**. Sidan **Redigera användarinställningar** öppnas.
1. Ange en e-postadress i fältet **[!UICONTROL Email]** och klicka på **[!UICONTROL Save]**. E-postmeddelandena skickas till den angivna e-postadressen när konverteringen har slutförts eller misslyckats.

   ![Ange e-postadress](/help/using/assets/specify-email.png)
1. Klicka på fliken **Grupper**. Skriv och markera gruppen **forms-users** på fliken Välj grupp.
1. Klicka på **Spara och stäng**. Användaren är nu medlem i gruppen för användare av formulär.

   ![Lägg till användargrupp](/help/using/assets/add-user-group.png)

## Anslut din AEM Forms-instans till tjänsten Automated Forms Conversion (AFCS) i Adobe Cloud

När en administratör har gett dig utvecklaråtkomst kan du ansluta din AEM Forms-instans till AFCS-tjänsten (Automated Forms Converting Service) som körs i Adobe Cloud.
Så här ansluter du AEM Forms-instansen till tjänsten Automated Forms Conversion:

[1. Konfigurera tjänst-API:erna på Adobe Developer Console](#configure-the-service-apis-on-adobe-developer-console)

[2. Skapa Adobe IMS-konfigurationer](#2-create-adobe-ims-configurations)

[3. Skapa konfiguration för automatisk formulärkonvertering](#3-create-automated-forms-conversion-configuration)

### 1. Konfigurera tjänst-API:erna på Adobe Developer Console

Om du vill använda tjänsten Automated Forms Conversion (AFCS) skapar du ett projekt och lägger till **Automated Forms Configuration Service** API i projektet på Adobe Developer Console. Integreringen genererar API-nyckel, klienthemlighet, ID för tekniskt konto, scope och organisations-ID.
Så här konfigurerar du API:t för tjänsten Automated Forms Conversion på Adobe Developer Console:

1. Logga in på https://developer.adobe.com/console. Använd ditt Adobe ID-utvecklarkonto som administratören har konfigurerat för inloggning på Adobe I/O-konsolen.
1. Välj organisation i det övre högra hörnet. Kontakta administratören om du inte känner till din organisation.
1. Klicka på **[!UICONTROL Create new project]**. En skärm för att komma igång med ditt nya projekt visas.

   ![Skapa nytt API-projekt](/help/using/assets/create-new-api-project.png)

1. Klicka på **[!UICONTROL Add API]**. En skärm med en lista över alla API:er som är aktiverade för ditt konto visas.
   ![Lägg till API](/help/using/assets/add-api.png)

1. Markera **[!UICONTROL Automated Forms Conversion service]** och klicka på **[!UICONTROL Next]**. En skärm som konfigurerar API:t visas.
   ![Välj AFCS API](/help/using/assets/select-afcs-api.png)

1. Välj autentiseringsmetoden **OAuth Server-to-Server**.
1. Ange **[!UICONTROL Credential Name]** och klicka på **[!UICONTROL Next]**.
   ![Ange autentiseringsuppgiftsnamn](/help/using/assets/specify-credential-name.png)
1. Välj en **produktprofil**. Välj till exempel en profil som **AFC_Flamingo_Test_Dev**.
1. Klicka på **[!UICONTROL Save configured API]**.
   ![Välj profil](/help/using/assets/select-profile.png)

   >[!NOTE]
   >
   > Välj den profil som skapades när du beviljade åtkomst till utvecklare i organisationen. Om du inte vet vilken profil du ska välja kontaktar du administratören.

1. Klicka på **[!UICONTROL OAuth Server-to-Server]** om du vill visa API-nyckeln, klienthemligheten och annan information som krävs för att ansluta din AEM-instans till tjänsten Automated Forms Conversion (AFCS).
   ![Välj autentiseringsuppgifter för sökväg](/help/using/assets/select-oauth-credential.png)

   Informationen på sidan används för att skapa IMS-konfiguration, vilket förklaras i avsnittet [Skapa IMS-teknisk konfiguration på AEM Author Instance](#2-create-ims-technical-configuration-on-aem-author-instance).

   ![Information om OAuth-autentiseringsuppgifter](/help/using/assets/oauth-credentials-details.png)

### 2. Skapa Adobe IMS-konfigurationer

Logga in på din författarinstans för att skapa Adobe IMS-konfigurationer. Använd **Information om OAuth-autentiseringsuppgifter** för att hämta API-nyckeln, klienthemligheten, det tekniska konto-ID:t, omfånget och organisations-ID:t.

1. Logga in på din AEM Forms-författarinstans. Navigera till **[!UICONTROL Tools]**> **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**.
1. Klicka på **[!UICONTROL Create]**.

   ![Skapa IMS Adobe-konfiguration](/help/using/assets/create-ims-conf.png)

1. Sidan **[!UICONTROL Adobe IMS Technical Account Configuration]** visas.

   ![Sidan Konfiguration av Adobe IMS Technical Account ](assets/adobe-ims-technical-account-configuration.png)
1. Välj **[!UICONTROL Automated Forms Conversion Service]** i **molnlösning**.
1. Ange följande:

   * **Titel**: Ange en titel.
   * **Auktoriseringsserver**: [https://ims-na1.adobelogin.com](https://ims-na1.adobelogin.com)
   * Hämta följande från [Konfigurera tjänst-API:erna i Adobe Developer Console](#1-configure-the-service-apis-on-adobe-developer-console)-avsnittet:
      * **Klient-ID**: Kopiera och klistra in **API-nyckel (klient-ID)**.
      * **Klienthemlighet**: Kopiera och klistra in **Klienthemlighet**.
      * **Omfång**: Kopiera och klistra in **Omfång**.
      * **Organisations-ID**: Kopiera och klistra in **Tekniskt konto-ID**.

     ![Skapa IMS Adobe-konfiguration](/help/using/assets/save-ims-configuration.png)

1. Klicka på **[!UICONTROL Save]**. Adobe IMS-konfigurationen skapas.

   >[!CAUTION]
   >
   > Skapa endast en IMS-konfiguration. Skapa inte fler än en IMS-konfiguration.

1. Välj **Adobe IMS-konfigurationen** och klicka på **[!UICONTROL Check Health]**. En dialogruta visas.
   ![Kontrollera hälsa](/help/using/assets/check-health.png)

   En **Check**-dialogruta visas.

1. Klicka på **[!UICONTROL Check]**.

   ![Kontrollera hälsa](/help/using/assets/check-dialog.png)

   Meddelandet *Token har hämtats* visas när en anslutning har skapats.

   ![När anslutningen lyckades visas det token som hämtats. ](/help/using/assets/healthy-dialog.png)

1. Klicka på **Stäng**.

### 3. Skapa konfiguration för automatisk formulärkonvertering

Skapa en konfiguration för automatisk formulärkonvertering för att ansluta din AEM-instans till konverteringstjänsten. Du kan också ange en mall, ett tema och formulärfragment för en konvertering. Du kan skapa flera olika molntjänstkonfigurationer separat för varje formuläruppsättning.
Du kan till exempel ha en separat konfiguration för säljavdelningsformulär och en separat konfiguration för kundsupportformulär. Så här skapar du en molntjänstkonfiguration:

1. Klicka på **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Tools]**> **[!UICONTROL Cloud Services]** > **[!UICONTROL Automate Forms Conversion Configuration]** på din AEM Forms-instans.
1. Markera mappen **[!UICONTROL Global]** och klicka på **[!UICONTROL Create]**.
Sidan **Skapa automatisk formulärkonverteringskonfiguration** visas. Konfigurationen skapas i mappen **Global**. Du kan också skapa konfigurationen i en annan mapp som finns eller skapa en mapp för dina konfigurationer.
   ![Välj global mapp](/help/using/assets/create-afcs-cloud-conf.png)
1. På sidan **[!UICONTROL Create Automated Forms Conversion Configuration]** anger du ett värde för följande fält och klickar på **[!UICONTROL Next]**.

   ![AFCS-konfiguration](/help/using/assets/create-afcs-config.png)

   | Fält | Beskrivning |
   |--- |--- |
   | Titel | Unik rubrik för konfigurationen. Titeln visas i användargränssnittet som används för att starta konverteringen. |
   | Namn | Unikt namn för konfigurationen. Konfigurationen sparas i CRX-databasen med det angivna namnet. Namnet kan vara identiskt med titeln. |
   | Miniatyrplats | Platsen för miniatyrbilden för konfigurationen. |
   | Tjänst-URL | URL för tjänsten Automated Forms Conversion (AFCS) på Adobe Cloud. Använd URL:en `https://aemformsconversion.adobe.io/`. |
   | Mall | Standardmall som ska användas för konverterade formulär. Du kan alltid ange en annan mall innan du påbörjar konverteringen. En mall innehåller grundläggande struktur och ursprungligt innehåll för ett adaptivt formulär. Du kan välja en mall bland de färdiga mallarna. Du kan också skapa en anpassad mall. |
   | Tema | Standardtema som ska användas på konverterade formulär. Du kan alltid ange ett annat tema innan du påbörjar konverteringen.  Du kan klicka på ikonen för att välja ett tema som ingår i rutan. Du kan också skapa ett anpassat tema. |
   | Befintliga segment | Placering av befintliga fragment, om sådana finns. |
   | Anpassad metamodell | Sökväg till .schema.json-filen för anpassad metamodell. Du kan skapa separata metamodeller för engelska, franska, tyska, spanska, italienska och portugisiska. |

1. Ange värdet för följande fält på fliken **[!UICONTROL Advanced]** på sidan **[!UICONTROL Create Automated Forms Conversion Configuration]**:
   ![AFCS-konfiguration](/help/using/assets/afcs-config.png)

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
   <td>(För AEM 6.5) Markera alternativet att aktivera Adobe Analytics för alla konverterade formulär. Kontrollera att Adobe Analytics är aktiverat för din AEM Forms-instans innan du använder alternativet.</td>
   </tr>
   </tbody>
   </table>

   * När källan är ett XFA-baserat formulär med tillägget .XDP, behåller DOR-utdatafilen XFA-layouten, annars använder konverteringstjänsten en mall som inte finns i rutan för att generera DOR för andra XFA-baserade formulär.
   * När ett XFA-formulär skickas sparas data från formuläret som ett XML-element eller ett attribut. Exempel: `<Amount currency="USD"> 10.00 </Amount>`. Valutan sparas som ett attribut och valutabelopp, 10.00 sparas som ett element. Skicka data från ett anpassat formulär har inga attribut, utan bara element. När ett XFA-baserat formulär konverteras till ett adaptivt formulär innehåller de adaptiva uppgifterna för att skicka formulär ett element för varje sådant attribut. Exempel:

   ```css
      {
         "Type": "Principal",
   
         "Amount": "10.00",
   
         "currency": "USD"
      }
   ```

1. Klicka på **[!UICONTROL Create]**. Molnkonfigurationen har skapats. Din AEM Forms-instans är redo att börja konvertera äldre formulär till Adaptiv Forms.
