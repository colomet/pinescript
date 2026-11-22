# [GEN81 Pack] RSI and MACD · Guía operativa

Cómo se añade y se ajusta. Qué dice la fuente y cómo se lee, en la guía técnica.

| Campo | Valor |
|---|---|
| Título en TradingView | `[GEN81 Pack] RSI and MACD` |
| Nombre corto | `GEN81 RSI+MACD` |
| Script | Versión 0.1.2.0 (ver control de cambios) |

---

## Cómo se añade

1. Abre el gráfico del activo, en el marco con el que operes.
2. En Indicadores, busca el título o el nombre corto y añádelo.
3. Se dibuja en un panel propio debajo del precio, con el RSI y el MACD juntos.

## Ajustes

Cuatro grupos: «RSI», «MACD (escala del dibujo)», «Aspecto» e «Info». Los ajustes del RSI, el zoom y el color de la línea cero llevan una explicación al pasar el ratón (tooltip).

| Ajuste | Por defecto | Qué hace | Cuándo tocarlo |
|---|---|---|---|
| Periodo RSI (velas) | 14 | Velas con las que se calcula el RSI (de 1 a 500). Menos velas, más nervioso; más velas, más suave | `[Aportado]`: 14 es el periodo de Trullás. Cambiarlo da otro RSI, no el suyo |
| Nivel clave RSI | 40 | Dibuja una línea horizontal en ese valor del RSI (de 0 a 100). Solo se dibuja: el script no da señal al cruzarla | `[Aportado]`: 40 es el nivel de Trullás. Cambiarlo solo mueve la línea de referencia |
| Zoom del MACD (factor) | 30 | Solo dibujo: multiplica línea, señal e histograma del MACD (de 1 a 200) para verlos junto al RSI, que va de 0 a 100. Con 1 se ve el MACD real | Si el MACD sale aplastado, súbelo; si se sale del panel, bájalo. El factor adecuado depende del precio del activo |
| Color línea RSI | verde | Color de la línea del RSI | A gusto: solo cambia el dibujo |
| Color línea MACD | azul | Color de la línea del MACD | A gusto: solo cambia el dibujo |
| Color línea de señal | rojo | Color de la línea de señal | A gusto: solo cambia el dibujo |
| Color histograma sobre cero | verde azulado | Color de las columnas positivas | A gusto: solo cambia el dibujo |
| Color histograma bajo cero | granate | Color de las columnas negativas | A gusto: solo cambia el dibujo |
| Color línea cero | gris | Color de la línea cero del MACD. Gris para que se vea en tema claro y oscuro | A gusto: solo cambia el dibujo |

El grupo «Info» trae un resumen de solo lectura. Los periodos del MACD (12, 26 y 9) y el color de la línea del nivel clave (gris) van fijos: no son ajustes.

## Equivalencia en tiempo

Son velas, no días. Con 5 sesiones por semana:

| Ajuste | Valor | En diario | En semanal |
|---|---|---|---|
| Periodo RSI (velas) | 14 | 14 sesiones, casi 3 semanas | 14 semanas, unos 3 meses |

Los periodos fijos del MACD también son velas: 12 y 26 para las dos medias, 9 para la señal.

## Colores y marcas

| Elemento | Color o forma | Qué indica |
|---|---|---|
| RSI | Línea verde, grosor 2 | El RSI del cierre, de 0 a 100 |
| Línea MACD (con zoom) | Línea azul, grosor 2 | Media exponencial de 12 menos la de 26, multiplicada por el zoom |
| Línea de señal (con zoom) | Línea roja, grosor 1 | Media exponencial de 9 del MACD, multiplicada por el zoom |
| Histograma MACD (con zoom) | Columnas verde azulado (sobre cero) y granate (bajo cero) | MACD menos señal, multiplicado por el zoom |
| Nivel clave RSI | Línea gris discontinua | El valor del ajuste (40 por defecto) |
| Línea cero | Línea gris continua | El cero del MACD |

## Alertas

Este script no define alertas.

## Marcos temporales

El del gráfico: el script no fuerza ninguno.

---

## Control de cambios

| Versión | Fecha | Cambios |
|---|---|---|
| 0.1.0.0 | 2026-11-14 | Creación (GEN61) |
| 0.1.1.0 | 2026-11-15 | Rangos de los ajustes, grupo «Info», color del nivel clave no ajustable |
| 0.2.0.0 | 2026-11-21 | Plantilla estándar. Describe el código 0.1.0.0 (GEN61) |
| 0.3.0.0 | 2026-11-22 | Renombrada a GEN81 Pack. Título `[GEN81 Pack] RSI and MACD`, nombre corto `GEN81 RSI+MACD`. Describe el código 0.1.2.0. Ajustes sin cambios |
