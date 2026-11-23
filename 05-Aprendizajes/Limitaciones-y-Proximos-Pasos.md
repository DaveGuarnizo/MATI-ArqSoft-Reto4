---
tags:
  - limitaciones
  - roadmap
  - aws
  - logisur-andina
---

---
title: Limitaciones y Próximos Pasos
tags:
  - limitaciones
  - roadmap
  - aws
  - logisur-andina
---

[🏠 Inicio](../README.md) | [⬅️ Bitácora](Bitacora-de-Hallazgos.md) | [🧭 Guión de Presentación](../00-Inicio/Mapa-de-Navegacion.md)

# 🔭 Limitaciones y Roadmap hacia Producción

## ⚠️ Amenazas a la Validez (Transparencia Técnica)
- **Una sola máquina (Apple M5 · 16 GB RAM · Docker Desktop)**: Las cifras absolutas son indicativas; el valor está en la **comparación controlada táctica vs. línea base**.
- **Red local sin WAN ni mTLS real** y **costo de detección simulado (`2 ms/señal`)**.
- **Caso borde de Redpanda**: Con falla de broker (`acks=all`), se perdieron `2` (`EXP-1`) y `4` (`EXP-1b`) señales de telemetría por error `producer_state` (**0 pánicos afectados**).

---

## 🚀 Roadmap de Siguientes Pasos

1. **AWS EC2 Multi-AZ**: Ejecutar el mismo [`docker-compose.yml`](../evidencia/docker-compose.yml) en múltiples instancias EC2 con red y discos independientes.
2. **Seguridad mTLS (`SEG-1`)**: Certificados por OBU y revocación `< 1 min`.
3. **Reglas dinámicas (`DIS-4` / `MOD-1`)**: Versionado en caliente sin reinicios.
4. **Proyector LSA Plus (`LAT-3`)**: Validación de agregados en cierre de mes (`p95 ≤ 3 s`).

---

[🏠 Volver a la Portada del Proyecto](../README.md)
