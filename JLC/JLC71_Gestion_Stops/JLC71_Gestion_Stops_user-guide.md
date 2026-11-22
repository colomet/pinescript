# [JLC71 Management] Stops: support / EMA20 / MACD invalidation · Guía operativa

Cómo se añade y se ajusta. Qué dice la fuente y cómo se lee, en la guía técnica.

| Campo | Valor |
|---|---|
| Título en TradingView | `[JLC71 Management] Stops: support / EMA20 / MACD invalidation` |
| Nombre corto | `JLC71 Stops` |
| Script | Versión 0.3.0.0 (ver control de cambios) |

---

## Cómo se añade

1. Abre el gráfico del valor, con posición abierta o en estudio de entrada. La cabecera del script pide el gráfico diario; el código no fuerza ningún marco y usa el del gráfico.
2. En Indicadores, busca el título o el nombre corto y añádelo.
3. Se dibuja sobre el precio, sin panel aparte: las líneas de stop de las reglas A y B, la media de referencia, las marcas de soporte nuevo y de stop tocado, y el fondo de la invalidación por MACD.
4. El script no sabe si tienes una posición abierta ni a qué precio entraste, y no coloca ni mueve órdenes. Calcula dónde caería el stop de cada regla en la barra actual; el nivel lo trasladas tú a la orden.
5. Las tres reglas se muestran a la vez, cada una con su interruptor. El lado corto viene apagado.

## Ajustes

Cuatro grupos en el diálogo del indicador: «Regla A · Soporte (EA Cap. I)», «Regla B · EMA20 (EA VIII.6.6)», «Regla C · Invalidación MACD (EA Cap. I)» y «General». EA es *El arte de especular*, de Cava. Los márgenes de las reglas A y B son `[Propuesta]`: Cava dice «ligeramente» y no da cifra.

| Ajuste | Por defecto | Qué hace | Cuándo tocarlo |
|---|---|---|---|
| Mostrar stop bajo soporte | Sí | Muestra el stop de la Regla A (último soporte menos el margen), las marcas de soporte nuevo y el aviso de stop A tocado. Apagado, desaparece toda la Regla A | Apágalo si solo quieres las reglas B o C |
| Pivote · velas izquierda | 5 | Velas a la izquierda con las que se compara un mínimo para darlo por aislado, es decir, por soporte (mínimo 1) | `[Propuesta]`: Cava, tomando a Drummond, define el mínimo aislado con un día a cada lado; el 5 es del script. Con menos velas, un mínimo cuenta antes como soporte aunque sea poco relevante |
| Pivote · velas derecha | 5 | Velas a la derecha con las que se compara. El soporte solo se confirma esas velas después de formarse (mínimo 1) | Con menos velas el stop A se actualiza antes y con menos confirmación; con más, más tarde |
| Regla A · margen | Múltiplo de ATR | Cómo se mide la distancia entre el soporte y el stop A: «Múltiplo de ATR» o «Porcentaje» | Pasa a Porcentaje si prefieres un margen fijo sobre el precio del soporte |
| Regla A · múltiplo de ATR bajo el soporte | 0,3 | Con el modo «Múltiplo de ATR», el stop queda a este múltiplo del ATR por debajo del último soporte (mínimo 0, paso 0,1). Tiene explicación al pasar el ratón (tooltip) | `[Propuesta]`: Cava dice «ligeramente por debajo» y no da cifra. Más valor, stop más lejano: más riesgo en dinero y menos salidas por ruido |
| Regla A · % bajo el soporte | 0,5 | Con el modo «Porcentaje», el stop queda a este porcentaje del último soporte, por debajo (mínimo 0, paso 0,1) | `[Propuesta]`. Solo cuenta con el modo «Porcentaje» |
| Mostrar stop bajo EMA20 | Sí | Muestra el stop de la Regla B (la media menos el margen), la propia media como referencia y el aviso de stop B tocado. Apagado, desaparece toda la Regla B | Apágalo si solo quieres las reglas A o C |
| Regla B · período EMA | 20 | Período de la media exponencial sobre la que se calcula el stop B (mínimo 1) | 20 es la media que cita Cava. Si lo cambias, la línea de referencia sigue llamándose «EMA20» pero usa tu período |
| Regla B · margen | Múltiplo de ATR | Igual que en la Regla A: «Múltiplo de ATR» o «Porcentaje» | Pasa a Porcentaje si prefieres un margen fijo sobre la media |
| Regla B · múltiplo de ATR bajo la media | 0,5 | Con el modo «Múltiplo de ATR», el stop queda a este múltiplo del ATR por debajo de la media (mínimo 0, paso 0,1). Tiene explicación al pasar el ratón (tooltip) | `[Propuesta]`: Cava dice «ligeramente» y no da cifra. 0,5 es el mismo margen por defecto que usa `JLC91 Systems`, para que las dos lecturas coincidan |
| Regla B · % bajo la media | 1,0 | Con el modo «Porcentaje», el stop queda a este porcentaje de la media, por debajo (mínimo 0, paso 0,1) | `[Propuesta]`. Solo cuenta con el modo «Porcentaje» |
| Mostrar invalidación por MACD (sistema EMA55) | Sí | Pinta un fondo rojo suave en la barra donde las líneas del MACD se cortan a la baja (Regla C). No cambia la alerta | Apágalo si el fondo molesta |
| MACD rápido | 12 | Período de la media rápida del MACD (mínimo 1) | 12, 26 y 9 son los períodos habituales del MACD que cita Cava. Cambiarlos cambia cuándo se cortan las líneas |
| MACD lento | 26 | Período de la media lenta del MACD (mínimo 1) | Como el anterior |
| MACD señal | 9 | Período de la línea de señal del MACD, la media de la línea rápida (mínimo 1) | Como el anterior |
| ATR · período (común a A y B) | 14 | Período del ATR, la amplitud media de las barras, con el que se miden los márgenes en el modo «Múltiplo de ATR» (mínimo 1) | Solo cuenta si la Regla A o la B usan ese modo |
| Calcular también el lado corto (simétrico) | No | Calcula el espejo para posiciones cortas: stops A y B por encima de la resistencia y de la media, marcas de resistencia, aspa de stop tocado bajo la barra y fondo verde en el cruce al alza del MACD | Actívalo solo si operas en corto |

En modo «Porcentaje», el margen de la Regla A se calcula sobre el último soporte, también en el lado corto; el de la Regla B, sobre la media.

## Equivalencia en tiempo

| Ajuste | Valor | En diario | En semanal |
|---|---|---|---|
| Pivote · velas izquierda | 5 | 5 sesiones | 5 semanas |
| Pivote · velas derecha | 5 | 5 sesiones | 5 semanas |
| Regla B · período EMA | 20 | 20 sesiones | 20 semanas |
| MACD rápido | 12 | 12 sesiones | 12 semanas |
| MACD lento | 26 | 26 sesiones | 26 semanas |
| MACD señal | 9 | 9 sesiones | 9 semanas |
| ATR · período (común a A y B) | 14 | 14 sesiones | 14 semanas |

El script usa el marco del gráfico; no fuerza ninguno. El soporte de la Regla A se confirma tantas barras después de formarse como indique «Pivote · velas derecha»: con 5, una semana en diario.

## Colores y marcas

| Elemento | Color o forma | Qué indica |
|---|---|---|
| Stop A · bajo soporte | Línea roja, grosor 1 | Stop de la Regla A: último soporte menos el margen. Cambia de nivel solo cuando se confirma un soporte nuevo |
| Stop A · sobre resistencia (corto) | Línea roja tenue, grosor 1 | Espejo del anterior para cortos: última resistencia más el margen. Solo con el lado corto |
| Stop B · bajo EMA20 | Línea naranja, grosor 1 | Stop de la Regla B: la media menos el margen. Se recalcula en cada barra |
| Stop B · sobre EMA20 (corto) | Línea naranja tenue, grosor 1 | Espejo del anterior para cortos: la media más el margen. Solo con el lado corto |
| EMA20 (referencia) | Línea gris muy tenue, grosor 1 | La media exponencial sobre la que se calcula el stop B |
| Nuevo soporte (pivote) | Triángulo verde tenue hacia arriba, bajo la barra, diminuto | Se confirma un mínimo aislado y el stop A pasa a ese nivel. Aparece en la barra de la confirmación, no sobre el propio mínimo |
| Nueva resistencia (pivote) | Triángulo rojo tenue hacia abajo, sobre la barra, diminuto | Se confirma un máximo aislado. Solo con el lado corto |
| STOP TOCADO (largo) | Aspa roja sobre la barra, pequeña | El cierre cruza a la baja el stop A o el stop B |
| STOP TOCADO (corto) | Aspa roja bajo la barra, pequeña | El cierre cruza al alza el stop A o el stop B del lado corto. Solo con el lado corto |
| Invalidación MACD (largo) | Fondo rojo suave | Las líneas del MACD se cortan a la baja: cierre por señal de la Regla C, sin nivel de precio |
| Invalidación MACD (corto) | Fondo verde suave | Las líneas del MACD se cortan al alza. Solo con el lado corto |

## Alertas

Seis, con estos nombres exactos. Se alerta el cambio, no el estado.

| Alerta | Salta cuando |
|---|---|
| `JLC71 Stop A tocado (bajo soporte)` | El cierre cruza a la baja el stop A. Necesita «Mostrar stop bajo soporte» activado |
| `JLC71 Stop B tocado (bajo EMA20)` | El cierre cruza a la baja el stop B. Necesita «Mostrar stop bajo EMA20» activado |
| `JLC71 Invalidación MACD (sistema EMA55, largo)` | Las líneas del MACD se cortan a la baja |
| `JLC71 Stop A tocado (sobre resistencia, corto)` | El cierre cruza al alza el stop A del lado corto. Necesita el lado corto y «Mostrar stop bajo soporte» activados |
| `JLC71 Stop B tocado (sobre EMA20, corto)` | El cierre cruza al alza el stop B del lado corto. Necesita el lado corto y «Mostrar stop bajo EMA20» activados |
| `JLC71 Invalidación MACD (sistema EMA55, corto)` | Las líneas del MACD se cortan al alza |

Para crearlas: botón de alerta, condición = este indicador, elegir la alerta de la lista. Cada una lleva su mensaje explicativo. Recomendado `[Propuesta]`: una vez por cierre de vela.

Las dos de invalidación por MACD no dependen de «Mostrar invalidación por MACD (sistema EMA55)» ni de «Calcular también el lado corto (simétrico)»: saltan con esos ajustes apagados.

Solo hay aviso cuando el cierre pasa de un lado de la línea al otro. Con el precio ya por debajo del stop no salta nada hasta que lo recupere y lo vuelva a perder. Mientras la barra se forma, el cierre es el último precio y el cruce puede deshacerse; «una vez por cierre de vela» solo avisa si la barra termina cruzada.

## Marcos temporales

El del gráfico. La cabecera del script pide el gráfico diario, y la fuente plantea las reglas B y C en diario; la A, con ejemplos en 15 minutos y en diario. El código no fuerza ningún marco: pivotes, media, MACD y ATR se miden en barras del marco que tengas abierto. El script no espera al cierre de la barra: mientras se forma, las marcas, el stop B y el fondo pueden aparecer y desaparecer; al cerrar, quedan fijos.

---

## Control de cambios

| Versión | Fecha | Cambios |
|---|---|---|
| 0.1.0.0 | 2026-11-21 | Primera versión, con la plantilla estándar. Describe el código 0.1.1.0: ajustes con su valor por defecto, equivalencia en tiempo, colores y marcas, alertas y marcos temporales |
| 0.2.0.0 | 2026-11-22 | Alineada con el código 0.3.0.0: versión del script y título (sin «(Cava)»); nombres de alerta con su prefijo exacto |
