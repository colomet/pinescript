# Bibliografía y fuentes

Aquí están las obras y los autores en los que se basan los scripts de este repositorio. Cada script cita además su fuente en la cabecera del código, con capítulo y página cuando la fuente es un libro.

Este proyecto es independiente: ninguna de las personas y entidades que figuran en este documento ha colaborado en los scripts, los ha revisado o aprobado, ni los respalda o patrocina. Se las cita solo como fuente. Más en [Independencia](#independencia).

## Cómo se cita

- Libros: autor, obra, capítulo y página. Cuando el script resume una idea del libro, la cabecera lo marca como paráfrasis.
- Scripts de otros autores: autor, nombre del script original y qué se ha cambiado.
- Lo que no viene de la fuente lleva una marca en el código (`[Propuesta]`, `[Aportado]`, `[Elaboración]`, `[Hueco declarado]`). Qué significa cada una está en el [README](README.md#marcas-que-aparecen-en-el-código).

## Libros

### Scripts `JLC`

| Obra | Autor | Editorial, año y edición | Scripts |
|---|---|---|---|
| *El arte de especular: las técnicas que mejor funcionan* | José Luis Cava | [Por confirmar] | JLC11, JLC12, JLC41, JLC42, JLC51, JLC61, JLC62, JLC63, JLC71, JLC81, JLC82, JLC91 |
| *Sistemas de especulación en bolsa* | José Luis Cava | [Por confirmar] | JLC31, JLC32 |

Capítulos principales de cada script (el detalle, con páginas, está en la cabecera del código):

| Script | Obra | Capítulos principales |
|---|---|---|
| JLC11 Sentimiento VIX | El arte de especular | II.2.3.2 |
| JLC12 Sentimiento Put/Call | El arte de especular | II.2.4 y II.2.4.1 |
| JLC31 Comparativa Murphy SMA/MACD | Sistemas de especulación en bolsa | IX.2 |
| JLC32 Comparativa OBV Liderazgo | Sistemas de especulación en bolsa | IX.2 |
| JLC41 Rector Semáforo | El arte de especular | I.5.3, IV.1, IV.2.2 y V.1.1 |
| JLC42 Rector Tablero | El arte de especular | I.5.3, III.1.4, IV, V, VII.3.1 y VIII.6 |
| JLC51 Régimen ADX/DI | El arte de especular | VIII |
| JLC61 Diagnóstico Precio/EMA20 | El arte de especular | VIII.6.6 |
| JLC62 Diagnóstico Estocástico | El arte de especular | V e I.5.3 |
| JLC63 Diagnóstico CCI | El arte de especular | VII |
| JLC71 Gestión Stops | El arte de especular | I y VIII.6.6 |
| JLC81 Pack Precio | El arte de especular | I.5.2, I y VIII.6.6 |
| JLC82 Pack Momento | El arte de especular | V, I.5.3, VII y VIII.6 |
| JLC91 Backtest Sistemas | El arte de especular | I, IV.1 y VIII.6 |

### Autores que aparecen dentro de esos libros

Algunas reglas de los libros las atribuyen a otros autores. Aquí se mencionan porque el código o las guías los nombran; sus obras originales no son fuente de este repositorio: las reglas se toman de la exposición del libro que las recoge.

| Autor | Qué se le atribuye | Dónde aparece |
|---|---|---|
| Murphy | Su forma de especular con medias de 10 y 40 semanas, MACD semanal y OBV | JLC31, JLC32 (*Sistemas de especulación en bolsa*, IX.2) |
| Lane | Estocástico | JLC62, JLC82 |
| Lambert | CCI | JLC63, JLC82 |
| Wilder | ADX/DI y su periodo de 14 | JLC51, JLC82, JLC91 |
| Elder | Regla de subida del ADX | JLC51, JLC82 |
| DiNapoli | Medias desplazadas (nota 14, p. 36 de *El arte de especular*) | JLC81 |

## Scripts de otros autores y fuentes sin libro

### Scripts `GEN`

| Script | Fuente | Qué se ha tomado y qué se ha cambiado |
|---|---|---|
| GEN21 Amplitud S&P 500 | Sin autor concreto | Código propio. Los símbolos S5FI y S5TH y los niveles 30/50/70 son convención técnica de uso general. |
| GEN41 Rector Canal de regresión largo plazo | okhanLAB, sobre el Linear Regression Channel de TradingView | Parte del código original, con su licencia (MPL 2.0). Añade las bandas de dispersión, el inicio fijo, automático o por fecha, una tabla en el gráfico y alertas. |
| GEN42 Rector Medias de control | David Trullás | Agrupación de tres medias simples y sus periodos por defecto (6, 70 y 200), citados por cortesía. El código es propio. |
| GEN44 Rector EMA 50 | TradingView, indicador integrado «Moving Average Exponential» | Plantilla oficial sin cambios de cálculo; el periodo por defecto pasa a 50. El periodo 50 no tiene fuente confirmada. |
| GEN71 Gestión SMMA 150 | Felix Prehn, Goat Academy (canal «Felix and Friends») | Criterio de salida al cortar la media de 150 sesiones, de un vídeo sin identificar. El código es propio. Tipo de media (SMMA) sin confirmar contra el vídeo. |
| GEN74 Gestión Seguimiento SMA | Felix, Goat Academy, script «Tríada de Medias Semanales (20 / 50 / 150)» | Adaptación: periodos 20, 50 y 150 y su uso. Añade estructura, ajustes con límites y comentarios; el cálculo es el del original. |
| GEN81 Pack RSI y MACD | David Trullás, script «RSI y MACD Completo» | Adaptación. El script original no declara licencia. Añade estructura, ayudas en los ajustes y línea cero ajustable; el cálculo es el del original. |
| GEN82 Pack Estocástico y RSI | Pablo Gil, script «Estocástico + RSI Unificados» | De Gil solo vienen los parámetros (estocástico 18-9-5 y RSI 14); el código es propio. |

### Indicadores estándar

Las medias móviles (SMA, EMA, SMMA), el RSI, el MACD, el ATR y el resto de indicadores de uso general se calculan con las funciones integradas de Pine Script (`ta.*`) de TradingView.

## Licencias

- Código propio: Mozilla Public License 2.0 ([`LICENSE`](LICENSE)).
- Código de otros autores: conserva su licencia original, que se indica en la cabecera del script.
- Los libros no se reproducen ni se incluyen en este repositorio: se cita capítulo y página.

## Errores y ampliaciones

Si una cita no coincide con el libro o falta una fuente, abre una incidencia o una propuesta de cambio como se explica en [`.github/CONTRIBUTING.md`](.github/CONTRIBUTING.md).

## Independencia

Este proyecto no tiene ninguna relación con TradingView ni con las personas y entidades que figuran en este documento: no han colaborado en los scripts, no los han revisado ni aprobado, y no los respaldan ni los patrocinan. Se las cita solo como fuente de las reglas, los indicadores o el código en los que se basan los scripts.

Las interpretaciones, las cifras que la fuente no da (marcadas en el código) y los errores son de este repositorio.

Los nombres y marcas citados pertenecen a sus titulares.
