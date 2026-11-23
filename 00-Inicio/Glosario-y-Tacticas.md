---
tags:
  - glosario
  - tacticas
  - arquitectura-software
  - logisur-andina
---

---
title: Glosario Técnico y Catálogo de Tácticas
tags:
  - glosario
  - tacticas
  - arquitectura-software
  - logisur-andina
---

[🏠 Inicio](../README.md) | [🧭 Mapa de Navegación](Mapa-de-Navegacion.md)

# 📖 Glosario Técnico y Catálogo de Tácticas

Referencia rápida de los conceptos de negocio, arquitectura y experimentación utilizados a lo largo del proyecto **LogiSur Andina (LSA)**.

---

## 🧩 Términos de Negocio y Dominio

| Término | Definición en el contexto de LSA | Dónde se usa |
| :--- | :--- | :--- |
| **OBU** (*On-Board Unit*) | Dispositivo embarcado en cada camión que captura GPS, velocidad, temperatura, puertas, cámaras y botón de pánico. Reintenta envíos hasta recibir acuse confirmado. | [Contexto](../01-Contexto-y-ASR/Contexto-de-Negocio.md) · [Prototipo](../03-Prototipo-y-Metodo/Arquitectura-del-Prototipo.md) |
| **Central de Emergencias** | Zona crítica `7x24x365` encargada de recibir pánicos (`< 2 s`) y detectar anomalías (`< 5 s`) sin pérdida de señales. | [Contenedores](../02-Arquitectura/Vista-de-Contenedores.md) |
| **LSA Plus** | Plataforma analítica y administrativa para clientes (tableros diarios/mensuales/anuales, facturación, roles). Aislada completamente de la central. | [Contenedores](../02-Arquitectura/Vista-de-Contenedores.md) |
| **ASR** (*Architecturally Significant Requirement*) | Requisito de atributo de calidad cuyo incumplimiento compromete el negocio o resulta muy costoso corregir tarde. | [Catálogo ASR](../01-Contexto-y-ASR/Catalogo-ASR-y-Prioridades.md) |

---

## 🛡️ Tácticas Arquitectónicas Implementadas

| Código | Táctica | Mecanismo concreto en LSA | ASR que atiende |
| :---: | :--- | :--- | :--- |
| **T1** | **Redundancia activa** | `3` receptores sin estado detrás de HAProxy, `2` despachadores en grupo de consumo, `3` brokers Redpanda con factor de replicación **`RF=3`**. | [DIS-1 ★](../04-Experimentos/EXP-1-Disponibilidad-y-Fallas.md) |
| **T2** | **Reintento en origen** | La OBU guarda localmente lo no confirmado y reintenta con *backoff* (`100 ms → 2 s`, timeout `5 s`) hasta recibir `HTTP 200`. | [DIS-1 ★](../04-Experimentos/EXP-1-Disponibilidad-y-Fallas.md) |
| **T3** | **Particionamiento determinista** | `24` particiones en el tópico de telemetría usando hash manual `FNV-1a(truck_id) mod 24`. Cada camión cae siempre en la misma cola. | [LAT-2 ★](../04-Experimentos/EXP-2-y-EXP-3-Picos-de-Carga.md) · [ESC-2 ★](../04-Experimentos/EXP-4-Reparto-y-Escalabilidad.md) |
| **T4** | **Concurrencia aislada** | `24` *pipelines* paralelos (`1` escritor COPY + `1` *worker* de detección por partición) sin estado compartido ni bloqueos mutuos. | [LAT-2 ★](../04-Experimentos/EXP-2-y-EXP-3-Picos-de-Carga.md) |
| **T5** | **Acuse tras replicar (`acks=all`)** | El receptor solo responde `HTTP 200` a la OBU cuando Redpanda confirma la réplica en los `3` brokers con `fsync` real. | [DIS-1 ★](../04-Experimentos/EXP-1-Disponibilidad-y-Fallas.md) |
| **T6** | **Commit tras persistir** | El despachador confirma el *offset* en el broker únicamente después de insertar el caso de pánico en PostgreSQL. | [DIS-1 ★](../04-Experimentos/EXP-1-Disponibilidad-y-Fallas.md) |
| **T7** | **Heartbeat / Monitor de salud** | Latidos cada `0,5 s` y sesión de grupo de `2 s` (ajustado en `EXP-1c`), logrando detección de caída en `~0,37 s`. | [EXP-1c](../04-Experimentos/EXP-1-Disponibilidad-y-Fallas.md) |

---

## 📐 Métricas y Conceptos de Validación

- **`p50`, `p95`, `p99`, `p99.9`**: Percentiles de latencia calculados sobre la unión de histogramas de las 5 repeticiones de cada escenario. `p99 < 5 s` significa que el 99 % de las señales se procesaron en menos de 5 segundos.
- **`SIGKILL`**: Señal del sistema operativo (`kill -9`) usada para simular una caída abrupta de un proceso o servidor sin darle oportunidad de cerrar conexiones ordenadamente.
- **Pérdida acusada (`perdidas_acusadas`)**: La falla más grave posible: el camión recibió confirmación de guardado (`HTTP 200`), dejó de reintentar, pero el registro **nunca quedó en la base de datos**.
- **PACELC**: Extensión del teorema CAP aplicada en la [Topología de Despliegue](../02-Arquitectura/Topologia-de-Despliegue.md) para replicación asíncrona inter-región (priorizando alta disponibilidad y baja latencia entre Colombia, Ecuador y Perú).
