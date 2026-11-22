# [GEN41 Trend] Long-term linear regression channel (300 bars) {1 sigma / 90-95-99 % dispersion} (okhanLAB) · Guía técnica

Qué es el script, qué dice la fuente y cómo se lee lo que dibuja. La configuración, en la guía operativa.

| Campo | Valor |
|---|---|
| Procedencia | GEN. Original de okhanLAB, «Linear Regression Channel - Auto Volume Based» (nombre corto LinRegAuto), que a su vez es una versión modificada del Linear Regression Channel de TradingView. Este script es una modificación de ese original. No es de Cava: según la cabecera del script, no hay capítulo ni página que citar. Las cifras del original son `[Aportado]` y el resto del diseño es `[Propuesta]` |
| Script | Versión 1.6.2.0 (ver control de cambios) |

---

## Qué es

La recta de mínimos cuadrados que mejor encaja con los cierres de un tramo, con dos pares de bandas paralelas: una a 1 sigma y otra, exterior, al 90, 95 o 99 % (95 % de serie). De serie el tramo son las últimas 300 barras, termina en el último cierre semanal y las líneas se prolongan una semana más. Con *Inicio = Automático* el tramo puede arrancar en la vela de más volumen de una ventana, y con *Inicio = Fecha*, donde se elija. Se dibuja sobre el precio y solo en la última barra: no deja rastro en el histórico. Usa siempre el cierre.

En el repositorio es de la familia 4, Rector: «¿Hay tendencia y hacia dónde?». El título en TradingView la llama Trend. Define seis alertas, que solo funcionan con *Final = Hoy* e *Inicio* distinto de *Fecha*.

## Qué dice la fuente

No es de Cava. Según la cabecera del script, el origen es el indicador de okhanLAB y no hay capítulo ni página que citar `[Aportado]`. Lo que sigue es lo que hace el original y lo que cambia este script.

- **El original** `[Aportado]`: según su cabecera, es una versión modificada del Linear Regression Channel de TradingView; su diferencia principal es que el largo ya no es fijo, sino que se ajusta a la acción reciente del precio, determinada por la vela de más volumen de las últimas 300 barras. Dibuja la recta de mínimos cuadrados de los cierres con bandas a 1 y a 2 sigmas y una etiqueta con la R de Pearson y el largo. Si la vela de más volumen está a 70 barras o más y a menos de 300, traza el canal desde ella; si no, conserva el último largo válido. Después compara ese canal con el de 70 barras y dibuja el de mayor R. Sus cifras son 70 (largo mínimo) y 300 (largo máximo).
- **Lo que conserva este script** `[Aportado]`: el cálculo de la recta de mínimos cuadrados y de la R de Pearson, la banda a 1 sigma y el criterio de dibujar el canal de mayor R entre el automático y el de largo mínimo.
- **Lo que cambia** `[Propuesta]`: el largo fijo de 300 barras de serie, con el automático como opción; la ventana de volumen de 600 y la mínima de 300, en lugar de 300 y 70; la banda exterior al 90, 95 o 99 % en lugar de 2 sigmas fijas; la sigma con divisor «barras menos 2» en lugar de «barras menos 1»; el final elegible (último cierre semanal, hoy o fecha fija), con el canal calculado con los datos hasta ese final; el inicio por fecha; las dos salidas para la vela «muy reciente» (el original conserva el último largo válido); la proyección de una semana; el panel de texto en lugar de la etiqueta; las marcas y la zona de búsqueda; el aviso de ventana que mezcla regímenes; el modo verificación; las seis alertas; y el cálculo siempre sobre el cierre, sin elegir la fuente de precio.

Los valores del original, 70 y 300, se pueden poner a mano en *Longitud mínima* y *Ventana de volumen*.

**Cifras del script y su origen**

| Cifra | Valor | Origen |
|---|---|---|
| Longitud mínima de serie | 300 barras (de 3 a 1000) | `[Propuesta]`. El original usa 70 de mínima y 300 de máxima `[Aportado]` |
| Ventana de volumen de serie | 600 barras (de 5 a 1000) | `[Propuesta]`. Es el doble de la mínima de serie: con *Automático* deja una zona de búsqueda de 300 barras |
| Banda interior | 1 sigma | `[Aportado]`: el original también la dibuja a 1 sigma |
| Banda exterior | 90, 95 o 99 % (95 % de serie), a 1,6449 · 1,9600 · 2,5758 sigmas | Los niveles son `[Propuesta]`. Los multiplicadores son los cuantiles de la distribución normal para esos niveles, calculados. El original dibuja 2 sigmas fijas `[Aportado]` |
| Sigma | Raíz de la suma de los cuadrados de las distancias de los cierres a la recta, dividida entre el número de barras menos 2 | `[Propuesta]`. El original divide entre el número de barras menos 1 `[Aportado]` |
| R de Pearson | De 0 a 1 | `[Aportado]`: se calcula como en el original |
| Elección entre canal automático y fijo | El de mayor R | `[Aportado]`: es el criterio del original |
| Aviso de mezcla de regímenes | Dos mitades sin solape, de 3 barras como mínimo cada una (6 en total) | `[Propuesta]` |
| Proyección | Una semana: la mayor, en barras, de las tres últimas semanas completas, con un máximo de 400 | `[Propuesta]` |
| Alcance hacia atrás | Las barras entre hoy y el final del canal, más el largo del canal (con *Automático*, la ventana de volumen), no pueden pasar de 4.900 | Del script (historial máximo de 5.000 barras). Si se pasa, el panel avisa de que el rango queda fuera del historial disponible |

## Qué se ve en el gráfico

| Elemento | Qué es | Cómo leerlo |
|---|---|---|
| Recta central (marrón) | La recta de mínimos cuadrados de los cierres del tramo | Su inclinación da el sentido de la tendencia media del tramo |
| Banda interior (1σ) | Dos líneas a 1 sigma de la recta | La distancia típica de los cierres a la recta. Si los cierres se repartieran como una normal, quedarían dentro unos 2 de cada 3 (68 %) `[Elaboración]` |
| Banda exterior (90, 95 o 99 %) | Dos líneas a 1,6449, 1,9600 o 2,5758 sigmas de la recta, según el nivel | El límite de lo habitual en el tramo. Salir de ella es salir de lo habitual para ese tramo, no una señal de giro |
| Proyección | Las cinco líneas, prolongadas una semana más allá del final del canal con la misma pendiente | No usa datos nuevos: prolonga la recta y las bandas. No es una previsión. Con *Extender líneas a la derecha* se prolongan sin límite |
| Extremo izquierdo de las líneas | La primera barra del canal | Con *Fijo*, la primera de las últimas N barras (N = la mínima); con *Automático*, la barra siguiente a la vela de más volumen si gana el canal automático y, si gana el fijo, la primera de las últimas N barras; con *Fecha*, la primera barra con fecha igual o posterior a la elegida |
| Raya vertical punteada de inicio (naranja o gris) | Dónde empieza el cálculo. Va entre las dos bandas interiores | Naranja: gana el canal automático y arranca en la vela de más volumen. Gris: el canal es el de la mínima (*Fijo*, o *Automático* cuando gana el fijo). No hay raya con *Inicio = Fecha* |
| Raya vertical punteada azul | Dónde termina el cálculo | Solo con *Final = Último cierre semanal* y cuando ya hay barras posteriores. Se quita con el mismo ajuste que la raya de inicio |
| Zona gris con borde punteado | La zona de búsqueda de la vela de más volumen | Solo con *Inicio = Automático*. Cubre las barras más antiguas que el canal fijo, hasta el límite de la ventana de volumen: el borde izquierdo es la barra más antigua de la ventana y el derecho, la barra anterior al canal fijo. Su altura va del máximo al mínimo de esas barras |
| ▼ naranja o gris sobre una vela | La vela de más volumen de la ventana | Naranja si gana el canal automático, gris si no. Con el ratón encima dice su fecha, hace cuántas barras fue y qué se hizo con ella: «usada como inicio», «muy reciente: se usa el canal de la mínima», «el canal fijo es más recto» o «el automático coincide con el fijo». Si el canal es el automático, arranca en la barra siguiente a esta vela |
| ◆ gris sobre una vela | La vela de más volumen de todas, cuando es «muy reciente» y no se usa como inicio | Solo con *Buscar la mayor anterior a la mínima*: la ▼ pasa entonces a la mayor anterior a la mínima y la ◆ marca la más reciente. Con el ratón encima dice hace cuántas barras fue y que no se usa como inicio |
| Panel | Tabla de texto de hasta cinco filas | *Inicio*, *Búsqueda* y *Final* (las tres juntas), *Resultado* y *Avisos* (solo si hay algo que avisar). Cómo se lee cada una, en la guía operativa |
| Marcas de las fechas | Una por cada ajuste de fecha, con un cuadrado azul abajo. No las dibuja el script: las pone TradingView al seleccionar el indicador | Arrastrarlas cambia el ajuste de fecha. Solo cuentan con *Inicio = Fecha* y *Final = Fecha fija* |

## Cómo funciona, paso a paso

1. **Final.** Fija la barra donde termina el canal: con *Último cierre semanal*, la última barra de la última semana completa (si la semana ya cerró, la última barra); con *Hoy*, la última barra; con *Fecha fija*, la última barra con fecha igual o anterior a la elegida. El canal se calcula solo con los cierres hasta esa barra.
2. **Largo.** Con *Fijo*, las últimas *Longitud mínima* barras hasta el final. Con *Fecha*, desde la primera barra con fecha igual o posterior a la elegida hasta el final. Con *Automático*, busca la vela de más volumen entre las últimas *Ventana de volumen* barras; la idea, ajustar el largo a la acción reciente del precio mediante la vela de más volumen, es del original `[Aportado]`. Si esa vela está a menos barras que la mínima es «muy reciente»: un canal desde ella sería más corto que el mínimo, y el script usa el canal de la mínima o, con la otra opción, busca la vela de más volumen entre las barras más antiguas que la mínima `[Propuesta]`. Si no es reciente, el canal automático va desde la barra siguiente a esa vela hasta el final. Si el símbolo no tiene volumen, usa el largo fijo y lo avisa.
3. **Recta, sigma y R.** La recta se ajusta por mínimos cuadrados a los cierres del tramo, con el número de barra como eje horizontal. La sigma es la raíz de la suma de los cuadrados de las distancias de cada cierre a la recta, dividida entre el número de barras menos 2 `[Propuesta]`. R es la correlación entre los cierres y la recta: va de 0 a 1 y no lleva signo; el sentido del tramo está en la pendiente.
4. **Elección.** Con *Automático*, calcula también el canal fijo y dibuja el de mayor R; si los dos largos coinciden o no hay volumen, dibuja el fijo. El criterio es el del original `[Aportado]`.
5. **Bandas.** La interior, a 1 sigma de la recta; la exterior, a z sigmas, con z = 1,6449 (90 %), 1,9600 (95 %) o 2,5758 (99 %). Todo se calcula sobre el cierre.
6. **Proyección.** Prolonga las cinco líneas una semana más allá del final del canal, con la misma pendiente y sin datos nuevos. La semana son las barras de las últimas semanas completas: se toma la mayor de las tres últimas, con un máximo de 400 `[Propuesta]`. Con un marco mayor que el semanal, la «semana» es una barra.
7. **Mezcla de regímenes.** Parte el canal dibujado en dos mitades con el mismo número de barras y sin solape (con un número impar queda fuera la barra central) y compara si la recta de cada mitad sube o baja. Si van en sentidos contrarios y el ajuste está activo, añade un aviso al panel `[Propuesta]`. Solo informa: no entra en las bandas ni en las alertas. No se evalúa con menos de 6 barras.
8. **Panel.** Escribe las filas con lo que ha decidido en los pasos anteriores y, en *Avisos*, los ⚠ que correspondan.
9. **Alertas.** Solo con *Final = Hoy*, con *Inicio* distinto de *Fecha* y solo en la última barra. Para distinguir salir de estar fuera, calcula también el canal que había con la barra anterior como final, con la misma regla. *Sale por arriba (por abajo)*: el cierre de hoy supera la banda exterior (queda por debajo de ella) y el de la barra anterior no estaba fuera de la banda de su propio canal. *Vuelve desde arriba (desde abajo)*: el de la barra anterior estaba fuera de la banda de su canal y el de hoy ya está dentro de la banda de hoy. *Cruza la recta central hacia arriba (hacia abajo)*: el cierre de la barra anterior estaba por debajo (por encima) de la recta de su canal y el de hoy está en la recta de hoy o por encima (o por debajo). Ninguna es regla de Cava `[Propuesta]`.
10. **Verificación.** Con el modo activado, publica los valores del canal en la ventana de datos, solo en la última barra.

**Qué se calcula con qué.** Hay dos zonas con dos propósitos. La zona de cálculo va de la primera barra del canal al final: con esas barras se calculan la recta y la sigma, y las líneas empiezan ahí. La zona de búsqueda de volumen es la sombreada: solo decide dónde empieza el canal y no entra en la recta ni en la sigma. Si la vela de más volumen cae dentro y el canal desde ella sale más recto que el fijo, el canal arranca en la barra siguiente a esa vela; si no, el canal fijo empieza una barra después del borde derecho de la zona. Por eso, con el canal fijo, solo cuentan las barras de la mínima, aunque la ventana sea mayor.

## Cómo leerlo en situaciones concretas

| Lectura | Significa | Qué no significa |
|---|---|---|
| El precio se mueve dentro de las bandas y la recta tiene una pendiente clara | Tendencia ordenada en el tramo | Una señal: es el estado normal del canal |
| El precio sale por la banda exterior | Un movimiento fuera de lo habitual para ese tramo | Una señal de giro: puede acelerar o agotarse |
| Con *Automático*, la fila *Búsqueda* dice «muy reciente» | Ha entrado una vela de mucho volumen hace poco y el script usa el canal de la mínima en lugar de anclarse en ella | Un fallo: es la regla del script para las velas demasiado recientes |
| R cerca de 1 | Los cierres del tramo siguen casi una recta | Que el precio vaya a seguir esa recta |
| R bajo, cerca de 0 | El tramo casi no tiene tendencia lineal | Que el precio vaya a quedarse quieto |
| `precio` en el panel cerca de ±1,64, ±1,96 o ±2,58 | El cierre del final del canal está en el borde de la banda exterior del 90, 95 o 99 % | Un aviso de giro |
| Con el final congelado, `hoy` en el panel | Dónde está el último precio respecto a la recta prolongada del canal de un día pasado | Una señal, ni una previsión de hacia dónde irá |
| El panel avisa de historial corto | El activo tiene menos barras que las pedidas: el canal es más corto de lo pedido y se apoya en menos datos `[Elaboración]` | Un canal tan largo como el que se pidió |
| El panel avisa de que la ventana mezcla regímenes | La recta del canal resume dos tramos que iban en sentidos contrarios | Una razón para operar o no: es un dato, no una señal |
| El panel dice que una fecha no tiene efecto | Se movió una fecha y el modo elegido no la usa: se ignora | Un fallo del canal: no lo afecta |

## Cuándo usarlo y cuándo no

- **Sí:** para ver de un vistazo hacia dónde va el último tramo y cuánto se dispersa el precio a su alrededor; para mirar el canal una vez por semana con el final de serie; para comparar lo ocurrido después con el canal de un día pasado (*Final = Fecha fija*).
- **No:** como previsión. Según la ayuda del script, hacia delante la banda del 95 % contiene solo unos 3 de cada 4 cierres de la semana siguiente `[Propuesta]`; salir de la banda no implica que el precio vaya a girar ni a seguir. Tampoco para decidir una entrada o una salida con una sola lectura del canal.
- **Sin volumen real** (índices, ratios): con *Inicio = Automático* usa el canal fijo y lo avisa; con *Fijo* o *Fecha* funciona igual que con volumen.
- **Mal uso frecuente** `[Elaboración]`: tomar la proyección de una semana por una previsión; tomar la banda del 95 % por un límite que el precio no puede superar; tomar el aviso de mezcla o el `hoy` del panel por una señal; creer que el canal automático acierta más que el fijo.

## Qué NO dice

- No predice. La proyección de una semana prolonga la recta y las bandas con la misma pendiente, sin datos nuevos; no dice que el precio vaya a seguirlas.
- No comprueba que el 90, el 95 o el 99 % de los cierres del tramo quede dentro de la banda exterior: esos niveles son los de una distribución normal. Tampoco comprueba que los cierres se repartan así `[Elaboración]`.
- No mide si el canal automático acierta más que el fijo: es una forma de elegir desde dónde mirar. Solo compara sus R.
- El aviso de mezcla no sirve para decidir: no dice si el canal es mejor o peor ni qué hará el precio.
- El `hoy` del panel dice dónde está el precio respecto a un canal congelado, no hacia dónde irá.
- No da entradas ni salidas. Las seis alertas describen dónde está el precio respecto al tramo ya pasado.
- No deja elegir la fuente de precio, a diferencia del original: usa siempre el cierre.
- `[Hueco declarado]` Con menos de 3 barras de historial no se dibuja el canal.

---

## Marcas de procedencia

Sin marca = regla de Cava con capítulo y página · `[Propuesta]` = cuantificación propia · `[Aportado]` = de terceros · `[Elaboración]` = extensión editorial · `[Hueco declarado]` = la fuente lo tiene y el código no.

## Control de cambios

| Versión | Fecha | Cambios |
|---|---|---|
| 0.1.0.0 | 2026-11-21 | Creación, a partir del contenido técnico de la guía de uso anterior (0.21.0.0), para el código 1.6.2.0. Contrastada con el código y con el script original de okhanLAB |
