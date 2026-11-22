# [GEN41 Trend] Long-term linear regression channel (300 bars) {1 sigma / 90-95-99 % dispersion} (okhanLAB) · Guía operativa

Cómo se añade y se ajusta. Qué dice la fuente y cómo se lee, en la guía técnica.

| Campo | Valor |
|---|---|
| Título en TradingView | `[GEN41 Trend] Long-term linear regression channel (300 bars) {1 sigma / 90-95-99 % dispersion} (okhanLAB)` |
| Nombre corto | `GEN41 LinReg channel` |
| Script | Versión 1.6.2.0 (ver control de cambios) |

---

## Cómo se añade

1. Abre el gráfico del activo, en el marco con el que operes.
2. En Indicadores, busca el título o el nombre corto y añádelo.
3. Se dibuja sobre el precio, sin panel propio: cinco líneas (la recta central y dos pares de bandas) y una tabla de texto, arriba a la derecha de serie.
4. De serie dibuja un canal fijo de 300 barras que termina en el último cierre semanal, con las líneas proyectadas una semana más. Solo se dibuja en la última barra: no deja rastro en el histórico. Usa siempre el cierre.

### Uso rápido

- **De serie:** *Inicio del canal = Fijo (longitud mínima)* y *Final del canal = Último cierre semanal*: canal fijo de 300 barras hasta el último cierre semanal, con las líneas proyectadas hasta el viernes próximo. En semanal son unos 6 años; en diario, unos 14 meses.
- **Otro largo:** cambia *Longitud mínima (barras)*. El mismo número de barras es más tiempo en semanal que en diario; el panel dice cuánto abarca el canal.
- **Que se recalcule con cada dato, y tener alertas:** *Final del canal = Hoy*. Es el único final con alertas.
- **Comparar lo ocurrido después con el canal de un día pasado:** *Final del canal = Fecha fija*, con *Extender líneas a la derecha* activado.
- **Ver desde qué vela de volumen parte el movimiento:** *Inicio del canal = Automático (vela de más volumen)*.
- **Dónde mirar las fechas:** la tabla de texto (el panel) tiene una fila por cada cosa: *Inicio*, *Búsqueda*, *Final*, *Resultado* y, si hace falta, *Avisos*. Es el mismo orden que los ajustes.
- **Ayuda:** cada ajuste lleva una explicación al pasar el ratón (tooltip), y el grupo «8 · Acerca de este indicador» trae un resumen de solo lectura.
- **Qué no es:** una previsión. La banda describe el tramo pasado y la proyección solo prolonga la recta (ver la guía técnica).

## Ajustes

Ocho grupos numerados, en el orden del panel: inicio, búsqueda, final y banda; después visualización, verificación, colores y un resumen de solo lectura. Las dos fechas y los ajustes «Zona de búsqueda de volumen» y «Marca de la vela de más volumen» se atenúan cuando el modo elegido no los usa. El resto de ajustes que dependen del inicio dicen «solo con…» en su ayuda y se ignoran fuera de él. No hay ajuste de fuente de precio: el canal se calcula siempre sobre el cierre.

### 1 · Inicio del canal

| Ajuste | Por defecto | Qué hace | Cuándo tocarlo |
|---|---|---|---|
| Inicio del canal | Fijo (longitud mínima) | Desde dónde empieza el canal. *Fijo (longitud mínima)*: las últimas N barras de la *Longitud mínima*, sin buscar velas de volumen. *Automático (vela de más volumen)*: busca la vela de más volumen de la ventana y dibuja el más recto entre el canal desde ella y el fijo. *Fecha*: la recta arranca en la primera barra con fecha igual o posterior a *Fecha de inicio*; no se elige entre automático y fijo y no hay alertas | *Automático*, para ver desde qué vela de volumen parte el movimiento. *Fecha*, para anclar en un suceso que eliges tú |
| Fecha de inicio | 2026-01-01 | Solo con *Inicio del canal = Fecha*. Si es posterior a la fecha final, o deja menos de 3 barras, el panel avisa y no se dibuja el canal. Con otro inicio se atenúa y se ignora | Solo con *Fecha*. También se cambia arrastrando su marca en el gráfico (ver «Colores y marcas») |
| Longitud mínima (barras) | 300 | Largo del canal en barras, de 3 a 1000. Con *Fijo* el canal usa siempre las últimas N barras: pon N aquí. Con *Automático* es el largo mínimo y el límite para considerar «muy reciente» la vela de volumen. No se usa con *Fecha* | Súbela para una tendencia más larga y estable (el precio sale menos de las bandas); bájala para que reaccione antes, con más ruido |

### 2 · Búsqueda de la vela de volumen (solo con Inicio = Automático)

| Ajuste | Por defecto | Qué hace | Cuándo tocarlo |
|---|---|---|---|
| Ventana de volumen (barras) | 600 | Solo con *Automático*. Hasta cuántas barras atrás busca la vela de más volumen, de 5 a 1000; es también el límite del largo del canal automático. La zona de búsqueda va de ahí hasta la barra de la *Longitud mínima*. Debe ser mayor que la mínima: si no lo es, el script baja la mínima a «ventana menos 1» y lo avisa en el panel | Súbela para anclarse en sucesos más antiguos (el canal sale más largo); bájala para mirar solo lo reciente |
| Si la vela más fuerte es muy reciente | Usar el canal de la mínima | Solo con *Automático*. La vela de más volumen es «muy reciente» si está a menos barras que la *Longitud mínima*: un canal desde ella sería demasiado corto. *Usar el canal de la mínima*: se ignora esa vela y se dibuja el canal de la *Longitud mínima*. *Buscar la mayor anterior a la mínima*: se busca otra vela de más volumen, más antigua, en la zona sombreada, y se dibuja el más recto entre el canal desde ella y el de la mínima | *Buscar la mayor anterior a la mínima*, si quieres ver desde qué suceso importante parte el movimiento. Con ventana = mínima + 1 solo hay una barra donde buscar y el canal dibujado es el mismo con las dos opciones |

### 3 · Final del canal

| Ajuste | Por defecto | Qué hace | Cuándo tocarlo |
|---|---|---|---|
| Final del canal | Último cierre semanal | Dónde termina el canal. *Último cierre semanal*: la última barra de la última semana completa; no cambia hasta que cierre la siguiente, y si la semana ya cerró (fin de semana) termina en la última barra. No da alertas; el panel dice a cuántas sigmas está hoy el precio. *Hoy*: la última barra; se recalcula con cada dato y es el único final con alertas. *Fecha fija*: la última barra con fecha igual o anterior a *Fecha final* | *Hoy*, para que se recalcule y para tener alertas. *Fecha fija*, para comprobar después lo ocurrido con el canal de un día pasado |
| Fecha final | 2026-10-15 | Solo con *Final del canal = Fecha fija*. El canal se calcula con los datos hasta ese día. Con otro final se atenúa y se ignora | Solo con *Fecha fija*. También se cambia arrastrando su marca en el gráfico |

### 4 · Banda de dispersión

| Ajuste | Por defecto | Qué hace | Cuándo tocarlo |
|---|---|---|---|
| Nivel de la banda exterior | 95 % | 90 %, 95 % o 99 %: el porcentaje de cierres del tramo que, según el script, quedan dentro de la banda exterior. Fija a cuántas sigmas está (1,6449 · 1,9600 · 2,5758). La banda interior (1σ) no cambia | Con más nivel, la banda es más ancha y salta menos la alerta de salida |

### 5 · Visualización

| Ajuste | Por defecto | Qué hace | Cuándo tocarlo |
|---|---|---|---|
| Mostrar el resultado en el panel (R · tiempo · banda) | Sí | Muestra u oculta la fila *Resultado* del panel: R, lo que abarca el canal, el nivel de la banda, `precio` y `hoy`. Los avisos salen siempre | — |
| Mostrar inicio, búsqueda y final en el panel | Sí | Muestra u oculta las tres primeras filas del panel | Desactívalas si el panel te ocupa mucho |
| Posición del panel | Arriba derecha | Esquina del gráfico donde va el panel entero: arriba o abajo, a la izquierda o a la derecha | Cámbiala si tapa las velas o la barra de dibujo de TradingView |
| Marcas de inicio y final del canal | Sí | Rayas verticales punteadas entre las dos bandas interiores: la de inicio (naranja o gris) y la de final (azul, solo con *Último cierre semanal* y cuando hay barras posteriores) | Desactívalas si molestan. Los colores se cambian en «7 · Colores» |
| Zona de búsqueda de volumen | Sí | Solo con *Automático*. Sombrea las barras donde busca la vela de más volumen, con borde punteado | Desactívala si molesta |
| Marca de la vela de más volumen | Sí | Solo con *Automático*. Dibuja ▼ y ◆ sobre las velas de más volumen; con el ratón encima explican qué son | Desactívala si molesta |
| Extender líneas a la izquierda | No | Prolonga las cinco líneas hacia el pasado, sin límite. No cambia el cálculo | Para ver el canal sobre más historia |
| Extender líneas a la derecha | No | Prolonga las cinco líneas hacia el futuro, sin límite. Con *Proyectar las líneas una semana más* ya llegan al viernes próximo; esto las alarga más | Con el final congelado (*Fecha fija*), para ver el precio posterior sobre el canal. No son un límite hacia el futuro |
| Avisar si la ventana mezcla regímenes | Sí | Añade al panel una línea ⚠ si la primera mitad del canal sube y la segunda baja, o al revés. Es solo un dato: no cambia el canal, las bandas ni las alertas | Desactívalo si no te aporta |
| Proyectar las líneas una semana más | Sí | Prolonga las cinco líneas una semana más allá del final del canal, con la misma pendiente. No usa datos nuevos y no es una previsión | Desactívalo si no quieres ver la proyección. No cambia el cálculo ni las alertas |

### 6 · Verificación

| Ajuste | Por defecto | Qué hace | Cuándo tocarlo |
|---|---|---|---|
| Modo verificación (ventana de datos) | Sí | Publica en la ventana de datos (barra lateral derecha) los campos de la tabla siguiente, solo en la última barra. No dibuja nada ni cambia el cálculo | Desactívalo si no vas a comprobar nada |

Campos que publica, para comparar el canal con una referencia externa:

| Campo | Qué es | Decimales |
|---|---|---|
| V · longitud del canal (barras) | Barras del canal dibujado | 0 |
| V · modo (0 mín, 1 auto, 2 manual) | 0 = canal fijo o de la mínima; 1 = automático; 2 = fecha | 0 |
| V · R de Pearson | Lo recto que es el tramo, de 0 a 1 | 3 |
| V · sigma del canal (precio) | Dispersión, en unidades de precio | 2 |
| V · pendiente (precio por barra) | Inclinación de la recta, en precio por barra | 3 |
| V · posición del precio en sigma, al final del canal | A cuántas sigmas de la recta cierra la barra final. Es el `precio` del panel | 2 |
| V · posición de hoy sobre el canal proyectado, en sigma | Solo con *Último cierre semanal* o *Fecha fija*: dónde está el precio de hoy respecto a la recta prolongada. Es el `hoy` del panel | 2 |
| V · recta al final del canal | Precio de la recta en la barra final | 2 |
| V · banda exterior superior al final | Precio de la banda exterior superior en la barra final | 2 |
| V · banda exterior inferior al final | Precio de la banda exterior inferior en la barra final | 2 |
| V · longitud automática candidata | La longitud que habría salido en modo automático | 0 |
| V · pico de volumen reciente (1 sí) | 1 si la vela de más volumen es «muy reciente» | 0 |
| V · hay volumen (1 sí) | 1 si el símbolo tiene volumen | 0 |

### 7 · Colores

| Ajuste | Por defecto | Qué hace | Cuándo tocarlo |
|---|---|---|---|
| Recta central | #915500 (marrón), transparencia 60 % | Color de la recta central | Rara vez |
| Banda 1σ | #2196F3 (azul), transparencia 85 % | Color de las dos líneas a 1 sigma. También es el color del texto del panel, sin transparencia | Rara vez |
| Banda exterior | #2196F3 (azul), transparencia 70 % | Color de las dos líneas de la banda exterior y de la raya de final | Rara vez |
| Marca de inicio: modo auto | #FF9800 (naranja), transparencia 20 % | Color de la raya de inicio y del ▼ cuando el canal arranca en la vela de más volumen | Rara vez |
| Marca de inicio: modo mín y fijo | #787B86 (gris), transparencia 20 % | Color de la raya de inicio del canal fijo, de los ▼ y ◆ grises y de la zona de búsqueda (borde y relleno suave) | Rara vez |

### 8 · Acerca de este indicador

Trae un resumen de solo lectura, la «Ficha»: no se puede cambiar.

### Cómo se combinan Longitud mínima y Ventana de volumen

Esto vale para *Inicio del canal = Automático*. Con *Fijo* solo cuenta la mínima. Los dos ajustes son barras: la **ventana** es hasta dónde mira el script hacia atrás para buscar la vela de más volumen, y la **mínima** es lo corto que puede ser el canal y también el canal de reserva. La mínima es un solo ajuste: la misma cifra es el largo del canal fijo y el mínimo del automático.

El script hace esto, en orden:

1. Busca la vela de más volumen dentro de la ventana.
2. Si está a menos barras que la mínima (es muy reciente), no se fía y dibuja el canal de la mínima.
3. Si está más lejos, traza el canal desde la barra siguiente a esa vela hasta el final: el automático, que mide entre la mínima y la ventana.
4. Compara el automático con el fijo y dibuja el más recto.

La ventana debe ser mayor que la mínima. La de serie es 600, el doble de la mínima: al cambiar a *Automático* hay una zona de búsqueda de 300 barras.

| Mínima · Ventana | Qué pasa con *Inicio del canal = Automático* |
|---|---|
| 300 · 600 (por defecto) | Mira las últimas 600 barras. Si la vela de más volumen está a menos de 300, canal de 300. Si no, canal desde esa vela (de 300 a 599 barras), el más recto de los dos |
| 70 · 300 (los del original) | Mira las últimas 300 barras. Si la vela de más volumen está a menos de 70, canal de 70. Si no, canal desde esa vela (de 70 a 299 barras), el más recto de los dos |
| 10 · 500 | Mira muy atrás, pero el canal fijo es muy corto: 10 barras. El automático puede medir hasta 499 |
| 500 · 600 | Canal largo: fijo de 500 barras o automático de 500 a 599 |
| 500 · 10 | Mínima mayor que la ventana: se ajusta la mínima a 9 y el panel dice «Mín ≥ ventana: Mín ajustado a 9». Sale un canal de 9 barras |
| 150 · 151 | La ventana deja 1 barra de margen: no hay nada que buscar. Canal de 150 barras, siempre. Con *Fijo* y mínima 150 sale lo mismo |

### Las nueve combinaciones de final e inicio

| Final | Inicio | Qué dibuja |
|---|---|---|
| Último cierre semanal | Fijo | El canal fijo de la longitud mínima en el último cierre semanal. **Es el valor de serie.** Sin alertas |
| Último cierre semanal | Automático | El canal que habría salido en el último cierre semanal, con la longitud que habría elegido entonces. Sin alertas |
| Último cierre semanal | Fecha | Una recta entre la fecha elegida y el último cierre semanal. Sin alertas |
| Hoy | Fijo | El canal fijo de la longitud mínima, recalculado con cada dato. Con alertas |
| Hoy | Automático | El canal desde la vela de más volumen o el fijo, el más recto, recalculado con cada dato. Con alertas |
| Hoy | Fecha | Una recta desde la fecha elegida hasta hoy. Sin alertas |
| Fecha fija | Fijo | El canal fijo de la longitud mínima tal como estaba ese día. Sin alertas |
| Fecha fija | Automático | El canal que habría salido ese día, con la longitud que habría elegido entonces. Sin alertas |
| Fecha fija | Fecha | Una recta entre las dos fechas. Sin alertas |

### Receta: canal fijo de N barras

Pon *Inicio del canal* = **Fijo (longitud mínima)** y *Longitud mínima (barras)* = N. Es el valor de serie, con N = 300. Con N = 150 sale un canal fijo de 150 barras, unos 7 meses en diario.

Cómo comprobarlo en el gráfico, con *Final del canal = Hoy* (con el final semanal, el canal acaba en el último cierre y la cuenta cambia en las barras de esta semana):

- **Panel, fila *Inicio*:** `Fijo · desde AAAA-MM-DD · 150 barras`.
- **Panel, fila *Búsqueda*:** `no hay: el canal es fijo`.
- **Raya punteada gris:** está en esa barra de inicio. No hay triángulos ni zona sombreada.
- **Ventana de datos:** *V · longitud del canal (barras)* = 150 y *V · modo (0 mín, 1 auto, 2 manual)* = 0.
- **Cuenta:** desde la raya hasta la última barra hay 150 barras.

## Equivalencia en tiempo

Son barras, no días. Con unas 21 sesiones por mes:

| Ajuste | Valor | En diario | En semanal |
|---|---|---|---|
| Longitud mínima (barras) | 300 (de serie) | unos 14 meses | unos 6 años |
| Longitud mínima (barras) | 150 (ejemplo) | unos 7 meses | unos 3 años |
| Ventana de volumen (barras) | 600 (de serie) | unos 28 meses | unos 11,5 años |
| Mínima · ventana del original | 70 · 300 | algo más de 3 meses · unos 14 meses | unos 16 meses · unos 6 años |
| Proyección de las líneas | una semana | 5 barras en acciones, 7 en cripto | 1 barra |

Para abarcar el mismo tiempo en semanal que en diario hacen falta unas 5 veces menos barras: 300 diarias son unas 60 semanales. Al cambiar de marco temporal cambian las fechas, no las barras. El panel da el tiempo real que abarca el canal (fila *Resultado*, «abarca ≈»).

## Colores y marcas

| Elemento | Color o forma | Qué indica |
|---|---|---|
| Recta central | Línea marrón | La tendencia media del tramo: su inclinación da el sentido |
| Banda interior (1σ) | Dos líneas azules claras | La distancia típica de los cierres a la recta |
| Banda exterior (90, 95 o 99 %) | Dos líneas azules más marcadas | El límite de lo habitual en el tramo, según el nivel elegido |
| Proyección | Las cinco líneas, más allá del final del canal | Con *Proyectar las líneas una semana más*, siguen una semana con la misma pendiente: con *Último cierre semanal*, hasta el viernes próximo. No usa datos nuevos |
| Raya de inicio | Vertical punteada, entre las dos bandas interiores: naranja o gris | Dónde empieza el cálculo. Naranja: el canal arranca en la vela de más volumen. Gris: es el canal fijo. No se dibuja con *Inicio del canal = Fecha* |
| Raya de final | Vertical punteada azul, entre las dos bandas interiores | Dónde termina el cálculo. Solo con *Último cierre semanal* y cuando ya hay barras posteriores |
| Zona de búsqueda | Rectángulo gris con borde punteado | Las barras donde se busca la vela de más volumen: el borde izquierdo es donde empieza la búsqueda y el derecho donde acaba. Solo con *Automático*. Una vela que caiga hacia hoy, fuera de la zona, es «muy reciente» |
| ▼ naranja o gris | Triángulo sobre una vela | La vela de más volumen de la ventana. Naranja: el canal arranca en ella (en la barra siguiente). Gris: no se usa. Con el ratón encima dice cuándo fue y por qué |
| ◆ gris | Rombo sobre una vela | La más fuerte de todas, descartada por reciente. Solo con *Buscar la mayor anterior a la mínima*. Con el ratón encima dice hace cuántas barras fue |
| Marcas de las fechas | Línea vertical con un cuadrado azul abajo, una por cada ajuste de fecha | Aparecen al seleccionar el indicador en el gráfico; al arrastrarlas cambia la fecha del ajuste. Solo se usan con *Inicio del canal = Fecha* y *Final del canal = Fecha fija* |
| Panel | Tabla de texto azul, arriba a la derecha de serie | Cinco filas (ver «El panel») |

### Qué verás según lo que elijas

| Si eliges… | Qué aparece en el gráfico | Dónde está cada fecha clave |
|---|---|---|
| *Inicio = Fijo* (de serie) | Raya punteada gris donde empieza el canal. Sin zona sombreada ni triángulos | Inicio: la raya gris y la fila *Inicio*. Búsqueda: no hay |
| *Inicio = Automático*, y el canal arranca en la vela de más volumen | Zona gris con borde punteado, ▼ naranja sobre esa vela y raya punteada naranja donde empieza el canal | Búsqueda: los bordes de la zona. Inicio: la raya naranja |
| *Inicio = Automático*, y gana el canal fijo | Zona gris, ▼ gris sobre la vela de más volumen, que no se usa, y raya gris donde empieza el canal fijo | Búsqueda: los bordes de la zona. Vela candidata: el ▼ gris. Inicio: la raya gris |
| *Automático*, vela «muy reciente» y *Usar el canal de la mínima* | Zona gris, ▼ gris sobre la vela reciente (fuera de la zona, hacia hoy) y raya gris | Igual que arriba. La fila *Búsqueda* dice «muy reciente: se usa el canal de la mínima» |
| *Automático*, vela «muy reciente» y *Buscar la mayor anterior a la mínima* | Zona gris, ▼ sobre la vela elegida dentro de la zona (naranja si el canal arranca en ella, gris si no) y ◆ gris sobre la más fuerte, que es reciente | La fila *Búsqueda* nombra las dos velas y sus fechas |
| *Inicio = Fecha* | Sin raya de inicio ni zona. La marca arrastrable de *Fecha de inicio* | Inicio: la marca de la fecha y la fila *Inicio* |
| *Final = Último cierre semanal* (de serie) | Raya punteada azul donde termina el canal; las líneas siguen hasta el viernes próximo | Final: la raya azul y la fila *Final* |
| *Final = Hoy* | Sin raya de final: el canal llega a la última barra. Las líneas siguen una semana | Final: la última barra |
| *Final = Fecha fija* | La marca arrastrable de *Fecha final* | Final: la marca de la fecha y la fila *Final* |

### El panel

| Fila | Qué dice |
|---|---|
| *Inicio* | Cómo empieza el canal, desde qué fecha y cuántas barras: `Fijo · desde AAAA-MM-DD · N barras`. La fecha es la de la primera barra del canal: con *Automático*, la barra siguiente a la vela de más volumen |
| *Búsqueda* | Con *Automático*, las fechas de los bordes de la zona de búsqueda, la vela de más volumen (fecha y hace cuántas barras) y qué ha pasado con ella. Con *Fijo* o *Fecha*, que no hay búsqueda |
| *Final* | Cómo termina, en qué fecha y cuánta proyección: `Último cierre semanal · AAAA-MM-DD · proyección de N barras` |
| *Resultado* | `R 0.957 · abarca ≈ 14 meses · banda 95 % · precio +0.35σ · hoy +1.8σ`. **R:** 1 = precios casi en línea recta, 0 = sin tendencia. **abarca:** el tiempo que cubre el canal. **banda:** el nivel de la banda exterior. **precio:** a cuántas sigmas de la recta cierra la última barra del canal; cerca de ±2 es el borde de la banda del 95 %. **hoy:** solo con el final congelado, a cuántas sigmas de la recta prolongada está el último precio |
| *Avisos* | Los ⚠. Va al final para que las otras filas no se muevan cuando aparece un aviso, y se muestra siempre, aunque ocultes las demás |

### Avisos del panel

| Aviso | Qué significa |
|---|---|
| Sin volumen: longitud fija | El símbolo no tiene volumen: con *Automático* el canal es siempre el fijo. No sale con *Fijo* ni con *Fecha* |
| Mín ≥ ventana: Mín ajustado a N | La mínima era igual o mayor que la ventana y se ha ajustado a ventana menos 1. Solo con *Automático* |
| Historial corto: canal de N barras en vez de M | Hay menos barras que la longitud pedida: el canal se ha recortado a las que hay |
| Historial corto: canal automático de N barras en vez de M | Lo mismo, con el canal automático |
| Menos de 3 barras de historial: no se dibuja el canal | No hay barras suficientes |
| Inicio anterior al primer dato: empieza en la primera barra | La fecha de inicio es anterior a los datos |
| Fecha final anterior al primer dato · Fecha de inicio posterior al último dato · Menos de 3 barras entre inicio y final | El rango elegido no es válido: no se dibuja el canal |
| Sin semana completa en el historial | Con *Último cierre semanal*, el historial aún no tiene una semana completa: no se dibuja el canal |
| Rango fuera del historial disponible | El rango pedido supera las 4.900 barras atrás |
| Fecha final sin efecto: Final no es Fecha fija · Fecha de inicio sin efecto: Inicio no es Fecha | Has movido una de las dos fechas y el modo elegido no la usa: se ignora. Solo sale si la fecha es distinta de la de serie |
| Ventana que mezcla regímenes (solo informativo) | La primera mitad del canal y la segunda tienen pendiente de signo contrario. Es un dato, no una señal |
| No se puede dibujar el canal | Aparece sola o con alguno de los avisos anteriores cuando no hay canal que dibujar |

## Alertas

Hay seis, y todas se evalúan solo en la última barra. **Solo funcionan con Final del canal = Hoy e Inicio del canal distinto de Fecha.** Con el valor de serie, *Último cierre semanal*, no hay alertas: para tenerlas, cambia *Final del canal* a *Hoy* antes de crearlas. Se alerta el cambio, no el estado. Los nombres son los que ves en el gestor de alertas de TradingView.

| Alerta | Salta cuando |
|---|---|
| `44 LinReg · sale por encima de la banda exterior` | El cierre de hoy está por encima de la banda exterior y el de la barra anterior no estaba por encima de la banda exterior de su propio canal. Salta al salir, no mientras sigue fuera |
| `44 LinReg · sale por debajo de la banda exterior` | Igual, por abajo |
| `44 LinReg · vuelve a la banda desde arriba` | La barra anterior cerró por encima de la banda exterior de su canal y hoy cierra en la banda exterior superior o por debajo de ella |
| `44 LinReg · vuelve a la banda desde abajo` | Igual, desde abajo |
| `44 LinReg · cruza la recta central hacia arriba` | El cierre pasa de debajo a encima de la recta central entre la barra anterior y hoy |
| `44 LinReg · cruza la recta central hacia abajo` | Igual, de encima a debajo |

- **Salida:** avisa de la barra en que el precio sale de la banda exterior, no de las siguientes mientras sigue fuera.
- **Vuelta a la banda:** da el momento en que el precio vuelve a lo habitual tras una salida.
- **Cruce de la recta:** salta en cada cruce, no solo tras salir de la banda. Con un canal corto o con el precio moviéndose junto a la recta puede saltar a menudo. Si lo que quieres es el cruce tras una salida, mira antes el panel: dice a cuántas sigmas está el precio.
- Las seis son de diseño propio del script `[Propuesta]`, no reglas de Cava. Ninguna es una previsión: describen dónde está el precio respecto al tramo ya pasado, y sus mensajes incluyen «Dispersión, no previsión».

Para crearlas: en el gestor de alertas de TradingView, condición este indicador (`GEN41 LinReg channel`) y, de la lista, una de las seis por su nombre. Las condiciones usan el cierre, y en la barra abierta el cierre es el precio del momento: con la frecuencia «Una vez por cierre de barra» («Once Per Bar Close») la alerta espera al cierre de la barra `[Elaboración]`.

## Marcos temporales

Funciona en cualquier marco: el canal cuenta barras del marco del gráfico (ver «Equivalencia en tiempo»). Con *Final del canal = Último cierre semanal*, la semana es la de calendario si el marco es de una semana o menos; con un marco mayor, la «semana» es una barra. La proyección de una semana mide, en barras, la mayor de las tres últimas semanas completas, con un máximo de 400 barras: si una semana tiene más de 400 barras, la proyección se queda en 400.

---

## Control de cambios

| Versión | Fecha | Cambios |
|---|---|---|
| 0.1.0.0 | 2026-10-27 | Creación, sobre el código 1.1.0.1 |
| 0.2.0.0 | 2026-10-31 | Se refiere al código 1.3.0.1. Recoge lo que antes iba en la cabecera del script y añade fechas manuales, avisos y modo verificación. Sustituye a la 0.1.0.0 |
| 0.3.0.0 | 2026-10-31 | Se refiere al código 1.3.0.1. Un dato, un sitio: sin cifras de evidencia ni número de versión del script fuera de este control de cambios |
| 0.4.0.0 | 2026-11-01 | Se refiere al código 1.3.1.0. Añade la marca de inicio y sus colores |
| 0.5.0.0 | 2026-11-01 | Se refiere al código 1.3.2.0. Añade `precio` en la etiqueta. Confirmados los tiradores de las fechas |
| 0.6.0.0 | 2026-11-01 | Se refiere al código 1.3.2.1. Añade cómo se combinan *Longitud mínima* y *Ventana de volumen* y la receta del canal fijo |
| 0.7.0.0 | 2026-11-01 | Se refiere al código 1.3.3.0. Añade el triángulo de la vela de más volumen |
| 0.8.0.0 | 2026-11-01 | Se refiere al código 1.3.4.1. Añade la tabla de fechas y la raya entre las bandas de 1σ |
| 0.9.0.0 | 2026-11-01 | Se refiere al código 1.3.5.0. Añade la zona de búsqueda de volumen y la tabla por propósito |
| 0.10.0.0 | 2026-11-01 | Se refiere al código 1.3.6.0. Añade el ajuste «Si la vela más fuerte es muy reciente» |
| 0.11.0.0 | 2026-11-01 | Se refiere al código 1.3.7.0. Añade el triángulo gris de la más fuerte |
| 0.12.0.0 | 2026-11-04 | Se refiere al código 1.3.8.0. Añade las alertas de vuelta a la banda y de cruce de la recta central (seis alertas) |
| 0.13.0.0 | 2026-11-07 | Se refiere al código 1.3.9.0. Añade el aviso de ventana que mezcla regímenes |
| 0.14.0.0 | 2026-11-09 | Se refiere al código 1.3.10.0. Añade «Último cierre semanal» y su aviso de historial |
| 0.15.0.0 | 2026-11-10 | Se refiere al código 1.3.11.0. Añade la atenuación de las fechas y los avisos de fecha sin efecto |
| 0.16.0.0 | 2026-11-10 | Se refiere al código 1.3.14.0. Añade `hoy` con el final congelado, *Inicio = Fijo*, qué ajustes usa cada inicio, las nueve combinaciones y las alertas con *Fijo* |
| 0.17.0.0 | 2026-11-11 | Se refiere al código 1.4.0.0. Cambian los valores de serie: *Inicio = Fijo*, *Longitud mínima* 300 y *Ventana de volumen* 600, antes automático con 70 y 300 |
| 0.18.0.0 | 2026-11-11 | Se refiere al código 1.4.1.0. Añade el tiempo que abarca el canal, el título sin «auto-longitud por volumen», «Uso rápido» y la aclaración de que la mínima es un solo ajuste |
| 0.19.0.0 | 2026-11-11 | Se refiere al código 1.5.0.0 y recoge también la 1.4.2.0. Añade el panel arriba a la derecha, el final de serie *Último cierre semanal*, la proyección de una semana y su ajuste, y la advertencia de que con el final semanal no hay alertas |
| 0.20.0.0 | 2026-11-11 | Se refiere al código 1.5.1.0. Cambian los nombres de tres ajustes y las ayudas de todos los ajustes, reescritas con frases cortas, con «solo con…» al principio en los que dependen del inicio. *Extender líneas a la izquierda* gana su ayuda. La Ficha incorpora un apartado «Configurar». «Uso rápido» remite a las ayudas y a la Ficha |
| 0.21.0.0 | 2026-11-12 | Se refiere al código 1.6.0.0 y recoge también la 1.5.2.0. Añade la sección «Qué verás según lo que elijas» y la explicación de «muy reciente». Los ajustes pasan a ocho grupos numerados en el orden inicio, búsqueda, final y banda, y el panel tiene cinco filas en ese mismo orden: *Inicio*, *Búsqueda*, *Final*, *Resultado* y *Avisos*. Desaparece el ajuste de fuente (el canal usa el cierre). La opción «Usar el canal fijo» pasa a «Usar el canal de la mínima». Nuevas marcas: raya azul de final, bordes punteados en la zona de búsqueda y ◆ para la vela más fuerte, con explicación al pasar el ratón. La posición del panel no sale en la línea de estado (1.5.2.0) |
| 0.22.0.0 | 2026-11-21 | Se refiere al código 1.6.2.0. La guía se parte en dos: esta queda para añadir y ajustar el script, y la parte técnica pasa a la guía técnica. Rehecha con la plantilla estándar: ajustes por grupo con el título y el valor por defecto del código (colores y fechas incluidos), equivalencia en tiempo, colores y marcas, alertas con el nombre del código y marcos temporales. Se retiran las cifras y remisiones que no se pueden comprobar con el código |
