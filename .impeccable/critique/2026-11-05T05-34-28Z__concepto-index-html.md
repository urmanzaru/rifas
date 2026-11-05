---
target: concepto/index.html
total_score: 27
max_score: 40
na_heuristics: 
p0_count: 0
p1_count: 2
target_identity: "file:/home/user/rifas/concepto/index.html"
target_fingerprint: "sha256:057f033e7e4a75773efdfce8cf95e2168a0eed3e324e21e2d286cebea7de39b4"
target_path: /home/user/rifas/concepto/index.html
timestamp: 2026-11-05T05-34-28Z
slug: concepto-index-html
---
Method: dual-agent (A: design review · B: detector + browser)

## Heurísticas: 27/40 (Aceptable, parte alta). Anterior: 26/40
| # | Heurística | Antes | Ahora | Problema |
|---|---|---|---|---|
| 1 | Visibilidad del estado | 2 | 3 | Tus números apartados se ven como de un extraño en la cuadrícula |
| 2 | Lenguaje del usuario | 3 | 3 | SPEI no se menciona antes de pedir datos; "Trae un" críptico |
| 3 | Control y libertad | 2 | 3 | No se puede cancelar el apartado ni corregir datos |
| 4 | Consistencia | 3 | 2 | Rojo sello sobrecargado; celdas libres con borde de 1px |
| 5 | Prevención de errores | 2 | 2 | "Ya transferí" no detiene el reloj; nada avisa fuera de horario |
| 6 | Reconocer vs recordar | 3 | 3 | El talón con apartado no muestra los números |
| 7 | Eficiencia | 3 | 3 | Gestión sin filtro "dice que ya transfirió"; sin flechas en cuadrícula |
| 8 | Diseño enfocado | 3 | 3 | Talón de 200px con apartado + carrito |
| 9 | Recuperación de errores | 3 | 2 | "0 libres" sin siguiente paso; "Venció sin pago" sin re-apartar |
| 10 | Ayuda | 2 | 3 | Bases no es link; sin FAQ |

## Especificidad
Muy específico; más fuerte en portada, comprobante y hoja de pago. Genérico: tarjetas de Gestión, cuadrícula de iniciales, escalera (lo más "casino").
Detector: 16 CLI (12 cramped-padding falsos, medidos; stripes intencionales en apartado; eyebrow en escritorio; skipped-heading en notas). Navegador: contraste VENCE 2.9:1, sello Apartado/hora 4.1:1, placeholder buscador 4.2:1; sin overflow. Rojo del talón ya no aparece.

## Problemas prioritarios
- [P1] "Ya transferí" no detiene el reloj: transferido vence como cualquier apartado e ignora horario. Congelar apartado hasta revisión; mensaje "Recibimos tu aviso"; avisar fuera de horario; agrupar en Gestión. → harden
- [P1] Tus números pierden identidad tras apartar: estado "tuyo sin pagar" en cuadrícula, mensaje al tocar, números en el talón, contar para la escalera. → clarify
- [P2] Carrito prellenado y pago no explicado antes de pedir datos: carrito vacío, enlace a la cuadrícula, línea "Pagas por SPEI · 2 h · no se cobra nada ahora". → onboard
- [P2] Modo oscuro invierte la cuadrícula; vendidos 2.3:1/2.0:1; borde de libres débil. → colorize
- [P2] Teclado/lector: 100 Tabs, tabs sin flechas, sin trampa de foco en la hoja, errores sin aria-invalid. → harden

## Personas
Casey: cuadrícula a ~2,060px sin enlace; fichas de 27px; hoja reabre arriba al volver.
Jordan: carrito prellenado; "Ya transferí" vs comprobante; nada sobre horario.
Sam: sin trampa de foco; sello "Ya lo tenemos" aria-hidden; dos h1.

## Menores
Precio en rojo sello; link reabre hoja aun pagado; folios consecutivos enumerables en producción (usar token); sin camino para monto que no coincide.

## Preguntas
1. ¿"Ya transferí" como momento en que se detiene el reloj, con sello "AVISO RECIBIDO"?
2. ¿Permiso de SEGOB o declaración honesta en la portada?
3. ¿Iniciales del dueño en la cuadrícula pública?
