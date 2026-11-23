---
tags:
  - metodo
  - experimentacion
  - verificacion
  - logisur-andina
---

---
title: Método Experimental y Verificación
tags:
  - metodo
  - experimentacion
  - verificacion
  - logisur-andina
---

[🏠 Inicio](../README.md) | [⬅️ Prototipo](Arquitectura-del-Prototipo.md) | [➡️ Dashboard de Resultados](../04-Experimentos/Dashboard-Resultados.md)

# 🧪 Método y Verificación (`75` Corridas)

> [!info] Rigor experimental
> **5 repeticiones** por escenario (`50` del plan + `25` extra `EXP-1b/1c`), estado limpio (`docker compose down -v`) antes de cada corrida y **cruce independiente por `(truck_id, seq)`** entre lo enviado (`gen.csv.gz`) y lo guardado en PostgreSQL.

---

## ⚙️ Perfiles de Carga

| Experimento | Carga | Evento clave |
| :--- | :--- | :--- |
| **EXP-1, 1b, 1c** | `150 s` a `5.000/s` + `400` pánicos c/5 s (`11.600`/corrida) | `SIGKILL` exacto en **`t = 60,5 s`** (en plena ráfaga) |
| **EXP-2 (`LAT-1`)** | `60 s @ 1.500/s` → `300 s @ 5.000/s` → `30 s @ 1.500/s` | `5,5 %` camiones pierden cobertura `120 s` (`1,98 %` atrasadas) |
| **EXP-3 (`LAT-2`)** | `30 s @ 1.500/s` → `300 s @ 5.000/s` → retorno `1.500/s` | Mide si el *backlog* vuelve a `≤ 1.500` sostenido `30 s` |

---

## 🔍 Qué Verifica `analyze.py` (Sin Confiar en Auto-Reporte)

- **`perdidas_acusadas`**: La falla más grave — el camión recibió `HTTP 200`, pero el registro no está en la BD.
- **`panicos_guardados_pct`**: Criterio formal `DIS-1` (`≥ 99,99 %`).
- **`duplicados` y `fuera_de_orden_worker`**: Auditados directamente en tablas sin índice y por secuencia del *worker*.
- **Percentiles (`p50`, `p95`, `p99`, `p99.9`)**: Calculados sobre la unión de histogramas de las 5 repeticiones.

---

**Siguiente:** [📈 Dashboard Visual de Resultados](../04-Experimentos/Dashboard-Resultados.md)
