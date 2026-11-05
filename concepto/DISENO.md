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
| Elegido por ti | **Rojo sello** relleno, texto blanco. Está en tu talón, todavía no apartado. |
| Apartado por ti | **Rayado rojo con contorno rojo sello.** Es el rayado de "apartado" con la marca de lo tuyo. Al tocarlo: "El 437 es tuyo (SM1-0214). Paga antes de 1:52:10." |
| Tuyo, pagado | **Relleno** añil con contorno rojo sello. Al tocarlo: "Ya está pagado." |

Así se distingue con el sol de frente, en pantallas baratas y para personas que no distinguen colores.

### 3. Tú pones las reglas
Seis reglas, en este orden: **Mi teléfono**, Termina en, Trae un, Uno exacto, Capicúas, Seguiditos.

- "Mi teléfono" va primero porque es lo más personal y lo único imposible en una rifa de medio millón.
- Al aplicar una regla, lo que no cumple se atenúa, las pestañas muestran cuántos libres cumplen y la vista salta a la primera centena con coincidencias.
- Si tu número exacto ya se vendió, sugerimos la regla más cercana ("Ver los que terminan en 87").
- Si quedan 20 o menos libres que cumplen, se ofrece "Agregar los N libres".

### 4. El talón: la única llamada a la acción
Mientras tienes un apartado, el talón muestra tu folio, el tiempo y **tus números**. Lo que ya apartaste **cuenta para la escalera de premios**: si tienes 2 apartados y eliges 3 más, el talón dice "3 nuevos + 2 apartados = 5" y ya entras al sorteo de $1,000. *Suposición a validar:* la escalera es por persona en la rifa, no por compra.

Fijo al pie. Muestra tus números (tocables para quitarlos), tu probabilidad ("1 en 500") y cuánto te falta para el siguiente escalón de la escalera de recompensas. El botón dice el monto exacto: "Apartar · $75".

### 5. Fecha dura arriba, siempre
"Viernes 27 de noviembre, **vendido o no**" vive en el boleto principal, no escondido en las bases.

### 6. Probabilidades como argumento
"1 en 1,000" en grande. Es nuestro diferenciador más defendible y nadie más lo dice.

### 7. Apartado → pago en tres pasos
Después de apartar: folio con sello y hora, cuenta regresiva de 2 h, y tres pasos numerados (transferir por SPEI → mandar comprobante por WhatsApp → te confirmamos). El mensaje de WhatsApp ya va escrito con folio, números, total, nombre y el link al apartado. El cliente no teclea nada.

### 7b. El pago dice a quién, cuánto y con qué concepto
El momento de más miedo es transferirle a desconocidos. La hoja de pago lo trata así:

- **Ficha de transferencia** con cinco datos: para (titular), banco, CLABE, monto y concepto. Los tres que se teclean en el banco (CLABE, monto, concepto) tienen botón de copiar, y se copian como los pide la app: CLABE sin espacios y monto sin "$" ni comas (`50.00`).
- **Aviso de verificación**: "Antes de enviar, tu banco te enseña a nombre de quién está la cuenta. Si no dice «TITULAR», no transfieras y escríbenos." Protege al comprador incluso de alguien que se haga pasar por nosotros.
- **El WhatsApp siempre visible** como número, no solo como botón.
- **Tiempo de confirmación**: "Te confirmamos en menos de 1 hora", con el horario.
- Si el navegador no deja copiar, el texto queda seleccionado para copiarlo a mano.

### 7c. Quiénes rifamos
Toda la confianza visual era papel; faltaba gente. Una sección con foto real, nombre y pueblo de los cuatro, justo después de "El premio ya lo tenemos", más el WhatsApp para dudas antes de comprar. En el prototipo las fotos y los pueblos están por confirmar.

### 8. El apartado no se pierde
Para pagar, el comprador sale a la app de su banco, y el navegador de Facebook muchas veces recarga la página al volver. Por eso:

- El apartado se guarda en el teléfono (`localStorage`) y tiene su propio link con el folio (`#SM1-0214` en el prototipo; en producción, `/apartado/SM1-0214` consultado al servidor). Ese link va en el mensaje de WhatsApp, así el chat mismo guarda el comprobante.
- Mientras exista, el talón muestra **tu apartado** arriba de todo, con el folio y lo que corresponda a su estado:

| Estado | Qué dice el talón | Botón |
| --- | --- | --- |
| Apartado | "Paga antes de 1:52:10" | Ver cómo pagar |
| Aviso recibido | "Tus números siguen apartados mientras revisamos tu pago." Sin reloj. | Ver datos |
| Pagado | "Ya son tuyos" con los números | Ver boleto |
| Vencido / cancelado | "Los números se liberaron" | Quitar aviso |

- El botón final de la hoja ya no dice "Listo" (sonaba a que todo había terminado). Ahora son "Ya transferí" y "Cerrar", con la nota de que el apartado queda guardado.

### 8b. "Ya transferí" detiene el reloj
**Regla propuesta (validar en la junta):** el apartado vence a las 2 horas *solo si el comprador no avisa*. Al tocar "Ya transferí", los números quedan apartados **sin límite**, hasta que Gestión marque "Ya pagó" o los libere.

Por qué: con el reloj corriendo, alguien que pagó y avisó podía ver "Venció sin pago". Es el momento que convierte la duda de "¿será fraude?" en una acusación pública.

- La hoja y el talón cambian a **"Aviso recibido"**, sin cuenta regresiva, y el sello del comprobante también.
- **Fuera de horario** (antes de 9:00, después de 21:00 o en domingo), antes de apartar se avisa cuándo llegará la confirmación ("el lunes a partir de las 9:00") y que avisar detiene el reloj. El paso 3 de la hoja usa la misma hora.
- En **Gestión**, quienes avisaron van arriba en su propio grupo, "Dicen que ya transfirieron", ordenados por quién avisó primero, con "avisó hace 52 min". El grupo de abajo, "Por pagar", sí vence solo.

**Riesgo:** alguien puede tocar "Ya transferí" sin haber pagado y bloquear números hasta que Gestión los libere. Por eso ese grupo va primero: hay que revisarlo seguido, sobre todo al abrir cada mañana. En producción conviene limitar cuántos apartados avisados puede tener un mismo WhatsApp.
- Al cerrar, el foco del teclado regresa al botón del talón.
- Si el navegador bloquea el almacenamiento, todo sigue funcionando mientras la página esté abierta.

### 9. Gestión con el mismo papel
La vista de conciliación es una lista de folios **ordenada por lo que vence primero**. El tiempo restante va en una etiqueta: contorno ámbar normalmente y rellena de rojo cuando faltan menos de 20 min. Quien concilia la usa con el banco en una mano y WhatsApp en la otra, así que:

- **Búsqueda** por folio, nombre, WhatsApp o número de boleto. Al buscar también aparecen los folios ya cerrados (pagados, vencidos, liberados), sin botones, para resolver "dice que pagó pero ya no aparece".
- **Cada tarjeta** muestra nombre, WhatsApp, números y **cuánto debe llegar** (`$75.00`), para compararlo con el banco.
- **"Ya pagó $75"** es el botón principal. **"Liberar números"** queda del otro lado, como enlace, y pide confirmación dentro de la misma tarjeta, diciendo qué pasa ("Sus 3 números vuelven a estar libres y Lupita R. pierde su apartado").
- **Deshacer** durante 8 segundos después de marcar pagado o liberar, en una barra dentro de Gestión. Deshacer no borra nada: agrega otra línea al registro. Si alguien ya apartó uno de esos números, no deja deshacer y lo dice.
- **Registro** con hora y una etiqueta de texto por movimiento: APARTA, AVISA, PAGO, LIBERA, VENCE, DESHACE.

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
| `--sello-texto` | `#B02A12` | `#FF6847` | Rojo sello para **texto chico** (sello del comprobante, errores, DESHACE). El `--sello` normal no llega a 4.5:1 sobre cartulina. |
| `--apartado-tx` | `#85590A` | `#E3AE3A` | Ámbar para **texto** (VENCE, LIBERA en el registro). El `--apartado` es solo para rayados y contornos. |
| `--burbuja` | `#DCF4D9` | `#1F4A3A` | Burbuja del mensaje de WhatsApp. |

**Regla de uso:** el rojo sello solo aparece en lo que es tuyo o en lo que tienes que hacer. Si todo es rojo, nada es urgente. Los avisos neutros ("El 487 ya está vendido") van en añil, no en rojo.

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

1. A qué cuenta entra el dinero y a nombre de quién. El titular que se muestra en la hoja de pago depende de esa decisión.
2. Validar la regla de "Ya transferí" (sección 8b): los números quedan apartados sin límite hasta que Gestión revise. ¿Cada cuánto se revisa ese grupo, y quién lo hace?
3. Fotos y pueblo de cada uno para "Quiénes rifamos".
4. El nombre. Cambiarlo toca solo la franja, la marca y el prefijo del folio (`SM1`).
5. Si la lista pública de vendidos muestra nombres o solo iniciales.
6. El regalo de 10+ boletos.
7. Si "Seguiditos" permite más de 50.
