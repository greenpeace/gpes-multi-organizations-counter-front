# Instrucciones

## Mostrar el contador

Este es el código html/javascript para mostrar el contador. El contador aparecerá donde inserteis este código

```html
    <!-- INICIO DEL CONTADOR -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/odometer@0.4.8/themes/odometer-theme-default.min.css" />
    <style>
        .odometer.odometer-auto-theme,
        .odometer {
            font-size: 25px;
            font-family: "Rubik", sans-serif;
            font-weight: 600;
        }
        .odometer.odometer-auto-theme .odometer-digit,
        .odometer .odometer-digit {
            color: #444;
            border: 1px solid #ddd;
        }
    </style>
    <script src="https://cdn.jsdelivr.net/npm/odometer@0.4.8/odometer.min.js" defer></script>
    <div id="odometer2container"><span id="odometer2" class="odometer2"></span> firmas</div>
    <script>
        /* jshint browser: true, esversion: 6 */
        /* global Odometer, odometer, jQuery, analytics, console */
        document.addEventListener("DOMContentLoaded", function() {
            jQuery.ajax({
                url: "https://apis.greenpeace.es/multi-organizations-counter/counter/"
            }).done(function( data ) {
                const counterValue = Number(data.signups);
                const el = document.querySelector('.odometer2');
                const odometer = new Odometer({
                    el: el,
                    format: '.ddd.ddd',
                    value: counterValue - Math.round( counterValue / 10 ),
                    duration: 2000,
                });
                odometer.update(counterValue);
            });
        });
    </script>
    <!-- FIN DEL CONTADOR -->

```

OBS: Si vuestro sitio web no usa jQuery, tendréis que cargar la librería con un código así:

```html
<script src="https://cdn.jsdelivr.net/npm/jquery@3.5.1/dist/jquery.min.js" defer></script>
```

## Mostrar el contador usando iframe

Si vuestro sistema da problemas en insertar CSS y Javscript en las páginas podreéis usar un iframe

https://apis.greenpeace.es/multi-organizations-counter/


## Incrementar el contador

Para incrementar el contador pondréis un pixel en la página de gracias de la petición. Cuidado para que se use apenas cuando alguien haya firmado la petición. El pixel es practicamente invisible. El código html para ponerlo es:

```html
<img src="https://apis.greenpeace.es/multi-organizations-counter/signup/" alt="" />
```

Ciertas organizaciones, como Greenpeace, no tienen página de gracias independiente. En ese caso tenéis que aseguraros que el seguiente código corre cada vez que alguien firma:

```javascript
{
    const container = document.getElementsByTagName("body");
    const conversion = document.createElement("img");
    conversion.src = "https://apis.greenpeace.es/multi-organizations-counter/signup/";
    container.appendChild(conversion);
}
```

## Haced pruebas

Antes de lanzar la petición pondremos el contador a cero. Así que haz tus pruebas cuanto antes y las veces que necesites.

## Instrucciones técnicas para programadores

Si eres programador puedes hacer tu proprio contador. Para ello estos enlaces serán útiles.

- [API contador para ver número de firmas](https://apis.greenpeace.es/multi-organizations-counter/counter/)

- [URL pixel para incrementar el contador](https://apis.greenpeace.es/multi-organizations-counter/signup/)

- [Librería odometer para crear contadores](https://github.hubspot.com/odometer/)
