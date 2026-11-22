# [JLC61 Diagnostic] Price: EMA20 + isolated max/min · Guía técnica

Qué es el script, qué dice la fuente y cómo se lee lo que dibuja. La configuración, en la guía operativa.

| Campo | Valor |
|---|---|
| Procedencia | JLC (regla de Cava del capítulo VIII de *El arte de especular*; en adelante EA). Los pivotes de 5 velas son `[Propuesta]` |
| Script | Versión 0.3.0.0 (ver control de cambios) |

---

## Qué es

Dibuja la media exponencial de 20 velas sobre el precio, marca los máximos y mínimos aislados con una línea desde el último de cada clase y avisa cuando el cierre cruza la media. Responde a una pregunta: ¿dónde está la zona de entrada tras un retroceso dentro de una tendencia y dónde va el stop? Es un indicador de diagnóstico: solo tiene sentido si ya se sabe que hay tendencia. No evalúa el ADX ni dibuja el stop.

## Qué dice la fuente

- **Mercado con tendencia (EA VIII.6.6, p. 216; VIII.6.5, p. 215):** con el ADX con clara pendiente positiva, por encima de 30 y por encima de los DI hay un mercado con tendencia (p. 216). Por encima de 30 la tendencia se considera fuerte, aunque el ADX pierda la pendiente positiva (p. 215).
- **Regla de la media de 20 sesiones (EA VIII.6.6, pp. 217-218):** Cava recoge que muchos especuladores aprovechan el retroceso hasta la media exponencial diaria de 20 sesiones para incorporarse a la tendencia cuando el ADX tiene pendiente positiva o, al menos, lecturas por encima de 30, con un stop de protección ligeramente por encima o por debajo de la media, en el sentido de la tendencia (p. 217). En tendencia alcista, si tras el retroceso el precio se gira al alza y vuelve a superar la media, compran con el stop por debajo de ella; en bajista, si tras el rebote se gira a la baja y vuelve a perforar la media, venden con el stop por encima (p. 217). Cava lo considera una buena señal, y sería muy conveniente que en ese momento la línea rápida del MACD estuviera girada y el estocástico cortado en el mismo sentido (pp. 217-218).
- **La media como soporte o resistencia (EA VIII.6.8, pp. 221-222):** algunos autores han comprobado que, cuando el ADX sube por encima de 30 y se para o se gira a la baja, el precio suele dirigirse hacia la media exponencial de 20 sesiones. En tendencia alcista, lo más probable es que la media actúe como soporte donde el precio rebote, con posiciones largas y el stop ligeramente por debajo (p. 221). En bajista, el rebote hacia la media admite posiciones cortas con el stop ligeramente por encima (p. 222).
- **Máximos y mínimos aislados (EA I.5.4, pp. 41-42):** Cava toma de Drummond la definición: un día marca un máximo aislado cuando su máximo queda por encima de los del día anterior y del posterior, y un mínimo aislado cuando su mínimo queda por debajo de los del día anterior y del posterior (p. 41). Pueden influir en el futuro porque representan zonas de resistencia y de soporte (p. 42).

**Cifras del script y su origen**

| Cifra | Valor | Origen |
|---|---|---|
| Media | Exponencial de 20 velas del cierre | EA VIII.6.6, p. 217: media exponencial diaria de 20 sesiones |
| Aviso «recupera la EMA» | El cierre pasa de debajo a encima de la media | EA VIII.6.6, p. 217: tras el retroceso, el precio vuelve a superar la media |
| Aviso «pierde la EMA» | El cierre pasa de encima a debajo de la media | EA VIII.6.6, p. 217: en bajista es la entrada; en alcista, la zona del stop, ligeramente por debajo de la media |
| Nivel del ADX | 30, o pendiente positiva; el script no lo evalúa | EA VIII.6.6, p. 217; VIII.6.5, p. 215 |
| Pivotes | 5 velas a cada lado | `[Propuesta]`: la definición de Drummond que recoge Cava usa un día a cada lado (EA I.5.4, p. 41) |
| Líneas desde el último máximo y mínimo | Extendidas a la derecha hasta que aparece otro pivote | `[Elaboración]`: la fuente habla de zonas de resistencia y de soporte (EA I.5.4, p. 42) y no las proyecta |

## Qué se ve en el gráfico

| Elemento | Qué es | Cómo leerlo |
|---|---|---|
| Línea azul | Media exponencial del cierre (20 velas por defecto) | En tendencia alcista, soporte probable; en bajista, resistencia (EA VIII.6.8, pp. 221-222) |
| Triángulo rojo sobre la vela | Máximo aislado | Pico rodeado de velas más bajas. Se confirma 5 velas después, con los valores por defecto: el triángulo aparece con retraso sobre la vela del pico |
| Triángulo verde bajo la vela | Mínimo aislado | Valle rodeado de velas más altas. Misma confirmación |
| Línea roja discontinua | Último máximo aislado, hacia la derecha | Resistencia de referencia hasta que aparezca otro |
| Línea verde discontinua | Último mínimo aislado, hacia la derecha | Soporte de referencia hasta que aparezca otro |

## Cómo funciona, paso a paso

1. Calcula la media exponencial del cierre con la longitud elegida.
2. Busca máximos y mínimos aislados: un máximo lo es si las velas de los dos lados, en el número elegido, quedan más bajas; un mínimo, si quedan más altas.
3. Un pivote solo se confirma cuando han pasado las velas de la derecha. Por eso el triángulo se dibuja sobre la vela del pico, pero aparece con retraso.
4. Dibuja la media, los triángulos y las dos líneas discontinuas desde el último máximo y el último mínimo. Cada pivote nuevo sustituye a la línea anterior de su clase.
5. Ofrece cuatro alertas: el cierre cruza la media al alza, la cruza a la baja, hay un nuevo máximo aislado y hay un nuevo mínimo aislado. Ninguna mira el ADX ni el sentido de la tendencia.

## Cómo leerlo en situaciones concretas

| Lectura | Significa | Qué no significa |
|---|---|---|
| El precio retrocede hasta la media | Parón dentro de la tendencia: es el retroceso que espera la fuente (EA VIII.6.6, p. 217) | Todavía no es entrada: la fuente entra cuando el precio vuelve a superar la media, no cuando la toca |
| Toca la media con el ADX sobre 30 | Retroceso dentro de una tendencia fuerte (EA VIII.6.5, p. 215) | Que vaya a girarse |
| Alerta «recupera la EMA» tras un retroceso | La entrada que describe la fuente en tendencia alcista, con el stop ligeramente por debajo de la media (EA VIII.6.6, p. 217) | Una orden: el script avisa, no comprueba el ADX ni dibuja el stop |
| Alerta «pierde la EMA» tras un rebote en tendencia bajista | La entrada que describe la fuente en bajista, con el stop ligeramente por encima de la media (EA VIII.6.6, p. 217) | Una venta confirmada: falta mirar el ADX |
| El cierre pierde la media con una posición larga abierta | El precio llega a la zona donde la fuente coloca el stop, ligeramente por debajo de la media (EA VIII.6.6, p. 217) | Que el stop haya saltado: va algo por debajo y el script no lo dibuja |
| Toca la media con el ADX cayendo bajo 30 | Una señal menos fiable: aumentan las señales falsas (EA VIII.6.6, p. 217) | Un lateral confirmado |
| Triángulo rojo o verde | Nivel de referencia | Señal de compra o de venta |

La entrada no es tocar la media sino volver a superarla después de tocarla, o perderla después de un rebote en bajista: son dos momentos distintos.

## Cuándo usarlo y cuándo no

- **Sí:** con tendencia definida y el ADX con pendiente positiva o por encima de 30 (EA VIII.6.6, p. 217). Gráfico diario, que es el marco de las 20 sesiones de la fuente.
- **No:** con el ADX cayendo bajo 30, donde la fuente avisa de más señales falsas (EA VIII.6.6, p. 217); en un lateral, donde el precio cruza la media una y otra vez y las alertas saltan igual. Tampoco como sistema completo: no lleva filtro de tendencia dentro.
- **Mal uso frecuente** `[Elaboración]`: entrar al tocar la media; actuar sobre una alerta sin mirar el ADX; usar los triángulos como señal.

## Qué NO dice

- No dice si el retroceso es una oportunidad o el principio de una caída.
- No comprueba el ADX: las alertas saltan igual con el ADX alto que bajo, y tampoco distinguen el sentido de la tendencia.
- No dibuja el stop: la fuente lo coloca ligeramente por debajo o por encima de la media, sin cifra (EA VIII.6.6, p. 217).
- No incluye las medias desplazadas de Cava; están en el pack `JLC81 Price`, que trae también la EMA 20 y los máximos y mínimos aislados. Conviene no cargar los dos a la vez.
- Reglas de la fuente que el script no implementa. `[Hueco declarado]`
  - El ADX con pendiente positiva o lecturas por encima de 30 como condición del retroceso (EA VIII.6.6, p. 217).
  - La confirmación con la línea rápida del MACD y el estocástico (EA VIII.6.6, pp. 217-218).
  - Las medias desplazadas 3x3, 7x5 y 25x5 (EA I.5.2, pp. 36-37).

---

## Marcas de procedencia

Sin marca = regla de Cava con capítulo y página · `[Propuesta]` = cuantificación propia · `[Aportado]` = de terceros · `[Elaboración]` = extensión editorial · `[Hueco declarado]` = la fuente lo tiene y el código no.

## Control de cambios

| Versión | Fecha | Cambios |
|---|---|---|
| 0.1.0.0 | 2026-11-15 | Primer borrador |
| 0.2.0.0 | 2026-11-20 | Contrastada con el código 0.1.1.0; solapamientos con JLC81 |
| 0.3.0.0 | 2026-11-21 | Adaptada a la plantilla estándar y al código 0.1.3.0. Citas contrastadas con EA (pp. 36-37, 41-42, 215-218, 221-222) |
| 0.4.0.0 | 2026-11-22 | Alineada con el código 0.3.0.0: versión del script y título (sin «(Cava)») |
