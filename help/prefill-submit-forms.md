---
title: Rekommenderade arbetsflöden för förifyllnad och inskickning av datakällor för anpassningsbara formulär
seo-title: Alternativ för förifyllning och sändning av anpassade formulär
description: Datakällsbaserade arbetsflöden för förifyllning och sändning av adaptiva formulär som genererats med automatisk Forms Conversion Service.
seo-description: Datakällsbaserade arbetsflöden för förifyllning och sändning av adaptiva formulär som genererats med automatisk Forms Conversion Service.
uuid: 91409a82-141c-4233-82b1-1539a0b250f8
contentOwner: khsingh
topic-tags: forms
discoiquuid: cad34fff-7f9f-4a27-8b5c-d0a523903eec
privatebeta: true
translation-type: tm+mt
source-git-commit: f598871fd41c402f98d94d7b2174ab8b2e487075

---


# Rekommenderade arbetsflöden för förifyllnad och inskickning av datakällor för anpassningsbara formulär {#recommended-data-source-btased-prefill-and-submit-workflows-for-adaptive-forms}

Du kan använda någon av följande datakällor med adaptiva formulär som har konverterats med tjänsten Automated Forms Conversion:

* Formulärdatamodell, OData eller någon annan tredjepartstjänst
* JSON-schema
* XSD-schema

Baserat på datakällan kan du välja att generera ett anpassningsbart formulär med eller utan en datamodell.

I den här artikeln beskrivs de rekommenderade arbetsflödena för att förifylla fältvärden och skicka-alternativ efter att du har valt en datakälla och genererat ett anpassat formulär med hjälp av konverteringstjänsten.

<table> 
 <tbody> 
  <tr> 
   <th><strong>Datakälla</strong></th> 
   <th><strong>Rekommenderat arbetsflöde</strong></th> 
  </tr> 
  <tr> 
   <td><p>Formulärdatamodell, OData eller någon annan tredjepartstjänst</p></td> 
   <td> 
    <p><strong>Alternativ 1</strong>: Du väljer formulärdatamodell, OData eller någon annan tredjepartstjänst som datakälla. Du <a href="#generate-adaptive-forms-with-no-data-binding">genererar ett anpassat formulär utan databindning</a> med hjälp av tjänsten Automated Forms Conversion. Du binder adaptiva formulärfält till formulärdatamodellenheter manuellt och använder alternativet för förifyllningstjänst för formulärdatamodell för att fylla i fältvärden i förväg. Du använder alternativet Skicka med formulärdatamodell för att skicka det adaptiva formuläret.</p></td> 
  </tr>
  <tr> 
   <td></td> 
   <td> 
   <p><strong>Alternativ 2</strong>: Du väljer formulärdatamodell, OData eller någon annan tredjepartstjänst som datakälla. Du <a href="#generate-adaptive-forms-with-no-data-binding">genererar ett anpassat formulär utan databindning</a> med hjälp av tjänsten Automated Forms Conversion. Du binder de adaptiva formulärfälten med regelredigeraren till förifyllda fältvärden. Ändra fältvärdena, om det behövs, och skicka data till crx-databasen.</p>
    </td> 
  </tr>
  <tr> 
   <td></td> 
   <td> 
    <p>Stegvisa instruktioner för hur du kör dessa arbetsflöden finns i <a href="#sqldatasource">Använd databas, OData eller en tredjepartstjänst som datakälla.</a></p> </td> 
  </tr>
  <tr>
  <td><p>JSON-schema</p></td> 
   <td> 
    <p>Du väljer JSON-schema som datakälla. Baserat på den valda datakällan:</p></td> 
  </tr>
  <tr>
  <td></td> 
   <td> 
    <p><strong>Alternativ 1</strong>: Du <a href="#generate-adaptive-forms-with-no-data-binding">genererar ett anpassat formulär utan databindning</a> med hjälp av tjänsten Automated Forms Conversion och konfigurerar JSON-schemat som datakälla. Du binder de adaptiva formulärfälten till JSON-schemat manuellt och <a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/prepopulate-adaptive-form-fields.html#Supportedprotocolsforprefillinguserdata" target="_blank">använder något av de protokoll</a> som stöds för att förifylla fältvärden. Ändra fältvärdena, om det behövs, och skicka data till crx-databasen.</p></td> 
  </tr>
  <tr>
  <td></td> 
   <td> 
    <p>Stegvisa instruktioner för att köra arbetsflöden finns i <a href="#jsondatasource">Använda JSON-schema som datakälla.</p></td> 
  </tr>
  <tr>
  <td></td> 
   <td> 
    <p><strong>Alternativ 2</strong>: Du <a href="#generate-adaptive-forms-with-json-binding">genererar ett anpassat formulär med JSON-databindning</a> med hjälp av tjänsten Automated Forms Conversion. Förifyllningstjänsten och funktionen för att skicka formulär fungerar smidigt. Du behöver inte utföra några konfigurationssteg.</p> </td> 
  </tr>
   <tr>
  <td></td> 
   <td> 
    <p>Stegvisa instruktioner för att köra arbetsflöden finns i <a href="#jsonwithdatabinding">Använda JSON-schema som datakälla.</a></p> </td> 
  </tr>
  <tr>
  <td><p>XSD-schema</p></td> 
   <td> 
    <p>Du väljer XSD-schema som datakälla. Baserat på den valda datakällan <a href="#generate-adaptive-forms-with-no-data-binding">genererar du ett adaptivt formulär utan databindning</a> med hjälp av tjänsten Automated Forms Conversion och konfigurerar XSD-schemat som datakälla. Du binder de adaptiva formulärfälten till XSD-schemat manuellt och <a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/prepopulate-adaptive-form-fields.html#Supportedprotocolsforprefillinguserdata" target="_blank">använder något av de protokoll</a> som stöds för att förifylla fältvärden. Ändra fältvärdena, om det behövs, och skicka data till crx-databasen.</p>
    </td> 
  </tr>
  <tr>
  <td></td> 
   <td> 
    <p>Stegvisa instruktioner för att köra arbetsflöden finns i <a href="#xsddatasource">Använda XSD-schema som datakälla.</a></p>
    </td> 
  </tr>
 </tbody> 
</table>


Mer information om tjänsten Automated Forms Conversion finns i följande artiklar:

* [Introduktion till tjänsten Automatiserad formulärkonvertering](introduction.md)
* [Konfigurera tjänsten Automated Forms Conversion](configure-service.md)
* [Konvertera tryckta formulär till anpassningsbara formulär](convert-existing-forms-to-adaptive-forms.md)
* [Granska och korrigera konverterade formulär](review-correct-ui-edited.md)

Informationen i den här artikeln bygger på antagandet att alla som läser den har grundläggande kunskaper i adaptiva formulärkoncept.

## Krav {#pre-requisites}

* Konfigurera en [AEM-författarinstans](https://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/deploy.html)
* Konfigurera [tjänsten Automated Forms Conversion på AEM-författarinstansen](configure-service.md)

## Exempel på anpassningsbart formulär {#sample-adaptive-form}

Ladda ned följande PDF-exempelfil om du vill köra användningsexemplen för att förifylla fältvärden i ett adaptivt formulär och skicka dem till datakällan.

Exempelblankett för låneansökan

[Hämta fil](assets/sample_loan_application_form.pdf)

PDF-filen fungerar som indata till tjänsten Automated Forms Conversion. Tjänsten konverterar den här filen till ett anpassat formulär. Följande bild visar exempellåneansökan i PDF-format.

![exempelformulär för låneansökan](assets/sample_form_new.png)

## Förbered data för formulärmodellen {#prepare-data-for-form-model}

Med dataintegrering i AEM Forms kan du konfigurera och ansluta till olika datakällor. När du har genererat ett anpassat formulär med konverteringsprocessen kan du definiera formulärmodellen baserat på en formulärdatamodell, XSD eller ett JSON-schema. Du kan använda en databas, Microsoft Dynamics eller någon annan tredjepartstjänst för att skapa en formulärdatamodell.

I den här självstudien används MySQL-databasen som källa för att skapa en formulärdatamodell. Skapa ett **lokalt** ansökningsschema i databasen och lägg till en **ansökartabell** i schemat baserat på de fält som är tillgängliga i det adaptiva formuläret.

![Exempeldata mysql](assets/sample_data_mysql.png)

Du kan använda följande DDL-programsats för att skapa **databastabellen** .

```sql
CREATE TABLE `applicant` (
   `name` varchar(45) DEFAULT NULL,
   `address` varchar(45) DEFAULT NULL,
   `phonenumber` int(11) NOT NULL,
   `email` varchar(45) DEFAULT NULL,
   `occupation` varchar(45) DEFAULT NULL,
   `annualsalary` varchar(45) DEFAULT NULL,
   `familymembers` int(11) DEFAULT NULL,
   PRIMARY KEY (`phonenumber`)
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

Om du använder ett XSD-schema som formulärmodell för att köra användningsexemplen skapar du en XSD-fil med följande text:

```xml
<?xml version="1.0" encoding="utf-8" ?>
    <xs:schema targetNamespace="http://adobe.com/sample.xsd"
                    xmlns="http://adobe.com/sample.xsd"
                    xmlns:xs="http://www.w3.org/2001/XMLSchema">

<xs:element name="sample" type="SampleType"/>

  <xs:complexType name="SampleType">
    <xs:sequence>
      <xs:element name="name" type="xs:string"/>
   <xs:element name="address" type="xs:string"/>
   <xs:element name="phonenumber" type="xs:int"/>
   <xs:element name="email" type="xs:string"/>
   <xs:element name="occupation" type="xs:string"/>
   <xs:element name="annualsalary" type="xs:string"/>
   <xs:element name="familymembers" type="xs:string"/>
 </xs:sequence>
  </xs:complexType>

  </xs:schema>
```

Eller hämta XSD-schemat till det lokala filsystemet.

Exempel på XSD-schema för låneansökan

[Hämta fil](assets/loanapplication.xsd)

Mer information om hur du använder XSD-schema som formulärmodell i adaptiva formulär finns i [Skapa adaptiva formulär med hjälp av XML-schema](https://helpx.adobe.com/experience-manager/6-5/forms/using/adaptive-form-xml-schema-form-model.html).

Om du använder ett JSON-schema som formulärmodell för att köra användningsfallen, skapar du en JSON-fil med följande text:

```JSON
{
    "$schema": "http://json-schema.org/draft-04/schema#",
    "definitions": {
        "loanapplication": {
            "type": "object",
            "properties": {
                "name": {
                    "type": "string"
                },
                "address": {
                    "type": "string"
                },
    "phonenumber": {
                    "type": "number"
                },
    "email": {
                    "type": "string"
                },
    "occupation": {
                    "type": "string"
                },
    "annualsalary": {
                    "type": "string"
                },
    "familymembers": {
                    "type": "number"
                }
            }
        }
 },
 "type": "object",
    "properties": {
        "employee": {
            "$ref": "#/definitions/loanapplication"
        }
    }
}
```

Eller hämta JSON-schemat till det lokala filsystemet.

Exempelschema för låneansökan - JSON

[Hämta fil](assets/demo_schema.json)

Mer information om hur du använder JSON-schema som formulärmodell i adaptiva formulär finns i [Skapa adaptiva formulär med JSON-schema](https://helpx.adobe.com/experience-manager/6-5/forms/using/adaptive-form-json-schema-form-model.html).

## Generera anpassningsbara formulär utan databindning {#generate-adaptive-forms-with-no-data-binding}

Använd tjänsten [Automated Forms Conversion för att konvertera](convert-existing-forms-to-adaptive-forms.md) exempellåneblanketten [](#sample-adaptive-form) till en anpassningsbar blankett utan databindning. Kontrollera att du markerar kryssrutan **[!UICONTROL Generate adaptive form(s) without data bindings]** för att generera det adaptiva formuläret utan databindning.

![Anpassad form utan databindning](assets/generate_af_without_binding.png)

När du har genererat ett anpassat formulär utan databindning väljer du en datakälla för det anpassningsbara formuläret:

* [Databas, OData eller någon tredjepartstjänst](#sqldatasource)
* [JSON-schema](#jsondatasource)
* [XSD-schema](#xsddatasource)

>[!NOTE]
> Om det adaptiva formuläret som du konverterar med hjälp av tjänsten Automated Forms Conversion innehåller flera fält med samma namn, ska du se till att dessa fält är bundna till datakällenheter för att undvika eventuella dataförluster under överföringen.


### Använd databas, OData eller någon annan tjänst från tredje part som datakälla {#sqldatasource}

Användningsfall: Du genererar ett adaptivt formulär utan databindning med hjälp av tjänsten Automated Forms Conversion och konfigurerar MYSQL-databasen som datakälla. Du binder adaptiva formulärfält till formulärdatamodellenheter manuellt och använder alternativet för att fylla i fältvärden i förväg **[!UICONTROL Form Data Model Prefill Service]** . Du kan använda alternativet **[!UICONTROL Submit using Form Data Model]** för att skicka det adaptiva formuläret.

Innan användningsexemplet körs:

* [Konfigurera MySQL-databasen som datakälla](https://helpx.adobe.com/experience-manager/6-5/forms/using/configure-data-sources.html#configurerelationaldatabase)
* [Skapa formulärdatamodellen](https://helpx.adobe.com/experience-manager/6-5/forms/using/work-with-form-data-model.html)

Baserat på användningsfallet skapar du **formulärdatamodellen för** låneprogrammet och binder lästjänstargumentet till ett **[!UICONTROL Literal]** värde. Det literala värdet för telefonnummer måste vara en av de poster som konfigurerats i det **sökande** schemat i MySQL-databasen. Tjänsterna använder värdet som argument för att hämta information från datakällan. Du kan också välja [Användarprofilattribut eller Begär attribut](https://helpx.adobe.com/experience-manager/6-5/forms/using/work-with-form-data-model.html#bindargument) i den **[!UICONTROL Binding To]** nedrullningsbara listan

![Konfigurera formulärdatamodell](assets/configure_model_object.png)

>[!NOTE]
>
>Se till att du lägger till **get** - och **insert** -tjänster i formulärdatamodellen, konfigurerar och testar tjänsterna innan du kör användningsexemplet.

Utför följande steg:

1. Välj det konverterade **exempelformuläret** för låneansökan i **[!UICONTROL output]** mappen och tryck sedan på **[!UICONTROL Properties]**.
1. Tryck på **[!UICONTROL Form Model]** fliken, välj **[!UICONTROL Form Data Model]** i den **[!UICONTROL Select From]** nedrullningsbara listan och tryck på **[!UICONTROL Select Form Data Model]** för att välja datamodellen för **låneprogramformulär** . Tryck **[!UICONTROL Save & Close]** för att spara formuläret.
1. Välj **exempelformuläret** för låneansökan och tryck **[!UICONTROL Edit]**.
1. Tryck på ikonen Konfigurera på **[!UICONTROL Content]** fliken:

   ![konfigurera formulärbehållare](assets/configure_form_container.png)

   1. I **[!UICONTROL Basic]** avsnittet väljer du **[!UICONTROL Form Data Model Prefill service]** i **[!UICONTROL Prefill Service]** listrutan.

   1. I **[!UICONTROL Submission]** avsnittet väljer du **[!UICONTROL Submit using Form Data Model]** i **[!UICONTROL Submit Action]** listrutan.

   1. Markera datamodellen med hjälp av **[!UICONTROL Data Model to submit]** fältet.
   1. Tryck på ![ikonen](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/chart-component/Done_Icon.png) Klar för att spara egenskaperna.

1. Tryck på textrutan Sökandes namn och välj ![konfigurationsikonen](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/configure_icon.png) (Konfigurera).

   1. Välj **Sökande** > **Namn** i fältet Bindningsreferens och tryck på ![ikonen](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/chart-component/Done_Icon.png) Klart för att spara egenskaperna. Skapa på samma sätt en databindning för **adress**, **telefonnummer**, **e-post**, **yrke**, **årlig lön (i dollar)****och¥No. av beroende familjemedlemmars** fält med formulärdatamodellsenheter.
   ![Bindningsreferenser](assets/bind_references.png)

1. Tryck **[!UICONTROL Preview]** för att visa förfyllda värden för anpassade formulärfält.
1. Ändra fältvärdena, om det behövs, och skicka det anpassade formuläret. Fältvärdena skickas till MySQL-databasen. Du kan uppdatera den **ansökande** tabellen i databasen för att visa de uppdaterade värdena i tabellen.

**** Användningsfall: Du genererar ett adaptivt formulär utan databindning med hjälp av tjänsten Automated Forms Conversion och konfigurerar MYSQL-databasen som datakälla. Du binder de adaptiva formulärfälten med regelredigeraren till förifyllda fältvärden. Ändra fältvärdena, om det behövs, och skicka data till crx-databasen.

Utför följande steg för att använda [regelredigeraren](https://helpx.adobe.com/experience-manager/6-5/forms/using/rule-editor.html) för att anropa formulärdatamodelltjänsten för att binda fält och förifyllda värden i ett anpassat formulär:

1. Markera **exempelformuläret** för låneansökan i **[!UICONTROL output]** mappen och tryck sedan på **[!UICONTROL Edit]**.
1. Tryck på ikonen Konfigurera på **[!UICONTROL Content]** fliken:

   ![konfigurera formulärbehållare](assets/configure_form_container.png)

   I **[!UICONTROL Basic]** avsnittet väljer du **[!UICONTROL Form Data Model Prefill service]** i **[!UICONTROL Prefill Service]** listrutan.

1. Tryck på **[!UICONTROL Applicant Name]** textrutan och tryck på **[!UICONTROL Edit Rules]**.

   ![Redigera regler för att skapa databindning](assets/edit_rules_bind_reference.png)

1. Tryck **[!UICONTROL Create]** på sidan Regelredigerare.
1. På **[!UICONTROL Rule Editor]** sidan:

   1. Välj ett tillstånd för textrutan Sökandes namn. Detta **[!UICONTROL is initialized]** resulterar exempelvis i att **[!UICONTROL Then]** villkoret verkställs när du återger formuläret i **[!UICONTROL Preview]** läge.

   1. I **[!UICONTROL Then]** avsnittet väljer du **[!UICONTROL Invoke Service]** i **[!UICONTROL Select Action]** listrutan. Alla tjänster på din Forms-instans visas i listrutan.

   1. Välj en **[!UICONTROL Get]** tjänst i avsnittet med formulärdatamodeller. I indatafältet visas **telefonnummer**, som är den primära nyckel som definierats för den **sökande** datamodellen. Systemet hämtar och fyller i förväg i värdena i det anpassade formuläret för fält i utdataavsnittet baserat på det här fältet.

   1. Skapa en bindning för anpassade formulärfält med formulärdatamodellenheter med hjälp av avsnittet Utdata. Du kan t.ex. binda **[!UICONTROL Applicant Name]** adaptiva formulärfält med **namnentiteten** .

   1. Tryck **[!UICONTROL Done]**. Tryck **[!UICONTROL Done]** igen på sidan Regelredigerare.
   ![Regelredigerare som binder referenser](assets/rule_editor_bind_references.png)

1. Tryck **[!UICONTROL Preview]** för att visa förfyllda värden för anpassade formulärfält.

   >[!NOTE]
   >
   >Se till att egenskapen **[!UICONTROL Return Array]** är AV för egenskapen **get** service i formulärdatamodellen som är kopplad till det adaptiva formuläret.

1. Ändra fältvärdena, om det behövs, och skicka det anpassade formuläret. De data som skickas finns på följande plats i crx-databasen:

   `http://host name:port/crx/de/index.jsp#/content/forms/fp/admin/submit/data/latest file available in the folder`

### Använd JSON-schema som datakälla {#jsondatasource}

**** Användningsfall: Du genererar ett anpassat formulär utan databindning med hjälp av tjänsten Automated Forms Conversion och konfigurerar JSON-schemat som datakälla. Du binder de adaptiva formulärfälten till JSON-schemat manuellt och använder alternativet **Förhandsgranska med data** för att förifylla fältvärden. Ändra fältvärdena, om det behövs, och skicka data till crx-databasen.

Kontrollera att du har:

* [ett giltigt JSON-schema som är kompatibelt med JSON-schemastrukturen](#prepare-data-for-form-model)
* [ett anpassningsbart formulär utan databindning](#generate-adaptive-forms-with-no-data-binding)

Utför följande steg:

1. Välj det konverterade **exempelformuläret** för låneansökan i **utdatamappen** och tryck **[!UICONTROL Properties]**.
1. Tryck på **[!UICONTROL Form Model]** fliken, välj **[!UICONTROL Schema]** i den **[!UICONTROL Select From]** nedrullningsbara listan och tryck på **[!UICONTROL Select Schema]** för att överföra det **demo.schema-JSON** -schema som har sparats i det lokala filsystemet. Tryck **[!UICONTROL Save & Close]** för att spara formuläret.
1. Välj **exempelformuläret** för låneansökan och tryck **[!UICONTROL Edit]**.
1. Tryck på textrutan Sökandes namn och välj ![konfigurationsikonen](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/configure_icon.png) (Konfigurera).

   Välj **Sökande** > **Namn** i fältet Bindningsreferens och tryck på ![ikonen](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/chart-component/Done_Icon.png) Klart för att spara egenskaperna. Skapa på samma sätt en databindning för **adress**, **telefonnummer**, **e-post**, **yrke**, **årlig lön (i dollar)****och¥No. av beroende familjemedlemmsfält** med JSON-schemaentiteter.

1. Markera det konverterade **exempellåneansökningsformuläret** som finns i **[!UICONTROL output]** mappen igen och välj **[!UICONTROL Preview]** > **[!UICONTROL Preview with Data]**.</br>

   Hämta exempeldatafil</br>

   [Hämta fil](assets/json_data_file.txt)</br>

1. Ändra fältvärdena, om det behövs, och skicka det anpassade formuläret. De data som skickas finns på följande plats i crx-databasen:

   `http://host name:port/crx/de/index.jsp#/content/forms/fp/admin/submit/data/latest file available in the folder`

### Använd XSD-schema som datakälla {#xsddatasource}

**** Användningsfall: Du genererar ett anpassat formulär utan databindning med hjälp av tjänsten Automated Forms Conversion och konfigurerar XSD-schemat som datakälla. Du binder de adaptiva formulärfälten till XSD-schemat manuellt och använder **Förhandsgranska med data** för att förifylla fältvärden. Ändra fältvärdena, om det behövs, och skicka data till crx-databasen.

Kontrollera att du har:

* [ett giltigt XSD-schema som är kompatibelt med XML-schemastrukturen](#prepare-data-for-form-model)
* [ett anpassningsbart formulär utan databindning](#generate-adaptive-forms-with-no-data-binding)

Utför följande steg:

1. Välj det konverterade **exempelformuläret** för låneansökan i **[!UICONTROL output]** mappen och tryck sedan på **[!UICONTROL Properties]**.
1. Tryck på **[!UICONTROL Form Model]** fliken, välj **[!UICONTROL Schema]** i den **[!UICONTROL Select From]** nedrullningsbara listan och tryck på **[!UICONTROL Select Schema]** för att överföra **det XSD-schema som sparats i det lokala filsystemet** . Välj rotelementet för XSD-schemat och tryck på **[!UICONTROL Save & Close]** för att spara formuläret.
1. Välj **exempelformuläret** för låneansökan och tryck **[!UICONTROL Edit]**.
1. Tryck på textrutan Sökandes namn och välj ![konfigurationsikonen](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/configure_icon.png) (Konfigurera).
I fältet Bindningsreferens väljer du **Sökande** > **Namn** och trycker på ![Klar-ikonen](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/chart-component/Done_Icon.png) för att spara egenskaperna. Skapa på samma sätt en databindning för **adress**, **telefonnummer**, **e-post**, **yrke**, **årlig lön (i dollar)****och¥No. av beroende familjemedlemmsfält** med XSD-schemaentiteter.

1. Markera det konverterade **exempellåneansökningsformuläret** som finns i **utdatamappen** igen och välj **[!UICONTROL Preview]** > **[!UICONTROL Preview with Data]**.</br>

   Hämta exempeldatafil</br>

   [Hämta fil](assets/loan-application-data-xml-data.zip)</br>


1. Ändra fältvärdena, om det behövs, och skicka det anpassade formuläret. De data som skickas finns på följande plats i crx-databasen:

   `http://host name:port/crx/de/index.jsp#/content/forms/fp/admin/submit/data/latest file available in the folder`

## Generera anpassningsbara formulär med JSON-bindning {#generate-adaptive-forms-with-json-binding}

Använd tjänsten [Automated Forms Conversion för att konvertera](convert-existing-forms-to-adaptive-forms.md) [exempellåneansökningsformuläret](#sample-adaptive-form) till ett anpassningsbart formulär med databindning. Se till att du inte markerar **[!UICONTROL Generate adaptive form(s) without data bindings]** kryssrutan när du genererar det anpassade formuläret.

![Adaptiv form med JSON-bindning](assets/generate_af_with_data_bindings.png)

### Använd JSON-schema som datakälla {#jsonwithdatabinding}

**** Användningsfall: Du genererar ett anpassat formulär med JSON-databindning med hjälp av tjänsten Automated Forms Conversion. Förifyllningstjänsten och funktionen för att skicka formulär fungerar smidigt. Du behöver inte utföra några konfigurationssteg.

Kontrollera att du har [ett anpassningsbart formulär med databindning](#generate-adaptive-forms-with-json-binding)innan du kör användningsexemplet.

Utför följande steg:

1. Markera det konverterade **exempellåneansökningsformuläret** som finns i **[!UICONTROL output]** mappen igen och välj **[!UICONTROL Preview]** > **[!UICONTROL Preview with Data]**.</br>

   Hämta exempeldatafil</br>

   [Hämta fil](assets/loan_application_data_source_json_data_binding.txt)</br>

1. Ändra fältvärdena, om det behövs, och skicka det anpassade formuläret. De data som skickas finns på följande plats i crx-databasen:

   `http://host name:port/crx/de/index.jsp#/content/forms/fp/admin/submit/data/latest file available in the folder`

## Konvertera inskickade JSON-data från adaptiva formulär till XML-format {#convert-submitted-adaptive-form-data-to-xml}

När du anger värden i anpassningsbara formulärfält och skickar dem är data tillgängliga i JSON-format i crx-databasen. Du kan konvertera formatet JSON-data till XML antingen med [API:t org.apache.sling.Commons.json.xml](https://sling.apache.org/apidocs/sling5/org/apache/sling/commons/json/xml/XML.html#toString) eller med följande exempelkod:

```
import org.apache.sling.commons.json.JSONException;
import org.apache.sling.commons.json.JSONObject;
import org.apache.sling.commons.json.xml.XML;
 
public class ConversionUtils {
 
    public static String jsonToXML(String jsonString) throws JSONException {
        //https://sling.apache.org/apidocs/sling5/org/apache/sling/commons/json/xml/XML.html#toString(java.lang.Object)
        //jar - http://maven.ibiblio.org/maven2/org/apache/sling/org.apache.sling.commons.json/2.0.18/
        //Note: Need to extract boundData part before converting to XML
        return XML.toString(new JSONObject(jsonString));
    }
}
```
