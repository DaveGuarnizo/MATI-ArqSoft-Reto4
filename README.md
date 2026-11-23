---
tags:
  - moc
  - logisur-andina
  - arquitectura-software
  - reto-4
---

---
title: LogiSur Andina (LSA) · Reto 4
curso: ARTI 4109 · Arquitectura de Software
programa: MATI · Universidad de los Andes
tags:
  - moc
  - logisur-andina
  - arquitectura-software
  - reto-4
---

# 🚛 LogiSur Andina (LSA) — Arquitectura y Validación Experimental

**Proyecto Final · Reto 4 · ARTI 4109 (Arquitectura de Software) · MATI · Universidad de los Andes**

![Arquitectura en Vivo LogiSur Andina](assets/00_hero_animado_lsa.svg)

> [!tip] Presentación 100 % Interactiva y Repositorios del Proyecto
> - **Presentación Web Interactiva**: Abre **[`index.html`](index.html)** (o visítala en GitHub Pages) para explorar los simuladores en vivo (`🔥 SIGKILL`, `▶️ Pico 5.000/s`, `⚖️ Escala 40k` y `🎤 Preguntas del Jurado`).
> - **Repositorio de Documentación y Presentación**: [github.com/DaveGuarnizo/MATI-ArqSoft-Reto4](https://github.com/DaveGuarnizo/MATI-ArqSoft-Reto4)
> - **Repositorio del Prototipo y Resultados Completos (75 corridas)**: [github.com/Feru34/Arquisoft-Reto4-Resultados](https://github.com/Feru34/Arquisoft-Reto4-Resultados)

---

## 🎯 Resultados Clave Validados (`75` Corridas Reales)

| Reto | Meta | Resultado Con Táctica | vs. Línea Base | Explorar |
| :--- | :---: | :---: | :---: | :---: |
| **Caída / pérdida de nodo (`DIS-1`)** | `≥ 99,99 %` pánicos | **`100 %` (`0` perdidos)** | `~35.600` perdidos (`~61 %`) | [🛡️ EXP-1 / 1b](04-Experimentos/EXP-1-Disponibilidad-y-Fallas.md) |
| **Latencia de pánico en falla** | `< 2,0 s` | **`1,08 s`** (`p99`, sesión `2 s`) | `4,73 s` (sesión `6 s`) | [⏱️ EXP-1c](04-Experimentos/EXP-1-Disponibilidad-y-Fallas.md) |
| **Procesamiento en pico `5.000/s`** | `p99 < 5 s` | **`0,75 s`** · normaliza `≤ 1,4 s` | `> 833 s` · `2,05 M` backlog | [🚀 EXP-2 / 3](04-Experimentos/EXP-2-y-EXP-3-Picos-de-Carga.md) |
| **Escalado a `40.000` camiones** | `≈ 11.000/s` | **`≈ 11.500/s`** (`24` colas · desv. `~3 %`) | `~480/s` (`1` cola) | [⚖️ EXP-4](04-Experimentos/EXP-4-Reparto-y-Escalabilidad.md) |

---

## 🧭 Navegación de la Bóveda / Repositorio

1. **Contexto y Prioridades** → [🌎 Contexto de Negocio](01-Contexto-y-ASR/Contexto-de-Negocio.md) · [🎯 Los 10 ASR](01-Contexto-y-ASR/Catalogo-ASR-y-Prioridades.md)
2. **Vistas de Arquitectura** → [⚡ Funcional y Concurrencia](02-Arquitectura/Vista-Funcional-y-Concurrencia.md) · [🧱 Contenedores](02-Arquitectura/Vista-de-Contenedores.md) · [☁️ Despliegue Multi-Región](02-Arquitectura/Topologia-de-Despliegue.md)
3. **Prototipo y Método** → [🐳 Stack y 12 Contenedores](03-Prototipo-y-Metodo/Arquitectura-del-Prototipo.md) · [🧪 Método y Verificación](03-Prototipo-y-Metodo/Metodo-y-Verificacion.md)
4. **Evidencia Experimental** → [📈 Dashboard Visual](04-Experimentos/Dashboard-Resultados.md) · [🛡️ Disponibilidad](04-Experimentos/EXP-1-Disponibilidad-y-Fallas.md) · [🚀 Picos](04-Experimentos/EXP-2-y-EXP-3-Picos-de-Carga.md) · [⚖️ 24 Particiones](04-Experimentos/EXP-4-Reparto-y-Escalabilidad.md)
5. **Aprendizajes y Cierre** → [🛠️ Bitácora](05-Aprendizajes/Bitacora-de-Hallazgos.md) · [🔭 Limitaciones y Roadmap](05-Aprendizajes/Limitaciones-y-Proximos-Pasos.md)

---

**Accesos rápidos:** [✨ Presentación Web Interactiva](index.html) · [🎤 Guión de Exposición](00-Inicio/Mapa-de-Navegacion.md) · [📖 Glosario](00-Inicio/Glosario-y-Tacticas.md) · [📄 One-Pager](LogiSur-Andina-Propuesta-Arquitectura.md) · [🌐 Informe HTML](evidencia/informe-experimental.html) · [🐳 Docker Compose](evidencia/docker-compose.yml)
