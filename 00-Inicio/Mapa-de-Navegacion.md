---
tags:
  - moc
  - presentacion
  - logisur-andina
---

---
title: Mapa de Navegación y Guión de Presentación
tags:
  - moc
  - presentacion
  - logisur-andina
---

[🏠 Inicio](../README.md) | ➡️ Siguiente: [🌎 Contexto de Negocio](../01-Contexto-y-ASR/Contexto-de-Negocio.md)

# 🧭 Mapa de Navegación y Guión de Presentación

Esta guía organiza el recorrido ideal para presentar el proyecto **LogiSur Andina (LSA)** ante una audiencia grande (directivos, arquitectos o jurado académico) en **15–20 minutos**, saltando directamente a cada nota y gráfico.

---

## 🗺️ Estructura Hiperconectada del Proyecto

```mermaid
graph TD
    HUB["🏠 README.md<br/>Portada Ejecutiva"] --> C1["🌎 01 · Contexto de Negocio"]
    HUB --> C2["🎯 01 · Catálogo ASR (10 ASR)"]
    C2 --> A1["⚡ 02 · Vista Funcional y Concurrencia"]
    C2 --> A2["🧱 02 · Vista de Contenedores"]
    C2 --> A3["☁️ 02 · Topología de Despliegue"]
    A1 --> P1["🐳 03 · Arquitectura del Prototipo"]
    P1 --> P2["🧪 03 · Método y Verificación (75 corridas)"]
    P2 --> E0["📈 04 · Dashboard de Resultados"]
    E0 --> E1["🛡️ EXP-1 / 1b / 1c (Disponibilidad)"]
    E0 --> E2["🚀 EXP-2 y EXP-3 (Picos 5.000/s)"]
    E0 --> E4["⚖️ EXP-4 (24 Colas y Escalado)"]
    E0 --> L1["🛠️ 05 · Bitácora de Hallazgos"]
    E0 --> L2["🔭 05 · Limitaciones y Roadmap"]
    HUB -.-> GL["📖 Glosario y Tácticas"]
```

---

## 🎤 Guión Sugerido para Exposición (Paso a Paso)

| Bloque | Tiempo | Nota a abrir en pantalla | Mensaje clave para la audiencia |
| :--- | :---: | :--- | :--- |
| **1. El gancho** | 2 min | [🏠 Portada](../README.md) + [🌎 Contexto](../01-Contexto-y-ASR/Contexto-de-Negocio.md) | Mostrar la animación en vivo y el dato real: en el último paro nacional un pánico tardó **4 minutos**; la flota pasará de `18.000` a `40.000` camiones. |
| **2. Qué importa de verdad** | 3 min | [🎯 Catálogo ASR](../01-Contexto-y-ASR/Catalogo-ASR-y-Prioridades.md) | Explicar por qué solo **4 de 10 ASR (`DIS-1`, `LAT-1`, `LAT-2`, `ESC-2`)** dictan la estructura arquitectónica y cómo el resto se resuelve sin complicar la central. |
| **3. La solución** | 4 min | [⚡ Funcional](../02-Arquitectura/Vista-Funcional-y-Concurrencia.md) · [🧱 Contenedores](../02-Arquitectura/Vista-de-Contenedores.md) · [☁️ Despliegue](../02-Arquitectura/Topologia-de-Despliegue.md) | Destacar las 4 tácticas (`T1–T4`), el **carril exclusivo de pánicos**, el aislamiento total de **LSA Plus** y la topología multi-región CO/EC/PE. |
| **4. Evidencia empírica** | 6 min | [📈 Dashboard](../04-Experimentos/Dashboard-Resultados.md) · [🛡️ EXP-1b/1c](../04-Experimentos/EXP-1-Disponibilidad-y-Fallas.md) · [🚀 EXP-3](../04-Experimentos/EXP-2-y-EXP-3-Picos-de-Carga.md) | Mostrar las dos pruebas estrella: **0 vs. ~35.600 pánicos perdidos** al morir un nodo (`EXP-1b`) y **`0,75 s` vs. `> 833 s`** con 24 colas frente a 1 cola (`EXP-3`). |
| **5. Rigor y cierre** | 3 min | [🛠️ Bitácora](../05-Aprendizajes/Bitacora-de-Hallazgos.md) · [🔭 Roadmap](../05-Aprendizajes/Limitaciones-y-Proximos-Pasos.md) | Mostrar transparencia técnica (el bypass de `fsync`, la sesión de `2 s`, las limitaciones de correr en 1 equipo) y el siguiente paso en **AWS EC2**. |

---

## 🔗 Enlaces Rápidos
- ¿Dudas sobre algún acrónimo técnico? Consulta el [📖 Glosario y Tácticas](Glosario-y-Tacticas.md).
- ¿Necesitas una vista condensada para imprimir o compartir? Revisa el [📄 One-Pager Ejecutivo](../LogiSur-Andina-Propuesta-Arquitectura.md).
