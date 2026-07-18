# 3B APP
# Documentación Funcional y Técnica

**Versión:** 1.0 (En construcción)

**Proyecto:** Migración de AppSheet a Microsoft Power Apps Canvas

**Documento:** 00_README.md

**Estado:** Documento Maestro

---

# Objetivo del Proyecto

Este repositorio contiene la documentación funcional, técnica y de arquitectura necesaria para reconstruir la aplicación **3B APP** en Microsoft Power Apps Canvas manteniendo el comportamiento de la aplicación original desarrollada en AppSheet.

La documentación será construida utilizando como fuentes principales:

- Aplicación original (AppSheet)
- Videos funcionales
- Conversaciones con usuarios del negocio
- Audios de levantamiento (SRT)
- Observación directa del funcionamiento de la aplicación

El objetivo es disponer de una especificación suficientemente detallada para desarrollar la nueva aplicación sin depender del sistema original.

---

# Alcance

El proyecto considera la reconstrucción completa de la aplicación incluyendo:

- Navegación
- Pantallas
- Formularios
- Listados
- Reglas de negocio
- Modelo de datos
- Arquitectura Power Apps
- Diseño SharePoint
- Componentes reutilizables
- Variables
- Colecciones
- Seguridad
- Backlog de implementación

No forma parte de esta documentación el código de la aplicación AppSheet existente.

---

# Objetivos Específicos

- Comprender completamente el funcionamiento del sistema actual.
- Documentar el comportamiento funcional de cada módulo.
- Identificar entidades y relaciones.
- Definir el modelo de datos definitivo.
- Diseñar la arquitectura Power Apps.
- Diseñar la estructura SharePoint.
- Reducir el riesgo durante la migración.

---

# Metodología

La documentación se desarrolla siguiendo el siguiente proceso.

```text
Sistema Original
        │
        ▼
Levantamiento Funcional
        │
        ▼
Documentación
        │
        ▼
Modelo de Datos
        │
        ▼
Arquitectura Power Apps
        │
        ▼
Implementación
```

---

# Fuentes de Información

Las decisiones documentadas deberán basarse únicamente en evidencia proveniente de alguna de las siguientes fuentes.

## Nivel 1 (Mayor prioridad)

- Aplicación original.
- Video de funcionamiento.
- Capturas oficiales.

## Nivel 2

- Audios de levantamiento.
- Reuniones con usuarios.

## Nivel 3

- Inferencias realizadas a partir del comportamiento observado.

Toda inferencia deberá quedar explícitamente marcada.

---

# Convenciones

Durante toda la documentación se utilizarán los siguientes estados.

| Estado | Significado |
|----------|-------------|
| ✅ Confirmado | Observado directamente en la aplicación o video. |
| 🎧 Confirmado por audio | Confirmado en conversaciones del negocio. |
| ⚠️ Inferido | Deducción razonable basada en evidencia parcial. |
| ❓ Pendiente | No existe evidencia suficiente para documentarlo. |

---

# Estructura de la Documentación

La documentación estará organizada de la siguiente forma.

```text
docs/

00_README.md

01_Arquitectura_General.md

02_Menu_Navegacion.md

03_Modulo_Inicio.md

04_Modulo_Vehiculos.md

05_Modulo_Cotizacion.md

06_Modulo_En_Preparacion.md

07_Modulo_En_Ruta.md

08_Modulo_Entregado.md

09_Modulo_Modulos.md

10_Modelo_Datos.md

11_SharePoint.md

12_PowerApps.md

13_Backlog.md

14_Catalogo_Componentes.md

15_Reglas_Negocio.md
```

Cada documento podrá evolucionar independientemente conforme avance el levantamiento funcional.

---

# Organización de cada Documento

Cada módulo seguirá la misma estructura para facilitar su lectura.

```text
Objetivo

Descripción

Pantallas

Componentes

Flujos

Casos de Uso

Campos

Botones

Validaciones

Reglas

Modelo de Datos

Power Apps

SharePoint

Pendientes
```

---

# Criterios de Calidad

Toda la documentación deberá cumplir los siguientes principios.

## Exactitud

No documentar funcionalidades que no hayan sido observadas o confirmadas.

## Trazabilidad

Cada regla importante debe poder relacionarse con una fuente.

## Consistencia

Todos los módulos utilizarán la misma estructura documental.

## Evolución

La documentación podrá actualizarse conforme aparezcan nuevos antecedentes.

---

# Arquitectura Objetivo

La nueva aplicación será desarrollada utilizando la siguiente arquitectura.

```text
Usuarios

        │

Power Apps Canvas

        │

Componentes Reutilizables

        │

Colecciones

        │

SharePoint Lists

        │

SharePoint Document Library
```

---

# Objetivos de Diseño

La nueva aplicación buscará:

- Reducir duplicidad.
- Reutilizar componentes.
- Mantener una única pantalla principal cuando sea posible.
- Centralizar reglas de negocio.
- Facilitar futuras mantenciones.

---

# Estado del Proyecto

| Actividad | Estado |
|-----------|--------|
| Levantamiento funcional | En proceso |
| Documentación | En proceso |
| Modelo de datos | Pendiente |
| Arquitectura Power Apps | Pendiente |
| Desarrollo | Pendiente |

---

# Convención de Nombres

## Pantallas

```
scrVehiculos
scrInicio
scrCotizacion
```

## Containers

```
conHeader
conMenu
conContenido
conDetalle
```

## Galerías

```
galVehiculos
galCotizaciones
```

## Formularios

```
frmVehiculo
frmCotizacion
```

## Variables

```
varModulo

varVehiculoSeleccionado

varMenuAbierto
```

## Colecciones

```
colVehiculos

colCotizaciones

colEstados
```

---

# Próximos Documentos

La siguiente documentación profundizará en:

1. Arquitectura general de la aplicación.
2. Navegación.
3. Análisis detallado de cada módulo.
4. Modelo de datos.
5. Arquitectura SharePoint.
6. Arquitectura Power Apps.

---

# Historial

| Versión | Fecha | Autor | Descripción |
|----------|-------|-------|-------------|
| 1.0 | 2026 | ChatGPT + Usuario | Creación inicial del documento maestro. |

---

# Observaciones

Este documento constituye el punto de entrada de toda la documentación del proyecto.

Las decisiones funcionales detalladas se encontrarán en los documentos específicos de cada módulo.

Las inferencias deberán ser reemplazadas por información confirmada a medida que avance el análisis de la aplicación original.