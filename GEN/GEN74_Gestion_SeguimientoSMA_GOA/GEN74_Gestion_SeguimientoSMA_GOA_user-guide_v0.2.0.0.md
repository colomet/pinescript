# [GEN74 Management] Follow-up SMAs 20/50/150 · Guía operativa

Cómo se añade y se ajusta. Qué dice la fuente y cómo se lee, en la guía técnica.

| Campo | Valor |
|---|---|
| Título en TradingView | `[GEN74 Management] Follow-up SMAs 20/50/150` |
| Nombre corto | `GEN74 Follow-up SMAs` |
| Script | Versión 0.1.1.0, estable |
| Probada en TradingView | Sí (Antonio, 22/11/2026: «funciona»; símbolo y marco sin anotar) |
| Validada en conector | No (no intentada) |

---

## Cómo se añade

1. Abre el gráfico del activo, en el marco con el que operes.
2. En Indicadores, busca el título o el nombre corto y añádelo.
3. Se dibujan sobre el precio tres líneas: verde (corta), amarilla (media) y roja (larga). Valen para cualquier marco: se calculan siempre sobre velas semanales.

## Ajustes

Siete ajustes: tres en el grupo «Medias», tres en «Aspecto» y una ficha de solo lectura en «Info». Todos llevan explicación al pasar el ratón (tooltip), salvo los colores y la ficha.

### Medias

| Ajuste | Por defecto | Qué hace | Cuándo tocarlo |
|---|---|---|---|
| SMA corta (velas semanales) | 20 | Velas semanales de la SMA corta (1 a 500). Según la fuente, el precio por debajo marca salida | `[Aportado]`: Goat Academy. Cambiarlo da otra media |
| SMA media (velas semanales) | 50 | Velas semanales de la SMA media (1 a 500). Según la fuente, el cruce al alza del precio confirma entrada | `[Aportado]`: Goat Academy |
| SMA larga (velas semanales) | 150 | Velas semanales de la SMA larga (1 a 1000). Según la fuente, con el precio por debajo no se compra | `[Aportado]`: Goat Academy |

### Aspecto

| Ajuste | Por defecto | Qué hace |
|---|---|---|
| Color SMA corta | Verde | Color de la línea corta |
| Color SMA media | Amarillo | Color de la línea media |
| Color SMA larga | Rojo | Color de la línea larga |

La «Ficha» (grupo Info) es un resumen de solo lectura; no se puede cambiar.

## Equivalencia en tiempo

Son velas semanales, con independencia del marco del gráfico. Con 52 semanas al año:

| Ajuste | Valor | Equivale a |
|---|---|---|
| SMA corta | 20 | 20 semanas, unos 4 meses y medio |
| SMA media | 50 | 50 semanas, casi 1 año |
| SMA larga | 150 | 150 semanas, casi 3 años |

## Colores y marcas

| Elemento | Color | Qué indica |
|---|---|---|
| SMA corta (salida) | Verde | La SMA de 20 velas semanales del cierre |
| SMA media (entrada) | Amarillo | La SMA de 50 velas semanales del cierre |
| SMA larga (filtro de fondo) | Rojo | La SMA de 150 velas semanales del cierre |

No hay más marcas.

## Alertas

Este script no define alertas.

## Marcos temporales

Cualquiera: el marco semanal está fijo en el código. Con el gráfico en un marco menor que el semanal, la media de la semana en curso puede cambiar hasta el cierre de la semana.

---

## Control de cambios

| Versión | Fecha | Cambios |
|---|---|---|
| 0.1.0.0 | 2026-11-22 | Creación para el código 0.1.1.0 |
| 0.2.0.0 | 2026-11-22 | Script probado por Antonio y declarado estable; sin cambios de contenido |
