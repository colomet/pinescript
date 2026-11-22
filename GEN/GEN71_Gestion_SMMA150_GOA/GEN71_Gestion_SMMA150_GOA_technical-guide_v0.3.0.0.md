# [GEN71 Management] SMMA 150 exit line · Guía técnica

Qué es el script, qué dice la fuente y cómo se lee lo que dibuja. La configuración, en la guía operativa.

| Campo | Valor |
|---|---|
| Procedencia | GEN. Criterio externo, atribuido en la cabecera del script a Felix Prehn (Goat Academy, canal «Felix and Friends»). No es de Cava. La regla y el periodo son `[Aportado]`; la implementación es del propio script |
| Script | Versión 0.1.1.0 (ver control de cambios) |

---

## Qué es

Una media móvil suavizada (SMMA) de 150 velas del cierre, dibujada sobre el precio. Según la cabecera del script, es una referencia de tendencia de fondo y una línea de salida: no sirve para entrar, sino para salir si el precio la cruza a la baja. Solo dibuja la línea: no define alertas ni marca el corte. Categoría 7, Management: «¿Cuándo salgo?».

## Qué dice la fuente

- **Origen** `[Aportado]`: según la cabecera, el criterio sale de Felix Prehn (Goat Academy, canal «Felix and Friends»): salir de la posición cuando el precio corta la media de 150 sesiones. El vídeo concreto y el minuto no están identificados `[Por confirmar]`.
- **Tipo de media** `[Por confirmar]`: el script usa SMMA; el criterio de origen podría referirse a una SMA. Antonio decidió mantener SMMA el 22/11/2026 y verificarlo contra el vídeo.
- **No es de Cava:** según la cabecera, ni la SMMA ni el periodo de 150 aparecen en sus dos libros. El script no tiene umbral ni fórmula de fuente de Cava.
- **Cómo lo trata el script:** como herramienta de contexto o de salida, independiente del sistema de Cava.

**Cifras del script y su origen**

| Cifra | Valor | Origen |
|---|---|---|
| Periodo | 150 velas (mínimo 1) | `[Aportado]`: el periodo de la regla que cita la cabecera |
| Serie de precio | El cierre, ajustable | Del script |
| Valor de arranque | La media simple de las primeras 150 velas | Del script |

## Qué se ve en el gráfico

| Elemento | Qué es | Cómo leerlo |
|---|---|---|
| Línea morada «SMMA» (#673AB7) | La media suavizada de 150 velas del cierre | Con el precio por encima, la tendencia de fondo se considera intacta; si el precio la cruza a la baja, es la salida que describe el criterio de origen |

## Cómo funciona, paso a paso

1. En la primera vela que ya tiene 150 velas de historial, toma la media simple de esas 150 velas. Hasta entonces no hay línea.
2. En las siguientes, calcula media = (media anterior × 149 + precio) / 150.
3. Dibuja la línea sobre el precio.

Es la recursión de la media suavizada de Wilder (SMMA, que TradingView también llama RMA): cada precio nuevo pesa 1/150, igual que en una SMA de 150 velas y casi la mitad que en una EMA del mismo periodo (2/151) `[Verificado: aritmética]`. Con el mismo periodo, la SMMA reacciona más despacio que una EMA.

## Cómo leerlo en situaciones concretas

| Lectura | Significa | Qué no significa |
|---|---|---|
| El precio se mantiene por encima de la línea | Según la cabecera, la tendencia de fondo se considera intacta | Una señal de entrada |
| El precio cruza la línea a la baja | La señal de salida del criterio de origen, según la cabecera | Una regla de Cava ni que el precio vaya a seguir cayendo |
| La línea queda muy lejos del precio | Hace tiempo que el precio va por un lado de su media lenta `[Elaboración]` | Una señal por sí sola |

## Cuándo usarlo y cuándo no

- **Sí:** como referencia de la tendencia de fondo y como línea de salida de posiciones largas, según la cabecera.
- **No:** como indicador de entrada. Tampoco para afinar el momento: reacciona despacio.
- **Mal uso frecuente** `[Elaboración]`: tratar el corte como regla del sistema de Cava; confundirla con una SMA o una EMA de 150; esperar un aviso, porque el script no define alertas.

## Qué NO dice

- No da entradas.
- No avisa del corte: no define alertas ni marca el cruce. Se lee a ojo sobre el gráfico.
- `[Hueco declarado]` La regla pide salir cuando el precio corte la media, pero el script solo dibuja la línea: no define qué cuenta como corte (cierre, mínimo u otro).
- No tiene respaldo de Cava ni umbral.

---

## Marcas de procedencia

Sin marca = regla de Cava con capítulo y página · `[Propuesta]` = cuantificación propia · `[Aportado]` = de terceros · `[Elaboración]` = extensión editorial · `[Hueco declarado]` = la fuente lo tiene y el código no.

## Control de cambios

| Versión | Fecha | Cambios |
|---|---|---|
| 0.1.0.0 | 2026-11-15 | Creación, a partir del código legado 0.1.0.0 |
| 0.2.0.0 | 2026-11-21 | Plantilla estándar para el código legado 0.1.0.0 |
| 0.3.0.0 | 2026-11-22 | Describe el código 0.1.1.0. Autor del criterio (Felix Prehn) y tipo de media SMMA con su duda; peso de la SMMA corregido respecto a la cabecera antigua (igual que la SMA, casi la mitad que la EMA) |
