# [JLC31 Comparative] SMA 10w/40w + weekly MACD · Guía operativa

Cómo se añade y se ajusta. Qué dice la fuente y cómo se lee, en la guía técnica.

| Campo | Valor |
|---|---|
| Título en TradingView | `[JLC31 Comparative] SMA 10w/40w + weekly MACD` |
| Nombre corto | `JLC31 SMA+MACD` |
| Script | Versión 0.3.0.0 (ver control de cambios) |

---

## Cómo se añade

1. Abre un gráfico semanal del ratio entre dos símbolos, por ejemplo un sector frente a su índice. En el cuadro de símbolo se escribe como una división: `A/B`. El script lee el símbolo del gráfico; no tiene símbolo propio en los ajustes.
2. En Indicadores, busca el título o el nombre corto y añádelo.
3. Las dos medias se dibujan sobre el gráfico del ratio. El MACD, su señal, el cero y el fondo de color quedan en un panel aparte, bajo el gráfico.

## Ajustes

| Ajuste | Por defecto | Qué hace | Cuándo tocarlo |
|---|---|---|---|
| Forzar temporalidad semanal | Sí | Calcula medias y MACD en semanal, sea cual sea el gráfico | Quítalo solo para leer el marco del gráfico; entonces los periodos se cuentan en barras de ese marco |
| Leer solo la barra cerrada | Sí | Lee la última barra cerrada del marco elegido: la señal no cambia después, a cambio de ir una barra por detrás | Quítalo para ver la barra en curso, sabiendo que puede variar hasta su cierre |
| SMA corta (semanas) | 10 | Media simple del cierre para la tendencia intermedia (mínimo 1) | Solo para probar otro periodo: con otro valor ya no es la media de 10 semanas |
| SMA larga (semanas) | 40 | Media simple del cierre para la tendencia larga (mínimo 1) | Solo para probar otro periodo: con otro valor ya no es la media de 40 semanas |
| MACD rápido | 12 | Periodo de la media rápida del MACD (mínimo 1); debe ser menor que el lento | Solo para probar otros periodos |
| MACD lento | 26 | Periodo de la media lenta del MACD (mínimo 1) | Solo para probar otros periodos |
| MACD señal | 9 | Periodo de la línea de señal (mínimo 1); sus cruces con el MACD generan los triángulos | Solo para probar otros periodos |

Cada ajuste lleva su explicación al pasar el ratón (tooltip). Los ajustes están en cuatro grupos: «Temporalidad», «Medias móviles», «MACD» y «Ficha». «Ficha» es un cuadro de solo lectura con un resumen de lo que dibuja y de la fuente.

## Equivalencia en tiempo

| Ajuste | Valor | En diario | En semanal |
|---|---|---|---|
| SMA corta (semanas) | 10 | Con semanal forzado: 10 semanas. Sin forzar: 10 sesiones; para 10 semanas, unas 50 | 10 semanas |
| SMA larga (semanas) | 40 | Con semanal forzado: 40 semanas. Sin forzar: 40 sesiones; para 40 semanas, unas 200 | 40 semanas |
| MACD rápido / lento / señal | 12 / 26 / 9 | Con semanal forzado: 12, 26 y 9 semanas. Sin forzar: sesiones | 12, 26 y 9 semanas |

Con «Forzar temporalidad semanal» activado, que es el valor por defecto, el marco del gráfico no cambia el cálculo: todo se mide en semanas.

## Colores y marcas

| Elemento | Color o forma | Qué indica |
|---|---|---|
| SMA 10s | Línea azul, sobre el gráfico principal | Media simple del cierre a 10 semanas |
| SMA 40s | Línea naranja, sobre el gráfico principal | Media simple del cierre a 40 semanas |
| MACD | Línea verde, grosor 2, en el panel propio | Línea MACD semanal |
| Señal | Línea roja, grosor 1, en el panel propio | Línea de señal del MACD |
| Cero | Línea gris continua, en el panel propio | Nivel de equilibrio del MACD |
| Cruce MACD a favor de tendencia (compra) | Triángulo verde hacia arriba, abajo del panel | El MACD cruza al alza su señal y la media de 10 semanas está por encima de la de 40 |
| Cruce MACD a favor de tendencia (venta) | Triángulo rojo hacia abajo, arriba del panel | El MACD cruza a la baja su señal y la media de 10 semanas está por debajo de la de 40 |
| Zona recomendada: verde | Fondo verde tenue, en el panel propio | El cierre está por encima de las dos medias |
| Zona recomendada: gris | Fondo gris tenue, en el panel propio | El cierre está por encima de la media de 40 semanas y no de la de 10 |
| Sin fondo | — | El cierre no supera la media de 40 semanas |

El fondo se colorea en el panel propio del indicador (el del MACD), no sobre el gráfico principal, donde solo van las dos medias.

## Alertas

Cuatro, con estos nombres exactos. Se alerta el cambio, no el estado.

| Alerta | Salta cuando |
|---|---|
| `JLC31 SMA+MACD · cruce MACD a favor (compra)` | el MACD semanal cruza al alza su señal con la media de 10 semanas por encima de la de 40 |
| `JLC31 SMA+MACD · cruce MACD a favor (venta)` | el MACD semanal cruza a la baja su señal con la media de 10 semanas por debajo de la de 40 |
| `JLC31 SMA+MACD · entra en zona recomendada` | el cierre pasa a estar por encima de las dos medias |
| `JLC31 SMA+MACD · pierde la SMA40` | el cierre deja de estar por encima de la media de 40 semanas |

No hay alerta para la entrada en el fondo gris.

Para crearlas: botón de alerta, condición = este indicador, elegir la alerta de la lista. Recomendado `[Propuesta]`: una vez por cierre de vela.

## Marcos temporales

Semanal, que es el marco del criterio: medias de 10 y 40 semanas y MACD semanal. Con «Forzar temporalidad semanal» activado también puede añadirse a un gráfico diario: el cálculo sigue siendo semanal y las señales salen al cierre de la semana. En un gráfico mensual no se recomienda con ese ajuste activado: el script pediría datos semanales, de un marco inferior al del gráfico. En marcos intradía no se recomienda: el criterio no los trata.

---

## Control de cambios

| Versión | Fecha | Cambios |
|---|---|---|
| 0.2.0.0 | 2026-11-21 | Guía de uso para el código 0.2.0.0 |
| 0.3.0.0 | 2026-11-21 | Rehecha con la plantilla estándar. Describe el código 0.2.0.0: ajustes con su valor por defecto, equivalencia en tiempo, colores y marcas, alertas con su nombre exacto y marcos temporales |
| 0.4.0.0 | 2026-11-22 | Alineada con el código 0.3.0.0: versión del script |
