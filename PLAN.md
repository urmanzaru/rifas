# Plan para continuar

Última actualización: 19 de noviembre de 2026 · Rama: `claude/eloquent-tesla-sgix3l`

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
| 3 | 28 / 40 | "Ya transferí" estaba separado de WhatsApp (P1 nuevo). El carrito llegaba lleno (P1). Cuadrícula invertida en oscuro, bordes débiles, teclado y lector de pantalla, talón alto (P2). |
| 4 | **sin correr** | Es lo primero que hay que hacer: medir los cambios de la tercera vuelta. |

Cada vuelta sube poco porque la revisión empieza desde cero y, con lo anterior resuelto, encuentra problemas que antes no se veían.

---

## Cómo retomar

1. **Correr la cuarta crítica** para medir lo hecho:

   ```
   /impeccable critique concepto/index.html
   ```

   La skill pide dos revisiones independientes (diseño y detector). Ninguna debe leer `.impeccable/critique/`, para no sesgarse.

2. **Elegir qué atacar** con la lista de abajo. La cuarta crítica puede reordenarla.

3. **Probar cada cambio** como se hizo en estas sesiones:
   - Servir la página por http, no como archivo, para que funcionen `localStorage` y el `#folio` del link: `python3 -m http.server 8766` desde la raíz del repo (con `run_in_background`; `nohup … &` lo bloquea el modo automático).
   - Usar Playwright (ya viene instalado en el contenedor) a 360×740, en claro y oscuro, más una pasada a 1280×900.
   - Para probar vencimientos y horario de atención, usar el reloj simulado: `page.clock.install({ time: new Date('2026-11-10T10:00:00') })` y `page.clock.fastForward('03:00:00')`.
   - Las celdas vendidas y apartadas tienen `aria-disabled`: Playwright no les da clic si no se pasa `{ force: true }`.
   - Correr el detector en el código: `.claude/skills/impeccable/scripts/impeccable detect --json concepto/index.html`.
   - Correr también el detector en el navegador: `impeccable live-server --background`, inyectar `http://localhost:PUERTO/detect.js` y leer la consola; al final, `impeccable live-server stop --keep-inject`. Encuentra cosas que el análisis del código no ve (por ejemplo, texto gris sobre color).
   - Guardar capturas y scripts en el scratchpad, nunca en el repo. Si un script de Node corre desde la raíz del repo, sus rutas relativas terminan dentro del repo.

4. **Volver a publicar la página** en el mismo link. El archivo publicado no lleva `<!doctype>`, `<html>`, `<head>` ni `<body>`: se genera quitándoselos a `concepto/index.html` y se publica con la herramienta Artifact usando la URL de arriba.

---

## Pendiente de diseño

### Lo que se corrigió después de la tercera crítica

- **Un solo botón para avisar y mandar el comprobante.** El paso 2 dice "Ya transferí · mandar comprobante": detiene el reloj y abre WhatsApp. Ya no hay un "Ya transferí" suelto al final de la hoja.
- **Carrito vacío al entrar.** El talón solo ofrece "Elegir mi número", que lleva a `#elige`. El boleto y el formulario dicen "Pagas por transferencia SPEI · tienes 2 h · no se cobra nada ahora". Los números elegidos se guardan en el teléfono.
- **Color de la cuadrícula.** Hay token `--vendido` (añil medio en oscuro) y número vendido en añil claro a 6.2:1 / 5.3:1. Las celdas libres tienen borde de 1.5 px. Lo seleccionado (regla, centena) ya no usa el relleno de vendido. El precio y "vendido o no" ya no van en rojo.
- **Teclado y lector de pantalla.** La cuadrícula y las centenas tienen una sola parada de Tab con flechas, y hay `tabpanel`. Las reglas usan `aria-pressed`. La hoja retiene el foco (`inert`). Cada campo tiene su error. Solo hay un `h1`. El sello "Ya lo tenemos" se lee en voz alta. Se quitaron los `aria-label` en `div` sin rol, y `dl.ficha` ya es válido.
- **Talón y objetivos.** Las fichas, el selector de vista y los botones chicos miden 44 px. Con un apartado y un carrito a la vez, el talón bajó de 238 a 183 px. El aviso sale dentro del talón y dura 3.5 s. "Paga antes de" ahora es "te quedan". Un apartado vencido vuelve a ofrecer "Elegir mi número".

### Observaciones de la tercera crítica (siguen abiertas)

- **La hoja de pago mide unos 1,600 px.** El botón del paso 2 ya está a la mitad (1,030 px), pero para copiar CLABE, monto y concepto hay que ir al banco tres veces. ¿Un "copiar los tres" o un formato que el banco lea de una sola vez?
- **El link con folio no hace nada en otro teléfono,** y no lo dice. Se resuelve con el backend (ver abajo), pero mientras tanto conviene un mensaje.
- **El link con folio reabre la hoja en cada recarga,** incluso cuando ya está pagado.
- **"4 cumplen · 0 libres" no sugiere nada.**
- **La escalera "Entre más llevas, más ganas"** es lo más parecido a un casino en la página, sobre todo con "10+ regalo, por definir". Una de las críticas preguntó si el 61 % vendido en la cuadrícula también se lee como presión de "ya se acaba".
- **El talón en oscuro es una franja muy clara** (es `--tinta`, que en oscuro es casi blanco). No es un error, pero es lo más brillante de la pantalla.
- **Gestión:**
  - Las 4 cifras en tarjetas de arriba son lo más genérico.
  - El WhatsApp del cliente es texto: falta un link `wa.me` para escribirle desde la tarjeta.
  - La barra de deshacer tapa la etiqueta "Por pagar".
  - No hay camino para un monto que no coincide, por ejemplo cuando alguien transfirió de menos.
  - El botón "Ya pagó" se ve igual haya avisado o no el comprador.
- **"Trae un" y "Capicúas"** no se entienden hasta tocarlos.
- **"Bases completas" y "Aviso de privacidad"** son texto, no links.
- **Fuentes:** son tres familias con siete pesos desde Google Fonts. En producción conviene alojarlas y reducirlas a lo que se usa.
- **Las notas del concepto** aparecen debajo de la app en el celular. Si se manda el link a compradores, hay que ocultarlas.
- **Una de las críticas propone un video de 10 segundos** de uno de los cuatro con el premio ya comprado, arriba de todo, como la señal de confianza más fuerte.

### Falsos positivos conocidos del detector (no corregir)

- **`cramped-padding` (13 avisos):** el detector estático no entiende `padding-block`, `max()`, `env()` ni `calc()`, ni el padding de los botones dentro de `.vista`. En el navegador no aparecen.
- **`tight-leading` (1 aviso, solo en el código):** dice "1.20x" sin línea ni elemento, y en el navegador no aparece. Ningún texto de varias líneas tiene ese interlineado.
- **`repeating-stripes-gradient`:** el rayado de "apartado" es intencional, porque marca el estado con la forma y no solo con el color.
- **`nested-cards`:** solo aparece en escritorio, porque ahí la app misma se dibuja como tarjeta.

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
