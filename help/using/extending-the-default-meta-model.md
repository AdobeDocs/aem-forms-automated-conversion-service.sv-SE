---
title: Utöka standardmetamodellen
seo-title: Extend the default meta-model
description: Utöka standardmetamodellen för att lägga till mönster, valideringar och enheter som är specifika för din organisation och tillämpa konfigurationer på anpassningsbara formulärfält medan du kör tjänsten Automated forms conversion.
seo-description: Extend the default meta-model to add pattern, validations, and entities specific to your organization and apply configurations to adaptive form fields while running the Automated Forms Conversion service.
uuid: f98b4cca-f0a3-4db8-aef2-39b8ae462628
topic-tags: forms
discoiquuid: cad72699-4a4b-4c52-88a5-217298490a7c
exl-id: f679059c-18aa-4cb5-8368-ed27e96c20de
source-git-commit: 298d6c0641d7b416edb5b2bcd5fec0232f01f4c7
workflow-type: tm+mt
source-wordcount: '2565'
ht-degree: 0%

---

# Utöka standardmetamodellen {#extend-the-default-meta-model}

Tjänsten Automated forms conversion identifierar och extraherar formulärobjekt från källformulär. Semantisk mappning hjälper tjänsten att bestämma hur de extraherade objekten ska visas i en adaptiv form. Ett källformulär kan t.ex. ha många olika typer av representationer av ett datum. Med semantisk mappning kan du mappa alla representationer av formulärobjekt för datum i källformuläret med datumkomponenten i de adaptiva formulären. Med semantisk mappning kan tjänsten förkonfigurera och tillämpa valideringar, regler, datamönster, hjälptext och hjälpmedelsegenskaper på adaptiva formulärkomponenter under konverteringen.

![](assets/meta-model.gif)

Metamodellen är ett JSON-schema. Innan du börjar med metamodellen måste du se till att du är väl insatt i JSON. Du måste ha erfarenhet av att skapa, redigera och läsa data som sparats i JSON-format.

## Standardmetamodell {#default-meta-model}

Tjänsten Automated forms conversion har en standardmetamodell. Det är ett JSON-schema och finns i Adobe Cloud tillsammans med andra komponenter i tjänsten Automated forms conversion. Du kan hitta en kopia av metamodellen på den lokala AEM på: http://&lt;server>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/metamodel/`global.schema.json`. Du kan också [klicka här](assets/en.globalschema.json) för att få tillgång till eller ladda ned det engelska språkschemat. Metamodellen för [Franska](assets/fr.globalschema.json), [Tyska](assets/de.globalschema.json) [Spanska](assets/es.globalschema.json), [Italienska](assets/it.globalschema.json)och [Portugisiska](assets/pt_br.globalschema.json) finns också för nedladdning.

Schemat för metamodellen härleds från schemaentiteter på https://schema.org/docs/schemas.html. Den har Person, PostalAddress, LocalBusiness och fler entiteter enligt definitionen på https://schema.org. Alla entiteter i metamodellen följer JSON-schemaobjekttypen. Följande kod representerar en exempelmetamodellstruktur:

```
   "Entity": {
      "id": "Entity",
      "properties": {
        "name": {
          "type": "string"
        },

        "description": {
          "type": "string",
          "description": "Description of the item"
        }
      }
    }
```

## Hämta standardmetamodellen {#download-the-default-meta-model}

Följ de här stegen för att hämta standardmetamodellen till det lokala filsystemet:

1. Logga in på din AEM Forms-instans.
1. Navigera till **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]** **>** **[!UICONTROL Meta Model]** mapp.
1. Välj **[!UICONTROL global.schema.json]** fil och trycka **[!UICONTROL Download]**. En dialogruta för hämtning visas. Välj **[!UICONTROL Download asset(s) as binary files]** alternativ. Tryck på **[!UICONTROL Download]**. Ett arkiv laddas ned.

   <!--
   Comment Type: draft

   <li><p>Extract the archive and open the global.schema.json file for editing. </p> </li>
   -->

   <!--
   Comment Type: draft

   <li>Step text</li>
   -->

## Metamodellen {#understanding-the-meta-model}

En metamodell refererar till en JSON-schemafil som innehåller entiteter. Alla entiteter i JSON-schemafilen innehåller ett namn och ett ID. Varje entitet kan innehålla flera egenskaper. Enheterna och dess egenskaper kan variera beroende på domän. Du kan utöka en schemafil med nyckelord och fältkonfigurationer för att mappa schemaegenskaper till adaptiva formulärkomponenter.

```
"Event": {
      "id": "Eventid",
      "allOf": [
        {
          "$ref": "#Entity"
        },
        {
          "properties": {
            "startDate": {
              "type": "string",
              "format": "date",
              "description": "Specify the start date and time of the event in ISO 8601 date format."
            },
            "endDate": {
              "type": "string",
              "format": "date",
              "description": "Specify the end date and time of the event in ISO 8601 date format."
            },
            "location": {
              "$ref": "#PostalAddress",
              "description": "Specify the location of the event."
            }
          }
        }
      ]
    }
```

I det här exemplet **Händelse** representerar namnet på en entitet med ett värde för **id** as **Eventid**. Händelseentiteten innehåller flera egenskaper:

* startDate
* endDate
* plats

The **allOf** i metamodellen aktiverar arv mellan entiteter.

Varje egenskap kan dessutom innehålla:

* [JSON-schemaegenskaper](#jsonschemaproperties)
* [Nyckelordsbaserad sökning som använder egenskaper för genererade adaptiva formulärfält](#keywordsearch)
* [Ytterligare egenskaper](#additionalproperties)

![Metamodegenskaper](assets/meta_model_elements.gif)

Baserat på de nyckelord som refereras med **aem:affKeyword** utför konverteringstjänsten en sökåtgärd på källformulärfälten. Konverteringstjänsten använder JSON-schemaegenskaperna och ytterligare egenskaper för de fält som uppfyller sökvillkoren.

I det här exemplet söker konverteringstjänsten efter nyckelorden telefon, telefon, mobiltelefon, arbetstelefon, hemtelefon, telefonnummer, telefonnummer och telefonnummer i källformuläret. Baserat på de fält som innehåller dessa nyckelord använder konverteringstjänsten typ, mönster och aem:afProperties på de adaptiva formulärfälten efter konverteringen.

### JSON-schemaegenskaper för genererade adaptiva formulärfält {#jsonschemaproperties}

Metamodellen stöder följande gemensamma egenskaper för JSON-schema för adaptiva formulärfält som genereras med tjänsten Automated forms conversion:

<table> 
 <tbody> 
  <tr> 
   <th><strong>Egenskapsnamn</strong></th> 
   <th><strong>Beskrivning</strong></th> 
  </tr> 
  <tr> 
   <td><p>title</p></td> 
   <td> 
    <p>Texten som omnämns i egenskapen title i en metamodell fungerar som ett söknyckelord för att utföra åtgärder i de genererade adaptiva formulärfälten. Du kan till exempel ändra etiketten för ett adaptivt formulärfält. Mer information finns i <strong>Ändra etiketten för ett formulärfält</strong> in <a href="#custommetamodelexamples">Exempel på anpassade metamodeller.</a></p> </td> 
  </tr>
  <td><p>description</p></td> 
   <td> 
    <p>Egenskapen description anger hjälptexten för det genererade adaptiva formulärfältet. Mer information finns i <strong>Lägga till hjälptext i ett formulärfält</strong> in <a href="#custommetamodelexamples">Exempel på anpassade metamodeller.</a></p> </td> 
  </tr>
  <td><p>type</p></td> 
   <td> 
    <p>Egenskapen type definierar datatypen för det genererade adaptiva formulärfältet. Möjliga värden för egenskapen title är:</p>
    <ul> 
     <li>sträng: Skapar ett anpassat formulärfält av textdatatyp.</li> 
     <li>tal: Skapar ett adaptivt formulärfält av numerisk datatyp.</li>
     <li>heltal: Skapar ett adaptivt formulärfält av numerisk datatyp med subtype inställd på heltal.</li>
     <li>boolesk: Skapar en adaptiv formulärkomponent för switch.</li>
     </ul><p>Mer information om hur du använder egenskapen type i en metamodell finns i <strong>Ändra typ av formulärfält</strong> in <a href="#custommetamodelexamples">Exempel på anpassade metamodeller.</a></p></td> 
  </tr>
  <td><p>mönster</p></td> 
   <td> 
    <p>Egenskapen pattern begränsar värdet för det genererade adaptiva formulärfältet baserat på ett reguljärt uttryck. Följande kod i metamodellen begränsar till exempel värdet för det genererade adaptiva formulärfältet till tio siffror:<br>"pattern": "/\\d{10}/"<br>Följande kod i metamodellen begränsar på liknande sätt värdet för ett fält till ett visst datumformat.<br> "pattern": "date{DD MMMM, YYYY}",</p> </td> 
  </tr>
  <td><p>format</p></td> 
   <td> 
    <p>Formategenskapen begränsar värdet för det genererade adaptiva formulärfältet baserat på ett namngivet mönster i stället för ett reguljärt uttryck. Möjliga värden för formategenskapen är:<ul><li>e-post: Skapar en formulärkomponent för e-postanpassning.</li><li>värdnamn: Skapar en adaptiv formulärkomponent för textrutor.</li></ul>Mer information om hur du använder formategenskapen i en metamodell finns i <strong>Ändra format för ett formulärfält</strong> in <a href="#custommetamodelexamples">Exempel på anpassade metamodeller.</a></p> </td> 
  </tr>
  <td><p>enum och enumNames</p></td> 
   <td> 
    <p>Egenskaperna enum och enumNames begränsar värdena för fälten för nedrullningsbara menyer, kryssrutor och alternativknappar till en fast uppsättning. Värden som anges i enumNames visas i användargränssnittet. Värdena som anges med enum-egenskapen används för beräkning.<br>Mer information finns i <strong>Konvertera ett formulärfält till kryssrutor med flera val i det adaptiva formuläret</strong>, <strong>Konvertera ett textfält till nedrullningsbar lista i det adaptiva formuläret</strong>och <strong>Lägg till ytterligare alternativ i listrutan</strong> in <a href="#custommetamodelexamples">Exempel på anpassade metamodeller.</a></p> </td> 
  </tr>
 </tbody> 
</table>

### Nyckelordsbaserad sökning som använder egenskaper för genererade adaptiva formulärfält {#keywordsearch}

Tjänsten Automated forms conversion utför en nyckelordssökning i källformuläret under konverteringen. När fälten som uppfyller sökvillkoren har filtrerats används egenskaperna som definierats för fälten i metamodellen av konverteringstjänsten för de anpassade formulärfälten som genererats.

Nyckelord refereras med **aem:affKeyword** -egenskap.

```
{
  "numberfields": {
      "type": "number",
      "aem:affKeyword": ["Bank account number"]
 }
}
```

I det här exemplet använder konverteringstjänsten texten i **aem:affKeyword** som ett söknyckelord. När du har hämtat **Bankkontonummer** text i formuläret konverteras fältet till **tal** text med **type** -egenskap.

### Ytterligare egenskaper för genererade adaptiva formulärfält {#additionalproperties}

Du kan använda **aem:afProperties** i metamodellen för att definiera följande ytterligare egenskaper för fält med adaptiva formulär som genererats med tjänsten Automated forms conversion:

<table> 
 <tbody> 
  <tr> 
   <th><strong>Egenskapsnamn</strong></th> 
   <th><strong>Beskrivning</strong></th> 
  </tr> 
  <tr> 
   <td><p>multiLine</p></td> 
   <td> 
    <p>Egenskapen multiLine konverterar ett källformulärfält till ett fält med flera rader i det adaptiva formuläret efter konverteringen. Mer information finns i <strong>Konvertera ett strängfält till ett flerradigt fält</strong> in <a href="#custommetamodelexamples">Exempel på anpassade metamodeller.</a></p> </td> 
  </tr>
  <td><p>obligatoriskt</p></td> 
   <td> 
    <p>Den obligatoriska egenskapen anger indata för ett adaptivt formulärfält efter konvertering som obligatoriskt.<br>Mer information finns i <strong>Lägga till valideringar i anpassade formulärfält</strong> in <a href="#custommetamodelexamples">Exempel på anpassade metamodeller.</a></p>
    </td> 
  </tr>
  <td><p>jcr:title</p></td> 
   <td> 
    <p>Egenskapen jcr:title, med JSON-schemaegenskapen title, gör att du kan ändra etiketten för ett adaptivt formulärfält efter konverteringen.<br>Mer information finns i <strong>Ändra etiketten för ett formulärfält</strong> in <a href="#custommetamodelexamples">Exempel på anpassade metamodeller.</a><br>Se <a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/adaptive-form-json-schema-form-model.html" target="_blank">Skapa anpassningsbara formulär med JSON-schema</a> om du vill ha information om fler egenskaper som du kan tillämpa på adaptiva formulärfält med hjälp av JSON-schema.</p>
    <p></p></td> 
  </tr>
  <td><p>sling:resourceType och guideNodeClass</p></td> 
   <td> 
    <p>sling:resourceType- och guideNodeClass-egenskaper gör att du kan mappa ett formulärfält till en motsvarande adaptiv formulärkomponent.<br>Mer information finns i <strong>Konvertera ett formulärfält till kryssrutor med flera val i det adaptiva formuläret</strong> och <strong>Konvertera ett textfält till nedrullningsbar lista i det adaptiva formuläret</strong> in <a href="#custommetamodelexamples">Exempel på anpassade metamodeller.</a></p> </td> 
  </tr>
  <td><p>validatePictureClause</p></td> 
   <td> 
    <p>Egenskapen validatePictureClause anger en validering av det format som tillåts i det adaptiva formulärfältet efter konvertering.<br>Mer information finns i <strong>Lägga till valideringar i anpassade formulärfält</strong> in <a href="#custommetamodelexamples">Exempel på anpassade metamodeller.</p> </td> 
  </tr>
 </tbody> 
</table>

## Skapa en anpassad metamodell på ditt eget språk{#language-specific-meta-model}

Du kan skapa en språkspecifik metamodell. En sådan metamodell hjälper dig att skapa mappningsregler på valfritt språk. Med tjänsten Automated forms conversion kan du skapa metamodeller på följande språk:

* Engelska (en)
* French(fr)
* German(de)
* Spanska
* Italian(it)
* Portugisiska (pt-br)

Lägg till *aem:Language* metatag-taggen längst upp i en metamodell för att ange dess språk. Till exempel,

```JSON
"metaTags": {
        "aem:Language": "fr"
    }
```

Om inget språk anges anser tjänsten att metamodellen är på engelska.

### Att tänka på när du skapar en språkspecifik metamodell

* Kontrollera att namnet på alla nycklar är på engelska. Till exempel emailAddress.
* Kontrollera att alla enhetsreferenser och fördefinierade värden för alla id-nycklar bara innehåller ASCII-tecken. Exempel:&quot;id&quot;: &quot;ContactPoint&quot; / &quot;$ref&quot;: &quot;#ContactPoint&quot;.
* Se till att alla värden som motsvarar följande nycklar är på det angivna metamodellspråket:
   * aem:affKeyword
   * title
   * description
   * enumNames
   * shortDescription
   * validatePictureClauseMessage

  När språket för metamodellen till exempel är franska (&quot;aem:Language&quot;: &quot;fr&quot;) måste du se till att alla beskrivningar och meddelanden är på franska.

* Se till att alla [JSON-schemaegenskaper](#jsonschemaproperties) använder endast värden som stöds. Egenskapen type kan till exempel bara omfatta de valda värdena String, Number, Integer och Boolean.

I följande bild visas exempel på metamodell för engelska och motsvarande metamodell för franska språket:

![](assets/language-specific-meta-model-comparison.png)

## Ändra anpassade formulärfält med anpassad metamodell {#modify-adaptive-form-fields-using-custom-meta-model}

Din organisation kan ha mönster och valideringar utöver de som anges i standardmetamodellen. Du kan utöka standardmetamodellen för att lägga till mönster, valideringar och entiteter som är specifika för din organisation. Tjänsten Automated forms conversion använder den anpassade metamodellen på formulärfälten under konverteringen. Du kan fortsätta uppdatera metamodellen när nya mönster, valideringar och enheter som är specifika för din organisation identifieras.

I Automated forms conversion-tjänsten används en standardmetamodell som sparas på följande plats för att mappa källformulärfält till anpassade formulärfält under konverteringen:

http://&lt;server>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/metamodel/global.schema.json

Du kan dock spara en anpassad metamodell i en mapp och ändra egenskaperna för konverteringstjänsten så att den anpassade metamodellen används vid konverteringen.

### Använd anpassad metamodell vid konvertering {#use-custom-meta-model-during-conversion}

Utför följande steg om du vill använda en anpassad metamodell under konverteringen:

1. Skapa en mapp i **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]** och överför den anpassade JSON-schemafilen för metamodellen till mappen.
1. Öppna egenskaperna för konverteringstjänsten med:

   **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Automated Forms Conversion Configuration]** > **&lt;properties of=&quot;&quot; selected=&quot;&quot; configuration=&quot;&quot;>**

1. I **[!UICONTROL Basic]** anger du platsen för den anpassade metamodellen på fliken **[!UICONTROL Custom Meta-model]** fält och knacka **[!UICONTROL Save & Close]**.
1. [Kör konverteringen](convert-existing-forms-to-adaptive-forms.md#start-the-conversion-process) om du vill använda den anpassade metamodellen i konverteringsprocessen.

### Exempel på anpassade metamodeller {#custommetamodelexamples}

Några vanliga exempel på hur du använder en anpassad metamodell för att ändra egenskaper för anpassningsbara formulärfält är:

* Ändra etiketten för ett formulärfält
* Ändra typ av formulärfält
* Lägga till hjälptext i ett formulärfält
* Konvertera ett formulärfält till alternativknappar med flera val i det adaptiva formuläret
* Ändra format för ett formulärfält
* Lägga till valideringar i anpassade formulärfält
* Konvertera ett formulärfält till listrutealternativ i det adaptiva formuläret
* Lägg till ytterligare alternativ i listrutan
* Konvertera ett strängfält till ett flerradigt fält

#### Ändra etiketten för ett formulärfält {#modify-the-label-of-a-form-field}

**Exempel:** Ändra etiketten för bankkontonumret i formuläret till Anpassat kontonummer i det adaptiva formuläret efter konvertering.

I den här anpassade metamodellen använder konverteringstjänsten **title** som ett söknyckelord. När du har hämtat **Bankkontonummer** text i formuläret ersätter konverteringstjänsten texten med **Kundkontonummer** strängen som anges med **jcr:title** -egenskapen i **aem:afProperties** -avsnitt.

```
{
  "numberfields": {
      "type": "number",
   "title": "Bank account number",
   "aem:afProperties" : {
    "jcr:title" : "Customer account number"
   }
   }
}
```

#### Ändra typ av formulärfält {#modify-the-type-of-a-form-field}

**Exempel**: Ändra **Bankkontonummer** textfält i formuläret före konvertering till ett taltypsfält i det adaptiva formuläret efter konvertering.

I den här anpassade metamodellen använder konverteringstjänsten texten i **aem:affKeyword** som ett söknyckelord. När du har hämtat **Bankkontonummer** text i formuläret konverteras fältet till en taltyp med hjälp av **type** -egenskap.

```
{
  "numberfields": {
      "type": "number",
      "aem:affKeyword": ["Bank account number"]
 }
}
```

#### Lägga till hjälptext i ett formulärfält {#add-help-text-to-a-form-field}

**Exempel**: Lägg till hjälptext i **Bankkontonummer** fält i anpassningsbart format.

I den här anpassade metamodellen använder konverteringstjänsten texten i **aem:affKeyword** som ett söknyckelord. När du har hämtat **Bankkontonummer** text i formuläret, lägger konverteringstjänsten till hjälptexten i det adaptiva formulärfältet med hjälp av **description** -egenskap.

```
{
  "numberfields": {
      "type": "number",
      "aem:affKeyword": ["Bank account number"],
   "description": "Specify your bank account number."
 }
}
```

#### Konvertera ett formulärfält till kryssrutor med flera val i det adaptiva formuläret {#convert-a-form-field-to-multiple-choice-check-boxes-in-the-adaptive-form}

**Exempel**: Konvertera **Land** fält av strängtyp i formuläret före konvertering till kryssrutor i det adaptiva formuläret efter konvertering.

I den här anpassade metamodellen använder konverteringstjänsten text i **aem:affKeyword** som ett söknyckelord. När du har hämtat **Land** text i formuläret konverteras fältet till följande kryssrutor med hjälp av **enum** egenskap:

* Indien
* England
* Australien
* Nya Zeeland

**sling:resourceType** och **guideNodeClass** egenskaperna mappar ett formulärfält till kryssrutans adaptiva formulärkomponent.

```
{
"title": {
    "aem:affKeyword": [
      "country"
    ],
    "type" : "string",
    "enum": [
      "India",
      "England",
      "Australia",
      "New Zealand"
    ],
    "aem:afProperties": {
      "sling:resourceType": "fd/af/components/guidecheckbox",
      "guideNodeClass": "guidecheckbox"
    }
  }
}
```

#### Ändra format för ett formulärfält {#modify-the-format-of-a-form-field}

**Exempel**: Ändra formatet för **E-postadress** till ett e-postformat.

I den här anpassade metamodellen använder konverteringstjänsten text i **aem:affKeyword** som ett söknyckelord. När du har hämtat **E-postadress** text i formuläret konverteras fältet till ett e-postformat med hjälp av **format** -egenskap.

```
{
   "additionalDetails" : {
      "aem:affKeyword": ["E-mail Address"],
       "type" : "string",
       "format" : "email"
  } 
}
```

#### Lägga till valideringar i anpassade formulärfält {#add-validations-to-adaptive-form-fields}

**Exempel 1:** Lägg till en validering i **Postnummer** fält i det adaptiva formuläret.

I den här anpassade metamodellen använder konverteringstjänsten text i **aem:affKeyword** som söknyckelord. När du har hämtat **Postnummer** text i formuläret lägger konverteringstjänsten till en validering i fältet med hjälp av **validatePictureClause** egenskap som definieras i **aem:afProperties** -avsnitt. Baserat på valideringen är indata som du anger för **Postnummer** fältet i det adaptiva formuläret efter konverteringen måste innehålla sex tecken.

```
{
   "postalCode" : {
      "aem:affKeyword": ["Postal Code"],
      "type" : "string",
      "aem:afProperties" : {
        "validatePictureClause" : "\\d{6}"
      } 
   }
}
```

**Exempel 2:** Lägg till en validering i **Bankkontonummer** fält i det adaptiva formuläret.

I den här anpassade metamodellen använder konverteringstjänsten text i **aem:affKeyword** som söknyckelord. När du har hämtat **Bankkontonummer** text i formuläret lägger konverteringstjänsten till en validering i fältet med hjälp av **obligatoriskt** egenskap som definieras i **aem:afProperties** -avsnitt. Baserat på valideringen måste du ange ett värde för **Bankkontonummer** fält innan formuläret skickas efter konvertering.

```
{
  "numberfields": {
      "type": "number",
      "aem:affKeyword": ["Bank account number"],
   "aem:afProperties" : {
        "mandatory": "true"
      }   
   }
}
```

#### Konvertera ett textfält till nedrullningsbar lista i det adaptiva formuläret {#convert-a-text-field-to-drop-down-list-in-the-adaptive-form}

**Exempel**: Konvertera **Land** fält av strängtyp i formuläret före konvertering till nedrullningsbara alternativ i det adaptiva formuläret efter konvertering.

I den här anpassade metamodellen använder konverteringstjänsten text i **aem:affKeyword** som söknyckelord. När du har hämtat **Land** text i formuläret konverterar konverteringstjänsten fältet till följande alternativ i listrutan med hjälp av **enum** egenskap:

* Indien
* England
* Australien
* Nya Zeeland

**sling:resourceType** och **guideNodeClass** egenskaperna mappar ett formulärfält till den nedrullningsbara adaptiva formulärkomponenten.

```
{
"title": {
    "aem:affKeyword": [
      "country"
    ],
    "type" : "string",
    "enum": [
      "India",
      "England",
      "Australia",
      "New Zealand"
    ],
    "aem:afProperties": {
      "sling:resourceType": "fd/af/components/guidedropdownlist",
      "guideNodeClass": "guideDropDownlist"
    }
  }
}
```

#### Lägg till ytterligare alternativ i listrutan {#add-additional-options-to-the-drop-down-list}

**Exempel:** Lägg till **Sri Lanka** som ett extra alternativ till en befintlig nedrullningsbar lista med en anpassad metamodell.

Om du vill lägga till ett extra alternativ uppdaterar du **enum** med det nya alternativet. I det här exemplet uppdaterar du **enum** egenskap med **Sri Lanka** som ett extra alternativ. Värden som anges i **enum** egenskapsvisning i listrutan.

```
{
"title": {
    "aem:affKeyword": [
      "country"
    ],
    "type" : "string",
    "enum": [
      "India",
      "England",
      "Australia",
      "New Zealand",
   "Sri Lanka"
    ],
    "aem:afProperties": {
      "sling:resourceType": "fd/af/components/guidecheckbox",
      "guideNodeClass": "guidecheckbox"
    }
  }
}
```

#### Konvertera ett strängfält till ett flerradigt fält {#convert-a-string-field-to-a-multi-line-field}

**Exempel:** Konvertera **Adress** fält av strängtyp till ett flerradigt fält i formuläret efter konvertering.

I den här anpassade metamodellen använder konverteringstjänsten text i **aem:affKeyword** som söknyckelord. När du har hämtat **Adress** text i formuläret, konverterar tjänsten textfältet till ett fält med flera rader med hjälp av **multiLine** egenskap som definieras i **aem:afProperties** -avsnitt.

```
{
 "multiLine" : {
   "aem:affKeyword": [
      "Address"
    ],
    "type" : "string",
    "aem:afProperties": {
      "multiLine": "true"
    }
  }
}
```
