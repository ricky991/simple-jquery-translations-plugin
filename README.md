# simple-jquery-translations-plugin
A lightweight simple translator using jQuery and a json file. Simple alternative to POEdit. Manage dynamic numbers too

## Installations
Import **jQuery** and **translations.js**
```
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.2.1/jquery.min.js"></script>
<script src="./translate-plugin/translations.js"></script>
```
Open or create your own **translations.json** that contains all the translations.
```
{
    "I'm a text that exist in English, Italian and Spanish": {
        "es": "Soy un texto que existe en Ingles, Italiano y Español",
        "it": "Sono un testo che esiste in Inglese, Italiano e Spagnolo" 
    },
    "I exist only in English and Italian": {
        "it": "Io esisto solo in Inglese e Italiano" 
    },
    "Me only in English":{
    },
    "I have only 1 single number": {
        "es": "Tengo solo 1 numero",
        "it": "Ho 1 solo numero" 
    },
    "I have %n numbers": {
        "es": "Tengo %n numeros",
        "it": "Ho %n numeri" 
    },
    "Your own text to translate": {
        "es": "Tu proprio texto de traducir",
        "it": "Il tuo testo da tradurre" 
    }
}
```
This means, that the principal language is English, than check if there are other language translations.
If there aren't other language translations, but there is only the English version, it return that.
If a phrase is not in the 'translations.json' file, it return an ERROR.

## Add the jQuery script
Add in an external file like **translations.js** or in a **<script></script>** tag the following code:
```
// Variables 
var lang= window.navigator.language, // Check the Browser language
translate; // Container of all translations

// Call translations json file and populate translate variable  
$.getJSON("translate-plugin/translations.json", function(texts) {
    translate=texts;

    // Translations Function: Get all the element with data-text
    $("[data-translate]").each(function() {
        let text= $(this).attr('data-translate'), // Save the Text into the variable
            numbers= text.match(/\d+/g),
            element=  $('[data-translate="'+text+'"]'),
            postHTML;

        if (numbers != null && numbers>1) 
                text= text.replace(numbers, '%n');
        
        if (translate[text]!==undefined) { // Check if exist the text in translation.json                      

            if (translate[text][lang]!==undefined) { // Check if exist the text in the browser language
                postHTML= translate[text][lang];
            } else { // If not exist the lang, show the text in primary Language (Recomend: English)
                postHTML= text;
            }

            if (numbers != null && numbers>1) 
                postHTML= postHTML.replace('%n', numbers);

            element.html(postHTML);

        } else {
            $('[data-translate="'+text+'"]').html("ERR").css({'color':'red','font-weight':'bold'});
        }
    });
});
```
Now, edit the **url** in the **getJSON** call
```
$.getJSON("URL_json_file", function(texts) {
```


## How to implement in HTML elements
Simply add to an element the **data-translate** attribute, example:
```
<span data-translate="Your own text to translate"></span>
```
In this case, if my lang is 'IT', it return :
```
<span data-translate="Your own text to translate">Il tuo testo da tradurre</span>
```

## Manage Dynamic Numbers
In *translations.json*  add **%n** like the example
```
  .......
    "I have %n numbers": {
        "es": "Tengo %n numeros",
        "it": "Ho %n numeri" 
    },
   ......
```
and you can recall this simply adding a number in the text:
```
  <span data-translate="I have 6 numbers"></span>

```

## NOTE
- It doesn't work with more than 1 number per phrase.
- Singular and plural must have 2 different JSON object
