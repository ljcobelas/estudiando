# Entrega Final · Ecosistema IA para consultas comerciales

Implementación de prueba para Electro Alem con **Make + Airtable + Groq + Gmail**. Dos escenarios exportados de Make: clasificación y borrador con aprobación humana; envío posterior de un lead aprobado.

## Revisión rápida

1. [PDF: arquitectura, datos, costos, seguridad y pruebas](documentacion/Entrega_Final_Ecosistema_IA_Electro_Alem.pdf)
2. [Escenario 01: triage y aprobación](blueprints/entrega_final_01_sanitizado.blueprint.json)
3. [Escenario 02: envío aprobado](blueprints/entrega_final_02_sanitizado.blueprint.json)
4. [Contratos JSON de las integraciones](documentacion/esquemas_transferencia.json)
5. [Capturas de evidencia](evidencias/)
6. [Dashboard Airtable público, solo lectura](https://airtable.com/app44u2el71v1uwh6/shrF1yS9OBBX56kww)

## Estado verificable (17/10/2026)

Cinco eventos auditados: 1 éxito, 1 pendiente de aprobación, 2 datos inválidos y 1 error de Groq. La tasa de error del conjunto de pruebas es 3/5 = **60 %**; incluye fallos provocados deliberadamente. La vista pública muestra las cinco filas y el error porcentual por evento. Ambos escenarios se probaron con Run once y aparecen **Inactive** en las capturas; queda pendiente activar la programación y verificar una ejecución automática para afirmar que funcionan en vivo.

## Seguridad y uso del blueprint

Las copias del repositorio omiten el correo que aparecía como nombre de la conexión Gmail. No contienen una clave Groq literal detectable; al importar se deben volver a configurar las conexiones de Airtable, Gmail y Groq y revisar las estructuras JSON de Make. No subir archivos originales ni capturas que muestren claves. El segundo escenario exige aprobación humana, borrador y ausencia de Mensaje ID. Si Gmail envía y falla la actualización posterior en Airtable, reconciliar el mensaje antes de reintentar.

## Casos de prueba

| Caso | Resultado |
| --- | --- |
| DEMO-004 | Borrador y aviso de aprobación; versión inicial sin evento auditado. |
| DEMO-005 | Aprobación, envío a Gmail y segunda ejecución sin duplicado. |
| DEMO-006 | Email faltante; evento de Ejecuciones agregado manualmente después. |
| DEMO-007 | Consulta faltante; ruta de dato inválido automática. |
| DEMO-008 | Modelo Groq inválido; ruta de Error API automática; modelo válido restaurado. |

El campo Tokens aún no se completa automáticamente. El PDF contiene una matriz de precios estimados, no gasto facturado.
