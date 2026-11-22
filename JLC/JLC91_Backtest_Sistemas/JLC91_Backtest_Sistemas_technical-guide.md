# [JLC91 Backtest] Systems: EMA55 + MACD / EMA20 + ADX · Guía técnica

Qué es el script, qué dice la fuente y cómo se lee lo que dibuja. La configuración, en la guía operativa.

| Campo | Valor |
|---|---|
| Procedencia | JLC (dos sistemas de Cava, del capítulo I y del VIII de *El arte de especular*; en adelante EA). La tolerancia del retroceso, el plazo, el margen del stop y el filtro opcional están rotulados `[Propuesta]` en el código |
| Script | Versión 0.3.0.0 (ver control de cambios) |

---

## Qué es

Estrategia de prueba histórica (backtest) que pone a prueba, de uno en uno, dos sistemas de Cava para entrar a favor de la tendencia tras un retroceso a una media exponencial. El Sistema A usa la media de 55 sesiones y el MACD (capítulo I). El Sistema B usa la media de 20 sesiones y el ADX (VIII.6.6). Se elige en los ajustes y el resultado sale en el probador de estrategias de TradingView: operaciones, rentabilidad y curva de capital.

Sobre el precio dibuja las dos medias, el stop de la posición abierta, los máximos y mínimos aislados (solo visuales) y, si se activa el filtro, el fondo del semáforo de tendencia. No define alertas. El resultado es el de la traducción que hace el script de las reglas de Cava, con sus cuantificaciones propias, no el del método de Cava.

## Qué dice la fuente

- **Sistema A, media de 55 sesiones y MACD (EA I.1.1, pp. 13-14):** el sistema sencillo de Cava sobre el NASDAQ 100 usa la media exponencial diaria de 55 sesiones (p. 13) y el MACD en diario (p. 14). En largo: el precio sobre la media, con pendiente positiva o plana; compra cuando el precio retrocede hasta la media y las dos líneas del MACD se cortan al alza por encima de cero. La posición larga se cancela cuando las líneas del MACD en diario se cortan a la baja. En corto, el espejo: el precio sube hasta la media de 55 sesiones, las líneas del MACD se cruzan a la baja, ambas por debajo de cero, y la cancelación llega cuando las líneas se cortan al alza (p. 14).
- **Disciplina del stop (EA I.1.1, pp. 15, 16 y 19):** el stop de cancelación se fija antes de entrar, con los criterios del sistema (p. 15). Mientras el precio se mantenga por encima del nivel donde las reglas lo situarían, la posición sigue hasta que el sistema dé la señal de cancelación (p. 16). Las reglas del stop son parte esencial del sistema (p. 19).
- **ADX y mercado con tendencia (EA VIII.6.6, pp. 216-217):** con el ADX con clara pendiente positiva, por encima de 30 y por encima de los DI hay un mercado con tendencia, y las señales de los sistemas seguidores de tendencia son muy fiables (p. 216). Con el ADX cayendo y lecturas inferiores a 30 esas señales son menos provechosas y aumentan las falsas (p. 217).
- **Nivel 30 del ADX (EA VIII.6.5, p. 215):** si el ADX sigue subiendo y supera 30, la tendencia se ha fortalecido; aunque pierda la pendiente positiva, mientras se mantenga sobre 30 se sigue considerando fuerte.
- **Sistema B, retroceso a la media de 20 sesiones (EA VIII.6.6, pp. 217-218):** Cava recoge que muchos especuladores aprovechan el retroceso hasta la media exponencial diaria de 20 sesiones para incorporarse a la tendencia cuando el ADX tiene pendiente positiva o, al menos, lecturas sobre 30, con un stop de protección ligeramente por encima o por debajo de la media, en el sentido de la tendencia (p. 217). En tendencia alcista, el precio retrocede hasta la media, o la perfora ligeramente, con el ADX con pendiente positiva y sobre 30; cuando se gira al alza y vuelve a superar la media, compran con el stop por debajo de ella. Cava lo considera una buena señal y sería muy conveniente que en ese momento estuviera girada al alza la línea rápida del MACD y cortado al alza el estocástico (p. 217). En tendencia bajista, el espejo: rebote hasta la media, o ligeramente por encima, giro a la baja y pérdida de la media, con el stop por encima (p. 217); la señal sería muy fiable con la línea rápida del MACD girada a la baja y el estocástico cortado a la baja (p. 218).
- **Período del ADX y de los DI (EA VIII.6.4, pp. 214-215):** Cava trabaja con 14, el de Wilder. Elder recomienda 13, y no existe un período mágico.
- **Períodos de las medias (EA VIII.6.6, nota 68, p. 216):** Cava suele trabajar con 5, 10, 20 y 40, sin valores mágicos y universales, y recomienda probar otros períodos. Muchos especuladores usan la serie de Fibonacci, que incluye el 55.
- **MACD (EA IV.1, p. 101):** la línea rápida es la diferencia entre dos medias exponenciales, que suelen ser de 12 y 26 períodos; la de señal es una media exponencial de 9 períodos de la rápida. Cada uno puede usar otros períodos.
- **Tendencia dominante, el semáforo (EA I.5.3, p. 37):** es alcista cuando el MACD mensual está cortado al alza, la línea rápida del MACD semanal está por encima de cero y la línea rápida del estocástico semanal está por encima de 60. Es bajista cuando el MACD mensual está cortado a la baja, la línea rápida del MACD semanal está por debajo de cero y la del estocástico semanal, por debajo de 40.
- **Señales subordinadas a la tendencia (EA VII.3.1, pp. 187-188):** las señales de los sistemas están siempre condicionadas al sentido de la tendencia: si es alcista se siguen las de compra y si es bajista, las de venta.
- **Máximos y mínimos aislados (EA I.5.4, pp. 41-42):** Cava toma de Drummond la definición: un día marca un máximo aislado cuando su máximo queda por encima de los del día anterior y del posterior, y un mínimo aislado cuando su mínimo queda por debajo de los del día anterior y del posterior (p. 41). Pueden influir en el futuro porque representan zonas de resistencia y de soporte (p. 42).

**Cifras del script y su origen**

| Cifra | Valor | Origen |
|---|---|---|
| Media del Sistema A | Exponencial de 55 sesiones | EA I.1.1, p. 13 |
| Media del Sistema B | Exponencial de 20 sesiones | EA VIII.6.6, p. 217 |
| MACD | 12, 26 y 9; los mismos en el semáforo | EA IV.1, p. 101 |
| Período del ADX y de los DI | 14 | EA VIII.6.4, pp. 214-215 |
| Nivel del ADX | 30, fijo | EA VIII.6.5, p. 215; VIII.6.6, pp. 216-217 |
| ADX del Sistema B | Sobre 30 o subiendo | EA VIII.6.6, p. 217: pendiente positiva o, al menos, lecturas sobre 30. `[Elaboración]`: el script traduce la pendiente a «sube respecto a la barra anterior». Los ejemplos de esa página piden pendiente positiva y lectura sobre 30 a la vez |
| Sentido en el Sistema B | +DI sobre -DI en largo; -DI sobre +DI en corto | `[Elaboración]`: la fuente pide el ADX por encima del -DI en tendencia alcista y del +DI en bajista (EA VIII.6.6, p. 216); el script compara los dos DI para fijar el sentido |
| Predisposición del Sistema A | Cierre sobre la EMA55 con pendiente positiva o nula; en corto, bajo la media con pendiente negativa o nula | EA I.1.1, p. 14 |
| Cruce del MACD del Sistema A | Las dos líneas se cortan al alza con ambas sobre cero; en corto, a la baja con ambas bajo cero | EA I.1.1, p. 14 |
| Salida del Sistema A | Cruce del MACD en sentido contrario | EA I.1.1, p. 14 |
| Tolerancia del retroceso a la media | 0,5 × ATR | `[Propuesta]`: la fuente dice que el precio retrocede hasta la media, o la perfora ligeramente, sin cifra (EA I.1.1, p. 14; VIII.6.6, p. 217) |
| Plazo entre el retroceso y la señal | 10 barras | `[Propuesta]`: la fuente no da plazo |
| Margen del stop | 0,5 × ATR bajo la media, sobre ella en corto; alternativa, 1,0 % de la media | `[Propuesta]`: la fuente dice «ligeramente» sin cifra (EA VIII.6.6, p. 217) |
| Stop del Sistema A | Bajo la EMA55, con el mismo margen | `[Elaboración]`: para el A la fuente da la cancelación por el MACD (EA I.1.1, p. 14) y la disciplina de fijar el stop antes de entrar (p. 15); el script le aplica el tipo de stop que Cava da para el B |
| Salida del Sistema B | El cierre pierde la EMA20; en corto, la supera | `[Elaboración]`: la fuente describe la entrada y el stop de este sistema, no una regla de salida (EA VIII.6.6, pp. 216-218) |
| ATR | 14 períodos | `[Propuesta]`: unidad elegida por el script para medir la tolerancia y el margen |
| Semáforo | MACD mensual sobre su señal, MACD semanal sobre cero y %K semanal sobre 60; el espejo, con 40 | EA I.5.3, p. 37 |
| «Cortado al alza» del MACD mensual | Línea rápida sobre su línea de señal, como estado | `[Elaboración]`: la fuente pide el MACD cortado al alza; el script lo traduce a un estado medible |
| %K semanal | 14 barras, sin suavizar | EA V.1.1, p. 141 |
| Semáforo como filtro | Opcional, apagado por defecto | `[Propuesta]`: no forma parte de ninguno de los dos sistemas; aplica la subordinación de las señales a la tendencia (EA VII.3.1, pp. 187-188) |
| Pivotes visuales | 5 velas a cada lado | `[Propuesta]`: la definición de Drummond que recoge Cava usa un día a cada lado (EA I.5.4, p. 41) |
| Capital, tamaño y comisión | 10.000, 20 % del patrimonio y 0,05 % | `[Propuesta]`: valores de referencia de la cabecera del script, no de la fuente |

## Qué se ve en el gráfico

| Elemento | Qué es | Cómo leerlo |
|---|---|---|
| EMA 55 (Sistema A) | Media exponencial de 55 sesiones del cierre | Gruesa y opaca cuando se prueba el Sistema A, que es cuando interviene. Fina y tenue en el B: se dibuja y no interviene |
| EMA 20 (Sistema B) | Media exponencial de 20 sesiones del cierre | Al revés: gruesa en el Sistema B, tenue en el A |
| Stop activo | Nivel del stop fijado al entrar | Línea roja con cortes, solo con posición abierta. Queda quieta hasta cerrar |
| Semáforo I.5.3 | Fondo suave, solo con el filtro activo | Verde: tendencia alcista según I.5.3. Rojo: bajista. Gris: ni una ni otra |
| Máximo aislado (solo visual) | Triángulo rojo hacia abajo sobre la barra | Aparece sobre la vela del máximo cuando han pasado 5 velas a cada lado, así que llega con retraso. No interviene en las órdenes |
| Mínimo aislado (solo visual) | Triángulo verde hacia arriba bajo la barra | Igual, para los mínimos |
| Entradas y salidas del probador | Marcas del probador de estrategias | `Largo` y `Corto` son las entradas; `Stop L` y `Stop C`, las salidas por stop; las salidas por señal llevan el comentario «MACD corta a la baja», «MACD corta al alza», «Pierde la EMA20» o «Supera la EMA20» |

## Cómo funciona, paso a paso

1. **Media activa.** La EMA de 55 sesiones en el Sistema A y la de 20 en el B. Las reglas miden contra ella.
2. **Predisposición (solo A).** Cierre sobre la media con pendiente positiva o nula; la pendiente es la diferencia de la media con la de la barra anterior. En corto, cierre bajo la media con pendiente negativa o nula.
3. **Retroceso.** Una barra cuenta como retroceso cuando su mínimo queda en la media más la tolerancia, o por debajo; en corto, cuando su máximo queda en la media menos la tolerancia, o por encima. El script recuerda la última barra así y la da por vigente durante la ventana de 10 barras. No comprueba que el precio viniera de estar por encima de la media.
4. **Entrada del Sistema A.** En la misma barra: predisposición, retroceso vigente, cruce del MACD al alza y las dos líneas sobre cero.
5. **Entrada del Sistema B.** En la misma barra: ADX sobre 30 o subiendo respecto a la barra anterior, retroceso vigente, cierre que supera la EMA20 y +DI sobre -DI.
6. **Filtro opcional.** Con el filtro activo, la entrada larga exige el semáforo alcista y la corta, el bajista. Los datos mensuales y semanales se piden por su cuenta, sin mirar al futuro, sea cual sea el marco del gráfico.
7. **Lado corto.** Espejo de todo lo anterior, solo con «Permitir posiciones cortas» activo.
8. **Orden y stop.** La orden se procesa al cierre de la barra de la señal. Al entrar, el script fija el stop a la distancia elegida de la media activa de esa barra, bajo ella en largo y sobre ella en corto, y no lo mueve hasta cerrar.
9. **Salida.** Por el stop o por la señal contraria. En el A, las líneas del MACD se cortan en sentido contrario. En el B, el cierre pierde la EMA20 en largo, o la supera en corto.
10. **Máximos y mínimos aislados.** Se calculan con 5 velas a cada lado y solo se dibujan.

**Barra en curso.** La estrategia se calcula al cierre de cada barra, no tick a tick. El semáforo no espera al cierre de la semana ni del mes: mientras están en curso, puede cambiar en cada cierre.

## Cómo leerlo en situaciones concretas

| Lectura | Significa | Qué no significa |
|---|---|---|
| `Largo` del Sistema A | Hubo un retroceso a la EMA55 en las últimas 10 barras y el MACD se cortó al alza sobre cero, con el cierre sobre una media que no baja (EA I.1.1, p. 14) | Que la tendencia dominante sea alcista: eso solo lo comprueba el semáforo si se activa el filtro |
| `Largo` del Sistema B | El precio retrocedió a la EMA20 y la volvió a superar, con el ADX sobre 30 o subiendo (EA VIII.6.6, p. 217) | Una señal confirmada: Cava considera muy conveniente que el MACD y el estocástico acompañen (EA VIII.6.6, p. 217) y el script no lo comprueba |
| `MACD corta a la baja` | Cancelación de la posición larga por la regla del Sistema A (EA I.1.1, p. 14) | Un stop: la orden de cierre sale con el cruce, a cualquier distancia del nivel del stop |
| `Pierde la EMA20` | Cierre de la posición larga del Sistema B porque el cierre queda bajo la media | Una regla de Cava: la fuente no recoge una salida para este sistema (EA VIII.6.6, pp. 216-218) `[Elaboración]` |
| `Stop L` o `Stop C` | El precio llegó al nivel fijado al entrar | Un stop que sigue a la media: se fija una vez y no se mueve |
| Fondo verde o rojo con el filtro activo | Semáforo alcista o bajista según I.5.3 (EA I.5.3, p. 37) | Una señal de entrada: solo condiciona las que generen los sistemas |
| Pocas operaciones | Una ventana corta, una tolerancia pequeña o el filtro limitan las entradas | Que el sistema falle: con pocas operaciones el resultado no se puede generalizar `[Elaboración]` |
| Sistema A y Sistema B sobre el mismo valor | Dos traducciones de dos reglas distintas, con el mismo capital y los mismos costes | Que uno sea mejor que el otro en general: depende del valor, del período y de las cifras propias `[Elaboración]` |

## Cuándo usarlo y cuándo no

- **Sí:** para ver, sobre un valor y en diario, cómo se habrían comportado las dos reglas de Cava con una traducción explícita y con costes; para comparar el A y el B con el mismo capital y la misma comisión; para medir el efecto del semáforo como filtro de cada uno. Los dos sistemas están formulados en diario (EA I.1.1, pp. 13-14; VIII.6.6, p. 217).
- **No:** como prueba de que el método de Cava funciona, porque la traducción lleva cifras propias; en otro marco que el diario, porque la fuente formula los dos sistemas en diario; con el ADX cayendo bajo 30, porque la fuente avisa de que los sistemas seguidores de tendencia dan entonces señales menos provechosas y más falsas (EA VIII.6.6, p. 217). El Sistema B no entra en ese caso; el A no mira el ADX.
- **Mal uso frecuente** `[Elaboración]`: comparar los dos sistemas con costes o tamaños distintos; dar por concluyente un resultado con pocas operaciones; olvidar que el capital, el tamaño y la comisión están en las propiedades de la estrategia y no en los ajustes del script; activar el filtro y atribuir su efecto al sistema.

## Qué NO dice

- La fuente no da cifra para «hasta la media» ni plazo entre el retroceso y la señal: la tolerancia de 0,5 × ATR y la ventana de 10 barras son `[Propuesta]`.
- No fija la distancia del stop: dice «ligeramente» (EA VIII.6.6, p. 217). El margen de 0,5 × ATR, o de 1,0 %, es `[Propuesta]`.
- Para el Sistema A no da un stop bajo la media de 55 sesiones, sino la cancelación por el MACD (EA I.1.1, p. 14) y la disciplina de fijar el stop antes de entrar (p. 15): el script le aplica el tipo de stop del B `[Elaboración]`.
- Para el Sistema B describe la entrada y el stop, no una salida (EA VIII.6.6, pp. 216-218): la salida por pérdida de la EMA20 es `[Elaboración]`.
- No fija el capital, el tamaño de la posición ni la comisión: son valores de referencia del script.
- Aplicar el semáforo como filtro de estos dos sistemas es del script, `[Propuesta]`: Cava subordina las señales al sentido de la tendencia (EA VII.3.1, pp. 187-188) y define esa tendencia con el semáforo (EA I.5.3, p. 37).
- Reglas de la fuente que el script no implementa. `[Hueco declarado]`
  - Sistema B: que en el momento de la señal la línea rápida del MACD esté girada al alza y el estocástico cortado al alza, o a la baja en corto (EA VIII.6.6, pp. 217-218).
  - Sistema B: que el ADX esté por encima del -DI en tendencia alcista y del +DI en bajista (EA VIII.6.6, p. 216); el script compara los dos DI entre sí.

---

## Marcas de procedencia

Sin marca = regla de Cava con capítulo y página · `[Propuesta]` = cuantificación propia · `[Aportado]` = de terceros · `[Elaboración]` = extensión editorial · `[Hueco declarado]` = la fuente lo tiene y el código no.

## Control de cambios

| Versión | Fecha | Cambios |
|---|---|---|
| 0.1.0.0 | 2026-11-15 | Primer borrador |
| 0.2.0.0 | 2026-11-21 | Adaptada a la plantilla estándar y al código 0.1.2.0. Citas contrastadas con EA (pp. 13-16, 19, 37, 41-42, 101, 141, 187-188, 214-218) |
| 0.3.0.0 | 2026-11-22 | Alineada con el código 0.3.0.0: versión del script y título (sin «(Cava)») |
