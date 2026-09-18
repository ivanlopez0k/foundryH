# Planificación - FoundryH (harness personalizable para opencode, antes LibreCode)

Estado: vision v0 acordada 2026-09-16. Base modificable.

## 1. Producto

Producto harness separado, no config de un proyecto puntual.
Objetivo: mismo harness instalado en cada integrante de un proyecto.
Stack base: 100% dedicado a opencode, full optimizacion con primitivos nativos.

Caso referencia (ejemplo, no cliente):
- ERP con SQLServer + .NET + TypeScript/Angular, equipo de 4 personas.

## 2. Arquitectura

CORE inmutable (no se edita por empresa):
- Ciclo SDD, transaccion atomica de review, un solo writer, dispatcher autoritativo, budget 400 lineas, ledgers de attempt y review.

Capas componibles (versionadas, declaradas en repo):
- stack pack: ERP / SAP / servicios / liviano. Ejemplo ERP: CodeGraph obligatorio, verificacion dotnet test + ng test/lint, review con peso en riesgo y resiliencia, cuidado especial en migraciones.
- org policy pack: arquitectura obligatoria, lenguajes permitidos, convenciones de commits, idioma de artefactos.
- team pack: tamano de equipo. 4 personas = single writer, PRs chicas a main, sin cadena compleja.
- budget pack: model assignments por fase, limites de tokens, estrategia single-pr vs auto-chain.

Regla de herencia:
- defaults globales -> org pack -> override de proyecto.
- Override solo puede endurecer por defecto. Aflojar exige exception registrada.

No hacer N packs de entrada. Arrancar con 2 para validar extremos:
- ERP exigente (.NET/Angular/SQLServer).
- Liviano generico.

## 3. Distribucion

El repo declara stack + equipo + versiones. Cada integrante sincroniza lo mismo.
Si alguien cambia algo local, debe ser visible por versionado, no silencioso.
Inspiracion: install/sync de gentle-ai.

Roadmap:
- v0 manual: seleccion de pack a mano, fijo en repo.
- v1 asistido: init sugiere pack tras 2-3 preguntas, humano aprueba.
- v2 auto: descripcion de proyecto propone harness, siempre con aprobacion humana. Nunca aplicado solo.

## 4. Init v0

Init con 2 preguntas acordadas:
1. stack (ERP .NET/Angular, SAP, servicios, liviano, otro).
2. tamano de equipo.

Deja pack fijo y versionado en repo.

Extension futura propuesta por usuario (pendiente de diseno, parkear para otra vez):
- division por sub-stack: cuantos trabajan en .NET vs Angular vs SQL.
- roles por integrante: backend, frontend, DB, reviewer, orchestrator.
- modo equipo: fijo o rotativo. Acordado 2026-09-16: rotativo debe ser opcion. Si es rotativo, preguntar cual es el area mayor a verificar para rutear verificacion y review.
- No incluir en v0 para no sumar ceremonia. Pasar a v1 como preguntas opcionales.

## 5. Tokens

Dolor secundario: gasto normalizado. Causas: leer de mas sin comprimir, reintentar sin ledger, PRs gigantes.
Mitigacion: bounded read, un solo mapper con CodeGraph, single writer, gatekeeper, attempt ledger, forecast antes de trabajo largo, verificacion por tiers.

## 6. SDD

No agregar fases obligatorias al ciclo SDD de gentle-ai en v0.
Escalar con gates y skills opcionales sobre el mismo ciclo.
Ciclo base respetado: init -> explore -> propose -> research opcional -> spec+design -> tasks -> apply -> verify -> archive.

## 7. Pendientes

- Nombre definido 2026-09-16: FoundryH con H final (reemplaza LibreCode).
- Detallar contenido exacto de stack pack ERP y liviano.
- Definir formato de declaracion en repo (archivo de version de pack).
- Disenar preguntas de roles y division por sub-stack para v1.
- Medir la línea base de contadores proxy (P1–P6) para comparar v0 con y sin harness.
