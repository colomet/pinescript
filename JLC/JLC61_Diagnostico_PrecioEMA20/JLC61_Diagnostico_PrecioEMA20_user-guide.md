# [JLC61 Diagnostic] Price: EMA20 + isolated max/min · Guía operativa

Cómo se añade y se ajusta. Qué dice la fuente y cómo se lee, en la guía técnica.

| Campo | Valor |
|---|---|
| Título en TradingView | `[JLC61 Diagnostic] Price: EMA20 + isolated max/min` |
| Nombre corto | `JLC61 Price EMA20` |
| Script | Versión 0.3.0.0 (ver control de cambios) |

---

## Cómo se añade

1. Abre un gráfico diario del activo.
2. En Indicadores, busca el título o el nombre corto y añádelo.
3. Queda sobre el precio, no en un panel aparte.

## Ajustes

| Ajuste | Por defecto | Qué hace | Cuándo tocarlo |
|---|---|---|---|
| Longitud EMA (velas) | 20 | Velas de la media exponencial (de 1 a 500) | Solo para probar otra media; la regla de Cava es 20 |
| Velas a la izquierda (filtro) | 5 | Velas más bajas (o más altas) que debe tener a su izquierda un pico para contar como aislado (de 1 a 50) | `[Propuesta]`. Más velas, menos marcas y más importantes |
| Velas a la derecha (confirmación) | 5 | Velas posteriores necesarias para confirmar el pico (de 1 a 50) | `[Propuesta]`. Más velas, más retraso y más seguridad |

Cada ajuste lleva su explicación al pasar el ratón (tooltip). Los ajustes están en el grupo «Cálculo»; el grupo «Información» trae un resumen de solo lectura. La línea se llama «EMA» y no cambia con la longitud.

## Equivalencia en tiempo

| Ajuste | Valor | En diario | En semanal |
|---|---|---|---|
| Longitud EMA (velas) | 20 | 20 sesiones, unas 4 semanas | 20 semanas |
| Velas a la izquierda (filtro) | 5 | 5 sesiones, una semana | 5 semanas |
| Velas a la derecha (confirmación) | 5 | 5 sesiones, una semana; el pico se confirma 5 sesiones después | 5 semanas |

## Colores y marcas

| Elemento | Color o forma | Qué indica |
|---|---|---|
| EMA | Línea azul, grosor 2 | Media exponencial |
| Máximo aislado | Triángulo rojo hacia abajo, sobre la vela | Pico confirmado |
| Mínimo aislado | Triángulo verde hacia arriba, bajo la vela | Valle confirmado |
| Último máximo | Línea roja discontinua a la derecha | Resistencia de referencia |
| Último mínimo | Línea verde discontinua a la derecha | Soporte de referencia |

Los colores van fijados en el código; no hay ajustes de color.

## Alertas

Cuatro, con estos nombres exactos. Se alerta el cambio, no el estado.

| Alerta | Salta cuando |
|---|---|
| `JLC61 Precio EMA20 · recupera la EMA` | el cierre cruza la media al alza |
| `JLC61 Precio EMA20 · pierde la EMA` | el cierre cruza la media a la baja |
| `JLC61 Precio EMA20 · nuevo máximo aislado` | se confirma un máximo aislado |
| `JLC61 Precio EMA20 · nuevo mínimo aislado` | se confirma un mínimo aislado |

Para crearlas: botón de alerta, condición = este indicador, elegir la alerta de la lista. Recomendado `[Propuesta]`: una vez por cierre de vela. **Ninguna comprueba el ADX**: antes de actuar, míralo. Si tienes alertas creadas con una versión anterior del script, recréalas: los nombres han cambiado.

## Marcos temporales

Diario, que es el marco de las 20 sesiones de la fuente. En semanal funciona igual pero con tiempos cinco veces mayores. En marcos intradía no hay regla de la fuente.

---

## Control de cambios

| Versión | Fecha | Cambios |
|---|---|---|
| 0.1.0.0 | 2026-11-20 | Creación. Describe la versión 0.1.1.0 del script |
| 0.2.0.0 | 2026-11-21 | Rehecha para el código 0.1.3.0: ajustes, línea y alertas con nombres nuevos |
| 0.3.0.0 | 2026-11-21 | Adaptada a la plantilla estándar. Describe el código 0.1.3.0: tabla de datos sin estado interno, nombres exactos de los ajustes en la equivalencia en tiempo y colores fijados en el código |
| 0.4.0.0 | 2026-11-22 | Alineada con el código 0.3.0.0: versión del script y título (sin «(Cava)») |
