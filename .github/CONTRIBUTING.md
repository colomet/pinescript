# Cómo colaborar

Gracias por el interés en este proyecto.

## Antes de empezar

Abre primero un issue para cualquier cosa más grande que una errata. Los
scripts siguen unas normas de nombres, estructura y versiones (están en el
[README](../README.md)); un cambio que las altere conviene acordarlo antes de
hacerlo.

## Qué se puede aportar

- Avisar de un fallo de un script, con la plantilla «Fallo en un script».
- Proponer una mejora o un script nuevo, con la plantilla «Propuesta».
- Corregir erratas o aclarar las guías.

## Cómo

1. Haz un **fork** del repositorio.
2. Crea una **rama** para el cambio: `git checkout -b fix/descripcion-corta`
3. Haz el cambio.
4. **Prueba el script en TradingView**: pégalo en el editor de Pine, guárdalo y
   añádelo al gráfico. Pine no se puede compilar fuera de TradingView, así que
   esa prueba es la única que vale.
5. Sube la versión en la cabecera del código y anota el cambio en el
   [`CHANGELOG.md`](../CHANGELOG.md). Qué cifra sube en cada caso está en la
   sección «Versiones» del README.
6. Abre un **pull request** con la plantilla.

## Qué va dónde

| Ruta | Qué lleva |
| :--- | :-------- |
| `JLC/` | Scripts que aplican reglas de José Luis Cava |
| `GEN/` | Todo lo demás: scripts propios y adaptaciones de otros autores |
| `.github/` | Plantillas y normas de la comunidad |
| Raíz | `README.md`, `CHANGELOG.md` y `LICENSE` |

Cada script tiene su carpeta, con el mismo nombre que su archivo `.pine` y sin
la versión en el nombre. Dentro van el código y, cuando existen, sus dos guías
(`user-guide.md` y `technical-guide.md`).

## Reglas del código

- Pine Script v6, licencia MPL 2.0, con el nombre del autor en la primera línea
  de la cabecera.
- Cada cifra que venga de una fuente lleva su capítulo y su página; lo que no
  viene de la fuente lleva su marca (están en el README). No se copian textos de
  libros: capítulo, página y paráfrasis.
- Sin enlaces, redes sociales, datos de contacto ni de pago en el código.
- Título del indicador en inglés y solo con caracteres ASCII, con la forma
  `[PRENN Family] Name: key params (Author)`. Los ajustes, los tooltips y las
  alertas, en castellano.
- Si el script parte de código de otro autor, conserva su licencia y lo cita en
  la cabecera: quién es, qué licencia tiene y qué se ha mejorado.

## Estilo

Mensajes de commit: en imperativo, una línea y sin punto final
(`corrige el umbral de salida del CCI`).

La documentación está en castellano, incluidas las plantillas de issues y de
pull requests.

## Avisar de un problema de seguridad

No abras un issue público. Usa el aviso privado de vulnerabilidades de GitHub
de este repositorio; el detalle está en [`SECURITY.md`](SECURITY.md).
