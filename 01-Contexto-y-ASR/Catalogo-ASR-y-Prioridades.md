---
tags:
  - asr
  - prioridades
  - logisur-andina
---

---
title: Catálogo de ASR y Prioridades
tags:
  - asr
  - prioridades
  - logisur-andina
---

[🏠 Inicio](../README.md) | [⬅️ Contexto](Contexto-de-Negocio.md) | [➡️ Vista Funcional](../02-Arquitectura/Vista-Funcional-y-Concurrencia.md)

# 🎯 Los 10 ASR y el Mapa de Prioridades

De **10 requisitos de calidad**, solo **4 críticos (★)** dictan la estructura de la central; los otros 6 se resuelven por diseño o se validan dentro de los mismos experimentos.

---

## 🔴 Los 4 ASR Críticos (★)

| ID | Qué resuelve | Meta | Qué nos obliga a decidir |
| :--- | :--- | :--- | :--- |
| **DIS-1 ★** | Caída de un servidor en ráfaga de pánicos | `≥ 99,99 %` pánicos guardados (`< 2 s`) | Réplicas activas (`RF=3`), acuse tras replicar y *heartbeat* → [EXP-1](../04-Experimentos/EXP-1-Disponibilidad-y-Fallas.md) |
| **LAT-1 ★** | Guardar señales en pico (`5.000/s`) | `p99 < 1 min` · `0` pérdidas | Receptores sin estado, canal durable y carril propio de pánico → [EXP-2](../04-Experimentos/EXP-2-y-EXP-3-Picos-de-Carga.md) |
| **LAT-2 ★** | Detectar anomalías en pico (`5.000/s`) | `p99 < 5 s` · `0` desorden | `24` colas por `hash(camionId)` con `1` *worker* por cola → [EXP-3](../04-Experimentos/EXP-2-y-EXP-3-Picos-de-Carga.md) |
| **ESC-2 ★** | Crecimiento `18.000 → 40.000` camiones | `≈ 11.000/s` · `0` cambios de código | `24` colas fijas desde el inicio + escalado horizontal → [EXP-4](../04-Experimentos/EXP-4-Reparto-y-Escalabilidad.md) |

---

## 🧭 Los Otros 6 ASR (Alta, Media y Baja)

| ID | Prioridad | Estímulo → Meta | Cómo se atiende |
| :--- | :---: | :--- | :--- |
| **ESC-1** | 🟠 Alta | Pico `5.000/s` (5 min) → normal en `≤ 10 min` | Medido dentro de [EXP-2 y EXP-3](../04-Experimentos/EXP-2-y-EXP-3-Picos-de-Carga.md) |
| **SEG-1** | 🟠 Alta | Falsa OBU inyectando señales → bloqueo `< 1 min` | Certificados mTLS por OBU + lista de revocación |
| **DIS-4** | 🟡 Media | Regla vieja en temperatura → recalcula `< 300 ms` | Verificación de versión en el motor de alertas |
| **MOD-1** | 🟡 Media | Analista cambia umbral → activo en `≤ 15 min` sin despliegue | Servicio de Gestión de Configuración versionado |
| **INT-1** | 🟡 Media | Integración con proveedores y ERP | Despacho paralelo, proveedor alterno e idempotencia |
| **LAT-3** | 🟢 Baja | Tablero anual cierre de mes → `p95 ≤ 3 s` (`≤ 15 min`) | Agregados precalculados (día/mes/año) + caché en LSA Plus |

---

**Siguiente:** [⚡ Vista Funcional y de Concurrencia](../02-Arquitectura/Vista-Funcional-y-Concurrencia.md)
