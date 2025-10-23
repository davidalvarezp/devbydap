+++
author = "davidalvarezp"
title = "Guía Sintaxis Markdown"
date = "2025-10-22"
description = "Artículo de ejemplo que muestra la sintaxis básica de Markdown y el formato de los elementos HTML."
tags = [
    "markdown",
]
categories = [
]
series = ["Guia de Temas"]
aliases = ["migrate-from-jekyl"]
image = "pawel-czerwinski-8uZPynIu-rQ-unsplash.jpg"
+++

Este artículo ofrece un ejemplo de la sintaxis básica de **Markdown** que puede utilizarse en los archivos de contenido de **Hugo**, y además muestra cómo se decoran los elementos HTML básicos con CSS dentro de un tema de Hugo.  
<!--more-->

## Encabezados

Los elementos HTML `<h1>`—`<h6>` representan seis niveles de encabezados de sección. `<h1>` es el nivel más alto, mientras que `<h6>` es el más bajo.

# H1  
## H2  
### H3  
#### H4  
##### H5  
###### H6  

## Párrafos

Xerum, quo qui aut unt expliquam qui dolut labo. Aque venitatiusda cum, voluptionse latur sitiae dolessi aut parist aut dollo enim qui voluptate ma dolestendit peritin re plis aut quas inctum laceat est volestemque commosa as cus endigna tectur, offic to cor sequas etum rerum idem sintibus eiur? Quianimin porecus evelectur, cum que nis nust voloribus ratem aut omnimi, sitatur? Quiatem. Nam, omnis sum am facea corem alique molestrunt et eos evelece arcillit ut aut eos eos nus, sin conecerem erum fuga. Ri oditatquam, ad quibus unda veliamenimin cusam et facea ipsamus es exerum sitate dolores editium rerore eost, temped molorro ratiae volorro te reribus dolorer sperchicium faceata tiustia prat.

¿Itatur? Quiatae cullecum rem ent aut odis in re eossequodi nonsequ idebis ne sapicia is sinveli squiatum, core et que aut hariosam ex eat.

## Citas en bloque

El elemento *blockquote* representa contenido citado de otra fuente, opcionalmente con una referencia o cita dentro de un elemento `footer` o `cite`, y con posibles cambios en línea como anotaciones o abreviaturas.

#### Cita sin atribución

> Tiam, ad mint andaepu dandae nostion secatur sequo quae.  
> **Nota** que puedes usar *sintaxis Markdown* dentro de una cita.

#### Cita con atribución

> No comuniques compartiendo memoria, comparte memoria comunicándote.<br>
> — <cite>Rob Pike[^1]</cite>

[^1]: La cita anterior está extraída de la [charla](https://www.youtube.com/watch?v=PAAkCSZUG1c) de Rob Pike durante el Gopherfest, el 18 de noviembre de 2015.

## Tablas

Las tablas no forman parte del estándar básico de Markdown, pero **Hugo** las admite de forma nativa.

   Nombre | Edad
----------|------
    Bob   | 27
   Alicia | 23

#### Markdown en línea dentro de tablas

| Italics   | Bold     | Code   |
| --------  | -------- | ------ |
| *italics* | **bold** | `code` |

| A                                                        | B                                                                                                             | C                                                                                                                                    | D                                                 | E                                                          | F                                                                    |
|----------------------------------------------------------|---------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------|------------------------------------------------------------|----------------------------------------------------------------------|
| Lorem ipsum dolor sit amet, consectetur adipiscing elit. | Phasellus ultricies, sapien non euismod aliquam, dui ligula tincidunt odio, at accumsan nulla sapien eget ex. | Proin eleifend dictum ipsum, non euismod ipsum pulvinar et. Vivamus sollicitudin, quam in pulvinar aliquam, metus elit pretium purus | Proin sit amet velit nec enim imperdiet vehicula. | Ut bibendum vestibulum quam, eu egestas turpis gravida nec | Sed scelerisque nec turpis vel viverra. Vivamus vitae pretium sapien |

## Bloques de código

#### Bloque de código con comillas invertidas

```html
<!doctype html>
<html lang="es">
<head>
  <meta charset="utf-8">
  <title>Documento HTML5 de ejemplo</title>
</head>
<body>
  <p>Prueba</p>
</body>
</html>
```

#### Bloque de código con indentación de cuatro espacios

    <!doctype html>
    <html lang="es">
    <head>
      <meta charset="utf-8">
      <title>Documento HTML5 de ejemplo</title>
    </head>
    <body>
      <p>Prueba</p>
    </body>
    </html>

#### Bloque de código con el shortcode interno de resaltado de Hugo
{{< highlight html >}}
<!doctype html>
<html lang="es">
<head>
  <meta charset="utf-8">
  <title>Documento HTML5 de ejemplo</title>
</head>
<body>
  <p>Prueba</p>
</body>
</html>
{{< /highlight >}}

#### Bloque de diferencias (*diff*)

```diff
[dependencies.bevy]
git = "https://github.com/bevyengine/bevy"
rev = "11f52b8c72fc3a568e8bb4a4cd1f3eb025ac2e13"
- features = ["dynamic"]
+ features = ["jpeg", "dynamic"]
```

## Tipos de listas

#### Lista ordenada

1. Primer elemento  
2. Segundo elemento  
3. Tercer elemento  

#### Lista desordenada

* Elemento de lista  
* Otro elemento  
* Y otro más  

#### Lista anidada

* Fruta
  * Manzana
  * Naranja
  * Plátano
* Lácteos
  * Leche
  * Queso

## Otros elementos — abbr, sub, sup, kbd, mark

<abbr title="Graphics Interchange Format">GIF</abbr> es un formato de imagen de mapa de bits.

H<sub>2</sub>O

X<sup>n</sup> + Y<sup>n</sup> = Z<sup>n</sup>

Pulsa <kbd>CTRL</kbd> + <kbd>ALT</kbd> + <kbd>Supr</kbd> para finalizar la sesión.

La mayoría de las <mark>salamandras</mark> son nocturnas y cazan insectos, gusanos y otras criaturas pequeñas.

## Imagen con hipervínculo

[![Google](https://www.google.com/images/branding/googlelogo/1x/googlelogo_light_color_272x92dp.png)](https://google.com)
