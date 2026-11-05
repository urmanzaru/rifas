---
target: concepto/index.html
total_score: 26
max_score: 40
na_heuristics: 
p0_count: 1
p1_count: 2
target_identity: "file:/home/user/rifas/concepto/index.html"
target_fingerprint: "sha256:6528f2d9f4a619db529c0c6033ec611e33080f7dfd8ee41d0d2fdb5629f920ba"
target_path: /home/user/rifas/concepto/index.html
timestamp: 2026-11-05T03-23-06Z
slug: concepto-index-html
closed: true
---
Method: dual-agent (A: design review · B: detector + browser)

## Heurísticas: 26/40 (Aceptable)
| # | Heurística | Calif. | Problema |
|---|---|---|---|
| 1 | Visibilidad del estado | 2 | El apartado desaparece tras "Listo"; aviso de "Ya pagó" sale en vista oculta |
| 2 | Lenguaje del usuario | 3 | "Trae un" críptico |
| 3 | Control y libertad | 2 | No se puede reabrir/cancelar apartado; Gestión sin deshacer; quitar regla no es obvio |
| 4 | Consistencia | 3 | Rojo sello usado en avisos neutros y errores |
| 5 | Prevención de errores | 2 | Liberar/Ya pagó juntos sin confirmar; demo abre con 2 números en el talón |
| 6 | Reconocer vs recordar | 3 | Al pagar hay que recordar folio, monto, CLABE |
| 7 | Eficiencia | 3 | Gestión sin búsqueda por folio |
| 8 | Diseño enfocado | 3 | Cuadrícula a ~1,500px; talón 16% de pantalla |
| 9 | Recuperación de errores | 3 | Un error a la vez, línea compartida |
| 10 | Ayuda | 2 | Bases no es link; sin número de WhatsApp visible |

## Especificidad
Muy específico (boleto, cuadrícula decenas×unidades, estado por forma, Lotería). Genérico: tarjetas de cifras en Gestión, línea de tiempo de escalera, píldora. Falta gente/lugar.
Detector: 12 CLI (7 cramped-padding falsos positivos; repeating-stripes mitad falso; hero-eyebrow-chip real en boleto y notas; skipped-heading en notas), navegador: low-contrast 3.1:1 rojo sobre añil en talón (real), stragglers, nested-cards solo escritorio (efecto del marco).

## Problemas prioritarios
- [P0] El apartado se pierde tras "Listo" / recarga en Facebook. Talón persistente con folio+reloj, guardar local y link ?folio=, link en mensaje de WhatsApp, renombrar "Listo". → harden
- [P1] Pago sin beneficiario: mostrar nombre, banco, CLABE, monto y folio copiables; aviso de verificación; WhatsApp visible; tiempo de confirmación; bloque de organizadores. → clarify
- [P1] Gestión: acciones instantáneas, pegadas, sin aviso ni deshacer; sin búsqueda. → harden
- [P2] Filtro atenúa todo incluidos tus números; salida oculta. → clarify
- [P2] Contraste (vendidos 2.3:1, talón 3.1:1), objetivos <44px (toggle 29.5, chips 27), 117 Tabs al CTA, pestañas sin flechas. → audit, adapt

## Personas
Casey: cuadrícula lejos, toques erróneos silenciosos, pierde todo al ir al banco, Gestión expuesta.
Jordan: llega con números preseleccionados, "concepto" sin explicar, sin plazo de confirmación.
Sam: tabs sin flechas, foco perdido tras Listo, error sin aria-invalid, límite de 2 h sin extensión.

## Menores
Oscuro invierte la saliencia; burbuja WhatsApp con color fijo; cero con diagonal; notas visibles en móvil; apartados nocturnos expiran fuera de horario.

## Preguntas
1. ¿La página de inicio tras apartar debería ser "tu boleto" con link en WhatsApp?
2. ¿Pausar el reloj fuera de horario o detenerlo al mandar comprobante?
3. ¿Quiénes son "nosotros"? Nombre y cara en la portada.
