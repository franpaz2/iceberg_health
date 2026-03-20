# Iceberg Health (SACA) 
**Sistema de Auditoría Clínica Automatizada para Pacientes Polimedicados**

![Python](https://img.shields.io/badge/Python-3.10+-blue?style=for-the-badge&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-005571?style=for-the-badge&logo=fastapi)
![HTMX](https://img.shields.io/badge/HTMX-336699?style=for-the-badge&logo=htmx&logoColor=white)
![TailwindCSS](https://img.shields.io/badge/Tailwind_CSS-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white)
![Claude](https://img.shields.io/badge/Claude_Sonnet_4.6-D97757?style=for-the-badge&logo=anthropic&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)

> **Iceberg Health** es un motor SaaS de auditoría clínica diseñado para transformar historias clínicas desestructuradas en alertas médicas deterministas. Combina el poder del NLP avanzado con un motor de reglas algorítmicas para prevenir errores de prescripción en milisegundos.

---

## El Problema Clínico
Los médicos de atención primaria y geriatras se enfrentan a diario a pacientes **polimedicados** (10+ fármacos diarios). Revisar manualmente el historial clínico desestructurado (*"toma paracetamol por la mañana, y a veces adiro"*) para detectar interacciones graves, dosis renales incorrectas o contraindicaciones tarda entre **15 y 30 minutos por paciente**. 

Este proceso manual es propenso a errores humanos que derivan en ingresos a urgencias por toxicidad farmacológica o fallos en la prescripción.

## La Solución
Iceberg Health automatiza esta revisión exhaustiva en un flujo de trabajo de 3 fases, protegiendo al paciente y ahorrando miles de horas de trabajo administrativo al sistema de salud.

---

## Arquitectura Técnica (Pipeline de 3 Fases)

El proyecto es una aplicación web full-stack reactiva construida sobre **FastAPI, HTMX y Tailwind CSS**, impulsada por un potente motor de auditoría en Python.

### Fase 1: Extracción NLP Libre (La Inteligencia)
El médico introduce el historial clínico en texto libre. El sistema realiza una llamada a la API de **Claude Sonnet 4.6** (vía OpenRouter) utilizando *Prompt Engineering* avanzado.
* **Input:** Texto clínico desestructurado.
* **Procesamiento:** Inferencia de sexo, edad, enfermedades crónicas (asma, riesgo de caídas, problemas renales) y medicación con posología.
* **Output:** JSON estructurado listo para computación.

### Fase 2: Taxonomía y Enriquecimiento Farmacológico
El sistema clasifica los fármacos extraídos en familias canónicas (ej. *AINEs, ISRS, Benzodiacepinas*) y ejecuta un análisis de cronofarmacología clínica para detectar errores posológicos (ej. fármacos recetados por la noche que requieren ayunas).

### Fase 3: Auditoría Industrial Determinista (El Cerebro)
**Cero alucinaciones médicas.** En lugar de depender de un LLM para evaluar interacciones, el sistema utiliza **Pandas** y un algoritmo propio de *Fuzzy Matching* para cruzar el JSON extraído contra una **Base de Datos Master con más de 30.000 registros de AEMPS(CIMA)**.
El motor evalúa instantáneamente:
- Interacciones severas entre los fármacos prescritos.
- Contraindicaciones por embarazo/lactancia.
- Ajustes de dosis por insuficiencia renal.
- Imposibilidad de triturar pastillas (pacientes con disfagia).
- Riesgo de caídas en pacientes geriátricos y alergias cruzadas.

---

## Impacto y Resultados

| Métrica | Proceso Tradicional | Con Iceberg Health |
| :--- | :--- | :--- |
| **Velocidad de Auditoría** | 15 - 30 minutos | **< 1 minuto** |
| **Fiabilidad** | Dependiente del factor humano | **100% Determinista y Trazable** |
| **UI / UX** | Software médico heredado (lento) | **Reactividad HTMX (Sin recargas)** |

## Stack Tecnológico
* **Backend:** Python 3.10+, FastAPI, Pandas, FuzzyWuzzy/TheFuzz.
* **Frontend:** HTMX, Tailwind CSS, Jinja2.
* **IA & NLP:** Claude Sonnet 4.6 (OpenRouter API), Prompt Engineering.
* **Datos:** Base de datos no relacional (AEMPS(CIMA)).

---
*Desarrollado como parte del ecosistema de soluciones de **Iceberg Datum**.*
