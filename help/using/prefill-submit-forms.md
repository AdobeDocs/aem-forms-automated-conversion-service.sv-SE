---
title: Rekommenderade arbetsflöden för förifyllnad och inskickning av datakällor för anpassningsbara formulär
description: Datakällsbaserade arbetsflöden för förifyllning och sändning av anpassningsbara formulär som genererats med tjänsten Automated forms conversion (AFCS).
solution: Experience Manager Forms
feature: Adaptive Forms
topic: Administration
topic-tags: forms
role: Admin, Developer
level: Beginner, Intermediate
contentOwner: khsingh
exl-id: 5deef8f5-5098-47c1-b696-b2db59e92931
source-git-commit: c2392932d1e29876f7a11bd856e770b8f7ce3181
workflow-type: tm+mt
source-wordcount: '2397'
ht-degree: 0%

---

# Rekommenderade arbetsflöden för förifyllnad och inskickning av datakällor för anpassningsbara formulär {#recommended-data-source-btased-prefill-and-submit-workflows-for-adaptive-forms}

Du kan använda någon av följande datakällor med adaptiva formulär som har konverterats med tjänsten Automated forms conversion (AFCS):

* Formulärdatamodell, OData eller någon annan tredjepartstjänst
* JSON-schema
* XSD-schema

Baserat på datakällan kan du välja att generera ett anpassningsbart formulär med eller utan en datamodell.

I den här artikeln beskrivs de rekommenderade arbetsflödena för att förifylla fältvärden och skicka-alternativ efter att du har valt en datakälla och genererat ett anpassat formulär med hjälp av konverteringstjänsten.

<table> 
 <tbody> 
  <tr> 
   <th><strong>Data Source</strong></th> 
   <th><strong>Rekommenderat arbetsflöde</strong></th> 
  </tr> 
  <tr> 
   <td><p>Formulärdatamodell, OData eller någon annan tredjepartstjänst</p></td> 
   <td> 
    <p><strong>Alternativ 1</strong>: Du väljer formulärdatamodell, OData eller någon annan tredjepartstjänst som datakälla. Du <a href="#generate-adaptive-forms-with-no-data-binding">genererar ett anpassat formulär utan databindning</a> med tjänsten Automated forms conversion (AFCS). Du binder adaptiva formulärfält till formulärdatamodellenheter manuellt och använder alternativet för förifyllningstjänst för formulärdatamodell för att fylla i fältvärden i förväg. Du använder alternativet Skicka med formulärdatamodell för att skicka det adaptiva formuläret.</p></td> 
  </tr>
  <tr> 
   <td></td> 
   <td> 
   <p><strong>Alternativ 2</strong>: Du väljer formulärdatamodell, OData eller någon annan tredjepartstjänst som datakälla. Du <a href="#generate-adaptive-forms-with-no-data-binding">genererar ett anpassat formulär utan databindning</a> med tjänsten Automated forms conversion (AFCS). Du binder de adaptiva formulärfälten med regelredigeraren till förifyllda fältvärden. Ändra fältvärdena, om det behövs, och skicka data till crx-databasen.</p>
    </td> 
  </tr>
  <tr> 
   <td></td> 
   <td> 
    <p>Stegvisa instruktioner för att köra dessa arbetsflöden finns i <a href="#sqldatasource">Använd databas, OData eller någon annan tjänst från tredje part som datakälla.</a></p> </td> 
  </tr>
  <tr>
  <td><p>JSON-schema</p></td> 
   <td> 
    <p>Du väljer JSON-schema som datakälla. Baserat på den valda datakällan:</p></td> 
  </tr>
  <tr>
  <td></td> 
   <td> 
    <p><strong>Alternativ 1</strong>: Du <a href="#generate-adaptive-forms-with-no-data-binding">genererar ett adaptivt formulär utan databindning</a> med tjänsten Automated forms conversion (AFCS) och konfigurerar JSON-schemat som datakälla. Du binder de adaptiva formulärfälten till JSON-schemat manuellt och <a href="https://helpx.adobe.com/se/experience-manager/6-5/forms/using/prepopulate-adaptive-form-fields.html#Supportedprotocolsforprefillinguserdata" target="_blank">använder något av de protokoll som stöds</a> för att förifylla fältvärden. Ändra fältvärdena, om det behövs, och skicka data till crx-databasen.</p></td> 
  </tr>
  <tr>
  <td></td> 
   <td> 
    <p>Stegvisa instruktioner för att köra arbetsflöden finns i <a href="#jsondatasource">Använd JSON-schema som datakälla.</p></td> 
  </tr>
  <tr>
  <td></td> 
   <td> 
    <p><strong>Alternativ 2</strong>: Du <a href="#generate-adaptive-forms-with-json-binding">skapar ett anpassat formulär med JSON-databindning</a> med tjänsten Automated forms conversion (AFCS). Förifyllningstjänsten och funktionen för att skicka formulär fungerar smidigt. Du behöver inte utföra några konfigurationssteg.</p> </td> 
  </tr>
   <tr>
  <td></td> 
   <td> 
    <p>Stegvisa instruktioner för att köra arbetsflöden finns i <a href="#jsonwithdatabinding">Använd JSON-schema som datakälla.</a></p> </td> 
  </tr>
  <tr>
  <td><p>XSD-schema</p></td> 
   <td> 
    <p>Du väljer XSD-schema som datakälla. Baserat på den valda datakällan <a href="#generate-adaptive-forms-with-no-data-binding">skapar du ett anpassat formulär utan databindning</a> med tjänsten Automated forms conversion (AFCS) och konfigurerar XSD-schemat som datakälla. Du binder de adaptiva formulärfälten till XSD-schemat manuellt och <a href="https://helpx.adobe.com/se/experience-manager/6-5/forms/using/prepopulate-adaptive-form-fields.html#Supportedprotocolsforprefillinguserdata" target="_blank">använder något av de protokoll som stöds</a> för att förifylla fältvärden. Ändra fältvärdena, om det behövs, och skicka data till crx-databasen.</p>
    </td> 
  </tr>
  <tr>
  <td></td> 
   <td> 
    <p>Stegvisa instruktioner för att köra arbetsflöden finns i <a href="#xsddatasource">Använd XSD-schema som datakälla.</a></p>
    </td> 
  </tr>
 </tbody> 
</table>


Mer information om tjänsten Automated forms conversion (AFCS) finns i följande artiklar:

* [Introduktion till tjänsten Automated forms conversion](introduction.md)
* [Konfigurera tjänsten Automated forms conversion](configure-service.md)
* [Konvertera tryckta formulär till anpassningsbara formulär](convert-existing-forms-to-adaptive-forms.md)
* [Granska och korrigera konverterade formulär](review-correct-ui-edited.md)

Informationen i den här artikeln bygger på antagandet att alla som läser den har grundläggande kunskaper i adaptiva formulärkoncept.

## Krav {#pre-requisites}

* Konfigurera en [AEM författarinstans](https://helpx.adobe.com/se/experience-manager/6-5/sites/deploying/using/deploy.html)
* Konfigurera tjänsten [Automated forms conversion (AFCS) på AEM författarinstans](configure-service.md)

## Exempel på anpassningsbart formulär {#sample-adaptive-form}

Om du vill köra användningsexemplen för att förifylla fältvärden i ett adaptivt formulär och skicka dem till datakällan hämtar du följande exempelfil i PDF.

Exempelblankett för låneansökan

[Hämta fil](assets/sample_loan_application_form.pdf)

Filen PDF fungerar som indata till tjänsten Automated forms conversion (AFCS). Tjänsten konverterar den här filen till ett anpassat formulär. Följande bild visar låneansökan i PDF-format.

![exempellåneansökningsformulär](assets/sample_form_new.png)

## Förbered data för formulärmodellen {#prepare-data-for-form-model}

Med AEM Forms dataintegrering kan du konfigurera och ansluta till olika datakällor. När du har genererat ett anpassat formulär med konverteringsprocessen kan du definiera formulärmodellen baserat på en formulärdatamodell, XSD eller ett JSON-schema. Du kan använda en databas, Microsoft Dynamics eller någon annan tredjepartstjänst för att skapa en formulärdatamodell.

I den här självstudien används MySQL-databasen som källa för att skapa en formulärdatamodell. Skapa ett **låneprogram**-schema i databasen och lägg till en **sökande**-tabell i schemat baserat på de fält som är tillgängliga i det adaptiva formuläret.

![Exempeldata mysql](assets/sample_data_mysql.png)

Du kan använda följande DDL-sats för att skapa tabellen **sökande** i databasen.

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

Mer information om hur du använder XSD-schema som formulärmodell i adaptiva formulär finns i [Skapa adaptiva formulär med XML-schema](https://helpx.adobe.com/se/experience-manager/6-5/forms/using/adaptive-form-xml-schema-form-model.html).

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

Mer information om hur du använder JSON-schema som formulärmodell i adaptiva formulär finns i [Skapa adaptiva formulär med JSON-schema](https://helpx.adobe.com/se/experience-manager/6-5/forms/using/adaptive-form-json-schema-form-model.html).

## Generera anpassningsbara formulär utan databindning {#generate-adaptive-forms-with-no-data-binding}

Använd tjänsten [Automated forms conversion för att konvertera](convert-existing-forms-to-adaptive-forms.md) exempellåneansökningsformuläret [&#128279;](#sample-adaptive-form) till ett anpassningsbart formulär utan databindning. Kontrollera att du markerar kryssrutan **[!UICONTROL Generate adaptive form(s) without data bindings]** för att generera det adaptiva formuläret utan databindning.

![Anpassat formulär utan databindning](assets/generate_af_without_binding.png)

När du har genererat ett anpassat formulär utan databindning väljer du en datakälla för det anpassningsbara formuläret:

* [Databas, OData eller någon tredjepartstjänst](#sqldatasource)
* [JSON-schema](#jsondatasource)
* [XSD-schema](#xsddatasource)

>[!NOTE]
> Om det adaptiva formuläret som du konverterar med hjälp av tjänsten Automated forms conversion (AFCS) innehåller flera fält med samma namn måste du se till att dessa fält är bundna till datakällenheter för att undvika eventuella dataförluster under överföringen.
>

### Använd databas, OData eller någon tredjepartstjänst som datakälla {#sqldatasource}

Användningsfall: Du genererar ett adaptivt formulär utan databindning med tjänsten Automated forms conversion (AFCS) och konfigurerar MYSQL-databasen som datakälla. Du binder de adaptiva formulärfälten till entiteter i formulärdatamodellen manuellt och använder alternativet **[!UICONTROL Form Data Model Prefill Service]** för att fylla i fältvärden i förväg. Du använder alternativet **[!UICONTROL Submit using Form Data Model]** för att skicka det adaptiva formuläret.

Innan användningsexemplet körs:

* [Konfigurera MySQL-databasen som datakälla](https://helpx.adobe.com/se/experience-manager/6-5/forms/using/configure-data-sources.html#configurerelationaldatabase)
* [Skapa formulärdatamodellen](https://helpx.adobe.com/se/experience-manager/6-5/forms/using/work-with-form-data-model.html)

Baserat på användningsfallet skapar du formulärdatamodellen **loanapplication** och binder lästjänstargumentet till ett **[!UICONTROL Literal]**-värde. Det literala värdet för telefonnummer måste vara en av de poster som konfigurerats i schemat **sökande** i MySQL-databasen. Tjänsterna använder värdet som argument för att hämta information från datakällan. Du kan också välja [Användarprofilattribut eller Begär attribut](https://helpx.adobe.com/se/experience-manager/6-5/forms/using/work-with-form-data-model.html#bindargument) i listrutan **[!UICONTROL Binding To]**

![Konfigurera formulärdatamodell](assets/configure_model_object.png)

>[!NOTE]
>
>Se till att du lägger till **get**- och **insert**-tjänster i formulärdatamodellen, konfigurerar och testar tjänsterna innan du kör användningsfallet.

Utför följande steg:

1. Välj det konverterade **exempelformuläret för låneansökan** i mappen **[!UICONTROL output]** och tryck sedan på **[!UICONTROL Properties]**.
1. Tryck på fliken **[!UICONTROL Form Model]**, välj **[!UICONTROL Form Data Model]** i listrutan **[!UICONTROL Select From]** och tryck på **[!UICONTROL Select Form Data Model]** för att välja formulärdatamodellen **loanapplication**. Tryck på **[!UICONTROL Save & Close]** för att spara formuläret.
1. Välj **exempellåneansökningsformuläret** och tryck på **[!UICONTROL Edit]**.
1. Tryck på konfigurationsikonen på fliken **[!UICONTROL Content]**:

   ![konfigurera formulärbehållare](assets/configure_form_container.png)

   1. I avsnittet **[!UICONTROL Basic]** väljer du **[!UICONTROL Form Data Model Prefill service]** i listrutan **[!UICONTROL Prefill Service]**.

   1. I avsnittet **[!UICONTROL Submission]** väljer du **[!UICONTROL Submit using Form Data Model]** i listrutan **[!UICONTROL Submit Action]**.

   1. Markera datamodellen med fältet **[!UICONTROL Data Model to submit]**.
   1. Tryck på ikonen ![klar](assets/save_icon.svg) för att spara egenskaperna.

1. Tryck på textrutan Sökandes namn och välj ![Konfigurera ikon](assets/configure_icon.svg) (Konfigurera).

   1. I fältet Bindningsreferens väljer du **Sökande** > **Namn** och trycker på ikonen ![Klart](assets/save_icon.svg) för att spara egenskaperna. Skapa på samma sätt en databindning för **Adress**, **Telefonnummer**, **E-post**, **Yrke**, **Årslön (i dollar)** och **Nej. för beroende familjemedlemmar**-fält med formulärdatamodellentiteter.

   ![Bindningsreferenser](assets/bind_references.png)

1. Tryck på **[!UICONTROL Preview]** för att visa de förfyllda anpassningsbara formulärfältsvärdena.
1. Ändra fältvärdena, om det behövs, och skicka det anpassade formuläret. Fältvärdena skickas till MySQL-databasen. Du kan uppdatera tabellen **sökande** i databasen för att visa de uppdaterade värdena i tabellen.

**Användningsfall:** Du genererar ett adaptivt formulär utan databindning med tjänsten Automated forms conversion (AFCS) och konfigurerar MYSQL-databasen som datakälla. Du binder de adaptiva formulärfälten med regelredigeraren till förifyllda fältvärden. Ändra fältvärdena, om det behövs, och skicka data till crx-databasen.

Utför följande steg för att använda [regelredigeraren](https://helpx.adobe.com/se/experience-manager/6-5/forms/using/rule-editor.html) för att anropa formulärdatamodelltjänsten för att binda fält och förifyllda värden i ett anpassat formulär:

1. Markera **exempelformuläret för låneansökan** i mappen **[!UICONTROL output]** och tryck på **[!UICONTROL Edit]**.
1. Tryck på konfigurationsikonen på fliken **[!UICONTROL Content]**:

   ![konfigurera formulärbehållare](assets/configure_form_container.png)

   I avsnittet **[!UICONTROL Basic]** väljer du **[!UICONTROL Form Data Model Prefill service]** i listrutan **[!UICONTROL Prefill Service]**.

1. Tryck på textrutan **[!UICONTROL Applicant Name]** och tryck på **[!UICONTROL Edit Rules]**.

   ![Redigera regler för att skapa databindning](assets/edit_rules_bind_reference.png)

1. Tryck på **[!UICONTROL Create]** på sidan Regelredigerare.
1. På sidan **[!UICONTROL Rule Editor]**:

   1. Välj ett tillstånd för textrutan Sökandes namn. Till exempel **[!UICONTROL is initialized]**, vilket resulterar i körning av villkoret **[!UICONTROL Then]** när du återger formuläret i läget **[!UICONTROL Preview]**.

   1. I avsnittet **[!UICONTROL Then]** väljer du **[!UICONTROL Invoke Service]** i listrutan **[!UICONTROL Select Action]**. Alla tjänster på din Forms-instans visas i listrutan.

   1. Välj en **[!UICONTROL Get]**-tjänst i det avsnitt som innehåller formulärdatamodeller. Indatafältet visar **phonenumber**, som är den primära nyckel som definierats för datamodellen **sökande**. Systemet hämtar och fyller i förväg i värdena i det anpassade formuläret för fält i utdataavsnittet baserat på det här fältet.

   1. Skapa en bindning för anpassade formulärfält med formulärdatamodellenheter med hjälp av avsnittet Utdata. Du kan t.ex. binda det adaptiva formulärfältet **[!UICONTROL Applicant Name]** till entiteten **name**.

   1. Tryck på **[!UICONTROL Done]**. Tryck på **[!UICONTROL Done]** igen på sidan Regelredigerare.

   ![Regelredigerare som binder referenser](assets/rule_editor_bind_references.png)

1. Tryck på **[!UICONTROL Preview]** för att visa de förfyllda anpassningsbara formulärfältsvärdena.

   >[!NOTE]
   >
   >Kontrollera att egenskapen **[!UICONTROL Return Array]** är inställd på AV för tjänstegenskapen **get** i formulärdatamodellen som är associerad med det adaptiva formuläret.

1. Ändra fältvärdena, om det behövs, och skicka det anpassade formuläret. De data som skickas finns på följande plats i crx-databasen:

   `http://host name:port/crx/de/index.jsp#/content/forms/fp/admin/submit/data/latest file available in the folder`

### Använd JSON-schema som datakälla {#jsondatasource}

**Användningsfall:** Du genererar ett adaptivt formulär utan databindning med tjänsten Automated forms conversion (AFCS) och konfigurerar JSON-schemat som datakälla. Du binder de adaptiva formulärfälten till JSON-schemat manuellt och använder alternativet **Förhandsgranska med data** för att fylla i fältvärden i förväg. Ändra fältvärdena, om det behövs, och skicka data till crx-databasen.

Kontrollera att du har:

* [ett giltigt JSON-schema som är kompatibelt med JSON-schemastrukturen](#prepare-data-for-form-model)
* [ett anpassningsbart formulär utan databindning](#generate-adaptive-forms-with-no-data-binding)

Utför följande steg:

1. Markera det konverterade **exempellåneansökningsformuläret** som finns i mappen **output** och tryck sedan på **[!UICONTROL Properties]**.
1. Tryck på fliken **[!UICONTROL Form Model]**, välj **[!UICONTROL Schema]** i listrutan **[!UICONTROL Select From]** och tryck på **[!UICONTROL Select Schema]** för att överföra det **demo.schema-JSON**-schema som sparats i det lokala filsystemet. Tryck på **[!UICONTROL Save & Close]** för att spara formuläret.
1. Välj **exempellåneansökningsformuläret** och tryck på **[!UICONTROL Edit]**.
1. Tryck på textrutan Sökandes namn och välj ![Konfigurera ikon](assets/configure_icon.svg) (Konfigurera).

   I fältet Bindningsreferens väljer du **Sökande** > **Namn** och trycker på ikonen ![Klart](assets/save_icon.svg) för att spara egenskaperna. Skapa på samma sätt en databindning för **Adress**, **Telefonnummer**, **E-post**, **Yrke**, **Årslön (i dollar)** och **Nej. för beroende familjemedlemmar**-fält med JSON-schemaentiteter.

1. Markera det konverterade **exempellåneansökningsformuläret** som finns i mappen **[!UICONTROL output]** igen och välj **[!UICONTROL Preview]** > **[!UICONTROL Preview with Data]**.</br>

   Hämta exempeldatafilen </br>

   [Hämta fil](assets/json_data_file.txt)</br>

1. Ändra fältvärdena, om det behövs, och skicka det anpassade formuläret. De data som skickas finns på följande plats i crx-databasen:

   `http://host name:port/crx/de/index.jsp#/content/forms/fp/admin/submit/data/latest file available in the folder`

### Använd XSD-schema som datakälla {#xsddatasource}

**Användningsfall:** Du genererar ett adaptivt formulär utan databindning med tjänsten Automated forms conversion (AFCS) och konfigurerar XSD-schemat som datakälla. Du binder de adaptiva formulärfälten till XSD-schemat manuellt och använder **Förhandsgranska med data** för att förifylla fältvärden. Ändra fältvärdena, om det behövs, och skicka data till crx-databasen.

Kontrollera att du har:

* [ett giltigt XSD-schema som är kompatibelt med XML-schemastrukturen](#prepare-data-for-form-model)
* [ett anpassningsbart formulär utan databindning](#generate-adaptive-forms-with-no-data-binding)

Utför följande steg:

1. Välj det konverterade **exempelformuläret för låneansökan** i mappen **[!UICONTROL output]** och tryck sedan på **[!UICONTROL Properties]**.
1. Tryck på fliken **[!UICONTROL Form Model]**, välj **[!UICONTROL Schema]** i listrutan **[!UICONTROL Select From]** och tryck på **[!UICONTROL Select Schema]** för att överföra XSD-schemat **loanapplication** som sparats i det lokala filsystemet. Välj rotelementet för XSD-schemat och tryck på **[!UICONTROL Save & Close]** för att spara formuläret.
1. Välj **exempellåneansökningsformuläret** och tryck på **[!UICONTROL Edit]**.
1. Tryck på textrutan Sökandes namn och välj ![Konfigurera ikon](assets/configure_icon.svg) (Konfigurera).
Välj **Sökande** > **Namn** i fältet Bindningsreferens och tryck sedan på ![Klar ikon](assets/save_icon.svg) för att spara egenskaperna. Skapa på samma sätt en databindning för **Adress**, **Telefonnummer**, **E-post**, **Yrke**, **Årslön (i dollar)** och **Nej. för beroende familjemedlemmar**-fält med XSD-schemaentiteter.

1. Markera det konverterade **exempellåneansökningsformuläret** som finns i mappen **output** igen och välj **[!UICONTROL Preview]** > **[!UICONTROL Preview with Data]**.</br>

   Hämta exempeldatafilen </br>

   [Hämta fil](assets/loan-application-data-xml-data.zip)</br>


1. Ändra fältvärdena, om det behövs, och skicka det anpassade formuläret. De data som skickas finns på följande plats i crx-databasen:

   `http://host name:port/crx/de/index.jsp#/content/forms/fp/admin/submit/data/latest file available in the folder`

## Generera anpassningsbara formulär med JSON-bindning {#generate-adaptive-forms-with-json-binding}

Använd tjänsten [Automated forms conversion (AFCS) för att konvertera](convert-existing-forms-to-adaptive-forms.md) exempellåneansökningsformuläret [&#128279;](#sample-adaptive-form) till ett anpassningsbart formulär med databindning. Kontrollera att du inte markerar kryssrutan **[!UICONTROL Generate adaptive form(s) without data bindings]** när du genererar det adaptiva formuläret.

![Anpassat formulär med JSON-bindning](assets/generate_af_with_data_bindings.png)

### Använd JSON-schema som datakälla {#jsonwithdatabinding}

**Användningsfall:** Du genererar ett adaptivt formulär med JSON-databindning med tjänsten Automated forms conversion (AFCS). Förifyllningstjänsten och funktionen för att skicka formulär fungerar smidigt. Du behöver inte utföra några konfigurationssteg.

Kontrollera att du har [ett adaptivt formulär med databindning](#generate-adaptive-forms-with-json-binding) innan du kör användningsexemplet.

Utför följande steg:

1. Markera det konverterade **exempellåneansökningsformuläret** som finns i mappen **[!UICONTROL output]** igen och välj **[!UICONTROL Preview]** > **[!UICONTROL Preview with Data]**.</br>

   Hämta exempeldatafilen </br>

   [Hämta fil](assets/loan_application_data_source_json_data_binding.txt)</br>

1. Ändra fältvärdena, om det behövs, och skicka det anpassade formuläret. De data som skickas finns på följande plats i crx-databasen:

   `http://host name:port/crx/de/index.jsp#/content/forms/fp/admin/submit/data/latest file available in the folder`

## Konvertera inskickade JSON-data från adaptiva formulär till XML-format {#convert-submitted-adaptive-form-data-to-xml}

När du anger värden i anpassningsbara formulärfält och skickar dem är data tillgängliga i JSON-format i crx-databasen. Du kan konvertera formatet JSON-data till XML antingen med API:t [org.apache.sling.Commons.json.xml](https://sling.apache.org/apidocs/sling5/org/apache/sling/commons/json/xml/XML.html#toString) eller med följande exempelkod:

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
