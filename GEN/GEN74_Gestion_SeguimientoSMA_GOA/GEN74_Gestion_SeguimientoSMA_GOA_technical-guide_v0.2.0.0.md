# [GEN74 Management] Follow-up SMAs 20/50/150 · Guía técnica

Qué es el script, qué dice la fuente y cómo se lee lo que dibuja. La configuración, en la guía operativa.

| Campo | Valor |
|---|---|
| Procedencia | GEN. Adaptación del script «Tríada de Medias Semanales (20 / 50 / 150)» de Felix (Goat Academy). No es regla de Cava. Periodos y usos: `[Aportado]` |
| Script | Versión 0.1.1.0, estable |
| Probada en TradingView | Sí (Antonio, 22/11/2026: «funciona»; símbolo y marco sin anotar) |
| Validada en conector | No (no intentada) |

---

## Qué es

Tres medias móviles simples (SMA) del cierre, calculadas sobre velas semanales y dibujadas sobre el precio: corta (20), media (50) y larga (150). Son los tramos de seguimiento de una posición según Goat Academy. No añade señales ni alertas. Categoría 7, Management `[Interpretación]`.

## Qué dice la fuente

- **Periodos 20, 50 y 150** `[Aportado]`: de Goat Academy (Felix), sin fuente que los fije en este script. Sin enlace a su publicación `[Por confirmar]`.
- **Usos** `[Aportado]`, según el manual del código original:
  - SMA 20: salida o stop tendencial; si el precio cierra por debajo, se vende.
  - SMA 50: entrada; el cruce del precio al alza confirma el inicio de la compra.
  - SMA 150: filtro de fondo; con el precio por debajo, se prohíben las compras.
- **No es de Cava:** el manual del original atribuye además lecturas a Cava (sobreextensión en la SMA 20, filtro de salud en la SMA 50, «Stage Analysis» de Weinstein en la SMA 150) y a Pablo Gil (ritmo e impulso, reincorporaciones, dirección de las «manos fuertes»). Ninguna de esas atribuciones se ha comprobado contra el libro ni contra su fuente, y la v0.1.1.0 no las cita `[Por confirmar]`.

**Cifras del script y su origen**

| Cifra | Valor | Origen |
|---|---|---|
| SMA corta | 20 velas semanales (1 a 500) | `[Aportado]`: Goat Academy |
| SMA media | 50 velas semanales (1 a 500) | `[Aportado]`: Goat Academy |
| SMA larga | 150 velas semanales (1 a 1000) | `[Aportado]`: Goat Academy |
| Serie de precio | El cierre, fijo | Del original |
| Marco de cálculo | Semanal, fijo | Del original |

## Qué se ve en el gráfico

| Elemento | Qué es | Cómo leerlo |
|---|---|---|
| Línea verde «SMA corta (salida)» | SMA de 20 velas semanales del cierre | Según la fuente, el precio por debajo marca salida |
| Línea amarilla «SMA media (entrada)» | SMA de 50 velas semanales del cierre | Según la fuente, el precio que la cruza al alza confirma entrada |
| Línea roja «SMA larga (filtro de fondo)» | SMA de 150 velas semanales del cierre | Según la fuente, con el precio por debajo no se compra |

## Cómo funciona, paso a paso

1. Pide al mismo símbolo el cierre en velas semanales con `request.security`.
2. Calcula sobre esas velas tres SMA con `ta.sma`: 20, 50 y 150.
3. Las dibuja sobre el precio, sea cual sea el marco del gráfico.
4. No hay desplazamiento ni opciones de reaparición: es la llamada del original.

## Cuándo usarlo y cuándo no

- **Sí:** como referencia visual de seguimiento de una posición en medio y largo plazo.
- **No:** como señal por sí solo: el script no genera señales ni alertas. Tampoco como regla de Cava.
- **Cuidado** `[Interpretación]`: en marcos menores que el semanal, la media de la semana en curso puede cambiar hasta que la semana cierre; el posible repintado entre histórico y tiempo real no se ha comprobado (T4 de pendientes).

## Qué NO dice

- No da entradas ni salidas y no tiene alertas.
- Los periodos y los usos no tienen respaldo de fuente en este script.
- No tiene respaldo de Cava.

---

## Marcas de procedencia

Sin marca = regla de la fuente con capítulo y página · `[Propuesta]` = cuantificación propia · `[Aportado]` = de terceros · `[Elaboración]` = extensión editorial · `[Hueco declarado]` = la fuente lo tiene y el código no.

## Control de cambios

| Versión | Fecha | Cambios |
|---|---|---|
| 0.1.0.0 | 2026-11-22 | Creación para el código 0.1.1.0 |
| 0.2.0.0 | 2026-11-22 | Script probado por Antonio y declarado estable; sin cambios de contenido |
