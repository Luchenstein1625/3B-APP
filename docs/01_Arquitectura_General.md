# 3B APP
# Arquitectura General

**Versión:** 1.0

**Documento:** 01_Arquitectura_General.md

**Estado:** En elaboración

---

# Objetivo

Este documento describe la arquitectura funcional observada de la aplicación **3B APP** y establece la arquitectura objetivo para su migración desde **AppSheet** hacia **Microsoft Power Apps Canvas**.

No pretende describir la implementación técnica, sino el funcionamiento de alto nivel del sistema y la relación entre sus distintos módulos.

---

# Visión General

La aplicación 3B APP corresponde a una aplicación de gestión operacional orientada al seguimiento y administración de distintos recursos utilizados por la empresa.

La navegación se realiza mediante un menú lateral permanente, mientras que el contenido principal cambia dinámicamente según el módulo seleccionado.

La aplicación mantiene una experiencia uniforme en prácticamente todos los módulos.

---

# Arquitectura Actual (AppSheet)

```text
                    Usuario
                       │
                       ▼
               Aplicación AppSheet
                       │
        ┌──────────────┼──────────────┐
        │              │              │
        ▼              ▼              ▼
     Menú         Formularios      Listados
        │              │              │
        └──────────────┼──────────────┘
                       │
                       ▼
                Fuente de Datos
```

Características observadas:

- Navegación centralizada.
- Formularios reutilizados.
- Vistas tipo lista.
- Paneles de detalle.
- Acciones rápidas.

---

# Arquitectura Objetivo (Power Apps)

```text
                 Usuario

                    │

                    ▼

          Power Apps Canvas

                    │

        ┌───────────┴────────────┐

        ▼                        ▼

     Componentes            Variables

        │                        │

        └───────────┬────────────┘

                    ▼

             Colecciones Locales

                    │

                    ▼

             SharePoint Online

        ┌───────────┴────────────┐

        ▼                        ▼

     Listas                 Documentos
```

---

# Principios de Diseño

La nueva aplicación deberá seguir los siguientes principios.

## 1. Reutilización

No duplicar pantallas.

Los módulos deben compartir la mayor cantidad posible de componentes.

---

## 2. Componentización

Todo elemento reutilizable deberá implementarse como componente.

Ejemplos:

- Header
- Menú
- Botones
- Tarjetas
- Paneles
- Formularios

---

## 3. Navegación Simple

La navegación debe mantenerse consistente.

Siempre existirán:

- Header
- Menú
- Contenido

---

## 4. Separación de Responsabilidades

Cada módulo será responsable únicamente de su información.

Las reglas comunes se implementarán de forma centralizada.

---

# Arquitectura de Pantallas

Se propone utilizar una única pantalla principal.

```text
App

│

└── scrPrincipal
```

Dentro de esta pantalla se utilizarán Containers para mostrar u ocultar cada módulo.

---

# Layout General

```text
+--------------------------------------------------------------+
| Header                                                       |
+--------------------------------------------------------------+
|                                                              |
|  Menú               Contenido Principal                      |
|                                                              |
|  Inicio             Módulo seleccionado                      |
|  Vehículos                                              |
|  Cotización                                              |
|  Ruta                                                   |
|  ...                                                    |
|                                                              |
+--------------------------------------------------------------+
| Footer                                                       |
+--------------------------------------------------------------+
```

---

# Estructura de Containers

```text
scrPrincipal

│

├── conHeader

├── conBody

│     ├── conMenu

│     └── conContenido

└── conFooter
```

---

# Contenido Principal

Dentro de `conContenido` existirán distintos containers.

```text
conContenido

│

├── conInicio

├── conVehiculos

├── conCotizacion

├── conPreparacion

├── conRuta

├── conEntregado

├── conModulos

├── conParking

└── ...
```

Cada container será visible únicamente cuando corresponda.

Ejemplo:

```powerapps
Visible =
varModulo = "Vehiculos"
```

---

# Navegación

La navegación será controlada mediante una única variable.

```powerapps
Set(varModulo,"Vehiculos")
```

Todos los módulos utilizarán esta variable para controlar su visibilidad.

---

# Menú

El menú será una Gallery.

```text
galMenu
```

Su origen será una colección.

```text
colMenu
```

Ejemplo.

```powerapps
Table(

{Titulo:"Inicio"},

{Titulo:"Vehículos"},

{Titulo:"Cotización"}

)
```

---

# Flujo General

```text
Usuario

↓

Selecciona módulo

↓

Actualiza variable

↓

Oculta containers

↓

Muestra módulo solicitado
```

---

# Patrón de Diseño

Todos los módulos deberán compartir exactamente la misma estructura.

```text
conModuloXXXX

│

├── Header

│

├── Barra Acciones

│

├── Listado

│

└── Panel Detalle
```

---

# Barra de Acciones

Cada módulo podrá disponer de una barra de acciones.

Ejemplo.

```text
Buscar

Agregar

Editar

Eliminar

Filtrar

Exportar
```

No todos los módulos utilizarán todas las acciones.

---

# Panel de Detalle

El panel derecho contendrá la información del elemento seleccionado.

Ejemplo.

```text
Imagen

Datos

Documentos

Cotización

Observaciones

Botones
```

---

# Modelo de Navegación

```text
Inicio

│

├── Vehículos

├── Cotización

├── Preparación

├── Ruta

├── Entregado

├── Módulos

├── Parking

└── Configuración
```

---

# Variables Globales

Se propone utilizar únicamente las variables necesarias.

```text
varModulo

varMenuAbierto

varRegistroSeleccionado

varModoFormulario
```

---

# Colecciones

Las colecciones permitirán reducir llamadas repetitivas.

```text
colMenu

colVehiculos

colCategorias

colEstados

colUsuarios
```

---

# Componentes

Se recomienda construir los siguientes componentes reutilizables.

```text
cmpHeader

cmpMenu

cmpToolbar

cmpCard

cmpImagen

cmpEstado

cmpBusqueda
```

---

# Beneficios Esperados

La arquitectura propuesta permitirá:

- Reducir duplicidad de pantallas.
- Simplificar el mantenimiento.
- Facilitar futuras ampliaciones.
- Mejorar la experiencia del usuario.
- Centralizar reglas de negocio.
- Reutilizar formularios.
- Reducir código Power Fx.

---

# Riesgos

Durante la migración deberán revisarse cuidadosamente:

- Reglas ocultas de AppSheet.
- Acciones automáticas.
- Validaciones.
- Dependencias entre módulos.
- Permisos de usuario.
- Automatizaciones.

---

# Próximo Documento

El siguiente documento describe la navegación completa de la aplicación.

```
02_Menu_Navegacion.md
```

En él se documentará:

- Todos los módulos observados.
- Relaciones entre pantallas.
- Flujo de navegación.
- Comportamiento del menú.
- Variables utilizadas.
- Recomendaciones específicas para Power Apps.

---

# Estado

| Actividad | Estado |
|-----------|--------|
| Arquitectura actual | ✅ Documentada |
| Arquitectura objetivo | ✅ Definida |
| Layout principal | ✅ Definido |
| Navegación | Parcial |
| Componentes | Parcial |
| Modelo de datos | Pendiente |
| Reglas de negocio | Pendiente |