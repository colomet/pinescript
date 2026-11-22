# [JLC71 Management] Stops: support / EMA20 / MACD invalidation · Guía técnica

Qué es el script, qué dice la fuente y cómo se lee lo que dibuja. La configuración, en la guía operativa.

| Campo | Valor |
|---|---|
| Procedencia | JLC (tres reglas de stop según Cava, capítulos I y VIII de *El arte de especular*; en adelante EA) |
| Script | Versión 0.3.0.0 (ver control de cambios) |

---

## Qué es

Calcula, en cada barra, a qué precio quedaría el stop de una posición larga según dos reglas de Cava, y avisa cuando el cierre lo pierde. Regla A: bajo el último soporte. Regla B: bajo la media exponencial de 20 sesiones. Añade una tercera, la Regla C, que no es un precio sino una señal de cierre: el cruce a la baja de las líneas del MACD en diario. Se dibuja sobre el precio. Con el lado corto activado calcula también el espejo para posiciones cortas.

Según la cabecera del script, se consulta antes de entrar: la distancia entre el precio y el stop decide si el riesgo de esa entrada encaja con el tamaño de la posición. No sabe si hay una posición abierta ni a qué precio se entró, y no coloca ni mueve órdenes: el nivel lo traslada quien lo usa.

## Qué dice la fuente

- **Normas del sistema (EA I.2.1, pp. 24-25):** un sistema de especulación es el conjunto de normas que se van a seguir; entre ellas, las de colocar el primer stop y las de moverlo según el precio (p. 24). La pérdida máxima potencial debería quedar limitada por el stop (p. 25).
- **Stop fijado antes de entrar (EA I.1.1, pp. 15, 16 y 19):** tras abrir una posición el precio suele ir en contra o quedarse parado; entonces hay que confiar en el sistema y colocar el stop de cancelación con los criterios fijados de antemano (p. 15). Mientras el precio se mantenga por encima del nivel donde las reglas del sistema situarían el stop, la posición se mantiene hasta que el sistema dé la señal de cancelación, y no se cancela por la sensación de haberse equivocado (p. 16). Las reglas para colocar el stop son parte esencial del sistema (p. 19).
- **Regla A, bajo el soporte (EA I.5.4, pp. 39-40):** en tendencia alcista se compra en los retrocesos hacia zonas de soporte, con el stop ligeramente por debajo del soporte, que es el mínimo de la onda C; en tendencia bajista se vende en el rebote cerca de zonas de resistencia, con el stop ligeramente por encima (p. 40). Si el soporte no resulta perforado en el retroceso, se compra con el stop ligeramente por debajo de él (p. 39). Cava advierte del inconveniente: se puede entrar justo cuando la tendencia se agota, y por eso conviene colocar los stops en un sitio adecuado y ejecutarlos si llega la ocasión; entrar en sobreventa dentro de una tendencia alcista deja margen para cancelar con pérdidas reducidas (p. 40).
- **Máximos y mínimos aislados (EA I.5.4, pp. 41-42):** Cava toma de Drummond la definición: un día marca un máximo aislado cuando su máximo queda por encima de los del día anterior y del posterior, y un mínimo aislado cuando su mínimo queda por debajo de los del día anterior y del posterior; el del día intermedio es una zona de resistencia o de soporte significativa (p. 41). Pueden influir en el futuro porque representan zonas de resistencia y de soporte (p. 42).
- **Regla B, bajo la media de 20 sesiones (EA VIII.6.6, pp. 217-218):** Cava recoge que muchos especuladores usan el retroceso a la media exponencial de 20 sesiones para incorporarse a la tendencia cuando el ADX tiene pendiente positiva o, al menos, lecturas por encima de 30, con un stop de protección ligeramente por encima o por debajo de la media, en el sentido de la tendencia (p. 217). En tendencia alcista: cuando, tras el retroceso, el precio gira al alza y vuelve a superar la media, posición larga con el stop por debajo de la media; le parece buena señal y sería muy conveniente que la línea rápida del MACD estuviera girada al alza y el estocástico cortado al alza (p. 217). El caso bajista es el espejo, con el stop por encima de la media (p. 217) y la confirmación con el MACD y el estocástico a la baja (p. 218).
- **Regla C, cancelación por MACD (EA I.1.1, pp. 13-14):** el sistema sencillo de Cava sobre el NASDAQ 100 usa la media exponencial diaria de 55 sesiones (p. 13) y el MACD en diario (p. 14). En largo: el precio sobre la media, con pendiente positiva o plana; compra cuando retrocede hasta la media y a continuación las dos líneas del MACD se cortan al alza por encima de cero. La posición larga se cancela cuando las líneas del MACD en diario se cortan a la baja, es decir, cuando la línea continua corta a la baja a la discontinua (p. 14). En corto, el espejo: la cancelación llega cuando las líneas se cortan al alza (p. 14).
- **MACD (EA IV.1, p. 101):** las líneas se calculan habitualmente con 12 y 26 períodos, y la de señal es una media exponencial de 9 períodos de la línea continua; cada persona puede usar otros períodos.
- **«Ligeramente» sin cifra (EA I.5.4, p. 40; VIII.6.6, p. 217):** Cava no cuantifica el margen en las dos reglas de precio.

**Cifras del script y su origen**

| Cifra | Valor | Origen |
|---|---|---|
| Soporte de la Regla A | Último mínimo aislado confirmado | `[Elaboración]`: la fuente habla del soporte y del mínimo de la onda C (EA I.5.4, p. 40) y define el mínimo aislado en la p. 41; usarlo como soporte de la regla es una aproximación del script |
| Pivote | 5 velas a la izquierda y 5 a la derecha | `[Propuesta]`: la definición de Drummond que recoge Cava usa un día a cada lado (EA I.5.4, p. 41) |
| Margen de la Regla A | 0,3 × ATR (alternativa: 0,5 % del soporte) | `[Propuesta]`: Cava dice «ligeramente por debajo» sin cifra (EA I.5.4, p. 40) |
| Media de la Regla B | EMA de 20 sesiones | EA VIII.6.6, p. 217 |
| Margen de la Regla B | 0,5 × ATR (alternativa: 1,0 % de la media) | `[Propuesta]`: Cava dice «ligeramente» sin cifra (EA VIII.6.6, p. 217). El 0,5 coincide con el margen por defecto de `JLC91 Systems` |
| ATR | 14 períodos, común a A y B | `[Propuesta]`: unidad elegida por el script para medir el margen |
| MACD de la Regla C | 12, 26 y 9 | EA IV.1, p. 101 |
| Cancelación de la Regla C | Cruce a la baja de las líneas del MACD | EA I.1.1, p. 14 |
| Lado corto | Apagado por defecto; espejo de A, B y C | EA I.5.4, p. 40 (A), VIII.6.6, pp. 217-218 (B) e I.1.1, p. 14 (C) |
| Detección del toque | El cierre cruza la línea del stop: a la baja en largos, al alza en cortos | `[Elaboración]`: la fuente pide ejecutar el stop si llega la ocasión (EA I.5.4, p. 40) y no define el cruce del cierre |

## Qué se ve en el gráfico

| Elemento | Qué es | Cómo leerlo |
|---|---|---|
| Línea roja (Stop A) | Último soporte menos el margen | Se mueve a saltos: solo cuando se confirma un mínimo aislado nuevo. Entre pivotes queda plana |
| Línea roja tenue (Stop A corto) | Última resistencia más el margen | Solo con el lado corto |
| Línea naranja (Stop B) | La media menos el margen | Se recalcula en cada barra: sube con la media y también baja con ella |
| Línea naranja tenue (Stop B corto) | La media más el margen | Solo con el lado corto |
| Línea gris muy tenue | La media exponencial de referencia | Sigue el período de la Regla B, aunque se llame «EMA20» |
| Triángulo verde tenue bajo la barra | Se confirma un soporte nuevo | Aparece tantas barras después del mínimo como velas a la derecha se hayan fijado; no se dibuja sobre el propio mínimo |
| Triángulo rojo tenue sobre la barra | Se confirma una resistencia nueva | Solo con el lado corto |
| Aspa roja sobre la barra | STOP TOCADO (largo) | El cierre cruza a la baja el stop A o el stop B |
| Aspa roja bajo la barra | STOP TOCADO (corto) | El cierre cruza al alza el stop A o el stop B del lado corto |
| Fondo rojo suave | Invalidación MACD (largo) | Las líneas del MACD se cortan a la baja: cierre por señal, sin nivel de precio |
| Fondo verde suave | Invalidación MACD (corto) | Las líneas del MACD se cortan al alza. Solo con el lado corto |

## Cómo funciona, paso a paso

1. **ATR.** Calcula el ATR del período fijado (14), común a las reglas A y B.
2. **Regla A.** Detecta mínimos aislados y máximos aislados con `ta.pivotlow` y `ta.pivothigh` y las velas fijadas a cada lado; guarda el último mínimo como soporte y el último máximo como resistencia. `[Elaboración]` El margen es un múltiplo del ATR o un porcentaje del último soporte. `[Propuesta]` Stop largo = soporte − margen; stop corto = resistencia + margen. Mientras no se confirma un pivote nuevo, el nivel no cambia.
3. **Regla B.** Calcula la EMA del cierre y le resta el margen, múltiplo del ATR o porcentaje de la media `[Propuesta]`. En corto, se lo suma. Se recalcula en cada barra.
4. **Regla C.** Calcula el MACD del cierre con 12, 26 y 9. La invalidación larga es el cruce a la baja de la línea del MACD bajo la de señal; la corta, el cruce al alza. No hay nivel de precio: solo la marca de fondo y la alerta.
5. **Stop tocado.** Marca el cruce del cierre con la línea del stop A o del B: a la baja en largos y, solo con el lado corto, al alza en cortos. Necesita que el stop exista. `[Elaboración]`
6. **Alertas.** Seis: stop A, stop B e invalidación por MACD, cada una en su versión larga y corta.
7. **Barra en curso.** El código no espera al cierre de la barra: una marca puede aparecer y desaparecer mientras se forma y queda fija al cierre.

## Cómo leerlo en situaciones concretas

| Lectura | Significa | Qué no significa |
|---|---|---|
| Línea roja plana durante muchas barras | El último soporte confirmado sigue vigente | Que no haya aparecido un soporte nuevo: se confirma varias barras después del mínimo |
| Línea naranja que sube con la media | El stop B acompaña a la media (EA VIII.6.6, p. 217) | Un stop que solo sube: si la media baja, baja con ella |
| Distancia grande entre el precio y la línea | Más riesgo en dinero en esa entrada concreta | Una entrada peor por sí sola: pide ajustar el tamaño de la posición |
| Aspa roja sobre la barra | El cierre ha cruzado a la baja el stop A o el stop B | Una orden ejecutada: el script no coloca órdenes |
| Precio por debajo de la línea sin aspa | Ya estaba por debajo o el cruce fue en una barra anterior | Que el stop siga sin perderse: el script marca el cruce, no el estado |
| Fondo rojo suave | Las líneas del MACD se cortan a la baja: cierre por señal de la Regla C (EA I.1.1, p. 14) | Un nivel de precio donde poner el stop |
| Línea roja por encima del precio | El último soporte confirmado quedó por encima del precio y aún no hay uno nuevo | Un stop útil para una posición abierta ahora |

## Cuándo usarlo y cuándo no

- **Sí:** antes de entrar, para ver a qué distancia quedaría el stop de cada regla y decidir si el riesgo encaja con el tamaño de la posición; y durante la posición, para seguir el nivel de cada regla y recibir los avisos. Con las reglas B y C en diario (EA VIII.6.6, p. 217; I.1.1, p. 14).
- **No:** como sustituto de la orden de stop en el bróker; como señal de entrada, porque no dice cuándo entrar; cuando importe el precio de entrada, que el script no conoce.
- **Mal uso frecuente** `[Elaboración]`: decidir el stop cuando la posición ya va perdiendo, cuando Cava pide fijarlo de antemano (EA I.1.1, p. 15); cancelar la posición por intuición en vez de por la regla del stop (EA I.1.1, p. 16); mirar el nivel y no la distancia al precio.

## Qué NO dice

- No sabe si hay posición abierta ni a qué precio se entró; no coloca ni mueve órdenes.
- No dice cuánto es «ligeramente»: los márgenes son `[Propuesta]`.
- No indica cuándo entrar: no comprueba tendencia, retroceso, ADX ni confirmaciones.
- Reglas de la fuente que el script no implementa. `[Hueco declarado]`
  - Condiciones de entrada de la Regla A: tendencia alcista o bajista definida y retroceso hacia la zona de soporte o de resistencia (EA I.5.4, pp. 38-40).
  - Condiciones de la Regla B: ADX con pendiente positiva o por encima de 30, y confirmación con la línea rápida del MACD girada y el estocástico cortado (EA VIII.6.6, pp. 217-218).
  - Entrada del sistema de la media de 55 sesiones: precio sobre la media con pendiente positiva o plana, retroceso a la media y cruce del MACD al alza por encima de cero, con el espejo bajista (EA I.1.1, p. 14). La Regla C solo implementa la cancelación.
  - Stop ligeramente por debajo de los mínimos del proceso correctivo, con el espejo en el rebote, en el sistema con RSI y MACD (EA Cap. VI, p. 178).

---

## Marcas de procedencia

Sin marca = regla de Cava con capítulo y página · `[Propuesta]` = cuantificación propia · `[Aportado]` = de terceros · `[Elaboración]` = extensión editorial · `[Hueco declarado]` = la fuente lo tiene y el código no.

## Control de cambios

| Versión | Fecha | Cambios |
|---|---|---|
| 0.1.0.0 | 2026-11-15 | Primer borrador |
| 0.2.0.0 | 2026-11-21 | Adaptada a la plantilla estándar y al código 0.1.1.0. Citas contrastadas con EA (pp. 13-16, 19, 24-25, 38-42, 101, 178, 217-218) |
| 0.3.0.0 | 2026-11-22 | Alineada con el código 0.3.0.0: versión del script y título (sin «(Cava)») |
