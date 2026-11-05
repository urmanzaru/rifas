# Concepto visual: Solo Mil (v0)

> El nombre es provisional. Todo este documento parte de la lluvia de ideas del 27 de julio de 2026 y está abierto a discusión.

Prototipo navegable: [`concepto/index.html`](./index.html). Ábrelo en el celular y pruébalo de preferencia **dentro del navegador de Facebook** (mándate el link por Messenger).

---

## La idea en una frase

**Un boleto impreso, no un casino.**

El comprador llega con una sola pregunta: *¿esto es fraude?* En la costa, lo que da confianza es lo físico: papel con folio, fecha y sello. Por eso la interfaz toma prestado ese lenguaje:

- El premio se presenta como un **boleto con talón perforado**.
- Los folios, la CLABE y el registro van en **letra de máquina de escribir**.
- Cuando algo es tuyo, se marca con **rojo de sello de goma**.
- El carrito es un **talón** pegado al pie de la pantalla.

## Lo que evitamos a propósito

| No | Por qué |
| --- | --- |
| Dorado, confeti, ruletas, neón | Es el lenguaje de casino y apuestas. Justo lo que da desconfianza. |
| Degradados morados, tarjetas idénticas con sombra | Es la plantilla SaaS de siempre. No dice nada de nosotros. |
| Fotos de catálogo del premio | La foto tiene que ser *nuestra*, con el premio ya comprado. |
| "Maquinita de la suerte" | Asignar al azar es resignación. Aquí el cliente pone la regla. |

---

## Decisiones de diseño

### 1. Cuadrícula 10 × 10 por centena
Mil botones en un celular de gama baja son imposibles de navegar. Se dividen en 10 pestañas (000–099 … 900–999) y cada una es una cuadrícula donde **fila = decena** y **columna = unidad**. El 487 está en la pestaña 4, fila 8, columna 7. Cada pestaña muestra una barrita con cuántos libres le quedan.

### 2. El estado se ve en la forma, no solo en el color
| Estado | Cómo se ve |
| --- | --- |
| Libre | Papel con borde fino. Se puede tocar. |
| Apartado | **Rayado** ámbar. No se puede tocar. Se libera solo a las 2 h. |
| Vendido | **Relleno** añil. No se puede tocar. |
| Tuyo | **Rojo sello**, texto blanco. |

Así se distingue con el sol de frente, en pantallas baratas y para personas que no distinguen colores.

### 3. Tú pones las reglas
Seis reglas, en este orden: **Mi teléfono**, Termina en, Trae un, Uno exacto, Capicúas, Seguiditos.

- "Mi teléfono" va primero porque es lo más personal y lo único imposible en una rifa de medio millón.
- Al aplicar una regla, lo que no cumple se atenúa, las pestañas muestran cuántos libres cumplen y la vista salta a la primera centena con coincidencias.
- Si tu número exacto ya se vendió, sugerimos la regla más cercana ("Ver los que terminan en 87").
- Si quedan 20 o menos libres que cumplen, se ofrece "Agregar los N libres".

### 4. El talón: la única llamada a la acción
Fijo al pie. Muestra tus números (tocables para quitarlos), tu probabilidad ("1 en 500") y cuánto te falta para el siguiente escalón de la escalera de recompensas. El botón dice el monto exacto: "Apartar · $75".

### 5. Fecha dura arriba, siempre
"Viernes 27 de noviembre, **vendido o no**" vive en el boleto principal, no escondido en las bases.

### 6. Probabilidades como argumento
"1 en 1,000" en grande. Es nuestro diferenciador más defendible y nadie más lo dice.

### 7. Apartado → pago en tres pasos
Después de apartar: folio con sello y hora, cuenta regresiva de 2 h, y tres pasos numerados (transferir por SPEI → mandar comprobante por WhatsApp → te confirmamos). El mensaje de WhatsApp ya va escrito con folio, números, total y nombre. El cliente no teclea nada.

### 8. Gestión con el mismo papel
La vista de conciliación es una lista de folios **ordenada por lo que vence primero**, con borde rojo cuando faltan menos de 20 min, y dos botones: "Ya pagó" y "Liberar". Debajo, el **registro**: cada movimiento con hora, que no se edita ni se borra.

---

## Tokens

### Color
| Token | Claro | Oscuro | Uso |
| --- | --- | --- | --- |
| `--papel` | `#F3F5F1` | `#101828` | Fondo. Frío, no crema. |
| `--carton` | `#E4EAE5` | `#19243A` | Superficies secundarias, campos. |
| `--tinta` | `#14223F` | `#E9EDF3` | Texto, vendido, talón. Añil oscuro. |
| `--tinta-2` | `#4B5A72` | `#9DA9BC` | Texto secundario. |
| `--sello` | `#CF3519` | `#FF6847` | Lo tuyo, la acción principal. |
| `--pacifico` | `#0B7A6F` | `#3CC4B2` | Pagado, confirmado, a tiempo. |
| `--apartado` | `#C2860A` | `#E3AE3A` | Rayado de apartado. Nunca como relleno sólido. |

**Regla de uso:** el rojo sello solo aparece en lo que es tuyo o en lo que tienes que hacer. Si todo es rojo, nada es urgente.

### Letra
| Rol | Fuente | Por qué |
| --- | --- | --- |
| Números y titulares | **Sofia Sans Extra Condensed** 800–900 | Condensada como rótulo pintado. Caben 3 cifras grandes en una celda de 30 px. |
| Texto | **Atkinson Hyperlegible** 400/700 | Diseñada para baja visión. Distingue bien 0/O e 1/l. |
| Folios, CLABE, registro | **Courier Prime** 700 | Máquina de escribir: se lee como documento. |

Todas con respaldo del sistema (`Roboto Condensed`, `Roboto`, `Courier New`) por si la fuente no carga con datos malos.

### Forma
- Radio chico (3–6 px). Es papel, no burbuja.
- Bordes de 1.5 px en tinta para lo que se puede tocar.
- Línea punteada = perforación. Se usa solo entre partes de un mismo boleto.
- Sin sombras dentro de la app.

---

## Restricciones técnicas (Facebook in-app, Android gama baja)

- **Sin framework** en el prototipo: HTML + CSS + JS, una sola página. En producción, lo que se elija debe pesar poco; la meta es < 100 KB de JS.
- **Nada depende de hover.**
- Botones de **44 px** mínimo; celdas de la cuadrícula de ~30 px (sobre el mínimo de 24 px de WCAG 2.2).
- **Contraste AA** en ambos temas.
- Los 100 botones de la cuadrícula se crean una vez y solo se actualizan: no se vuelve a pintar el DOM en cada toque.
- El salto a WhatsApp es la interacción más frágil: en producción, `https://wa.me/52XXXXXXXXXX?text=…` con el mensaje codificado, más un botón de "copiar mensaje" de respaldo.

## Lo que el prototipo **no** es

- Los datos son de ejemplo (generados con semilla fija). No hay backend.
- La CLABE, el horario y el WhatsApp son de ejemplo.
- El premio, el precio y la fecha son la propuesta "Medio" del documento, no una decisión.

## Abierto a discusión

1. El nombre. Cambiarlo toca solo la franja, la marca y el prefijo del folio (`SM1`).
2. Si la lista pública de vendidos muestra nombres o solo iniciales.
3. El regalo de 10+ boletos.
4. Si "Seguiditos" permite más de 50.
