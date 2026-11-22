# [JLC63 Diagnostic] CCI: 14 {threshold +/-50 in / 0 out} · Guía operativa

Cómo se añade y se ajusta. Qué dice la fuente y cómo se lee, en la guía técnica.

| Campo | Valor |
|---|---|
| Título en TradingView | `[JLC63 Diagnostic] CCI: 14 {threshold +/-50 in / 0 out}` |
| Nombre corto | `JLC63 CCI` |
| Script | Versión 0.3.0.0 (ver control de cambios) |

---

## Cómo se añade

1. Abre el gráfico del valor o índice en el marco con el que operes. El script no fuerza ningún marco: usa el del gráfico.
2. En Indicadores, busca el título o el nombre corto y añádelo.
3. Queda en un panel aparte, bajo el gráfico: la línea del CCI, el nivel 0, los dos umbrales y las marcas de entrada y de cancelación.
4. Fija el ajuste «Tendencia dominante» según la tendencia del activo: el script no la calcula.

## Ajustes

| Ajuste | Por defecto | Qué hace | Cuándo tocarlo |
|---|---|---|---|
| Período CCI (n) | 14 | Número de barras con las que se calculan la media del precio y la desviación media (mínimo 1) | 14 es el periodo que Cava usa en todos los marcos. Con un periodo más corto el CCI alcanza antes los umbrales |
| Umbral sobrecompra/sobreventa (±) | 50 | Nivel que debe cruzar el CCI para marcar una entrada: +umbral al alza (largas) o −umbral a la baja (cortas) (mínimo 1). Tiene explicación al pasar el ratón (tooltip) | 50 es el umbral de Cava. Pasa a 100 solo si, observando el activo, ves que ese nivel es más significativo |
| Tendencia dominante (filtra qué señales se muestran) | Ambas | Elige qué señales se muestran: Alcista, solo las largas (entrada y cancelación); Bajista, solo las cortas; Ambas, las dos | Ponla en Alcista o Bajista según la tendencia dominante del activo. La fijas tú a mano; `JLC41 Trend light` resuelve las tres condiciones con las que Cava la define. Con la tendencia indefinida, déjala en Ambas y toma las señales como información |

El nivel 0 (cancelación) es fijo y no se ajusta.

## Equivalencia en tiempo

| Ajuste | Valor | En diario | En semanal |
|---|---|---|---|
| Período CCI (n) | 14 | 14 sesiones | 14 semanas |

El script usa el marco del gráfico; no fuerza ninguno.

## Colores y marcas

| Elemento | Color o forma | Qué indica |
|---|---|---|
| CCI | Línea morada, grosor 2 | Distancia del precio a su media, medida en su desviación habitual; no tiene techo ni suelo fijos |
| Nivel 0 | Línea gris continua | Nivel de cancelación de la posición |
| Umbrales +U y −U | Líneas grises discontinuas | Sobrecompra (+U) y sobreventa (−U); por defecto ±50 |
| Banda gris muy tenue, entre −U y +U | Relleno | Zona sin señal de entrada |
| Entrada larga | Triángulo verde hacia arriba, abajo del panel, pequeño | El CCI cruza al alza el +U, con la tendencia en Alcista o Ambas y sin larga abierta |
| Cancela larga | Aspa verde clara, abajo del panel, pequeña | Con una larga abierta, el CCI pierde el nivel 0 |
| Entrada corta | Triángulo rojo hacia abajo, arriba del panel, pequeño | El CCI cruza a la baja el −U, con la tendencia en Bajista o Ambas y sin corta abierta |
| Cancela corta | Aspa roja clara, arriba del panel, pequeña | Con una corta abierta, el CCI supera el nivel 0 |

El script lleva la cuenta de las posiciones abiertas: solo cancela lo que antes ha entrado y no repite la entrada mientras la posición sigue abierta.

## Alertas

Este indicador no define alertas: las marcas se ven en el gráfico y no generan aviso.

## Marcos temporales

El del gráfico, el que operes. Cava usa los 14 periodos igual en semanal, diario e intradiario. El script no espera al cierre de la barra: mientras se forma, una marca puede aparecer y desaparecer; al cerrar, queda fija.

---

## Control de cambios

| Versión | Fecha | Cambios |
|---|---|---|
| 0.1.0.0 | 2026-11-21 | Primera versión, con la plantilla estándar. Describe el código 0.1.1.0: ajustes con su valor por defecto, equivalencia en tiempo, colores y marcas, ausencia de alertas y marcos temporales |
| 0.2.0.0 | 2026-11-22 | Alineada con el código 0.3.0.0: versión del script y título (sin «(Cava)») |
