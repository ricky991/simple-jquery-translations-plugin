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
