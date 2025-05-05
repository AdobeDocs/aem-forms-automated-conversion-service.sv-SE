---
title: Utöka standardmetamodellen
description: Utöka standardmetamodellen för att lägga till mönster, valideringar och enheter som är specifika för din organisation och tillämpa konfigurationer på anpassningsbara formulärfält när du kör tjänsten Automated forms conversion (AFCS).
solution: Experience Manager Forms
feature: Adaptive Forms
topic: Administration
topic-tags: forms
role: Admin, Developer
level: Beginner, Intermediate
exl-id: f679059c-18aa-4cb5-8368-ed27e96c20de
source-git-commit: c2392932d1e29876f7a11bd856e770b8f7ce3181
workflow-type: tm+mt
source-wordcount: '2569'
ht-degree: 0%

---

# Utöka standardmetamodellen {#extend-the-default-meta-model}

Tjänsten Automated forms conversion (AFCS) identifierar och extraherar formulärobjekt från källformulär. Semantisk mappning hjälper tjänsten att bestämma hur de extraherade objekten ska visas i en adaptiv form. Ett källformulär kan t.ex. ha många olika typer av representationer av ett datum. Med semantisk mappning kan du mappa alla representationer av formulärobjekt för datum i källformuläret med datumkomponenten i de adaptiva formulären. Med semantisk mappning kan tjänsten förkonfigurera och tillämpa valideringar, regler, datamönster, hjälptext och hjälpmedelsegenskaper på adaptiva formulärkomponenter under konverteringen.

![](assets/meta-model.gif)

Metamodellen är ett JSON-schema. Innan du börjar med metamodellen måste du se till att du är väl insatt i JSON. Du måste ha erfarenhet av att skapa, redigera och läsa data som sparats i JSON-format.

## Standardmetamodell {#default-meta-model}

Tjänsten Automated forms conversion (AFCS) har en standardmetamodell. Det är ett JSON-schema och finns i Adobe Cloud tillsammans med andra komponenter i tjänsten Automated forms conversion (AFCS). Du kan hitta en kopia av metamodellen på den lokala AEM på: http://&lt;server>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/metamodel/`global.schema.json`. Du kan också [klicka här](assets/en.globalschema.json) för att komma åt eller hämta det engelska språkschemat. Metamodellen för [franska](assets/fr.globalschema.json), [tyska](assets/de.globalschema.json) [spanska](assets/es.globalschema.json), [italienska](assets/it.globalschema.json) och [portugisiska](assets/pt_br.globalschema.json) är också tillgänglig för hämtning.

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
1. Navigera till mappen **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]** **>** **[!UICONTROL Meta Model]**.
1. Markera filen **[!UICONTROL global.schema.json]** och tryck på **[!UICONTROL Download]**. En dialogruta för hämtning visas. Välj alternativet **[!UICONTROL Download asset(s) as binary files]**. Tryck på **[!UICONTROL Download]**. Ett arkiv laddas ned.

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

I det här exemplet representerar **Event** namnet på en entitet med ett värde för **id** som **EventID**. Händelseentiteten innehåller flera egenskaper:

* startDate
* endDate
* plats

Konstruktorn **allOf** i metamodellen möjliggör arv mellan entiteter.

Varje egenskap kan dessutom innehålla:

* [JSON-schemaegenskaper](#jsonschemaproperties)
* [Nyckelordsbaserad sökning som använder egenskaper för genererade adaptiva formulärfält](#keywordsearch)
* [Ytterligare egenskaper](#additionalproperties)

![Metamodellegenskaper](assets/meta_model_elements.gif)

Baserat på nyckelorden som refereras med **aem:affKeyword**, utför konverteringstjänsten en sökåtgärd på källformulärfälten. Konverteringstjänsten använder JSON-schemaegenskaperna och ytterligare egenskaper för de fält som uppfyller sökvillkoren.

I det här exemplet söker konverteringstjänsten efter nyckelorden telefon, telefon, mobiltelefon, arbetstelefon, hemtelefon, telefonnummer, telefonnummer och telefonnummer i källformuläret. Baserat på de fält som innehåller dessa nyckelord använder konverteringstjänsten typ, mönster och aem:afProperties på de adaptiva formulärfälten efter konverteringen.

### JSON-schemaegenskaper för genererade adaptiva formulärfält {#jsonschemaproperties}

Metamodellen stöder följande gemensamma egenskaper för JSON-schema för adaptiva formulärfält som genereras med tjänsten Automated forms conversion (AFCS):

<table> 
 <tbody> 
  <tr> 
   <th><strong>Egenskapsnamn</strong></th> 
   <th><strong>Beskrivning</strong></th> 
  </tr> 
  <tr> 
   <td><p>title</p></td> 
   <td> 
    <p>Texten som omnämns i egenskapen title i en metamodell fungerar som ett söknyckelord för att utföra åtgärder i de genererade adaptiva formulärfälten. Du kan till exempel ändra etiketten för ett adaptivt formulärfält. Mer information finns i <strong>Ändra etiketten för ett formulärfält</strong> i <a href="#custommetamodelexamples">Exempel på anpassade metamodeller.</a></p> </td> 
  </tr>
  <td><p>description</p></td> 
   <td> 
    <p>Egenskapen description anger hjälptexten för det genererade adaptiva formulärfältet. Mer information finns i <strong>Lägga till hjälptext i ett formulärfält</strong> i <a href="#custommetamodelexamples">Exempel på anpassade metamodeller.</a></p> </td> 
  </tr>
  <td><p>type</p></td> 
   <td> 
    <p>Egenskapen type definierar datatypen för det genererade adaptiva formulärfältet. Möjliga värden för egenskapen title är:</p>
    <ul> 
     <li>string: Skapar ett adaptivt formulärfält av textdatatyp.</li> 
     <li>number: Skapar ett adaptivt formulärfält av numerisk datatyp.</li>
     <li>heltal: Skapar ett adaptivt formulärfält av numerisk datatyp med subtype inställd på heltal.</li>
     <li>booleskt: Skapar en adaptiv formulärkomponent för switch.</li>
     </ul><p>Mer information om hur du använder type-egenskapen i en metamodell finns i <strong>Ändra typ av formulärfält</strong> i <a href="#custommetamodelexamples">Exempel på anpassade metamodeller.</a></p></td> 
  </tr>
  <td><p>mönster</p></td> 
   <td> 
    <p>Egenskapen pattern begränsar värdet för det genererade adaptiva formulärfältet baserat på ett reguljärt uttryck. Följande kod i metamodellen begränsar till exempel värdet för det genererade adaptiva formulärfältet till tio siffror: <br>"pattern": "/\\d{10}/"<br>På samma sätt begränsar följande kod i metamodellen värdet för ett fält till ett visst datumformat.<br> "pattern": "date{DD MMMM, YYYY}",</p> </td> 
  </tr>
  <td><p>format</p></td> 
   <td> 
    <p>Formategenskapen begränsar värdet för det genererade adaptiva formulärfältet baserat på ett namngivet mönster i stället för ett reguljärt uttryck. Möjliga värden för formategenskapen är:<ul><li>e-post: Skapar en formulärkomponent för e-postanpassning.</li><li>värdnamn: Skapar en adaptiv formulärkomponent för textrutor.</li></ul>Mer information om hur du använder formategenskapen i en metamodell finns i <strong>Ändra formatet för ett formulärfält</strong> i <a href="#custommetamodelexamples">Exempel på anpassade metamodeller.</a></p> </td> 
  </tr>
  <td><p>enum och enumNames</p></td> 
   <td> 
    <p>Egenskaperna enum och enumNames begränsar värdena för fälten för nedrullningsbara menyer, kryssrutor och alternativknappar till en fast uppsättning. Värden som anges i enumNames visas i användargränssnittet. Värdena som anges med enum-egenskapen används för beräkning.<br>Mer information finns i <strong>Konvertera ett formulärfält till kryssrutor med flera val i det adaptiva formuläret</strong>, <strong>Konvertera ett textfält till nedrullningsbar lista i det adaptiva formuläret</strong> och <strong>Lägg till ytterligare alternativ i listrutan</strong> i <a href="#custommetamodelexamples">Exempel på anpassade metamodeller.</a></p> </td> 
  </tr>
 </tbody> 
</table>

### Nyckelordsbaserad sökning som använder egenskaper för genererade adaptiva formulärfält {#keywordsearch}

Tjänsten Automated forms conversion (AFCS) utför en nyckelordssökning i källformuläret under konverteringen. När fälten som uppfyller sökvillkoren har filtrerats används egenskaperna som definierats för fälten i metamodellen av konverteringstjänsten för de anpassade formulärfälten som genererats.

Nyckelord refereras med egenskapen **aem:affKeyword** .

```
{
  "numberfields": {
      "type": "number",
      "aem:affKeyword": ["Bank account number"]
 }
}
```

I det här exemplet använder konverteringstjänsten texten inom **aem:affKeyword** som söknyckelord. När texten **Bankkontonummer** har hämtats i formuläret konverteras fältet till en **number**-typ med hjälp av egenskapen **type**.

### Ytterligare egenskaper för genererade adaptiva formulärfält {#additionalproperties}

Du kan använda egenskapen **aem:afProperties** i metamodellen för att definiera följande ytterligare egenskaper för adaptiva formulärfält som genererats med tjänsten Automated forms conversion (AFCS):

<table> 
 <tbody> 
  <tr> 
   <th><strong>Egenskapsnamn</strong></th> 
   <th><strong>Beskrivning</strong></th> 
  </tr> 
  <tr> 
   <td><p>multiLine</p></td> 
   <td> 
    <p>Egenskapen multiLine konverterar ett källformulärfält till ett fält med flera rader i det adaptiva formuläret efter konverteringen. Mer information finns i <strong>Konvertera ett strängfält till ett flerradigt fält</strong> i <a href="#custommetamodelexamples">Exempel på anpassade metamodeller.</a></p> </td> 
  </tr>
  <td><p>obligatoriskt</p></td> 
   <td> 
    <p>Den obligatoriska egenskapen anger indata för ett adaptivt formulärfält efter konvertering som obligatoriskt.<br>Mer information finns i <strong>Lägga till valideringar i adaptiva formulärfält</strong> i <a href="#custommetamodelexamples">Exempel på anpassade metamodeller.</a></p>
    </td> 
  </tr>
  <td><p>jcr:title</p></td> 
   <td> 
    <p>Egenskapen jcr:title, med JSON-schemaegenskapen title, gör att du kan ändra etiketten för ett adaptivt formulärfält efter konverteringen.<br>Mer information finns i <strong>Ändra etiketten för ett formulärfält</strong> i <a href="#custommetamodelexamples">Exempel på anpassade metamodeller.</a><br>Se <a href="https://helpx.adobe.com/se/experience-manager/6-5/forms/using/adaptive-form-json-schema-form-model.html" target="_blank">Skapa adaptiva formulär med JSON-schema</a> för mer information om fler egenskaper som du kan tillämpa på adaptiva formulärfält med JSON-schema.</p>
    <p></p></td> 
  </tr>
  <td><p>sling:resourceType och guideNodeClass</p></td> 
   <td> 
    <p>sling:resourceType- och guideNodeClass-egenskaper gör att du kan mappa ett formulärfält till en motsvarande adaptiv formulärkomponent.<br>Mer information finns i <strong>Konvertera ett formulärfält till kryssrutor med flera val i det adaptiva formuläret</strong> och <strong>Konvertera ett textfält till nedrullningsbar lista i det adaptiva formuläret</strong> i <a href="#custommetamodelexamples">Exempel på anpassade metamodeller.</a></p> </td> 
  </tr>
  <td><p>validatePictureClause</p></td> 
   <td> 
    <p>Egenskapen validatePictureClause anger en validering av det format som tillåts i det adaptiva formulärfältet efter konvertering.<br>Mer information finns i <strong>Lägga till valideringar i adaptiva formulärfält</strong> i <a href="#custommetamodelexamples">Exempel på anpassade metamodeller.</p> </td> 
  </tr>
 </tbody> 
</table>

## Skapa en anpassad metamodell på ditt eget språk{#language-specific-meta-model}

Du kan skapa en språkspecifik metamodell. En sådan metamodell hjälper dig att skapa mappningsregler på valfritt språk. Med tjänsten Automated forms conversion (AFCS) kan du skapa metamodeller på följande språk:

* Engelska (en)
* French(fr)
* German(de)
* Spanska
* Italian(it)
* Portugisiska (pt-br)

Lägg till metataggen *aem:Language* i den översta metamodellen för att ange dess språk. Exempel:

```JSON
"metaTags": {
        "aem:Language": "fr"
    }
```

Om inget språk anges anser tjänsten att metamodellen är på engelska.

### Att tänka på när du skapar en språkspecifik metamodell

* Kontrollera att namnet på alla nycklar är på engelska. Till exempel emailAddress.
* Kontrollera att alla enhetsreferenser och fördefinierade värden för alla id-nycklar bara innehåller ASCII-tecken. Exempel: &quot;id&quot;: &quot;ContactPoint&quot; / &quot;$ref&quot;: &quot;#ContactPoint&quot;.
* Se till att alla värden som motsvarar följande nycklar är på det angivna metamodellspråket:
   * aem:affKeyword
   * title
   * description
   * enumNames
   * shortDescription
   * validatePictureClauseMessage

  Om t.ex. metamodellens språk är franska (&quot;aem:Language&quot;: &quot;fr&quot;) kontrollerar du att alla beskrivningar och meddelanden är på franska.

* Se till att alla [JSON-schemaegenskaper](#jsonschemaproperties) bara använder värden som stöds. Egenskapen type kan till exempel bara omfatta de markerade värdena String, Number, Integer och Boolean.

I följande bild visas exempel på metamodell för engelska och motsvarande metamodell för franska språket:

![](assets/language-specific-meta-model-comparison.png)

## Ändra anpassade formulärfält med anpassad metamodell {#modify-adaptive-form-fields-using-custom-meta-model}

Din organisation kan ha mönster och valideringar utöver de som anges i standardmetamodellen. Du kan utöka standardmetamodellen för att lägga till mönster, valideringar och entiteter som är specifika för din organisation. Tjänsten Automated forms conversion (AFCS) tillämpar den anpassade metamodellen på formulärfälten under konverteringen. Du kan fortsätta uppdatera metamodellen när nya mönster, valideringar och enheter som är specifika för din organisation identifieras.

I tjänsten Automated forms conversion (AFCS) används en standardmetamodell som sparas på följande plats för att mappa källformulärfält till anpassade formulärfält under konverteringen:

http://&lt;server>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/metamodel/global.schema.json

Du kan dock spara en anpassad metamodell i en mapp och ändra egenskaperna för konverteringstjänsten så att den anpassade metamodellen används vid konverteringen.

### Använd anpassad metamodell vid konvertering {#use-custom-meta-model-during-conversion}

Utför följande steg om du vill använda en anpassad metamodell under konverteringen:

1. Skapa en mapp i **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]** och överför den anpassade JSON-schemafilen för metamodell till mappen.
1. Öppna egenskaperna för konverteringstjänsten med:

   **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Automated Forms Conversion Configuration]** > **&lt;Egenskaper för markerad konfiguration>**

1. Ange platsen för den anpassade metamodellen i fältet **[!UICONTROL Custom Meta-model]** på fliken **[!UICONTROL Basic]** och tryck sedan på **[!UICONTROL Save & Close]**.
1. [Kör konverteringen](convert-existing-forms-to-adaptive-forms.md#start-the-conversion-process) för att använda den anpassade metamodellen i konverteringsprocessen.

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

**Exempel:** Ändra etiketten för bankkontonummer i formuläret till Anpassat kontonummer i det adaptiva formuläret efter konvertering.

I den här anpassade metamodellen använder konverteringstjänsten egenskapen **title** som söknyckelord. När texten **Bankkontonummer** har hämtats i formuläret ersätter konverteringstjänsten texten med strängen **Kundkontonummer** som anges med egenskapen **jcr:title** i avsnittet **aem:afProperties** .

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

**Exempel**: Ändra fältet **Bankkontonummer** för texttypen i formuläret före konvertering till ett nummertypfält i det adaptiva formuläret efter konvertering.

I den här anpassade metamodellen använder konverteringstjänsten texten inom **aem:affKeyword** som söknyckelord. När texten **Bankkontonummer** har hämtats i formuläret konverteras fältet till en nummertyp med hjälp av egenskapen **type**.

```
{
  "numberfields": {
      "type": "number",
      "aem:affKeyword": ["Bank account number"]
 }
}
```

#### Lägga till hjälptext i ett formulärfält {#add-help-text-to-a-form-field}

**Exempel**: Lägg till hjälptext i fältet **Bankkontonummer** i anpassat format.

I den här anpassade metamodellen använder konverteringstjänsten texten inom **aem:affKeyword** som söknyckelord. När texten **Bankkontonummer** har hämtats i formuläret lägger konverteringstjänsten till hjälptexten i det adaptiva formulärfältet med egenskapen **description** .

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

**Exempel**: Konvertera fältet **Land** av strängtyp i formuläret före konvertering till kryssrutor i det adaptiva formuläret efter konvertering.

I den här anpassade metamodellen använder konverteringstjänsten text inom **aem:affKeyword** som söknyckelord. När du har hämtat texten **Country** i formuläret konverterar konverteringstjänsten fältet till följande kryssrutor med egenskapen **enum** :

* Indien
* England
* Australien
* Nya Zeeland

Egenskaperna **sling:resourceType** och **guideNodeClass** mappar ett formulärfält till kryssrutans adaptiva formulärkomponent.

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

**Exempel**: Ändra formatet för fältet **E-postadress** till ett e-postformat.

I den här anpassade metamodellen använder konverteringstjänsten text inom **aem:affKeyword** som söknyckelord. När du har hämtat texten **E-postadress** i formuläret konverteras fältet till ett e-postformat med hjälp av egenskapen **format**.

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

**Exempel 1:** Lägg till en validering i fältet **Postnummer** i det adaptiva formuläret.

I den här anpassade metamodellen använder konverteringstjänsten text inom **aem:affKeyword** som söknyckelord. När texten **Postnummer** har hämtats i formuläret lägger konverteringstjänsten till en validering i fältet med egenskapen **validatePictureClause** som definieras i avsnittet **aem:afProperties** . Baserat på valideringen måste de indata som du anger för fältet **Postnummer** i det adaptiva formuläret efter konverteringen innehålla sex tecken.

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

**Exempel 2:** Lägg till en validering i fältet **Bankkontonummer** i det adaptiva formuläret.

I den här anpassade metamodellen använder konverteringstjänsten text inom **aem:affKeyword** som söknyckelord. När texten **Bankkontonummer** har hämtats i formuläret lägger konverteringstjänsten till en validering i fältet med egenskapen **mandatory** som definieras i avsnittet **aem:afProperties** . Baserat på valideringen måste du ange ett värde för fältet **Bankkontonummer** innan du skickar formuläret efter konverteringen.

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

#### Konvertera ett textfält till listruta i det adaptiva formuläret {#convert-a-text-field-to-drop-down-list-in-the-adaptive-form}

**Exempel**: Konvertera fältet **Land** med strängtyp i formuläret före konvertering till listrutealternativ i det adaptiva formuläret efter konvertering.

I den här anpassade metamodellen använder konverteringstjänsten text inom **aem:affKeyword** som söknyckelord. När du har hämtat texten **Country** i formuläret konverterar konverteringstjänsten fältet till följande alternativ i listrutan med hjälp av egenskapen **enum**:

* Indien
* England
* Australien
* Nya Zeeland

Egenskaperna **sling:resourceType** och **guideNodeClass** mappar ett formulärfält till den adaptiva formulärkomponenten i listrutan.

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

**Exempel:** Lägg till **Sri Lanka** som ett extra alternativ i en befintlig nedrullningsbar lista med en anpassad metamodell.

Om du vill lägga till ett extra alternativ uppdaterar du egenskapen **enum** med det nya alternativet. I det här exemplet uppdaterar du egenskapen **enum** med **Sri Lanka** som ett extra alternativ. Värden som visas i egenskapen **enum** visas i listrutan.

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

**Exempel:** Konvertera fältet **Adress** av strängtyp till ett flerradigt fält i formuläret efter konvertering.

I den här anpassade metamodellen använder konverteringstjänsten text inom **aem:affKeyword** som söknyckelord. När du har hämtat texten **Address** i formuläret konverterar tjänsten textfältet till ett flerradigt fält med hjälp av egenskapen **multiLine** som definieras i avsnittet **aem:afProperties** .

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
