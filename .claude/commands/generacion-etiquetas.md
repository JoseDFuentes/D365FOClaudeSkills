---
name: generacion-etiquetas
description: Genera etiquetas en código cuando se utiliza en sentencias info, warning, error o para desplegar mensajes o retorno y que además usen la función strfmt()
---

En cada subcarpeta se especificará en la carpeta docs un archivo que contendrá la ruta del archivo de etiquetas que se utilizará y el nombre del archivo de etiquetas. Si la carpeta 'labels' no existe, se debe crear.

Si el archivo especifica que el ID de etiqueta es LBL entonces deben generarse los archivos para idiomas en inglés y en español con las siguientes rutas:

para las etiquetas en inglés
..\labels\en-US\LBL.en-US.txt

para las etiquetas en español
..\labels\es\LBL.es.txt

Las etiquetas nuevas se deben ir colocando al final.

Los textos deben tener el formato:
IdEtiqueta=Contenido de la etiqueta

Por ejemplo para inglés y español respectivamente:
IdLabel=ID Label

IdLabel=Código de etiqueta

Los Id de etiqueta deben crearse como formas abreviadas del contenido de la etiqueta, evitar usar autonuméricos o consecutivos.

No Permitido:

Label1=Id Label
N00001=Id Label

Permitido:

IdLabel=ID Label

De tal forma que en el código se pueda ver algo así:

info('@LBL:IdLabel');
