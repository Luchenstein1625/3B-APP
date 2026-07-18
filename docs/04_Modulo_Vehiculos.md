# 3B APP
# Módulo Vehículos

**Versión:** 1.0

**Documento:** 04_Modulo_Vehiculos.md

**Parte:** 1 de 8

**Estado:** En construcción

---

# Objetivo

El módulo Vehículos corresponde al núcleo operacional de la aplicación.

Su propósito es administrar el parque vehicular de la empresa, manteniendo la información de cada vehículo, su estado operativo, documentación, imágenes y trazabilidad durante todo su ciclo de utilización.

Este módulo constituye además el origen de otros procesos de la aplicación, ya que desde él se generan los distintos estados operacionales utilizados posteriormente por otros módulos.

---

# Objetivos Funcionales

El módulo permite:

- Registrar vehículos.
- Consultar vehículos existentes.
- Modificar información.
- Administrar fotografías.
- Administrar documentación.
- Consultar estado operacional.
- Buscar rápidamente un vehículo.
- Filtrar información.
- Acceder al detalle completo.

---

# Alcance

Este módulo administra únicamente la información maestra de cada vehículo.

Los procesos posteriores (Preparación, Ruta y Entregado) utilizan la información registrada aquí.

---

# Arquitectura Funcional

```text
                        Vehículos

                             │

     ┌───────────────────────┼────────────────────────┐

     ▼                       ▼                        ▼

Listado General          Detalle                Acciones

                             │

      ┌───────────────┬──────────────┬───────────────┐

      ▼               ▼              ▼

Información        Fotografías    Documentos

```

---

# Flujo General

```text
Usuario

↓

Ingresa módulo Vehículos

↓

Visualiza listado

↓

Selecciona vehículo

↓

Carga información

↓

Visualiza detalle

↓

Realiza acción

↓

Guardar cambios
```

---

# Layout General

```text
+--------------------------------------------------------------------------+

HEADER

+-------------------+------------------------------------------------------+

|                   |                                                      |
|                   |                                                      |
|                   |              Toolbar                                 |
|                   |------------------------------------------------------|
|                   |                                                      |
|                   |                                                      |
|      MENÚ         |              Listado Vehículos                       |
|                   |                                                      |
|                   |                                                      |
|                   |                                                      |
|                   |------------------------------------------------------|
|                   |                                                      |
|                   |             Panel de Detalle                         |
|                   |                                                      |
|                   |                                                      |

+-------------------+------------------------------------------------------+

FOOTER
```

---

# Componentes

El módulo se divide en cuatro zonas.

## Header

Contiene la información general de la aplicación.

---

## Toolbar

Permite ejecutar acciones.

Ejemplos.

- Buscar
- Agregar
- Editar
- Eliminar
- Filtrar

---

## Listado

Contiene todos los vehículos disponibles.

Representa la principal vista de trabajo.

---

## Panel de Detalle

Presenta toda la información del vehículo seleccionado.

---

# Flujo Operacional

```text
Seleccionar vehículo

↓

Mostrar detalle

↓

Editar

↓

Guardar

↓

Actualizar listado
```

---

# Navegación

Desde el menú lateral.

```text
Inicio

↓

Vehículos

↓

Listado
```

La navegación propuesta en Power Apps será.

```powerapps
Set(
    varModulo,
    "Vehiculos"
)
```

El container correspondiente será visible cuando:

```powerapps
Visible =
varModulo = "Vehiculos"
```

---

# Pantalla

Se propone reutilizar la pantalla principal.

```text
scrPrincipal
```

El módulo se implementará mediante un Container.

```text
conVehiculos
```

---

# Containers

```text
conVehiculos

│

├── conToolbar

├── conListado

└── conDetalle
```

---

# Toolbar

La barra superior concentra todas las acciones disponibles para el usuario.

```text
+--------------------------------------------------------------+

Buscar

Agregar

Editar

Eliminar

Filtrar

Actualizar

+--------------------------------------------------------------+
```

Cada botón ejecutará una única responsabilidad.

---

# Listado Principal

El listado representa el punto de entrada al módulo.

Cada fila corresponde a un vehículo registrado.

```text
┌───────────────────────────────────────────────────────────────┐

Vehículo 001

Vehículo 002

Vehículo 003

Vehículo 004

Vehículo 005

...

└───────────────────────────────────────────────────────────────┘
```

---

# Comportamiento del Listado

El listado debe:

- Permitir desplazamiento.
- Mantener el registro seleccionado.
- Refrescar automáticamente después de guardar.
- Permitir búsqueda.
- Permitir filtros.
- Mantener orden consistente.

---

# Selección de Registro

Al seleccionar un vehículo.

```text
Click

↓

Guardar registro seleccionado

↓

Actualizar panel derecho

↓

Mostrar información completa
```

Variable propuesta.

```powerapps
Set(
    varVehiculoSeleccionado,
    ThisItem
)
```

---

# Panel de Detalle

El panel derecho muestra la información completa del vehículo.

Su estructura propuesta es.

```text
Imagen principal

↓

Información general

↓

Características

↓

Documentación

↓

Fotografías

↓

Observaciones

↓

Acciones
```

---

# Información General

Cada vehículo dispone de un conjunto de datos principales.

Ejemplos de información a documentar durante el levantamiento funcional:

- Identificador.
- Patente.
- Marca.
- Modelo.
- Año.
- Estado.
- Responsable.
- Ubicación.
- Observaciones.

> **Nota:** El listado definitivo de campos se consolidará durante el análisis detallado del formulario y del modelo de datos en las siguientes partes del documento.

---

# Modelo de Interacción

```text
Usuario

↓

Listado

↓

Registro seleccionado

↓

Detalle

↓

Editar

↓

Guardar

↓

Actualizar
```

---

# Variables

Variables propuestas para este módulo.

```text
varVehiculoSeleccionado

varModoFormulario

varFiltroVehiculo

varBusquedaVehiculo

varNuevoVehiculo
```

---

# Colecciones

```text
colVehiculos

colEstadosVehiculo

colTiposVehiculo

colMarcas
```

---

# Componentes Reutilizables

```text
cmpToolbar

cmpBusqueda

cmpListado

cmpDetalleVehiculo

cmpEstado

cmpFotografia
```

---

# Consideraciones de Diseño

El módulo deberá priorizar:

- Facilidad de búsqueda.
- Acceso rápido a la información.
- Baja cantidad de clics.
- Reutilización de componentes.
- Escalabilidad para nuevos campos.
- Compatibilidad con dispositivos de escritorio.

---

# Próxima Parte

**Parte 2 de 8**

Se documentará:

- Búsqueda.
- Filtros.
- Toolbar completa.
- Acciones CRUD.
- Ordenamiento.
- Reglas de visualización.
- Navegación interna del módulo.
- Estados de interacción del usuario.

# 3B APP
# Módulo Vehículos

**Versión:** 1.0

**Documento:** 04_Modulo_Vehiculos.md

**Parte:** 2 de 8

---

# Búsqueda de Vehículos

El módulo deberá disponer de un buscador permanente que permita localizar rápidamente cualquier vehículo registrado.

La búsqueda debe ser inmediata, sin necesidad de presionar un botón de consulta.

---

## Objetivos

Permitir encontrar un vehículo mediante diferentes criterios.

Ejemplos:

- Patente
- Código interno
- Marca
- Modelo
- Responsable
- Estado
- Ubicación

---

## Flujo

```text
Usuario

↓

Escribe texto

↓

Sistema filtra registros

↓

Gallery actualizada

↓

Usuario selecciona vehículo
```

---

# Implementación Power Apps

Control

```text
txtBuscarVehiculo
```

Variable

```text
varBusquedaVehiculo
```

Ejemplo

```powerapps
OnChange:

Set(
    varBusquedaVehiculo,
    Self.Text
)
```

---

# Gallery

Ejemplo de Items

```powerapps
Filter(
    colVehiculos,
    StartsWith(Patente,varBusquedaVehiculo)
        ||
    StartsWith(Marca,varBusquedaVehiculo)
        ||
    StartsWith(Modelo,varBusquedaVehiculo)
)
```

---

# Estados de la búsqueda

## Sin búsqueda

```text
Todos los vehículos
```

---

## Búsqueda activa

```text
Sólo resultados encontrados
```

---

## Sin resultados

```text
No existen coincidencias.
```

---

# Filtros

Además del buscador, el módulo debe permitir aplicar filtros sobre el listado.

Los filtros pueden combinarse.

---

## Estado

Ejemplo

```text
Disponible

En preparación

En ruta

Entregado

Fuera de servicio
```

---

## Marca

Ejemplo

```text
Toyota

Hyundai

Mercedes

Chevrolet

...
```

---

## Responsable

```text
Todos

Usuario 1

Usuario 2

Usuario 3
```

---

## Ubicación

```text
Casa Matriz

Sucursal Norte

Sucursal Sur

Bodega
```

---

# Flujo de filtros

```text
Seleccionar filtro

↓

Actualizar colección

↓

Actualizar Gallery

↓

Actualizar contador
```

---

# Contador

El listado debería mostrar un resumen.

Ejemplo.

```text
Vehículos encontrados

25 registros
```

---

# Ordenamiento

El usuario podrá ordenar el listado.

Ejemplos.

```text
Patente

Marca

Modelo

Estado

Fecha creación

Fecha modificación
```

---

# Toolbar

La barra superior concentra las acciones principales.

```text
+----------------------------------------------------------------+

Buscar

Agregar

Editar

Duplicar

Eliminar

Actualizar

Filtrar

Exportar

+----------------------------------------------------------------+
```

---

# Acción Agregar

Objetivo

Registrar un nuevo vehículo.

Flujo.

```text
Nuevo

↓

Formulario vacío

↓

Completar información

↓

Guardar

↓

Actualizar listado
```

---

## Botón

```powerapps
btnNuevoVehiculo
```

---

## Acción

```powerapps
NewForm(frmVehiculo);

Set(
    varModoFormulario,
    "Nuevo"
)
```

---

# Acción Editar

Objetivo

Modificar un vehículo existente.

Flujo.

```text
Seleccionar vehículo

↓

Editar

↓

Modificar información

↓

Guardar
```

---

## Acción

```powerapps
EditForm(frmVehiculo);

Set(
    varModoFormulario,
    "Editar"
)
```

---

# Acción Eliminar

Objetivo

Eliminar un registro.

Flujo.

```text
Seleccionar

↓

Confirmar

↓

Eliminar

↓

Actualizar Gallery
```

---

## Confirmación

Debe existir una ventana de confirmación antes de eliminar.

```text
¿Desea eliminar este vehículo?

[Cancelar]

[Eliminar]
```

---

# Acción Actualizar

Permite refrescar la información del módulo.

```powerapps
Refresh(
    Vehiculos
);

ClearCollect(
    colVehiculos,
    Vehiculos
)
```

---

# Acción Exportar

Dependiendo de los requerimientos del negocio se podrá exportar.

Ejemplos.

```text
Excel

PDF

CSV
```

---

# Estados del Registro

Cada registro puede encontrarse en diferentes estados visuales.

## Normal

No seleccionado.

---

## Seleccionado

Resaltado.

---

## Edición

Formulario habilitado.

---

## Nuevo

Formulario vacío.

---

## Eliminado

Registro removido del listado.

---

# Navegación Interna

```text
Listado

↓

Detalle

↓

Editar

↓

Guardar

↓

Listado
```

---

# Variables

```text
varBusquedaVehiculo

varFiltroEstado

varFiltroMarca

varOrden

varModoFormulario
```

---

# Colecciones

```text
colVehiculos

colEstados

colMarcas

colUbicaciones
```

---

# Componentes

```text
cmpBusqueda

cmpToolbar

cmpFiltro

cmpGallery

cmpPaginacion
```

---

# Validaciones Generales

Antes de guardar un registro deberán verificarse como mínimo:

- Campos obligatorios.
- Duplicidad de identificadores.
- Formato de patente.
- Valores válidos para listas desplegables.
- Integridad de relaciones con otras entidades.

Las validaciones específicas de cada campo se documentarán en la sección del formulario.

---

# Próxima Parte

**Parte 3 de 8**

Se documentará:

- Formulario completo del vehículo.
- Todos los campos.
- Distribución del formulario.
- Validaciones por campo.
- Carga y edición de información.
- Fotografías principales.
- Datos asociados al vehículo.


