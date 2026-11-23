---
tags:
  - bitacora
  - lecciones-aprendidas
  - logisur-andina
---

---
title: Bitácora de Hallazgos y Correcciones
tags:
  - bitacora
  - lecciones-aprendidas
  - logisur-andina
---

[🏠 Inicio](../README.md) | [⬅️ EXP-4 Reparto](../04-Experimentos/EXP-4-Reparto-y-Escalabilidad.md) | [➡️ Limitaciones y Roadmap](Limitaciones-y-Proximos-Pasos.md)

# 🛠️ Bitácora de Hallazgos (7 Correcciones Reales)

| # | Problema detectado | Corrección aplicada |
| :---: | :--- | :--- |
| **1** | **Bypass de `fsync` activo en Redpanda** | Se activó persistencia real (`unsafe-bypass-fsync=false`, `write_caching=false`). |
| **2** | **Pausas `> 4 s` al producir** | Se desactivó `enable_leader_balancer` y se bajó `MetadataMinAge` a `250 ms`. |
| **3** | **Falla inyectada fuera de la ráfaga en `EXP-1`** | Se sincronizó `SIGKILL` en `t = 60,5 s` y se reinició `EXP-1` desde cero. |
| **4** | **Falsos positivos por reloj de VM Docker** | Se midió el orden directamente en el *worker* (`fuera_de_orden_worker`). |
| **5** | **Videollamada contaminó 4 corridas extra** | Se descartaron y se repitieron con el equipo dedicado. |
| **6** | **Reinicio en `~1 s` ocultaba falta de réplicas** | Se diseñó **[EXP-1b](../04-Experimentos/EXP-1-Disponibilidad-y-Fallas.md)** (pérdida definitiva de máquina). |
| **7** | **`p99` de pánico en `4,73 s` (> 2 s)** | Se diseñó **[EXP-1c](../04-Experimentos/EXP-1-Disponibilidad-y-Fallas.md)** (sesión `2 s`, latido `0,5 s` → `1,08 s`). |

**Cronología real:** 13-nov `00:17` → 14-nov `05:07` (`50/50` corridas del plan) · 14-nov `10:20` → `11:43` (`25/25` pruebas extra `EXP-1b/1c`).

---

**Siguiente:** [🔭 Limitaciones y Próximos Pasos](Limitaciones-y-Proximos-Pasos.md)
