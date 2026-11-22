# [JLC11 Sentiment] VIX vs SMA10 + bands · Guía operativa

Cómo se añade y se ajusta. Qué dice la fuente y cómo se lee, en la guía técnica.

| Campo | Valor |
|---|---|
| Título en TradingView | `[JLC11 Sentiment] VIX vs SMA10 + bands` |
| Nombre corto | `JLC11 VIX` |
| Script | Versión 0.3.0.0 (ver control de cambios) |

---

## Cómo se añade

1. Abre un gráfico diario de cualquier activo. El script no usa el símbolo del gráfico: lee el VIX de los ajustes.
2. En Indicadores, busca el título o el nombre corto y añádelo.
3. Queda en un panel aparte, bajo el gráfico.

## Ajustes

| Ajuste | Por defecto | Qué hace | Cuándo tocarlo |
|---|---|---|---|
| Símbolo del VIX | `CBOE:VIX` | Símbolo del que se lee el VIX | Si no está en tu plan de datos, prueba `TVC:VIX` |
| Símbolo del VIX3M | `CBOE:VIX3M` | Símbolo del VIX a tres meses `[Aportado]` | Si no carga, prueba `TVC:VIX3M` |
| Período SMA del VIX | 10 | Sesiones de la media simple del VIX (de 1 a 200) | Solo para probar otra media: con otro valor el script se aleja de las cifras de la fuente |
| Mostrar VIX3M y estructura de plazo | Sí | Dibuja el VIX3M y colorea el fondo cuando el VIX lo supera `[Aportado]` | Quítalo si el VIX3M no carga o solo quieres el sistema de la fuente |
| Marcar la sesión de cancelación (+5) | Sí | Marca con una cruz la quinta sesión tras la señal de compra | Quítalo si no usas la cancelación a 5 sesiones |

Cada ajuste lleva su explicación al pasar el ratón (tooltip). Los ajustes están en dos grupos, «Datos» y «Visualización». Al final aparece un cuadro de solo lectura, «Ficha», con la fuente.

## Equivalencia en tiempo

| Ajuste | Valor | En diario | En semanal |
|---|---|---|---|
| Período SMA del VIX | 10 | 10 sesiones (dos semanas de mercado) | 10 semanas |
| Sesión de cancelación | 5 | 5 sesiones (una semana de mercado) | 5 semanas |

La fuente mide en diario. En semanal el script calcula lo mismo con velas semanales, pero la regla de la fuente no está medida así.

## Colores y marcas

| Elemento | Color o forma | Qué indica |
|---|---|---|
| VIX | Línea casi negra, grosor 2 | Cierre del VIX |
| SMA10 VIX | Línea gris oscura | Media simple de 10 sesiones |
| +12 % | Línea verde | Banda de señal de compra |
| +5 % | Línea verde tenue | Banda de sesgo alcista a 5 sesiones |
| −5 % | Línea roja | Banda de sesgo bajista a 5 sesiones |
| VIX3M `[Aportado]` | Línea morada | VIX a tres meses |
| Señal de compra | Triángulo verde hacia arriba, abajo del panel | El VIX cruza al alza la banda +12 % |
| Cancelación | Cruz gris, abajo del panel | Quinta sesión tras la señal |
| Backwardation `[Aportado]` | Fondo naranja suave | El VIX está por encima del VIX3M |

## Alertas

Tres, con estos nombres exactos. Se alerta el cambio, no el estado.

| Alerta | Salta cuando |
|---|---|
| `JLC11 VIX · señal de compra (+12% sobre SMA10)` | el VIX cruza por encima de la banda +12 % de su media de 10 sesiones |
| `JLC11 VIX · sesgo bajista (-5% bajo SMA10)` | el VIX cruza por debajo de la banda −5 % |
| `JLC11 VIX · entrada en backwardation` | el VIX pasa a estar por encima del VIX3M `[Aportado]` |

Para crearlas: botón de alerta, condición = este indicador, elegir la alerta de la lista. Recomendado `[Propuesta]`: una vez por cierre de vela.

## Marcos temporales

Diario, que es el marco de la fuente. En semanal o mensual hay cálculo, pero no regla de la fuente. En marcos intradía no se recomienda: la fuente no los trata.

---

## Control de cambios

| Versión | Fecha | Cambios |
|---|---|---|
| 0.1.0.0 | 2026-11-21 | Primer borrador, para el código 1.1.0.0 |
| 0.2.0.0 | 2026-11-21 | Rehecha con la plantilla estándar. Describe la versión 1.2.0.0 del script: ajustes con su valor por defecto, equivalencia en tiempo, colores y marcas, alertas con su nombre exacto |
| 0.3.0.0 | 2026-11-22 | Alineada con el código 0.3.0.0: versión del script |
