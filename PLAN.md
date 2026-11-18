# Plan para continuar

Última actualización: 18 de noviembre de 2026 · Rama: `claude/hopeful-newton-jsbf31`

Este archivo es para retomar el trabajo en otra sesión sin repetir lo que ya se hizo. Léelo junto con [`concepto/DISENO.md`](concepto/DISENO.md), que explica cada decisión de diseño.

---

## Dónde estamos

**Qué existe:**

- **[`concepto/index.html`](concepto/index.html)**: prototipo navegable en un solo archivo (HTML, CSS y JS sin framework), con vista de cliente y vista de Gestión. Usa datos de ejemplo y no tiene backend.
- **[`concepto/DISENO.md`](concepto/DISENO.md)**: la idea ("un boleto impreso, no un casino"), las decisiones, los colores y fuentes, y las restricciones técnicas.
- **Página publicada:** https://claude.ai/artifact/D2UGFrumVYkFNBSjr2yW6M (privada; se comparte desde el menú Share).
- **Skills de diseño en el repo:** `.claude/skills/impeccable` y `.claude/skills/ui-ux-pro-max`. De dónde salen está en [`.claude/skills/FUENTES.md`](.claude/skills/FUENTES.md). `frontend-design` está instalada en la cuenta, no en el repo.
- **Críticas guardadas:** `.impeccable/critique/`.

**Calificación de `/impeccable critique`:**

| Vuelta | Calificación | Qué se corrigió después |
|---|---|---|
| 1 | 26 / 40 | El apartado se perdía al salir a pagar (P0). El pago no decía a quién transferir (P1). Gestión actuaba sin confirmar ni deshacer (P1). |
| 2 | 27 / 40 | "Ya transferí" no detenía el reloj (P1). Tus números se veían como de un extraño (P1). Tres contrastes bajos. |
| 3 | **sin correr** | Es lo primero que hay que hacer: medir los cambios de la segunda vuelta. |

La segunda vuelta subió solo un punto porque la revisión empieza desde cero cada vez y, con el flujo completo funcionando, encontró problemas que antes no se veían.

---

## Cómo retomar

1. **Correr la tercera crítica** para medir lo hecho:

   ```
   /impeccable critique concepto/index.html
   ```

   La skill pide dos revisiones independientes (diseño y detector). Ninguna debe leer `.impeccable/critique/`, para no sesgarse.

2. **Elegir qué atacar** con la lista de abajo. Los P2 vienen de la segunda crítica, y la tercera puede reordenarlos.

3. **Probar cada cambio** como se hizo en esta sesión:
   - Servir la página por http, no como archivo, para que funcionen `localStorage` y el `#folio` del link: `python3 -m http.server 8766` desde la raíz del repo.
   - Usar Playwright (ya viene instalado en el contenedor) a 360×740, en claro y oscuro, más una pasada a 1280×900.
   - Para probar vencimientos y horario de atención, usar el reloj simulado: `page.clock.install({ time: new Date('2026-11-10T10:00:00') })` y `page.clock.fastForward('03:00:00')`.
   - Correr el detector: `.claude/skills/impeccable/scripts/impeccable detect --json concepto/index.html`.
   - Guardar capturas y scripts en el scratchpad, nunca en el repo. Si un script de Node corre desde la raíz del repo, sus rutas relativas terminan dentro del repo.

4. **Volver a publicar la página** en el mismo link. El archivo publicado no lleva `<!doctype>`, `<html>`, `<head>` ni `<body>`: se genera quitándoselos a `concepto/index.html` y se publica con la herramienta Artifact usando la URL de arriba.

---

## Pendiente de diseño

### P2 de la segunda crítica (acordados para la siguiente vuelta)

**1. El carrito llega lleno y no se explica el pago antes de pedir datos** · `/impeccable onboard`

- Al entrar ya hay una regla puesta ("Termina en 7") y dos números en el talón con "Apartar · $50". Lo marcaron las dos críticas; para alguien que se pregunta si es fraude, parece un truco.
- El pago por transferencia SPEI no se menciona hasta después de pedir nombre y WhatsApp.
- **Arreglo:** carrito vacío al entrar. El talón vacío lleva a `#elige`. Agregar en la portada y en el formulario: "Pagas por transferencia SPEI · tienes 2 h · no se cobra nada ahora".
- Código: la preselección de demo está al final del script (`if (!misApartados().length) for (...) tuyos.add(n)`) y la regla inicial en `regla = 'termina'`.

**2. En modo oscuro la cuadrícula se invierte** · `/impeccable colorize`

- Los vendidos quedan como lo más brillante y los libres como lo más apagado.
- El número dentro de las celdas vendidas tiene 2.3:1 de contraste en claro y 2.0:1 en oscuro.
- Las celdas libres tienen borde de 1 px con baja opacidad; DISENO.md promete 1.5 px de tinta para lo que se puede tocar.
- **Arreglo:** un color propio para "vendido" en oscuro (relleno medio, no tinta), borde de 1.5 px en celdas libres, y subir el número de los vendidos a 4.5:1 u ocultarlo a propósito (la etiqueta accesible ya lo dice).

**3. Teclado y lector de pantalla** · `/impeccable harden`, luego `/impeccable audit`

- La cuadrícula tiene 100 paradas de Tab. Usar un solo punto de Tab con movimiento por flechas (*roving tabindex*).
- Las pestañas de centena tienen `role="tab"` pero no responden a flechas ni tienen `tabpanel` ni `aria-controls`.
- La hoja de pago no retiene el foco: Tab desde "Cerrar" se sale a la página.
- Los errores del formulario usan una sola línea compartida: falta `aria-invalid` y `aria-describedby` por campo.
- El selector Cliente/Gestión mide 30 px y las fichas de número del talón 27 px. Deberían medir 44.
- Hay dos `h1` (premio y notas) y las notas saltan de `h1` a `h3`.
- El sello "Ya lo tenemos" tiene `aria-hidden`, así que esa promesa de confianza no llega al lector de pantalla.
- `.marca` tiene `aria-label` en un `div` sin rol, y `dl.ficha` mete botones dentro de sus `div`.

### Observaciones menores (cuando haya tiempo)

- **El talón crece hasta 200 px** (27% de la pantalla) cuando hay un apartado y un carrito al mismo tiempo, y el aviso flotante tapa filas de la cuadrícula.
- **La hoja de pago mide unos 1,480 px.** Al volver del banco reabre arriba, y "Ya transferí" queda hasta el final.
- **El link con folio reabre la hoja en cada recarga,** incluso cuando ya está pagado.
- **"4 cumplen · 0 libres" no sugiere nada,** y "Venció sin pago" solo ofrece "Quitar aviso", sin opción de volver a apartar.
- **El precio de $25 va en rojo sello,** contra la regla de usar rojo solo para lo tuyo y la acción principal.
- **La escalera "Entre más llevas, más ganas"** es lo más parecido a un casino en la página, sobre todo con "10+ regalo, por definir".
- **Gestión:**
  - Las 4 cifras en tarjetas de arriba son lo más genérico.
  - No hay camino para un monto que no coincide, por ejemplo cuando alguien transfirió de menos.
  - El botón "Ya pagó" se ve igual haya avisado o no el comprador.
- **"Trae un" y "Capicúas"** no se entienden hasta tocarlos.
- **"Bases completas" y "Aviso de privacidad"** son texto, no links.
- **Fuentes:** son tres familias con siete pesos desde Google Fonts. En producción conviene alojarlas y reducirlas a lo que se usa.
- **Las notas del concepto** aparecen debajo de la app en el celular. Si se manda el link a compradores, hay que ocultarlas.

### Falsos positivos conocidos del detector (no corregir)

- **`cramped-padding` (12 avisos):** el detector estático no entiende `padding-block`, `max()`, `env()` ni `calc()`. En el navegador no aparecen, y se midieron uno por uno.
- **`repeating-stripes-gradient`:** el rayado de "apartado" es intencional, porque marca el estado con la forma y no solo con el color.
- **`nested-cards`:** solo aparece en escritorio, porque ahí la app misma se dibuja como tarjeta.
- **`hero-eyebrow-chip`:** el de las notas no es producto. El del boleto lleva datos reales (rifa #1 y combo); hay que decidir si se queda.

---

## Pendiente de decidir entre los cuatro

Estas decisiones bloquean datos que hoy son de ejemplo en el prototipo:

1. **A qué cuenta entra el dinero y a nombre de quién.** El aviso de la hoja de pago ("si no dice «TITULAR», no transfieras") depende de esto. Es la decisión más importante.
2. **Validar la regla de "Ya transferí"** (DISENO.md, sección 8b): los números quedan apartados sin límite hasta que Gestión revise. ¿Quién revisa ese grupo y cada cuánto, sobre todo al abrir cada mañana?
3. **La escalera de premios:** ¿cuenta por persona en toda la rifa (como está hoy) o por cada compra?
4. **Fotos reales, pueblo de cada uno y nombre completo de Famero** para "Quiénes rifamos". Revisar que "de aquí de la costa" sea cierto para los cuatro.
5. **El número de WhatsApp real** y el horario de atención (hoy: lunes a sábado, de 9:00 a 21:00).
6. **El nombre.** "Solo Mil" es provisional; cambiarlo toca la franja, la marca y el prefijo del folio (`SM1`).
7. **El permiso de SEGOB:** ¿hay número de permiso, o una explicación honesta para mostrar en la portada? Una de las críticas lo propone como la señal de confianza más fuerte.
8. **La lista pública de vendidos:** ¿con nombres, con iniciales o sin dueño?
9. **El regalo de 10+ boletos** y el límite de "Seguiditos" (hoy 50).
10. **El premio, el precio y la fecha** del prototipo son la propuesta "Medio" de la lluvia de ideas, no una decisión.

---

## Para el backend (José María)

Lo que el prototipo simula y producción tiene que resolver en el servidor:

- **Link del apartado con un código que no se pueda adivinar.** Hoy es `#SM1-0214`. Con folios consecutivos, `/apartado/SM1-0214` dejaría ver nombres y números de otros cambiando el número.
- **Consultar el apartado en el servidor desde el link,** para que funcione en otro teléfono. Hoy solo vive en el `localStorage` de quien apartó.
- **El vencimiento a 2 horas aplica solo a `apartado`, nunca a `transferido`.** Debe correr como tarea del servidor y ser confiable: un error aquí es dinero perdido.
- **Limitar cuántos apartados avisados ("Ya transferí") puede tener un mismo WhatsApp,** para que nadie bloquee números sin pagar.
- **Estados del apartado:** `apartado`, `transferido`, `pagado`, `vencido`, `liberado`. En el prototipo hay además `descartado`, que es solo del lado del cliente.
- **Registro de movimientos que no se edita ni se borra.** Deshacer agrega una línea nueva. Etiquetas: APARTA, AVISA, PAGO, LIBERA, VENCE, DESHACE.
- **Gestión detrás de inicio de sesión.** En el prototipo es un botón visible.
- **`organizador_id` en todas las tablas desde el primer día,** como pide la lluvia de ideas.
- **Bloqueo de números al apartar:** dos personas no pueden apartar el mismo número al mismo tiempo, y deshacer una liberación debe fallar si alguien ya tomó esos números (el prototipo ya lo comprueba).

---

## Después del prototipo

Cuando el diseño esté validado con el equipo:

1. **Probar en un Android de gama baja dentro del navegador de Facebook** (mandar el link por Messenger). Nunca se probó en un dispositivo real; solo en Chromium de escritorio.
2. **Elegir el stack del frontend real con José María.** Debe ser ligero: la meta es menos de 100 KB de JS.
3. **Pasar los colores de DISENO.md a tokens del proyecto real** (`/impeccable extract` o `/impeccable document`).
4. **Correr `/impeccable init`** para crear `PRODUCT.md`. Hoy `impeccable` corre sin contexto de producto y lo infiere del código.
