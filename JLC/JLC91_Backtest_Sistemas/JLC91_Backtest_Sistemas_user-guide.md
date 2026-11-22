# [JLC91 Backtest] Systems: EMA55 + MACD / EMA20 + ADX · Guía operativa

Cómo se añade y se ajusta. Qué dice la fuente y cómo se lee, en la guía técnica.

| Campo | Valor |
|---|---|
| Título en TradingView | `[JLC91 Backtest] Systems: EMA55 + MACD / EMA20 + ADX` |
| Nombre corto | `JLC91 Systems` |
| Script | Versión 0.3.0.0 (ver control de cambios) |

---

## Cómo se añade

1. Abre el gráfico diario del valor: es el marco en que la fuente formula los dos sistemas. El script usa el marco del gráfico y no lo fuerza.
2. En Indicadores, busca el título o el nombre corto y añádelo. Es una estrategia de prueba histórica (backtest): las operaciones, la rentabilidad y la curva de capital salen en el probador de estrategias de TradingView, en el panel inferior.
3. Se prueba un sistema cada vez: se elige en «Sistema a probar». El A es la media exponencial de 55 sesiones con el MACD. El B es el retroceso a la media exponencial de 20 sesiones con el ADX.
4. Sobre el precio dibuja las dos medias, el stop mientras hay posición abierta, los máximos y mínimos aislados (solo visuales) y, si se activa el filtro, el fondo del semáforo. Las entradas y las salidas las dibuja TradingView.
5. Los parámetros de la estrategia, que no están entre los ajustes del script sino en las propiedades de la estrategia de TradingView, vienen así: capital inicial 10.000, tamaño 20 % del patrimonio, comisión 0,05 %, sin pirámide y órdenes procesadas al cierre de la barra. Son valores de referencia: según la cabecera del script, el 20 % equivale a una cartera de 3 a 5 posiciones simultáneas. Ajústalos a tu bróker y a tu cartera antes de sacar conclusiones.

## Ajustes

Ocho grupos en el diálogo de ajustes: «Sistema», «Medias», «MACD (EA IV.1)», «ADX (EA VIII)», «Cuantificaciones no presentes en la fuente», «Stop (EA VIII.6.6: 'ligeramente por debajo de la media')», «Filtro de tendencia dominante» y «Presentación». Los tres ajustes `[Propuesta]` y «Permitir posiciones cortas» llevan descripción emergente.

| Ajuste | Por defecto | Qué hace | Cuándo tocarlo |
|---|---|---|---|
| Sistema a probar | A · EMA55 + MACD (Cap. I) | Elige el sistema que se prueba: «A · EMA55 + MACD (Cap. I)» o «B · EMA20 + ADX (Cap. VIII.6.6)» | Para comparar los dos sistemas sobre el mismo activo, con los mismos costes |
| Permitir posiciones cortas | No | Activa el lado corto, simétrico del largo | Los dos sistemas tienen lado corto en la fuente. Viene apagado porque la operativa de la cartera es larga |
| EMA del Sistema A | 55 | Período de la media del Sistema A (mínimo 1) | 55 es el período de Cava |
| EMA del Sistema B | 20 | Período de la media del Sistema B (mínimo 1) | 20 es el período de Cava |
| MACD rápido | 12 | Media rápida del MACD (mínimo 1) | 12, 26 y 9 son los valores habituales de la fuente. Solo afectan al Sistema A y al semáforo |
| MACD lento | 26 | Media lenta del MACD (mínimo 1) | Ídem |
| MACD señal | 9 | Media de la línea de señal del MACD (mínimo 1) | Ídem |
| Período ADX/DI | 14 | Período de los DI y del ADX (mínimo 1) | 14 es el de Cava, siguiendo a Wilder. Solo afecta al Sistema B |
| [Propuesta] Tolerancia del retroceso a la media (× ATR) | 0,5 | Hasta qué distancia de la media, en múltiplos de ATR, se da por hecho el retroceso (mínimo 0, paso 0,1) | `[Propuesta]`: la fuente dice «hasta la media» sin fijar cuánto debe acercarse el precio; en el Sistema B admite que la perfore ligeramente. Con 0 se exige tocarla. Con más tolerancia hay más entradas |
| [Propuesta] Ventana entre retroceso y cruce del MACD (barras) | 10 | Barras que pueden pasar entre el retroceso a la media y la señal de entrada (mínimo 1). También rige el Sistema B, donde la señal es volver a superar la media | `[Propuesta]`: la fuente no da plazo entre ambos hechos. Con una ventana corta hay menos entradas |
| Stop · modo | Múltiplo de ATR | Cómo se mide la distancia del stop a la media: «Múltiplo de ATR» o «Porcentaje» | Según prefieras medir el margen. En cortos, la distancia se mide por encima de la media |
| Stop · múltiplo de ATR bajo la media | 0,5 | Distancia del stop a la media, en múltiplos de ATR (mínimo 0,1, paso 0,1). Solo cuenta con el modo «Múltiplo de ATR» | La fuente dice «ligeramente» sin cifra: el margen es `[Propuesta]`. Un stop más cercano corta antes |
| Stop · % bajo la media | 1,0 | Distancia del stop a la media, en porcentaje de la media (mínimo 0,1, paso 0,1). Solo cuenta con el modo «Porcentaje» | Ídem |
| ATR · período | 14 | Período del ATR con el que se miden la tolerancia y el stop (mínimo 1) | Solo si cambias el ATR de referencia |
| [Propuesta] Exigir semáforo I.5.3 a favor | No | Con el filtro activo solo se entra en largo con el semáforo alcista y en corto con el bajista. Pinta el fondo | Para ver el resultado de cada sistema solo a favor de la tendencia dominante. El filtro no forma parte de ninguno de los dos sistemas |
| Mostrar máximos/mínimos aislados (solo visual) | Sí | Marca los máximos y los mínimos aislados. No intervienen en las órdenes | Apágalo si estorban |
| Pivotes · velas izquierda | 5 | Velas a la izquierda con las que se compara cada máximo o mínimo (mínimo 1) | Solo cambia el dibujo |
| Pivotes · velas derecha | 5 | Velas a la derecha con las que se compara (mínimo 1) | Solo cambia el dibujo |

Vienen fijos en el código y no se ajustan: el nivel 30 del ADX, el estocástico semanal de 14 barras del semáforo con sus umbrales 60 y 40, y el nivel cero del MACD.

## Equivalencia en tiempo

| Ajuste | Valor | En diario | En semanal |
|---|---|---|---|
| EMA del Sistema A | 55 | 55 sesiones | 55 semanas |
| EMA del Sistema B | 20 | 20 sesiones | 20 semanas |
| MACD rápido | 12 | 12 sesiones | 12 semanas |
| MACD lento | 26 | 26 sesiones | 26 semanas |
| MACD señal | 9 | 9 sesiones | 9 semanas |
| Período ADX/DI | 14 | 14 sesiones | 14 semanas |
| [Propuesta] Ventana entre retroceso y cruce del MACD (barras) | 10 | 10 sesiones, dos semanas | 10 semanas |
| ATR · período | 14 | 14 sesiones | 14 semanas |
| Pivotes · velas izquierda | 5 | 5 sesiones, una semana | 5 semanas |
| Pivotes · velas derecha | 5 | 5 sesiones, una semana | 5 semanas |

La tolerancia, el múltiplo de ATR del stop y el porcentaje del stop no se miden en tiempo.

## Colores y marcas

| Elemento | Color o forma | Qué indica |
|---|---|---|
| EMA 55 (Sistema A) | Línea azul; gruesa si se prueba el Sistema A, fina y tenue si no | Media exponencial de 55 sesiones |
| EMA 20 (Sistema B) | Línea naranja; gruesa si se prueba el Sistema B, fina y tenue si no | Media exponencial de 20 sesiones |
| Stop activo | Línea roja fina, con cortes, solo con posición abierta | Nivel del stop fijado al entrar. No se mueve hasta cerrar |
| Semáforo I.5.3 | Fondo verde, rojo o gris muy suave, solo con el filtro activo | Verde: semáforo alcista. Rojo: bajista. Gris: ni lo uno ni lo otro |
| Máximo aislado (solo visual) | Triángulo rojo hacia abajo, sobre la barra, diminuto y semitransparente | Máximo aislado confirmado. No interviene en las órdenes |
| Mínimo aislado (solo visual) | Triángulo verde hacia arriba, bajo la barra, diminuto y semitransparente | Mínimo aislado confirmado. No interviene en las órdenes |

En la lista de operaciones del probador de estrategias, las órdenes se llaman así: entrada `Largo` o `Corto`; salida por stop `Stop L` o `Stop C`; salida por señal, con el comentario «MACD corta a la baja» o «Pierde la EMA20» en largo y «MACD corta al alza» o «Supera la EMA20» en corto.

## Alertas

Este script no define alertas. Es una estrategia de prueba histórica: se usa en el probador de estrategias.

## Marcos temporales

El del gráfico, que conviene que sea el diario: la fuente formula la media de 55 sesiones y el MACD en diario, y la media de 20 sesiones también en diario. El filtro del semáforo no depende del marco del gráfico: pide por su cuenta el MACD mensual, el MACD semanal y el estocástico semanal, sin anticipación. El script no espera al cierre de la semana ni del mes: mientras están en curso, el semáforo puede cambiar en cada cierre.

---

## Control de cambios

| Versión | Fecha | Cambios |
|---|---|---|
| 0.1.0.0 | 2026-11-21 | Primera versión, con la plantilla estándar. Describe el código 0.1.2.0: ajustes con su valor por defecto, equivalencia en tiempo, colores y marcas, alertas y marcos temporales |
| 0.2.0.0 | 2026-11-22 | Alineada con el código 0.3.0.0: versión del script y título (sin «(Cava)») |
