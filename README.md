# Sintaxgram

[![Sintaxgram](https://img.shields.io/badge/Sintaxgram-an%C3%A1lisis%20sint%C3%A1ctico-blue)](https://sintaxgram.pablozd.ar)
![Herramienta web](https://img.shields.io/badge/herramienta-web-brightgreen)
![Lingüística](https://img.shields.io/badge/ling%C3%BC%C3%ADstica-sintaxis-purple)
![SVG](https://img.shields.io/badge/exporta-SVG%20%7C%20PNG-lightgrey)
![Licencia](https://img.shields.io/badge/licencia-MIT%20%7C%20LPPL%20%7C%20CC--BY-blue)

**Sintaxgram** es una herramienta web simple para generar diagramas de análisis sintáctico a partir de una notación textual compacta.

Está pensada para uso docente en gramática, sintaxis y análisis de oraciones. Permite escribir una oración anotada con funciones sintácticas y obtener automáticamente una visualización con etiquetas, subrayados, cajas abiertas y líneas superiores.

→ **[sintaxgram.pablozd.ar](https://sintaxgram.pablozd.ar)**

## Características

- Interfaz web en un único archivo HTML.
- No requiere instalación ni servidor backend.
- Renderizado automático en SVG.
- Exportación como SVG.
- Exportación como PNG.
- Copia directa del SVG al portapapeles.
- Soporte para etiquetas inferiores, cajas abiertas y líneas superiores.
- Notación textual anidable.
- Compatible con uso local o publicación como sitio estático.

## Ejemplo rápido

Entrada:

```txt
SES{N{Juan}} PVS{construyó OD*{MD{una} N{casa}}}
```

Salida esperada:

- `SES{...}` genera una línea superior para el sujeto.
- `PVS{...}` genera una línea superior para el predicado verbal simple.
- `OD*{...}` genera una caja abierta inferior.
- `MD{...}` y `N{...}` generan etiquetas inferiores.

## Notación básica

La herramienta usa una sintaxis de comandos con llaves:

```txt
COMANDO{contenido}
```

Los comandos pueden anidarse:

```txt
SES{N{Juan}} PVS{NV{compró} OD*{MD{un} N{libro}}}
```

## Tipos de marcas

### Líneas superiores

Se usan para marcar constituyentes mayores por encima del texto.

Ejemplos:

```txt
SES{...}
PVS{...}
PVC{...}
SEC{...}
ST{...}
OS{...}
```

### Cajas abiertas

Los comandos con asterisco generan una caja abierta inferior.

Ejemplos:

```txt
OD*{...}
OI*{...}
MI*{...}
CCL*{...}
COMP*{...}
MD*{...}
CL*{...}
CM*{...}
PSO*{...}
PSNO*{...}
POO*{...}
ACT*{...}
ACL*{...}
ACM*{...}
ACF*{...}
ACC*{...}
MG*{...}
Ap*{...}
```

### Etiquetas inferiores

Los comandos sin asterisco generan una etiqueta inferior.

Ejemplos:

```txt
N{...}
NN{...}
NV{...}
NP{...}
NA{...}
NAD{...}
MD{...}
OD{...}
OI{...}
MG{...}
Ap{...}
MF{...}
ACT{...}
ACL{...}
ACM{...}
ACF{...}
ACC{...}
```

Algunas etiquetas, como `OD`, `OI`, `NN` y `NV`, incorporan subrayado automático.

## Uso local

1. Descargá el archivo HTML.
2. Abrilo directamente en el navegador.
3. Escribí o pegá el análisis en el área de texto.
4. Exportá el resultado como SVG o PNG.

No se necesita compilar nada.

## Publicación como sitio estático

El proyecto puede publicarse en cualquier servidor web estático.

Por ejemplo, con Nginx:

```bash
sudo mkdir -p /var/www/stxgrama
sudo cp index.html /var/www/stxgrama/index.html
```

Configuración mínima:

```nginx
server {
    listen 80;
    server_name stxgrama.ejemplo.com;

    root /var/www/stxgrama;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

También puede publicarse en GitHub Pages, Netlify, Vercel o cualquier hosting que sirva HTML estático.

## Estructura del proyecto

Versión mínima:

```txt
.
├── index.html
└── README.md
```

El archivo `index.html` contiene:

- la interfaz;
- los estilos CSS;
- el parser de la notación;
- el cálculo de layout;
- el render SVG;
- las funciones de descarga y copia.

## Personalización

Algunas constantes permiten ajustar el diseño visual:

```js
const CW = 8.5;     // ancho aproximado de carácter
const SW = 8;       // separación horizontal entre unidades
const FS = 16;      // tamaño de fuente
```

Para las líneas superiores:

```js
const SL_GAP = -2;  // separación vertical entre texto y spanline
const SL_XPAD = 2;  // padding horizontal de spanline
```

Para las cajas abiertas:

```js
const OB_XPAD = 3;  // padding horizontal de openbox
```

Estos valores pueden modificarse para obtener diagramas más compactos o más aireados.

## Estado del proyecto

Proyecto en desarrollo. La versión actual está orientada a generar diagramas sintácticos de manera rápida para materiales docentes, clases y ejercicios.

## Licencia

Pendiente de definir.

Una opción razonable para este tipo de herramienta es MIT, si se quiere permitir reutilización, modificación y distribución con pocas restricciones.