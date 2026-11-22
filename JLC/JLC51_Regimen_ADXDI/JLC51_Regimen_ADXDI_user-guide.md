# [JLC51 Regime] ADX/DI: 14 {40/30/20} · Guía operativa

Cómo se añade y se ajusta. Qué dice la fuente y cómo se lee, en la guía técnica.

| Campo | Valor |
|---|---|
| Título en TradingView | `[JLC51 Regime] ADX/DI: 14 {40/30/20}` |
| Nombre corto | `JLC51 ADX` |
| Script | Versión 0.3.0.0 (ver control de cambios) |

---

## Cómo se añade

1. Abre el gráfico del valor o índice en el marco con el que operas, diario o semanal. El script no fuerza ningún marco: usa el del gráfico.
2. En Indicadores, busca el título o el nombre corto y añádelo.
3. Queda en un panel aparte, bajo el gráfico: tres líneas (ADX, +DI y -DI), tres niveles horizontales (20, 30 y 40) y las marcas de señal.

## Ajustes

| Ajuste | Por defecto | Qué hace | Cuándo tocarlo |
|---|---|---|---|
| Período ADX/DI (n) | 14 | Periodo del ADX y de los dos DI (mínimo 1) | 14 es la recomendación de Wilder que sigue Cava. En gráficos semanales Cava apunta que quizá convenga 7, a decidir por prueba y error |
| Caducidad de la condición previa (barras) | 60 | Barras máximas entre la última lectura baja del ADX (bajo 20 y bajo los dos DI) y el disparo de la mejor señal (mínimo 1). Pasado ese plazo, la condición previa se anula. Tiene explicación al pasar el ratón (tooltip) | Súbelo para admitir señales más tardías tras un tramo bajo; bájalo para exigir más cercanía. Es una propuesta del script: la fuente no da plazo `[Propuesta]` |
| Desarmar si el ADX supera el nivel 30 sin disparar | Sí | Anula la condición previa si el ADX supera 30 antes de que salga la mejor señal: por encima de 30 la tendencia ya está fortalecida y no es una que emerge. Tiene explicación al pasar el ratón (tooltip) | Quítalo si quieres que la condición previa dependa solo del plazo |

Los niveles 20, 30 y 40 y el rango de la regla de Elder (de 4 a 12 puntos) los fija la fuente y no se ajustan.

## Equivalencia en tiempo

| Ajuste | Valor | En diario | En semanal |
|---|---|---|---|
| Período ADX/DI (n) | 14 | 14 sesiones | 14 semanas |
| Caducidad de la condición previa (barras) | 60 | 60 sesiones (unos tres meses de mercado) | 60 semanas |

El script usa el marco del gráfico; no fuerza ninguno.

## Colores y marcas

| Elemento | Color o forma | Qué indica |
|---|---|---|
| ADX | Línea verde, grosor 2 | Fuerza de la tendencia, no su dirección |
| +DI | Línea azul, grosor 1 | Presión compradora |
| -DI | Línea roja, grosor 1 | Presión vendedora |
| Nivel 40 | Línea gris discontinua | Tendencia muy fuerte si el ADX además sube |
| Nivel 30 | Línea gris continua | Tendencia ya fortalecida |
| Nivel 20 | Línea gris discontinua | Lectura baja: condición previa de la mejor señal |
| Banda gris muy tenue, de 0 a 20 | Relleno | Zona de ADX bajo |
| Fondo gris claro | Fondo del panel | El ADX está por encima de 30. Si además supera 40 y sube, el fondo es verde en lugar de gris |
| Fondo verde | Fondo del panel | El ADX está por encima de 40 y subiendo. No indica dirección |
| Mejor señal de compra | Triángulo verde hacia arriba, abajo del panel | Tras un tramo con el ADX bajo 20 y bajo los dos DI, el ADX gira al alza y supera al -DI con el +DI dominante y subiendo y el -DI bajando |
| Mejor señal de venta | Triángulo rojo hacia abajo, arriba del panel | Lo mismo en sentido contrario: el ADX supera al +DI con el -DI dominante y subiendo y el +DI bajando |
| Giro del ADX (regla de Elder) | Círculo naranja pequeño, abajo del panel | Tras caer bajo los dos DI, el ADX sube de 4 a 12 puntos desde su mínimo |

Cada marca sale una sola vez: tras una señal hay que volver a pasar por la condición previa para que salga otra.

## Alertas

Este indicador no define alertas: las marcas se ven en el gráfico y no generan aviso.

## Marcos temporales

El marco del gráfico, diario, semanal o el que operes. El script no espera al cierre de la barra: mientras se forma, una marca puede aparecer y desaparecer; al cerrar, queda fija.

---

## Control de cambios

| Versión | Fecha | Cambios |
|---|---|---|
| 0.1.0.0 | 2026-11-21 | Primera versión, con la plantilla estándar. Describe el código 0.1.1.0: ajustes con su valor por defecto, equivalencia en tiempo, colores y marcas, ausencia de alertas y marcos temporales |
| 0.2.0.0 | 2026-11-22 | Alineada con el código 0.3.0.0: versión del script y título (sin «(Cava)») |
