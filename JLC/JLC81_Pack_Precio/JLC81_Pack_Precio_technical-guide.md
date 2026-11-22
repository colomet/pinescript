# [JLC81 Pack] Price: moving averages + displaced averages + pivots · Guía técnica

Qué es el script, qué dice la fuente y cómo se lee lo que dibuja. La configuración, en la guía operativa.

| Campo | Valor |
|---|---|
| Procedencia | JLC (medias, medias desplazadas y máximos y mínimos aislados según Cava, capítulos I y VIII de *El arte de especular*; en adelante EA). La EMA 50 y la SMMA 150 son de terceros, `[Aportado]` |
| Script | Versión 0.3.0.0 (ver control de cambios) |

---

## Qué es

Agrupa en un solo indicador, sobre el precio: la EMA 20 y la EMA 55, las tres medias desplazadas 3x3, 7x5 y 25x5, y los máximos y mínimos aislados con sus líneas proyectadas. Trae además, apagadas por defecto, una EMA 50 y una SMMA 150 que no son de Cava. Todo se activa por separado. Calcula también el criterio de tendencia por medias desplazadas (el precio sobre las tres o bajo las tres), que puede pintar el fondo y avisar. No incluye el ADX ni dibuja stops.

## Qué dice la fuente

- **EMA 20 (EA VIII.6.6, pp. 217-218):** Cava recoge que muchos especuladores usan el retroceso a la media exponencial diaria de 20 sesiones para incorporarse a la tendencia cuando el ADX tiene pendiente positiva o, al menos, lecturas por encima de 30, con un stop de protección ligeramente por encima o por debajo de la media (p. 217). En tendencia alcista: cuando, tras el retroceso, el precio gira al alza y vuelve a superar la media, posición larga con el stop por debajo de ella; le parece buena señal y sería muy conveniente que la línea rápida del MACD estuviera girada al alza y el estocástico cortado al alza (p. 217). El caso bajista es el espejo (pp. 217-218).
- **EMA 55 (EA I.1.1, pp. 13-14):** el sistema sencillo de Cava sobre el NASDAQ 100 se basa en la media exponencial diaria de 55 sesiones, número de la serie de Fibonacci (p. 13). Con el precio por encima de la media y pendiente positiva o plana, predisposición alcista; por debajo y con pendiente negativa o plana, predisposición bajista (p. 14). En su ejemplo, el precio del NASDAQ 100 fluctúa por encima de la media de 55 sesiones, que actúa de soporte (EA I.5.4, p. 38).
- **Medias desplazadas (EA I.5.2, pp. 36-37):** algunos autores, entre los que Cava destaca a Joe DiNapoli, definen la tendencia con medias desplazadas: alcista cuando el precio se coloca por encima de la media desplazada y bajista cuando está por debajo (p. 36). Las tres más utilizadas son la media simple de 3 períodos desplazada 3 hacia delante (3x3), la de 7 desplazada 5 (7x5) y la de 25 desplazada 5 (25x5); se pueden usar en diario, semanal y mensual, e incluso en intradiario (p. 36). La 3x3 y la 7x5 se suelen aplicar a gráficos semanales y diarios (p. 37). En opinión de Cava, el criterio funciona bien con tendencia fuerte, pero da numerosas señales falsas cerca de su conclusión o cuando el precio queda atrapado en un lateral amplio, con pauta plana o triángulo (p. 37).
- **Máximos y mínimos aislados (EA I.5.4, pp. 41-42):** Cava toma de Drummond la definición: un día marca un máximo aislado cuando su máximo queda por encima de los del día anterior y del posterior, y un mínimo aislado cuando su mínimo queda por debajo de los del día anterior y del posterior; el del día intermedio es una zona de resistencia o de soporte significativa (p. 41). Pueden influir en el futuro porque representan zonas de resistencia y de soporte (p. 42).
- **EMA 50 y SMMA 150:** según la cabecera del script, no proceden de Cava. La SMMA 150 viene de un criterio externo de salida, cuando el precio corta la media, de un vídeo de Goat Academy; de la EMA 50 la cabecera dice que no tiene fuente confirmada. El script las marca `[Aportado]`.

**Cifras del script y su origen**

| Cifra | Valor | Origen |
|---|---|---|
| EMA 20 | 20 sesiones | EA VIII.6.6, p. 217 |
| EMA 55 | 55 sesiones, sobre el cierre | EA I.1.1, p. 13 |
| Desplazadas | SMA 3 desplazada 3, SMA 7 desplazada 5, SMA 25 desplazada 5 | EA I.5.2, p. 36 |
| Criterio de cada desplazada | Precio por encima = alcista; por debajo = bajista | EA I.5.2, p. 36 |
| Precio de cálculo de las medias | Cierre | `[Elaboración]`: la fuente lo precisa solo para la EMA 55 |
| Criterio de las tres a la vez | Alcista si el precio está sobre las tres; bajista si está bajo las tres; sin criterio si discrepan | `[Elaboración]`: la fuente aplica el criterio a cada media por separado (EA I.5.2, p. 36) |
| Máximo o mínimo aislado | Pivote de 5 velas a cada lado | `[Propuesta]`: la definición de Drummond que recoge Cava usa un día a cada lado (EA I.5.4, p. 41) |
| Líneas proyectadas | Una por tipo, desde el último pivote hacia la derecha | `[Elaboración]`: la fuente habla de zonas de resistencia y de soporte (EA I.5.4, pp. 41-42) |
| EMA 50 | 50 sesiones | `[Aportado]` |
| SMMA 150 | Media de Wilder (RMA) de 150 | `[Aportado]` |

## Qué se ve en el gráfico

| Elemento | Qué es | Cómo leerlo |
|---|---|---|
| Línea azul gruesa | EMA 20 | Referencia de los retrocesos en tendencia fuerte (EA VIII.6.6, p. 217) |
| Línea verde azulada gruesa | EMA 55 | Con el precio por encima y pendiente positiva o plana, predisposición alcista (EA I.1.1, p. 14) |
| Línea naranja fina | SMA 3x3 | Media de 3 períodos desplazada 3 hacia delante |
| Línea amarilla fina | SMA 7x5 | Media de 7 períodos desplazada 5 hacia delante |
| Línea marrón fina | SMA 25x5 | Media de 25 períodos desplazada 5 hacia delante |
| Fondo verde o rojo muy suave | Criterio de las tres desplazadas | Verde: precio sobre las tres. Rojo: bajo las tres. Sin color: discrepan. Solo si se activa |
| Triángulo rojo sobre la barra | Máximo aislado | Zona de resistencia candidata (EA I.5.4, pp. 41-42) |
| Triángulo verde bajo la barra | Mínimo aislado | Zona de soporte candidata (EA I.5.4, pp. 41-42) |
| Línea roja o verde discontinua a la derecha | Nivel del último máximo o del último mínimo aislado | Solo queda la última de cada tipo |
| Línea gris o violeta fina | EMA 50 o SMMA 150 | Piezas `[Aportado]`, apagadas por defecto |

## Cómo funciona, paso a paso

1. **Medias.** Calcula con `ta.ema` sobre el cierre la EMA 20, la EMA 55 y la EMA 50, y con `ta.rma` la SMMA 150 (la media de Wilder).
2. **Desplazadas.** Calcula tres `ta.sma` del cierre, de 3, 7 y 25 períodos, y las dibuja con el desplazamiento del propio trazado, 3, 5 y 5 barras hacia delante. El cálculo no se desplaza: por eso los últimos tramos caen sobre barras que aún no existen.
3. **Criterio.** Compara el cierre con el valor que cada media desplazada muestra hoy, el que se calculó hace tantas barras como su desplazamiento. Si el cierre queda sobre las tres, todas alcistas; si queda bajo las tres, todas bajistas; si discrepan, sin criterio. `[Elaboración]`
4. **Fondo.** Con el ajuste activado, verde si las tres son alcistas y rojo si las tres son bajistas.
5. **Aislados.** Detecta máximos y mínimos con `ta.pivothigh` y `ta.pivotlow` y las velas fijadas a cada lado. El pivote se confirma tantas barras después como velas a la derecha; el triángulo se dibuja retrasado esas barras, sobre el propio pivote. `[Propuesta]`
6. **Líneas.** Desde cada pivote nuevo dibuja una línea discontinua que se extiende a la derecha y borra la anterior del mismo tipo. `[Elaboración]`
7. **Alertas.** Cinco: el cierre cruza la EMA 20 al alza o a la baja, el cierre cruza la EMA 55 a la baja, y las tres desplazadas pasan a alcistas o a bajistas. Se calculan siempre, estén o no visibles las líneas.
8. **Barra en curso.** El código no espera al cierre de la barra: una marca puede aparecer y desaparecer mientras se forma y queda fija al cierre.

## Cómo leerlo en situaciones concretas

| Lectura | Significa | Qué no significa |
|---|---|---|
| Fondo verde: precio sobre las tres desplazadas | Tendencia alcista según el criterio de las medias desplazadas (EA I.5.2, p. 36) | Una señal de compra: Cava avisa de numerosas señales falsas cerca del final de la tendencia o en un lateral amplio (EA I.5.2, p. 37) |
| Fondo rojo: precio bajo las tres desplazadas | Tendencia bajista según ese criterio (EA I.5.2, p. 36) | Una señal de venta, por la misma razón |
| Sin fondo con las desplazadas activas | Las tres desplazadas discrepan: el precio está entre ellas | Una lectura de Cava: es del script `[Elaboración]` |
| Alerta `Precio · recupera la EMA20` | El cierre vuelve a superar la media de 20 sesiones: primer paso de la regla de EA VIII.6.6 | La entrada completa: falta el ADX con pendiente positiva o sobre 30, el MACD girado y el estocástico cortado (p. 217), que el indicador no calcula |
| Alerta `Precio · pierde la EMA55` | El precio deja de estar sobre la media de la predisposición alcista (EA I.1.1, p. 14) | Un cambio de tendencia: la predisposición también depende de la pendiente de la media (p. 14) |
| Triángulo y línea discontinua | Máximo o mínimo aislado: zona de resistencia o de soporte candidata (EA I.5.4, pp. 41-42) | Un nivel definido como lo define Cava: Cava usa un día a cada lado y el script, 5 por defecto |
| Línea gris o violeta | EMA 50 o SMMA 150, activadas a propósito | Reglas de Cava |

## Cuándo usarlo y cuándo no

- **Sí:** para ver en un solo indicador los criterios de precio de Cava, con tendencia fuerte; la EMA 20 como referencia de retroceso cuando el ADX acompaña (EA VIII.6.6, p. 217); las desplazadas 3x3 y 7x5 en semanal y diario (EA I.5.2, p. 37).
- **No:** con el precio atrapado en un lateral amplio o cerca del final de la tendencia, donde las desplazadas dan numerosas señales falsas (EA I.5.2, p. 37); como entrada completa de la regla de la EMA 20 sin mirar el ADX; tratando la EMA 50 o la SMMA 150 como reglas de Cava.
- **Mal uso frecuente** `[Elaboración]`: leer una media desplazada como previsión del precio, cuando es una media pasada dibujada más a la derecha; operar el cruce del precio con una desplazada sin mirar la fuerza de la tendencia (EA I.5.2, p. 37).

## Qué NO dice

- No incluye el ADX, el MACD ni el estocástico, que condicionan la regla de la EMA 20 (EA VIII.6.6, p. 217). El ADX lo calcula `JLC51 ADX`.
- No dibuja stops: Cava dice «ligeramente» y no da cifra (EA VIII.6.6, p. 217). Los stops, en `JLC71 Stops`.
- La EMA 50 y la SMMA 150 no tienen fuente en Cava, según la cabecera del script.
- Reglas de la fuente que el script no implementa. `[Hueco declarado]`
  - Condiciones de la regla de la EMA 20: ADX con pendiente positiva o por encima de 30, MACD girado al alza y estocástico cortado al alza (EA VIII.6.6, p. 217), y sus espejos (p. 218).
  - Pendiente de la EMA 55 en la predisposición alcista o bajista (EA I.1.1, p. 14).
  - Confirmación del máximo o del mínimo aislado cuando el mercado se mantiene tres días por debajo o por encima de su nivel (EA I.5.4, p. 41).

---

## Marcas de procedencia

Sin marca = regla de Cava con capítulo y página · `[Propuesta]` = cuantificación propia · `[Aportado]` = de terceros · `[Elaboración]` = extensión editorial · `[Hueco declarado]` = la fuente lo tiene y el código no.

## Control de cambios

| Versión | Fecha | Cambios |
|---|---|---|
| 0.1.0.0 | 2026-11-15 | Primer borrador |
| 0.2.0.0 | 2026-11-21 | Adaptada a la plantilla estándar y al código 0.1.2.0. Citas contrastadas con EA (pp. 13-14, 36-38, 41-42, 217-218) |
| 0.3.0.0 | 2026-11-22 | Alineada con el código 0.3.0.0: versión del script y título (sin «(Cava)») |
