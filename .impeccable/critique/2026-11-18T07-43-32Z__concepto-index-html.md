---
target: concepto/index.html
total_score: 28
max_score: 40
na_heuristics: 
p0_count: 0
p1_count: 2
target_identity: "file:/home/user/rifas/concepto/index.html"
target_fingerprint: "sha256:2143db8cf24459da0b73c521e6c7d66b5f916211f33fd19cc2bd44eb2be10f19"
target_path: /home/user/rifas/concepto/index.html
timestamp: 2026-11-18T07-43-32Z
slug: concepto-index-html
---
Method: dual-agent (A: revisión de diseño · B: detector y navegador)

## Calificación: 28/40 (Bueno)

| # | Heurística | Nota | Problema principal |
|---|---|---|---|
| 1 | Visibilidad del estado | 3 | El aviso flotante dura 2.2 s y aparece encima de la cuadrícula. |
| 2 | Coincidencia con el mundo real | 3 | «Paga antes de 1:59:59» se lee como hora del día; «Trae un» es ambiguo. |
| 3 | Control y libertad | 3 | El talón llega precargado; «Venció sin pago» solo ofrece «Quitar aviso». |
| 4 | Consistencia y estándares | 2 | El relleno añil significa seleccionado y vendido. El rojo sello se usa fuera de lo tuyo. La celda libre no lleva el borde de 1.5 px. |
| 5 | Prevención de errores | 2 | Quien manda el comprobante por WhatsApp y nunca toca «Ya transferí» ve vencer un apartado pagado. |
| 6 | Reconocer en vez de recordar | 3 | La leyenda queda bajo el talón; los ejes miden 11 px. |
| 7 | Flexibilidad y eficiencia | 3 | En Gestión, el WhatsApp del cliente no es un link. |
| 8 | Estética y minimalismo | 3 | La cuadrícula empieza a 3.5 pantallas del inicio. |
| 9 | Recuperación de errores | 3 | Una sola línea de error sin aria-invalid; vencido no tiene salida. |
| 10 | Ayuda y documentación | 3 | «Bases completas» no es un link. |

## ¿Es propio de esta rifa?
Sí. Lo genérico: las 4 cifras en tarjetas de Gestión, el selector de pastilla y las 3 tarjetas del historial.
Detector: 15 avisos (cramped-padding ×11 FP, hero-eyebrow-chip ×2, skipped-heading ×1 en las notas, repeating-stripes ×1 FP). En el navegador: nested-cards ×2 FP en escritorio y «catálogo.» sola en su línea a 1280 px.
Mediciones: 100 paradas de Tab en la cuadrícula. Fichas del talón 49×27 px, selector de vista 30 px, celdas 28×26 px. Vendido 2.26:1 en claro y 2.02:1 en oscuro. Celdas atenuadas entre 1.1 y 1.6:1. Dos h1. Cuatro div con aria-label sin rol.

## Problemas prioritarios
1. [P1] «Ya transferí» queda separado de WhatsApp y llega al final. El aviso y abrir WhatsApp deberían ser un solo toque. Comando: clarify.
2. [P1] El talón llega precargado («Termina en 7», 437 y 457). Arreglo: carrito vacío, botón a #elige y aviso de SPEI antes de pedir datos. Comando: onboard.
3. [P2] En oscuro la cuadrícula se invierte y el relleno tiene doble significado. Comando: colorize.
4. [P2] La celda libre tiene el borde más débil; los ejes miden 11 px. Comando: polish.
5. [P2] Teclado y lector de pantalla: 100 paradas de Tab, pestañas sin flechas, foco que se escapa de la hoja, errores sin asociar, objetivos de 27 y 30 px, dos h1, sello oculto, talón de 238 px. Comando: harden y después audit.

## Señales por persona
- Casey: los números elegidos sin apartar no se guardan; tres viajes al banco; «Ya transferí» al fondo; fichas de 27 px.
- Riley: puede tocar «Ya transferí» sin pagar; el link no sirve en otro teléfono y no lo dice; vencido no deja volver a apartar.
- Jordan: «2 boletos · Apartar · $50» parece compra hecha; no sabe si basta con WhatsApp o con «Ya transferí».

## Observaciones menores
- El precio en rojo sello llega a 4.12:1.
- El aviso fuera de horario es un párrafo de 4 líneas.
- El WhatsApp de Gestión no es link y la barra de deshacer tapa «Por pagar».
- El pie no tiene links.
- En escritorio, el talón tapa el sello al cargar.
- «catálogo.» sola en su línea.

## Preguntas
- ¿Para qué un segundo botón si WhatsApp es la prueba?
- ¿Un 61 % vendido transmite urgencia de casino?
- ¿Pesa más la ficha perfecta o un video de 10 s con el premio?
