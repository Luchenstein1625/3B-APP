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

# 3B APP
# Módulo Vehículos

**Versión:** 1.0

**Documento:** 04_Modulo_Vehiculos.md

**Parte:** 3 de 8

---

# Formulario de Vehículos

El formulario permite registrar y modificar la información asociada a cada vehículo.

Debe utilizarse tanto para la creación de nuevos registros como para la actualización de vehículos existentes.

---

# Objetivos del Formulario

El formulario debe permitir:

- Registrar un nuevo vehículo.
- Editar un vehículo existente.
- Consultar información en modo lectura.
- Validar campos obligatorios.
- Evitar registros duplicados.
- Asociar imágenes y documentos.
- Guardar trazabilidad de creación y modificación.
- Mantener consistencia entre los distintos estados operacionales.

---

# Modos del Formulario

El formulario puede operar en tres modos.

| Modo | Descripción |
|---|---|
| Nuevo | Permite crear un vehículo. |
| Editar | Permite modificar un vehículo existente. |
| Consulta | Muestra la información sin permitir cambios. |

Variable propuesta:

```powerapps
varModoFormulario
```

Valores posibles:

```text
Nuevo

Editar

Consulta
```

---

# Control Principal

Se propone utilizar un formulario de Power Apps.

```text
frmVehiculo
```

Propiedad `Item`:

```powerapps
varVehiculoSeleccionado
```

---

# Cambio de Modo

## Nuevo

```powerapps
NewForm(frmVehiculo);;

Set(
    varModoFormulario;
    "Nuevo"
);;

Set(
    varVehiculoSeleccionado;
    Blank()
)
```

---

## Editar

```powerapps
EditForm(frmVehiculo);;

Set(
    varModoFormulario;
    "Editar"
)
```

---

## Consulta

```powerapps
ViewForm(frmVehiculo);;

Set(
    varModoFormulario;
    "Consulta"
)
```

---

# Estructura Propuesta del Formulario

El formulario puede dividirse en bloques funcionales.

```text
Formulario Vehículo

│

├── Identificación

├── Características generales

├── Información operacional

├── Responsable y ubicación

├── Documentación

├── Fotografías

├── Observaciones

└── Auditoría
```

---

# Distribución Visual

```text
+-----------------------------------------------------------------------+

                        DATOS DEL VEHÍCULO

+-----------------------------------------------------------------------+

| Patente                    | Código interno                           |

| Marca                      | Modelo                                  |

| Año                        | Tipo                                    |

| Estado                     | Ubicación                               |

| Responsable                | Fecha de ingreso                        |

+-----------------------------------------------------------------------+

| Observaciones                                                       |

|                                                                       |

+-----------------------------------------------------------------------+

| Fotografía principal       | Documentos asociados                    |

+-----------------------------------------------------------------------+

| Cancelar                                   Guardar                    |

+-----------------------------------------------------------------------+
```

La distribución definitiva deberá respetar el diseño visual de la aplicación original y adaptarse a la experiencia de escritorio definida para Power Apps.

---

# Sección Identificación

Esta sección contiene la información utilizada para identificar de manera única al vehículo.

## Campos Propuestos

| Campo | Tipo de dato | Obligatorio | Descripción |
|---|---|---:|---|
| ID | Número | Sí | Identificador interno generado por la fuente de datos. |
| Código interno | Texto | Por confirmar | Código utilizado por la organización. |
| Patente | Texto | Sí | Identificador principal visible del vehículo. |
| Nombre o descripción | Texto | Por confirmar | Nombre descriptivo del registro. |

---

# Campo ID

El identificador debe ser generado automáticamente por SharePoint.

No debe ser editable por el usuario.

Control propuesto:

```text
lblVehiculoId
```

Valor:

```powerapps
varVehiculoSeleccionado.ID
```

---

# Campo Patente

La patente representa uno de los principales criterios de identificación y búsqueda.

Control propuesto:

```text
txtPatente
```

## Comportamiento

- Convertir el valor a mayúsculas.
- Eliminar espacios innecesarios.
- Validar que no exista otro vehículo con la misma patente.
- No permitir guardar un registro vacío.
- Mantener un formato consistente.

Ejemplo de normalización:

```powerapps
Upper(
    Trim(txtPatente.Text)
)
```

---

# Validación de Duplicidad

Ejemplo propuesto:

```powerapps
If(
    CountRows(
        Filter(
            Vehiculos;
            Patente = Upper(Trim(txtPatente.Text))
                &&
            ID <> Coalesce(varVehiculoSeleccionado.ID; 0)
        )
    ) > 0;
    Notify(
        "Ya existe un vehículo registrado con esta patente.";
        NotificationType.Error
    )
)
```

La validación debe excluir el registro actual cuando el formulario se encuentre en modo edición.

---

# Campo Código Interno

Control propuesto:

```text
txtCodigoInterno
```

El código interno puede utilizarse como identificador complementario.

Validaciones propuestas:

- Eliminar espacios al inicio y al final.
- Validar duplicidad cuando el negocio lo requiera.
- Mantener formato uniforme.
- Impedir caracteres no válidos, si corresponde.

---

# Sección Características Generales

Esta sección contiene los atributos descriptivos del vehículo.

## Campos Propuestos

| Campo | Tipo | Control sugerido |
|---|---|---|
| Marca | Opción o búsqueda | `cmbMarca` |
| Modelo | Texto o búsqueda | `cmbModelo` / `txtModelo` |
| Año | Número | `txtAnio` |
| Tipo de vehículo | Opción | `cmbTipoVehiculo` |
| Color | Texto u opción | `cmbColor` |
| Número de chasis | Texto | `txtNumeroChasis` |
| Número de motor | Texto | `txtNumeroMotor` |
| Kilometraje | Número | `txtKilometraje` |

> Los campos definitivos deberán confirmarse contra la aplicación original y su fuente de datos.

---

# Campo Marca

Control recomendado:

```text
cmbMarca
```

Items:

```powerapps
Sort(
    colMarcas;
    Nombre;
    SortOrder.Ascending
)
```

Debe permitirse seleccionar una marca válida desde un catálogo.

Cuando la marca no exista, su creación deberá depender de los permisos definidos para el usuario.

---

# Campo Modelo

El modelo podrá depender de la marca seleccionada.

Ejemplo:

```powerapps
Filter(
    colModelos;
    MarcaId = cmbMarca.Selected.ID
)
```

Esto permite impedir combinaciones inválidas entre marca y modelo.

---

# Campo Año

Control propuesto:

```text
txtAnio
```

Validaciones:

- Debe ser numérico.
- Debe tener cuatro dígitos.
- No debe ser menor al año mínimo definido por el negocio.
- No debe exceder de forma injustificada el año actual.

Ejemplo:

```powerapps
If(
    !IsNumeric(txtAnio.Text);
    Notify(
        "El año debe ser numérico.";
        NotificationType.Error
    )
)
```

---

# Campo Tipo de Vehículo

Control recomendado:

```text
cmbTipoVehiculo
```

Valores de ejemplo:

```text
Automóvil

Camioneta

Camión

Furgón

Motocicleta

Otro
```

Los valores definitivos deberán administrarse mediante una lista de opciones o un catálogo independiente.

---

# Campo Kilometraje

Control propuesto:

```text
txtKilometraje
```

Validaciones:

- Solo valores numéricos.
- No permitir valores negativos.
- Verificar que el nuevo kilometraje no sea menor al previamente registrado, salvo autorización.
- Mantener unidad de medida consistente.

Ejemplo:

```powerapps
If(
    Value(txtKilometraje.Text) < 0;
    Notify(
        "El kilometraje no puede ser negativo.";
        NotificationType.Error
    )
)
```

---

# Sección Información Operacional

Esta sección registra la situación operacional actual del vehículo.

## Campos Propuestos

| Campo | Tipo | Descripción |
|---|---|---|
| Estado | Opción | Estado actual del vehículo. |
| Fecha de ingreso | Fecha | Fecha en que se incorporó al sistema. |
| Fecha de disponibilidad | Fecha | Fecha estimada o efectiva de disponibilidad. |
| Estado de ruta | Opción | Estado operacional utilizado por los filtros del sistema. |
| Activo | Sí/No | Indica si el registro continúa vigente. |

---

# Regla de Estados Operacionales

Los estados:

```text
En preparación

En ruta

Entregado
```

no deben modelarse como entidades independientes.

Corresponden a filtros aplicados sobre la tabla o lista principal de vehículos.

Ejemplo conceptual:

```powerapps
Filter(
    colVehiculos;
    EstadoRuta = varEstado
)
```

Por lo tanto, el formulario deberá guardar el estado operacional en el registro del vehículo o en la relación operacional que se defina en el modelo de datos.

---

# Campo Estado

Control propuesto:

```text
cmbEstadoVehiculo
```

Ejemplos de estado general:

```text
Activo

Disponible

En mantenimiento

Fuera de servicio

Inactivo
```

El estado general del vehículo no debe confundirse con el estado de ruta.

---

# Campo Estado de Ruta

Control propuesto:

```text
cmbEstadoRuta
```

Valores identificados para el flujo:

```text
En preparación

En ruta

Entregado
```

Podrá existir además un valor inicial, por ejemplo:

```text
Sin asignar
```

La existencia y nombre exacto de ese estado inicial deberá confirmarse.

---

# Sección Responsable y Ubicación

Esta sección permite identificar quién tiene asignado o administra el vehículo y dónde se encuentra.

## Campos Propuestos

| Campo | Tipo | Control sugerido |
|---|---|---|
| Responsable | Persona o búsqueda | `cmbResponsable` |
| Conductor | Persona o búsqueda | `cmbConductor` |
| Ubicación | Opción o búsqueda | `cmbUbicacion` |
| Sucursal | Opción o búsqueda | `cmbSucursal` |

---

# Campo Responsable

El campo podrá utilizar una columna Persona de SharePoint.

Control:

```text
cmbResponsable
```

Items de ejemplo:

```powerapps
Office365Users.SearchUser(
    {
        searchTerm: cmbResponsable.SearchText;
        top: 25
    }
)
```

La fuente definitiva dependerá de si el responsable corresponde a un usuario corporativo o a una entidad propia de la aplicación.

---

# Campo Ubicación

Control:

```text
cmbUbicacion
```

La ubicación debe seleccionarse desde un catálogo controlado.

Esto evita diferencias como:

```text
Bodega Central

bodega central

Bodega central
```

---

# Sección Observaciones

Control propuesto:

```text
txtObservacionesVehiculo
```

Características:

- Campo de texto multilínea.
- No debe reemplazar campos estructurados.
- Puede registrar información complementaria.
- Debe limitarse a una cantidad razonable de caracteres.
- No debe utilizarse para guardar información crítica que requiera búsqueda o filtrado.

Ejemplo:

```powerapps
MaxLength = 2000
```

---

# Sección Auditoría

Los datos de auditoría deben ser generados automáticamente.

| Campo | Origen |
|---|---|
| Creado | SharePoint |
| Creado por | SharePoint |
| Modificado | SharePoint |
| Modificado por | SharePoint |
| Fecha de registro operacional | Aplicación o SharePoint |
| Usuario de la acción | `User()` o SharePoint |

No deberán ser editables desde el formulario funcional.

---

# Botones del Formulario

## Guardar

Control:

```text
btnGuardarVehiculo
```

Acción general:

```powerapps
SubmitForm(frmVehiculo)
```

---

## Cancelar

Control:

```text
btnCancelarVehiculo
```

Acción:

```powerapps
ResetForm(frmVehiculo);;

ViewForm(frmVehiculo);;

Set(
    varModoFormulario;
    "Consulta"
)
```

---

## Editar

Control:

```text
btnEditarVehiculo
```

Acción:

```powerapps
EditForm(frmVehiculo);;

Set(
    varModoFormulario;
    "Editar"
)
```

---

## Cerrar

El botón Cerrar debe ocultar el panel o regresar al listado sin cambiar el módulo principal.

Ejemplo:

```powerapps
Set(
    varVehiculoSeleccionado;
    Blank()
);;

Set(
    varModoFormulario;
    "Consulta"
)
```

---

# Validación General Antes de Guardar

Antes de ejecutar `SubmitForm`, deberán validarse las reglas adicionales que no estén cubiertas por las propiedades obligatorias del formulario.

Ejemplo:

```powerapps
If(
    IsBlank(Trim(txtPatente.Text));
    Notify(
        "Debe ingresar la patente.";
        NotificationType.Error
    );

    IsBlank(cmbMarca.Selected);
    Notify(
        "Debe seleccionar una marca.";
        NotificationType.Error
    );

    CountRows(
        Filter(
            Vehiculos;
            Patente = Upper(Trim(txtPatente.Text))
                &&
            ID <> Coalesce(varVehiculoSeleccionado.ID; 0)
        )
    ) > 0;
    Notify(
        "La patente ya se encuentra registrada.";
        NotificationType.Error
    );

    SubmitForm(frmVehiculo)
)
```

---

# Evento OnSuccess

Cuando el formulario se guarde correctamente:

```powerapps
Notify(
    If(
        varModoFormulario = "Nuevo";
        "Vehículo registrado correctamente.";
        "Vehículo actualizado correctamente."
    );
    NotificationType.Success
);;

Refresh(Vehiculos);;

Set(
    varVehiculoSeleccionado;
    frmVehiculo.LastSubmit
);;

ViewForm(frmVehiculo);;

Set(
    varModoFormulario;
    "Consulta"
)
```

---

# Evento OnFailure

```powerapps
Notify(
    "No fue posible guardar la información del vehículo. Revise los campos e intente nuevamente.";
    NotificationType.Error
)
```

También deberá evaluarse el contenido de:

```powerapps
frmVehiculo.Error
```

para presentar una explicación más específica cuando sea posible.

---

# Habilitación de Controles

Los campos solo deberán estar habilitados en los modos Nuevo o Editar.

Ejemplo:

```powerapps
DisplayMode =
If(
    varModoFormulario = "Consulta";
    DisplayMode.View;
    DisplayMode.Edit
)
```

---

# Visibilidad de Botones

## Guardar

```powerapps
Visible =
varModoFormulario = "Nuevo"
    ||
varModoFormulario = "Editar"
```

## Cancelar

```powerapps
Visible =
varModoFormulario = "Nuevo"
    ||
varModoFormulario = "Editar"
```

## Editar

```powerapps
Visible =
varModoFormulario = "Consulta"
    &&
!IsBlank(varVehiculoSeleccionado)
```

---

# Prevención de Pérdida de Cambios

Si el formulario contiene cambios sin guardar, la aplicación deberá evitar cerrar el detalle de manera accidental.

Propiedad útil:

```powerapps
frmVehiculo.Unsaved
```

Ejemplo:

```powerapps
If(
    frmVehiculo.Unsaved;
    Set(
        varMostrarConfirmacionSalida;
        true
    );
    Set(
        varVehiculoSeleccionado;
        Blank()
    )
)
```

---

# Confirmación de Cancelación

```text
Existen cambios sin guardar.

¿Desea descartarlos?

[Continuar editando]

[Descartar cambios]
```

---

# Reglas Iniciales del Formulario

| Código | Regla |
|---|---|
| RV-FOR-001 | La patente no puede quedar vacía. |
| RV-FOR-002 | No deben existir dos vehículos activos con la misma patente. |
| RV-FOR-003 | Los campos de catálogo deben seleccionarse desde valores válidos. |
| RV-FOR-004 | El kilometraje no puede ser negativo. |
| RV-FOR-005 | Los datos de auditoría no son editables. |
| RV-FOR-006 | En modo consulta los campos deben permanecer bloqueados. |
| RV-FOR-007 | Los cambios deben confirmarse antes de abandonar el formulario. |
| RV-FOR-008 | El estado de ruta se almacena como atributo del vehículo o de su operación asociada. |
| RV-FOR-009 | En preparación, En ruta y Entregado funcionan como filtros, no como tablas independientes. |

---

# Campos Pendientes de Confirmación

| Estado | Campo o regla | Observación |
|---|---|---|
| ❓ | Código interno | Confirmar existencia y obligatoriedad. |
| ❓ | Número de chasis | Confirmar si se administra en la aplicación actual. |
| ❓ | Número de motor | Confirmar si se administra en la aplicación actual. |
| ❓ | Kilometraje | Confirmar si corresponde al registro maestro o a otra operación. |
| ❓ | Conductor | Confirmar si es parte del vehículo o de una asignación. |
| ❓ | Responsable | Confirmar fuente y relación. |
| ❓ | Estado general | Identificar catálogo exacto. |
| ❓ | Estado inicial de ruta | Confirmar nombre y comportamiento. |
| ❓ | Fecha de ingreso | Confirmar si es ingresada por el usuario o automática. |
| ❓ | Campos obligatorios | Validar contra la aplicación de referencia. |

---

# Próxima Parte

**Parte 4 de 8**

Se documentará:

- Fotografías del vehículo.
- Imagen principal.
- Galería de imágenes.
- Documentos adjuntos.
- Carga, consulta y eliminación de archivos.
- Estructura recomendada en SharePoint.
- Validaciones de formato y tamaño.
- Componentes multimedia en Power Apps.
