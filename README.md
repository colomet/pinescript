# pinescript

Indicadores para TradingView escritos en Pine Script v6. Los documentos y la interfaz de los indicadores (ajustes, etiquetas y alertas) están en castellano; el título del indicador en TradingView va en inglés.

Es un proyecto independiente: las personas y entidades en las que se basa se citan como fuente y no participan en él (ver [Independencia](#independencia)).

## Qué hay aquí

| Carpeta | Qué contiene |
|---|---|
| [`JLC/`](JLC/README.md) | Indicadores que aplican reglas publicadas por José Luis Cava en sus libros. Cada script cita en su cabecera el capítulo y la página de donde sale la regla. |
| [`GEN/`](GEN/README.md) | Todo lo demás: scripts propios y adaptaciones de scripts de otros autores, siempre con su crédito. |

Cada carpeta tiene su índice con los scripts que contiene y el enlace a la carpeta de cada uno. En la raíz están también el [`CHANGELOG.md`](CHANGELOG.md), con el historial de versiones de cada script, la [`LICENSE`](LICENSE) y la [`BIBLIOGRAFIA.md`](BIBLIOGRAFIA.md), con las fuentes de los scripts.

Para colaborar, mira [`.github/CONTRIBUTING.md`](.github/CONTRIBUTING.md). Para avisar de un problema de seguridad, [`.github/SECURITY.md`](.github/SECURITY.md).

## Estado

Los scripts de `JLC/` están probados en TradingView sin errores de código. Falta verificar su funcionamiento (que las señales sean las que dice la regla); hasta entonces están en fase de pruebas.

## Cómo está organizado cada script

Cada script tiene su carpeta, con el mismo nombre que su archivo de código:

```text
GEN/GENNN_Familia_Nombre[_AUT]/
├── GENNN_Familia_Nombre[_AUT].pine
├── GENNN_Familia_Nombre[_AUT]_user-guide.md
└── GENNN_Familia_Nombre[_AUT]_technical-guide.md
```

Las carpetas de `JLC/` tienen la misma forma, con `JLCNN_Familia_Nombre`.

| Archivo | Para qué sirve |
|---|---|
| `.pine` | El código. Es lo que se pega en TradingView. |
| `…_user-guide.md` | Guía de uso: cómo se añade al gráfico, qué hace cada ajuste, colores, alertas y marcos temporales. |
| `…_technical-guide.md` | Guía técnica: qué es, de dónde sale la regla, cómo se lee en el gráfico, cuándo sirve y cuándo no, y qué no dice. |

Si una carpeta todavía no tiene guías, lleva solo el código.

## Cómo usar un script

1. Abrir la carpeta del script. Si tiene guía de uso (`…_user-guide.md`), leerla primero.
2. Pegar el código del `.pine` en el editor de Pine de TradingView, guardarlo y añadirlo al gráfico.
3. Para saber qué mide y cuándo sirve, leer su guía técnica (`…_technical-guide.md`). Si todavía no existe, la cabecera del código dice qué es y de dónde sale la regla.

## Cómo se llaman los scripts

`PRENN_Familia_Nombre[_AUT]`. Por ejemplo, `JLC63_Diagnostico_CCI`.

| Parte | Qué es |
|---|---|
| `PRE` | `JLC` si el script aplica una regla publicada por José Luis Cava; `GEN` para todo lo demás. |
| `NN` | Dos cifras. La primera es la familia; la segunda, el orden dentro de la familia y del prefijo. |
| `Familia`, `Nombre` | Sin tildes ni espacios. |
| `_AUT` | Solo en `GEN`: tres letras de quien hizo el script original (una persona o una entidad), como `DTR`, `GOA` o `PGI`. `ADL` son los scripts del autor de este repositorio. Sin sufijo si el script no es de nadie en concreto. |

La familia dice para qué sirve el script, no de dónde viene:

| Primera cifra | Familia | Pregunta que responde |
|---|---|---|
| 1 | Sentimiento | ¿Qué creen los participantes? |
| 2 | Amplitud | ¿Qué hacen los valores? |
| 3 | Comparativa | ¿Qué activo o sector es el fuerte? |
| 4 | Rector | ¿Hay tendencia y hacia dónde? |
| 5 | Régimen | ¿Qué tipo de sistema aplica hoy? |
| 6 | Diagnóstico | ¿Cuándo entro? |
| 7 | Gestión | ¿Cuándo salgo? |
| 8 | Pack | Varios de los anteriores reunidos en un solo indicador. |
| 9 | Backtest | ¿Habría funcionado? |

En TradingView el título del indicador va en inglés y sin tildes, con la forma `[PRENN Category] Indicator: key params`, sin nombre de autor. Por ejemplo, `[JLC63 Diagnostic] Indicator: CCI`.

## Marcas que aparecen en el código

Las cabeceras y las cifras del código llevan una marca cuando algo no es regla de la fuente:

| Marca | Significa |
|---|---|
| (sin marca) | Regla de la fuente, con cita |
| `[Propuesta]` | Cuantificación propia de algo que la fuente dice en prosa |
| `[Aportado]` | Pieza de terceros dentro de un script JLC |
| `[Elaboración]` | Simétrico o extensión de una regla de la fuente |
| `[Hueco declarado]` | La fuente lo tiene y el código no |

## Versiones

La versión de cada script (`W.X.Y.Z`, sistema Explicit Versioning) está en la cabecera del código:

| Cifra | Sube cuando |
|---|---|
| W | Cambia el diseño del script. |
| X | Cambian las señales o la forma de usarlo. |
| Y | Se corrige algo sin cambiar la señal. |
| Z | Solo cambian comentarios o cabecera. |

El historial de cada versión está en [`CHANGELOG.md`](CHANGELOG.md). Los archivos no llevan la versión en el nombre; las versiones anteriores están en el historial de Git.

## Licencia y créditos

- El código propio se publica con la Mozilla Public License 2.0 ([`LICENSE`](LICENSE)). Cada script la indica al principio de su cabecera, con el nombre del autor.
- Si un script parte de código de otro autor, conserva la licencia original y lleva su crédito: quién es el autor, qué licencia tiene y qué se ha mejorado. Se ve en la cabecera del código y en la tabla de su carpeta (`GEN/` o `JLC/`).
- Las reglas de José Luis Cava se citan por capítulo y página. Cada script indica en su cabecera de dónde sale su regla. Todas las fuentes están en [`BIBLIOGRAFIA.md`](BIBLIOGRAFIA.md).

## Aviso

Los scripts son herramientas para analizar gráficos. No son asesoramiento financiero ni una recomendación de compra o venta, y no garantizan ningún resultado.

## Independencia

Este proyecto es independiente. No tiene ninguna relación con TradingView ni con las personas y entidades que figuran como fuentes en [`BIBLIOGRAFIA.md`](BIBLIOGRAFIA.md): no han colaborado en los scripts, no los han revisado ni aprobado, y no los respaldan ni los patrocinan. Se las cita solo como fuente de las reglas, los indicadores o el código en los que se basan los scripts.

Las interpretaciones, las cifras que la fuente no da (marcadas en el código) y los errores son de este repositorio.

Los nombres y marcas citados pertenecen a sus titulares.
