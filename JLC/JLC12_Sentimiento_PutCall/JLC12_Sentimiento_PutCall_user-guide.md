# [JLC12 Sentiment] Put/Call ratio + Bollinger bands · Guía operativa

Cómo se añade y se ajusta. Qué dice la fuente y cómo se lee, en la guía técnica.

| Campo | Valor |
|---|---|
| Título en TradingView | `[JLC12 Sentiment] Put/Call ratio + Bollinger bands` |
| Nombre corto | `JLC12 PutCall` |
| Script | Versión 0.3.0.0 (ver control de cambios) |

---

## Cómo se añade

1. Abre un gráfico diario de cualquier activo. El script no usa el símbolo del gráfico: lee el ratio de los ajustes.
2. En Indicadores, busca el título o el nombre corto y añádelo.
3. Queda en un panel aparte, bajo el gráfico.

## Ajustes

| Ajuste | Por defecto | Qué hace | Cuándo tocarlo |
|---|---|---|---|
| Símbolo del ratio put/call | `USI:PCC` | Símbolo del que se lee el ratio. Según el propio script, `USI:PCC` es el ratio global (acciones e índices), el del rango 0,52-1,13 de la fuente | Para probar `USI:PCCE`, solo de acciones, con rango propio en la fuente (0,35-0,75) |
| Período | 20 | Sesiones de las bandas de Bollinger (de 1 a 200) | Solo para probar: con otro valor el script se aleja de la regla de la fuente |
| Desviación | 2 | Desviaciones típicas de las bandas (de 0,1 a 10) | Solo para probar: ídem |
| Mostrar niveles absolutos 0,52 y 1,13 | Sí | Dibuja dos líneas discontinuas con los niveles de giro del ratio global | Quítalas si solo quieres leer las bandas |
| Suavizado de lectura (SMA) `[Aportado]` | 10 | Sesiones de una media simple del ratio, como ayuda visual (de 1 a 200) | Si el ratio te resulta muy nervioso o quieres otra media |

Cada ajuste lleva su explicación al pasar el ratón (tooltip). Los ajustes están en tres grupos: «Datos», «Bandas de Bollinger» y «Visualización». Al final aparece un cuadro de solo lectura, «Ficha», con la fuente.

## Equivalencia en tiempo

| Ajuste | Valor | En diario | En semanal |
|---|---|---|---|
| Período de las bandas | 20 | 20 sesiones (cuatro semanas de mercado) | 20 semanas |
| Suavizado de lectura | 10 | 10 sesiones (dos semanas de mercado) | 10 semanas |

La fuente mide en diario. En semanal el script calcula lo mismo con velas semanales, pero la regla de la fuente no está medida así.

## Colores y marcas

| Elemento | Color o forma | Qué indica |
|---|---|---|
| Put/Call | Línea verde, grosor 2 | Cierre del ratio |
| Suavizado `[Aportado]` | Línea verde clara, grosor 1 | Media simple del ratio |
| Bollinger superior e inferior | Líneas grises con relleno gris claro | Bandas de 20 sesiones y desviación 2 |
| Bollinger base | Línea gris tenue | Media de 20 sesiones |
| Suelo (1,13) y techo (0,52) | Líneas grises discontinuas | Niveles de giro del ratio global que da la fuente |
| Extremo de miedo | Punto rojo, arriba del panel | Primer cierre del ratio sobre la banda superior |
| Extremo de complacencia `[Elaboración]` | Punto verde, abajo del panel | Primer cierre del ratio bajo la banda inferior |

## Alertas

Dos, con estos nombres exactos. Se alerta el cambio, no el estado.

| Alerta | Salta cuando |
|---|---|
| `JLC12 Put/Call · extremo de miedo` | el ratio cierra por encima de su banda superior de Bollinger (20/2), en la primera barra del tramo |
| `JLC12 Put/Call · extremo de complacencia` | el ratio cierra por debajo de su banda inferior de Bollinger (20/2), en la primera barra del tramo `[Elaboración]` |

Para crearlas: botón de alerta, condición = este indicador, elegir la alerta de la lista. Recomendado `[Propuesta]`: una vez por cierre de vela.

## Marcos temporales

Diario, que es el marco de la fuente. En otros marcos el script pide el ratio en ese marco; si el símbolo no ofrece datos en él, el panel queda vacío.

---

## Control de cambios

| Versión | Fecha | Cambios |
|---|---|---|
| 0.1.0.0 | 2026-11-21 | Primer borrador, para el código 0.2.0.0 |
| 0.2.0.0 | 2026-11-21 | Versión para el código 1.0.0.0 |
| 0.3.0.0 | 2026-11-21 | Rehecha con la plantilla estándar: ajustes con su valor por defecto, equivalencia en tiempo, colores y marcas, alertas con su nombre exacto, marcos temporales |
| 0.4.0.0 | 2026-11-22 | Alineada con el código 0.3.0.0: versión del script |
