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

# 3B APP
# Módulo Vehículos

**Versión:** 1.0

**Documento:** 04_Modulo_Vehiculos.md

**Parte:** 4 de 8

---

# Fotografías y Archivos Asociados

Esta parte documenta el tratamiento de la imagen principal del vehículo y de los archivos asociados a los procesos operacionales relacionados.

La evidencia disponible permite distinguir dos tipos de contenido:

1. Fotografía principal del vehículo.
2. Archivos asociados a registros operacionales, como cotización, MOP, OC, OT, Packing List y Plan de Amarre.

No se ha confirmado que los documentos operacionales se almacenen directamente en el registro maestro del vehículo.

---

# Fuentes Revisadas

La documentación de esta parte utiliza las siguientes fuentes:

| Estado | Fuente | Información obtenida |
|---|---|---|
| ✅ | Video `ModuloVehiculos(1).mp4` | Imagen principal, miniaturas, formulario de edición y acción `Retake`. |
| ✅ | Video `ModuloVehiculos(1).mp4` | Visualización y apertura de archivos asociados a procesos operacionales. |
| 🎧 | Audios de levantamiento | El módulo Vehículos debe utilizarse como mantenedor principal para replicar comportamientos. |
| ❓ | Configuración interna de AppSheet | No fue proporcionada y no puede determinarse desde el video. |
| ❓ | Fuente de datos actual | No se observan las tablas ni carpetas utilizadas internamente. |

---

# Imagen Principal del Vehículo

Cada vehículo dispone de una imagen principal utilizada para facilitar su identificación visual.

La imagen se observa en los siguientes lugares:

- Como miniatura dentro del listado de vehículos.
- En el formulario de edición.
- Como referencia visual del registro seleccionado.

---

# Comportamiento Observado

| Estado | Comportamiento |
|---|---|
| ✅ | El listado muestra una miniatura asociada a cada vehículo. |
| ✅ | La miniatura aparece junto al modelo o nombre del vehículo. |
| ✅ | Al editar un vehículo se muestra una imagen de mayor tamaño. |
| ✅ | Existe una acción denominada `Retake`. |
| ✅ | La imagen puede mantenerse mientras se modifican otros datos. |
| ❓ | No se confirma si la imagen puede cargarse desde un archivo local. |
| ❓ | No se confirma si `Retake` abre exclusivamente la cámara o también permite seleccionar un archivo. |
| ❓ | No se confirma si es posible eliminar la imagen sin reemplazarla. |
| ❓ | No se observan varias imágenes asociadas al mismo vehículo. |

---

# Flujo de Consulta de Imagen

```text
Usuario ingresa a Vehículos

↓

Sistema carga el listado

↓

Cada registro muestra su miniatura

↓

Usuario selecciona o edita un vehículo

↓

Sistema muestra la imagen principal ampliada

# 3B APP
# Módulo Vehículos

**Versión:** 1.0

**Documento:** 04_Modulo_Vehiculos.md

**Parte:** 5 de 8

---

# Relaciones Operacionales del Vehículo

Esta parte documenta cómo un vehículo se relaciona con los distintos procesos operacionales observados en la aplicación.

Las relaciones se visualizan mediante registros denominados **Inicio Inline** y mediante secciones asociadas a:

- Cotización.
- MOP.
- OC.
- OT.
- Packing List.
- Plan de Amarre.

Estas relaciones permiten consultar el historial operacional de un vehículo sin abandonar el módulo Vehículos.

---

# Fuentes Revisadas

| Estado | Fuente | Información obtenida |
|---|---|---|
| ✅ | Video `ModuloVehiculos(1).mp4` | Listado de inicios asociados a cada vehículo. |
| ✅ | Video `ModuloVehiculos(1).mp4` | Panel lateral denominado `Detalles de inicio`. |
| ✅ | Video `ModuloVehiculos(1).mp4` | Indicadores de equipo, origen, destino y estados operacionales. |
| ✅ | Video `ModuloVehiculos(1).mp4` | Secciones relacionadas de Cotización, MOP, OC, OT, Packing List y Plan de Amarre. |
| 🎧 | Audios de levantamiento | Preparación, En ruta y Entregado corresponden a filtros aplicados sobre una misma entidad operacional. |
| ❓ | Configuración interna de AppSheet | No se dispone de las tablas, referencias ni expresiones internas. |

---

# Concepto de Inicio Inline

`Inicio Inline` representa un registro operacional relacionado con un vehículo.

Un mismo vehículo puede participar en más de un inicio u operación.

Ejemplo observado:

```text
Vehículo

↓

LTM 1650

↓

Inicio Inline

├── Operación 1
├── Operación 2
└── Operación 3

# 3B APP
# Módulo Vehículos

**Versión:** 1.0

**Documento:** 04_Modulo_Vehiculos.md

**Parte:** 5 de 8

---

# Relaciones Operacionales del Vehículo

Esta parte documenta cómo un vehículo se relaciona con los distintos procesos operacionales observados en la aplicación.

Las relaciones se visualizan mediante registros denominados **Inicio Inline** y mediante secciones asociadas a:

- Cotización.
- MOP.
- OC.
- OT.
- Packing List.
- Plan de Amarre.

Estas relaciones permiten consultar el historial operacional de un vehículo sin abandonar el módulo Vehículos.

---

# Fuentes Revisadas

| Estado | Fuente | Información obtenida |
|---|---|---|
| ✅ | Video `ModuloVehiculos(1).mp4` | Listado de inicios asociados a cada vehículo. |
| ✅ | Video `ModuloVehiculos(1).mp4` | Panel lateral denominado `Detalles de inicio`. |
| ✅ | Video `ModuloVehiculos(1).mp4` | Indicadores de equipo, origen, destino y estados operacionales. |
| ✅ | Video `ModuloVehiculos(1).mp4` | Secciones relacionadas de Cotización, MOP, OC, OT, Packing List y Plan de Amarre. |
| 🎧 | Audios de levantamiento | Preparación, En ruta y Entregado corresponden a filtros aplicados sobre una misma entidad operacional. |
| ❓ | Configuración interna de AppSheet | No se dispone de las tablas, referencias ni expresiones internas. |

---

# Concepto de Inicio Inline

`Inicio Inline` representa un registro operacional relacionado con un vehículo.

Un mismo vehículo puede participar en más de un inicio u operación.

```text
Vehículo

↓

Inicios relacionados

├── Operación 1
├── Operación 2
└── Operación 3
```

Cada inicio contiene información relacionada con el traslado o servicio realizado.

---

# Relación General

```text
Vehículo

    │

    └── Inicios relacionados

            │

            ├── Cotización
            ├── MOP
            ├── OC
            ├── OT
            ├── Packing List
            └── Plan de Amarre
```

La relación observada corresponde a:

```text
Un vehículo

↓

Puede tener varios inicios

↓

Cada inicio puede tener diferentes documentos y procesos asociados
```

---

# Flujo de Navegación

```text
Usuario ingresa a Vehículos

↓

Selecciona un vehículo

↓

Sistema muestra los inicios relacionados

↓

Usuario selecciona un inicio

↓

Sistema abre Detalles de inicio

↓

Usuario consulta estados y documentos asociados
```

---

# Listado de Inicios

Al seleccionar un vehículo, la aplicación presenta una vista con sus registros `Inicio Inline`.

Los campos observados incluyen:

| Estado | Campo |
|---|---|
| ✅ | Origen |
| ✅ | Entregado |
| ✅ | Fecha |
| ✅ | Modelo |
| ✅ | N.º Interno |
| ✅ | Fecha Origen |
| ✅ | Destino |
| ✅ | Fecha Destino |
| ✅ | Preparación |
| ❓ | Otros campos disponibles mediante desplazamiento horizontal |

La presencia exacta de algunos campos puede depender del ancho disponible y del desplazamiento horizontal.

---

# Búsqueda y Filtros de Inicios

Cuando el usuario navega al listado de inicios, el buscador superior cambia su contexto a:

```text
Buscar Inicio Inline
```

Esto indica que la búsqueda se aplica a los registros operacionales visibles y no al listado maestro de vehículos.

Entre los filtros observados se encuentran:

- IDInicio.
- Fecha.
- Modelo.
- N.º Interno.
- Origen.
- Fecha Origen.
- Destino.
- Fecha Destino.
- Preparación.

---

# Reglas de Contexto

| Código | Estado | Regla |
|---|---|---|
| RV-INI-001 | ✅ | Los inicios visibles deben pertenecer al vehículo seleccionado. |
| RV-INI-002 | ✅ | La búsqueda se aplica al listado actualmente visible. |
| RV-INI-003 | ✅ | El usuario puede seleccionar un inicio para consultar su detalle. |
| RV-INI-004 | ✅ | Un vehículo puede mostrar varios inicios relacionados. |
| RV-INI-005 | ⚠️ | Al cambiar de vehículo debe limpiarse el inicio seleccionado. |
| RV-INI-006 | ⚠️ | No debe mostrarse información de un inicio perteneciente a otro vehículo. |

---

# Panel Detalles de Inicio

Al seleccionar un inicio se abre un panel lateral denominado:

```text
Detalles de inicio
```

Este panel concentra:

- Resumen operacional.
- Identificación del inicio.
- Cotización.
- MOP.
- OC.
- OT.
- Packing List.
- Plan de Amarre.

La disponibilidad de cada sección depende de los registros asociados.

---

# Resumen Operacional

En la parte superior del detalle se observan indicadores de:

- Equipo.
- Origen.
- Destino.
- En Preparación.
- En Ruta.
- Entregado.

La aplicación utiliza colores e iconos para representar su estado.

| Estado visual | Interpretación observada |
|---|---|
| Verde | Elemento disponible, completado o afirmativo. |
| Rojo | Elemento pendiente, no disponible o negativo. |
| Azul | Información o acceso al equipo relacionado. |

> ⚠️ La interpretación exacta debe confirmarse con el negocio antes de definir la regla definitiva de colores.

---

# Identificador del Inicio

El panel muestra un campo:

```text
IDInicio
```

Este valor identifica la operación seleccionada. Se observó, por ejemplo, el valor `3B14`.

La estructura definitiva del identificador y su mecanismo de generación se encuentran pendientes de confirmación.

---

# Cotización Asociada

El detalle del inicio puede contener una o más cotizaciones.

El número ubicado junto al título indica la cantidad de registros relacionados.

```text
COTIZACIÓN 1
```

Campos observados:

| Estado | Campo |
|---|---|
| ✅ | Número de cotización |
| ✅ | ID de cotización |
| ✅ | Fecha |
| ✅ | Estado |
| ✅ | Acceso al documento |
| ❓ | Otros campos mediante desplazamiento horizontal |

Se observaron estados como `CARGADO` y `Aprobado`.

Las acciones visibles incluyen consultar, abrir el documento, expandir el listado y agregar una cotización.

---

# MOP Asociado

El detalle puede contener registros MOP relacionados con el inicio.

Se observa:

- Contador de registros.
- Listado relacionado.
- Acción `Agregar`.
- Acción `Expand`.
- Acceso al detalle cuando existe información.

Los campos definitivos deberán consolidarse en el documento específico del módulo MOP.

---

# OC Asociada

El inicio puede contener una o más órdenes de compra.

Campos observados:

| Estado | Campo |
|---|---|
| ✅ | Fecha |
| ✅ | Número OC |
| ✅ | Comentarios |
| ✅ | Acceso a documento |
| ❓ | Estado exacto de la OC |
| ❓ | Proveedor |
| ❓ | Monto |
| ❓ | Moneda |

Acciones visibles:

```text
Expand

Agregar
```

---

# OT Asociada

El detalle dispone de una sección `OT` con un contador de registros relacionados.

Cuando no existen registros se presenta:

```text
OT 0

No items

Agregar
```

Los campos específicos de la OT no se observan completamente en el video.

---

# Packing List Asociado

El detalle puede contener uno o más Packing List.

Se observan campos como:

| Estado | Campo |
|---|---|
| ✅ | Número PL |
| ✅ | Estado PL |
| ✅ | Fecha |
| ✅ | Archivo PL |
| ❓ | Comentarios |
| ❓ | Responsable |
| ❓ | Versión |

Se observó el estado `CARGADO` y un control que permite identificar el archivo asociado.

---

# Plan de Amarre Asociado

El detalle contiene una sección `PLAN DE AMARRE`.

La cabecera muestra la cantidad de registros relacionados.

```text
PLAN DE AMARRE 0
```

Cuando no existen registros se presenta `No items` y se mantiene disponible la acción `Agregar`.

También se observó un listado con información como:

- Identificador.
- Origen.
- Fecha.
- Estado.
- Número relacionado.

Los nombres definitivos de las columnas deberán confirmarse en el documento específico del Plan de Amarre.

---

# Contadores de Registros

Cada sección relacionada muestra un contador.

```text
COTIZACIÓN 1

OC 1

OT 0

PLAN DE AMARRE 0
```

El contador representa la cantidad de registros relacionados con el inicio seleccionado.

Ejemplo propuesto para Power Apps:

```powerapps
CountRows(
    Filter(
        colCotizaciones;
        InicioId = varInicioSeleccionado.ID
    )
)
```

> La fórmula es una propuesta y deberá adaptarse al modelo definitivo.

---

# Estado Sin Registros

Cuando una sección no tiene información, la aplicación muestra `No items` y permite iniciar la creación mediante `Agregar`.

```text
Contador = 0

↓

Mostrar No items

↓

Mantener disponible Agregar
```

---

# Acción Agregar

La acción `Agregar` crea un registro relacionado con el inicio seleccionado.

```text
Usuario selecciona un inicio

↓

Selecciona Agregar en una sección

↓

Sistema abre el formulario correspondiente

↓

La relación con el inicio se completa automáticamente

↓

Usuario guarda el registro

↓

Sistema actualiza el listado y el contador
```

---

# Reglas de Asociación Automática

| Código | Estado | Regla |
|---|---|---|
| RV-REL-001 | ⚠️ | El nuevo registro debe asociarse automáticamente al inicio seleccionado. |
| RV-REL-002 | ⚠️ | El vehículo relacionado debe obtenerse desde el inicio. |
| RV-REL-003 | ⚠️ | El usuario no debe modificar manualmente identificadores internos. |
| RV-REL-004 | ⚠️ | Después de guardar debe actualizarse la sección correspondiente. |
| RV-REL-005 | ⚠️ | Después de guardar debe actualizarse el contador. |

---

# Acción Expand

La acción `Expand` permite acceder a una vista más amplia del listado relacionado.

```text
Usuario selecciona Expand

↓

Sistema abre el listado completo

↓

Usuario consulta y selecciona un registro

↓

Sistema muestra su detalle
```

---

# Navegación Jerárquica

La aplicación utiliza paneles laterales y una ruta de navegación.

Ejemplos observados:

```text
Vehículos > LTM 1650 > Inicio Inline
```

```text
Vehículos > CONTENEDOR 20 FT > Inicio Inline
```

Esta ruta identifica:

1. El módulo actual.
2. El vehículo seleccionado.
3. La relación o vista abierta.

---

# Propuesta para Power Apps

Variables propuestas:

```text
varVehiculoSeleccionado

varInicioSeleccionado

varRelacionSeleccionada

varRegistroRelacionado

varPanelDetalle
```

Selección del vehículo:

```powerapps
Set(
    varVehiculoSeleccionado;
    ThisItem
);;

Set(
    varInicioSeleccionado;
    Blank()
);;

Set(
    varPanelDetalle;
    "Inicios"
)
```

Selección del inicio:

```powerapps
Set(
    varInicioSeleccionado;
    ThisItem
);;

Set(
    varPanelDetalle;
    "DetalleInicio"
)
```

---

# Containers Propuestos

```text
conVehiculos

│

├── conListadoVehiculos

├── conIniciosVehiculo

└── conDetalleInicio

      ├── conResumenInicio
      ├── conCotizacionesInicio
      ├── conMopInicio
      ├── conOcInicio
      ├── conOtInicio
      ├── conPackingListInicio
      └── conPlanAmarreInicio
```

---

# Galerías Propuestas

```text
galIniciosVehiculo

galCotizacionesInicio

galMopInicio

galOcInicio

galOtInicio

galPackingListInicio

galPlanAmarreInicio
```

---

# Componente Reutilizable

Cada sección relacionada presenta el patrón:

```text
Título

Contador

Listado

Expand

Agregar
```

Se propone implementar:

```text
cmpRelacionOperacional
```

Entradas propuestas:

- Título.
- Cantidad.
- Colección.
- Permitir agregar.
- Permitir expandir.

Salidas propuestas:

- Registro seleccionado.
- Agregar seleccionado.
- Expandir seleccionado.

---

# Modelo de Datos Conceptual

```text
Vehiculo
   │
   │ 1
   │
   └──────── N Inicio
                  │
                  ├──────── N Cotizacion
                  ├──────── N MOP
                  ├──────── N OC
                  ├──────── N OT
                  ├──────── N PackingList
                  └──────── N PlanAmarre
```

Este modelo corresponde a una interpretación basada en el comportamiento visible. La cardinalidad definitiva deberá confirmarse revisando la fuente de datos actual.

---

# Estructura SharePoint Propuesta

## Lista Vehículos

```text
Vehiculos
```

## Lista Inicios

```text
Inicios
```

Campos iniciales propuestos:

| Campo | Tipo |
|---|---|
| ID | Número generado |
| CodigoInicio | Texto |
| VehiculoId | Búsqueda |
| OrigenId | Búsqueda |
| DestinoId | Búsqueda |
| Fecha | Fecha |
| FechaOrigen | Fecha |
| FechaDestino | Fecha |
| EstadoPreparacion | Sí/No o elección |
| EstadoRuta | Sí/No o elección |
| EstadoEntregado | Sí/No o elección |

Listas relacionadas propuestas:

```text
Cotizaciones

MOP

OrdenesCompra

OrdenesTrabajo

PackingLists

PlanesAmarre
```

Cada lista deberá contener una referencia al inicio mediante `InicioId` y, cuando resulte necesario para las consultas, `VehiculoId`.

> ⚠️ La necesidad de almacenar ambas referencias deberá evaluarse para evitar duplicidad e inconsistencias.

---

# Reglas Operacionales Iniciales

| Código | Estado | Regla |
|---|---|---|
| RV-OP-001 | ✅ | Un vehículo puede presentar varios inicios relacionados. |
| RV-OP-002 | ✅ | Cada inicio puede mostrar cotizaciones y documentos relacionados. |
| RV-OP-003 | ✅ | Las secciones muestran la cantidad de registros asociados. |
| RV-OP-004 | ✅ | Una sección vacía muestra `No items`. |
| RV-OP-005 | ✅ | Las secciones vacías pueden mantener disponible la acción `Agregar`. |
| RV-OP-006 | ✅ | Existe navegación desde el vehículo hasta el detalle del inicio. |
| RV-OP-007 | 🎧 | Preparación, En ruta y Entregado corresponden a estados o filtros de una misma entidad operacional. |
| RV-OP-008 | ⚠️ | Los registros creados desde un inicio deben conservar automáticamente la relación. |
| RV-OP-009 | ⚠️ | Los contadores deben actualizarse después de agregar o modificar un registro. |
| RV-OP-010 | ⚠️ | El cierre del panel debe limpiar la selección correspondiente. |

---

# Elementos No Confirmados

No existe evidencia suficiente para confirmar:

- Si un inicio puede relacionarse con más de un vehículo.
- Si una cotización puede utilizarse en varios inicios.
- Si existe aprobación por niveles.
- Si los estados cambian automáticamente.
- Si la carga de un documento modifica el estado.
- Si existe historial de cambios.
- Si existen notificaciones.
- Si existen flujos automáticos.
- Si los registros pueden eliminarse.
- Si las relaciones cambian según el perfil del usuario.
- Si todos los tipos de vehículo utilizan los mismos procesos.

---

# Pendientes de Confirmación

| Estado | Elemento | Observación |
|---|---|---|
| ❓ | Definición formal de Inicio | Confirmar significado de negocio. |
| ❓ | Cardinalidad vehículo-inicio | Confirmar si siempre corresponde a uno a muchos. |
| ❓ | Campos completos | Revisar tablas o capturas adicionales. |
| ❓ | Estados de Cotización | Confirmar catálogo completo. |
| ❓ | Estados de MOP | Confirmar catálogo completo. |
| ❓ | Estados de OC | Confirmar catálogo completo. |
| ❓ | Estados de OT | Confirmar catálogo completo. |
| ❓ | Estados de Packing List | Confirmar catálogo completo. |
| ❓ | Estados de Plan de Amarre | Confirmar catálogo completo. |
| ❓ | Permisos de creación | Confirmar perfiles autorizados. |
| ❓ | Eliminación | No probar en producción. |
| ❓ | Automatizaciones | Confirmar si existen acciones posteriores al guardado. |

---

# Resumen de Evidencia

| Funcionalidad | Estado |
|---|---|
| Vehículo con varios inicios | ✅ Confirmado |
| Listado Inicio Inline | ✅ Confirmado |
| Detalles de inicio | ✅ Confirmado |
| Equipo, origen y destino | ✅ Confirmado |
| Estados Preparación, Ruta y Entregado | ✅ Confirmado |
| Cotización relacionada | ✅ Confirmado |
| MOP relacionado | ✅ Confirmado |
| OC relacionada | ✅ Confirmado |
| OT relacionada | ✅ Confirmado |
| Packing List relacionado | ✅ Confirmado |
| Plan de Amarre relacionado | ✅ Confirmado |
| Contadores por sección | ✅ Confirmado |
| Acción Agregar | ✅ Confirmado visualmente |
| Acción Expand | ✅ Confirmado visualmente |
| Eliminación de relaciones | ❓ No probada |
| Automatizaciones | ❓ No confirmadas |
| Estructura física de datos | ❓ No confirmada |

---

# Próxima Parte

**Parte 6 de 8**

Se documentará:

- Estados operacionales.
- En Preparación.
- En Ruta.
- Entregado.
- Relación entre los tres estados.
- Filtros del menú.
- Transiciones observadas.
- Indicadores visuales.
- Reglas de consistencia.
- Propuesta de implementación en Power Apps.


# 3B APP
# Módulo Vehículos

**Versión:** 1.0

**Documento:** 04_Modulo_Vehiculos.md

**Parte:** 6 de 8

---

# Estados Operacionales

Esta parte documenta los estados operacionales relacionados con los vehículos y sus registros de inicio.

Los estados principales observados son:

- En Preparación.
- En Ruta.
- Entregado.

Estos nombres aparecen como opciones independientes en el menú, pero no corresponden a tres mantenedores ni a tres entidades diferentes.

De acuerdo con el levantamiento realizado, las tres opciones muestran registros de una misma entidad operacional aplicando un filtro distinto según su estado.

---

# Fuentes Revisadas

| Estado | Fuente | Información obtenida |
|---|---|---|
| ✅ | Video `ModuloVehiculos(1).mp4` | Opciones `EN PREPARACIÓN`, `EN RUTA` y `ENTREGADO` en el menú. |
| ✅ | Video `ModuloVehiculos(1).mp4` | Indicadores visuales de preparación, ruta y entrega dentro del detalle operacional. |
| ✅ | Video `ModuloVehiculos(1).mp4` | Registros `Inicio Inline` relacionados con cada vehículo. |
| 🎧 | Audio de levantamiento del 17-07-2026 | Las tres opciones utilizan la misma lista y solamente filtran por estado. |
| 🎧 | Audio de levantamiento del 17-07-2026 | No existen tres mantenedores independientes. |
| ❓ | Configuración AppSheet | No se proporcionaron las expresiones que calculan los estados. |

---

# Regla Funcional Principal

```text
Entidad operacional única

        │

        ├── Filtro: En Preparación
        ├── Filtro: En Ruta
        └── Filtro: Entregado
```

Por tanto:

```text
En Preparación ≠ Tabla independiente

En Ruta ≠ Tabla independiente

Entregado ≠ Tabla independiente
```

Las tres opciones deben consultar la misma fuente y presentar solamente los registros que cumplen el criterio seleccionado.

---

# Entidad Operacional

En esta documentación se utilizará provisionalmente el nombre:

```text
Inicio
```

Este nombre proviene de la vista observada `Inicio Inline`.

La denominación de negocio definitiva se encuentra pendiente de confirmación.

Cada inicio se relaciona con un vehículo y contiene información del movimiento u operación correspondiente.

---

# Modelo Conceptual

```text
Vehículo

    │

    └── Inicio u operación

            │

            ├── Preparación
            ├── Ruta
            └── Entrega
```

Los estados pertenecen al inicio o a la operación relacionada, no necesariamente al registro maestro del vehículo.

---

# Diferencia entre Estado del Vehículo y Estado Operacional

El video muestra dos conceptos diferentes.

## Estado del vehículo

Describe la disponibilidad general del equipo.

Estados observados:

- Disponible.
- En Taller.
- Fuera de servicio.

## Estado operacional

Describe el avance de un inicio, traslado o servicio.

Estados observados:

- En Preparación.
- En Ruta.
- Entregado.

---

# Regla de Separación

```text
Estado del vehículo

Disponible / En Taller / Fuera de servicio

        ≠

Estado de la operación

En Preparación / En Ruta / Entregado
```

Esta diferencia debe conservarse en Power Apps y SharePoint para evitar que el estado de una operación modifique incorrectamente la condición general del vehículo.

---

# En Preparación

La opción `EN PREPARACIÓN` muestra los registros que se encuentran en la etapa de preparación operacional.

Su objetivo es permitir identificar las operaciones que todavía no han iniciado su ruta.

---

# Comportamiento de En Preparación

```text
Usuario selecciona EN PREPARACIÓN

↓

Sistema conserva la fuente de datos operacional

↓

Aplica filtro de preparación

↓

Muestra solamente registros en esa condición
```

---

# Información Visible en Preparación

El video muestra indicadores de estado dentro del resumen operacional y del listado principal.

Entre los elementos relacionados se encuentran:

- Equipo.
- Fecha.
- Origen.
- Destino.
- Indicador de preparación.
- Indicador de ruta.
- Indicador de entrega.
- Acciones relacionadas con documentos.

La composición exacta de la vista `EN PREPARACIÓN` deberá confirmarse con capturas específicas de esa opción.

---

# En Ruta

La opción `EN RUTA` muestra los registros cuya operación se encuentra en traslado o ejecución.

No corresponde a un mantenedor separado.

---

# Comportamiento de En Ruta

```text
Usuario selecciona EN RUTA

↓

Sistema consulta la misma entidad operacional

↓

Aplica filtro de ruta

↓

Muestra solamente registros en ruta
```

---

# Entregado

La opción `ENTREGADO` muestra los registros cuya operación aparece marcada como entregada.

El video permite observar el valor:

```text
ENTREGADO
```

en el listado de `Inicio Inline` y un indicador de entrega dentro del detalle operacional.

---

# Comportamiento de Entregado

```text
Usuario selecciona ENTREGADO

↓

Sistema consulta la misma entidad operacional

↓

Aplica filtro de entrega

↓

Muestra solamente registros entregados
```

---

# Indicadores del Detalle

En el panel `Detalles de inicio` se observan indicadores para:

```text
En Preparación

En Ruta

Entregado
```

Los indicadores permiten reconocer el estado del registro seleccionado sin depender exclusivamente de la vista del menú.

---

# Colores e Iconos

La aplicación utiliza iconografía y colores para representar los estados.

| Estado visual | Interpretación observada |
|---|---|
| Verde | Estado afirmativo, disponible o completado. |
| Rojo | Estado negativo, pendiente o no completado. |
| Azul | Información o referencia al equipo. |

> ⚠️ La equivalencia exacta de cada color debe validarse con el negocio antes de implementarla como regla definitiva.

---

# Estados Independientes o Secuenciales

El video muestra indicadores separados para Preparación, Ruta y Entrega.

Sin embargo, no existe evidencia suficiente para asegurar si los estados:

- Se calculan automáticamente.
- Se actualizan manualmente.
- Se habilitan al cargar determinados documentos.
- Se comportan como una secuencia obligatoria.
- Pueden permanecer activos simultáneamente.
- Guardan fecha y usuario de cada cambio.

Por esta razón, la secuencia siguiente se considera conceptual:

```text
En Preparación

↓

En Ruta

↓

Entregado
```

No debe implementarse como automatización hasta confirmar sus reglas.

---

# Posibles Representaciones del Estado

Existen al menos dos formas posibles de representar los estados.

## Alternativa A: estado único

```text
EstadoOperacion

Preparación
Ruta
Entregado
```

En esta alternativa solamente puede existir un estado activo.

## Alternativa B: indicadores independientes

```text
EnPreparacion = Sí/No

EnRuta = Sí/No

Entregado = Sí/No
```

En esta alternativa pueden existir varios indicadores afirmativos simultáneamente.

---

# Decisión Pendiente del Modelo

El video muestra visualmente varios indicadores simultáneos, pero no permite determinar la estructura interna que los origina.

Por tanto:

| Estado | Decisión |
|---|---|
| ✅ | Las tres opciones del menú consultan una misma entidad. |
| ✅ | Cada opción aplica un filtro diferente. |
| ❓ | No se confirma si existe un campo único o tres indicadores. |
| ❓ | No se confirma si los valores son manuales o calculados. |
| ❓ | No se confirma si la secuencia es obligatoria. |

---

# Filtros del Menú

El menú debe actuar como selector de vista.

Variable propuesta:

```text
varVistaOperacional
```

Valores propuestos:

```text
Preparacion

Ruta

Entregado
```

---

# Selección de En Preparación

```powerapps
Set(
    varVistaOperacional;
    "Preparacion"
)
```

---

# Selección de En Ruta

```powerapps
Set(
    varVistaOperacional;
    "Ruta"
)
```

---

# Selección de Entregado

```powerapps
Set(
    varVistaOperacional;
    "Entregado"
)
```

---

# Filtro Propuesto con Estado Único

Si el modelo definitivo utiliza un solo campo de estado:

```powerapps
Switch(
    varVistaOperacional;
    "Preparacion";
        Filter(colInicios; EstadoOperacion.Value = "En Preparación");
    "Ruta";
        Filter(colInicios; EstadoOperacion.Value = "En Ruta");
    "Entregado";
        Filter(colInicios; EstadoOperacion.Value = "Entregado");
    colInicios
)
```

> ⚠️ Los nombres de columnas y valores son propuestos.

---

# Filtro Propuesto con Indicadores Independientes

Si el modelo definitivo utiliza tres indicadores:

```powerapps
Switch(
    varVistaOperacional;
    "Preparacion";
        Filter(colInicios; EnPreparacion = true);
    "Ruta";
        Filter(colInicios; EnRuta = true);
    "Entregado";
        Filter(colInicios; Entregado = true);
    colInicios
)
```

> ⚠️ Esta fórmula no debe considerarse definitiva hasta confirmar el modelo de datos.

---

# Reutilización de la Vista

No se deben construir tres galerías ni tres pantallas independientes si presentan la misma estructura.

Se propone reutilizar:

```text
galOperaciones
```

y cambiar únicamente su origen según:

```text
varVistaOperacional
```

---

# Arquitectura Propuesta

```text
scrPrincipal

│

└── conOperacion

      ├── cmpMenu
      ├── cmpEncabezadoOperacion
      ├── cmpFiltrosOperacion
      ├── galOperaciones
      └── conDetalleOperacion
```

La misma galería deberá utilizarse para las tres opciones del menú.

---

# Encabezado Dinámico

El título de la vista puede depender del filtro seleccionado.

```powerapps
Switch(
    varVistaOperacional;
    "Preparacion"; "En Preparación";
    "Ruta"; "En Ruta";
    "Entregado"; "Entregado";
    "Operaciones"
)
```

---

# Búsqueda Combinada con Estado

La búsqueda deberá aplicarse después del filtro operacional o combinar ambos criterios.

Ejemplo conceptual:

```powerapps
Filter(
    colInicios;
    EstadoOperacion.Value = varVistaOperacional;
    IsBlank(txtBuscarOperacion.Text)
        || StartsWith(Modelo; txtBuscarOperacion.Text)
        || StartsWith(Origen; txtBuscarOperacion.Text)
        || StartsWith(Destino; txtBuscarOperacion.Text)
)
```

> ⚠️ La fórmula deberá ajustarse al tipo real de las columnas SharePoint.

---

# Contadores del Menú

No se observan contadores junto a las tres opciones del menú.

Si el negocio los solicita, podrían calcularse sin crear fuentes independientes.

```powerapps
CountRows(
    Filter(
        colInicios;
        EstadoOperacion.Value = "En Ruta"
    )
)
```

Esta funcionalidad se considera propuesta, no observada.

---

# Cambio de Estado

El video no muestra la ejecución completa de un cambio entre preparación, ruta y entrega.

Por ello no se puede confirmar:

- Qué botón inicia el cambio.
- Qué campos son obligatorios.
- Qué perfil está autorizado.
- Si se exige una fecha.
- Si se exige documentación.
- Si existe confirmación.
- Si el cambio puede revertirse.

---

# Validaciones Propuestas para un Cambio de Estado

Antes de cambiar un estado se debería validar, como mínimo:

- Existencia del inicio.
- Existencia del vehículo relacionado.
- Permisos del usuario.
- Estado actual válido.
- Fecha del cambio.
- Consistencia entre preparación, ruta y entrega.
- Documentación requerida, cuando el negocio lo confirme.

Estas validaciones son propuestas y no deben activarse hasta obtener las reglas definitivas.

---

# Auditoría Propuesta

Para mantener trazabilidad se propone registrar:

| Campo | Propósito |
|---|---|
| EstadoAnterior | Valor antes del cambio. |
| EstadoNuevo | Valor posterior. |
| FechaCambio | Fecha y hora. |
| UsuarioCambio | Usuario responsable. |
| InicioId | Operación modificada. |
| Observacion | Motivo o comentario. |

La existencia de este historial no se confirmó en la aplicación original.

---

# Propuesta SharePoint

La definición final depende de si el estado es único o se representa mediante indicadores.

## Modelo con estado único

Lista:

```text
Inicios
```

Columnas:

| Columna | Tipo propuesto |
|---|---|
| EstadoOperacion | Elección |
| FechaPreparacion | Fecha y hora |
| FechaInicioRuta | Fecha y hora |
| FechaEntrega | Fecha y hora |

## Modelo con indicadores

| Columna | Tipo propuesto |
|---|---|
| EnPreparacion | Sí/No |
| EnRuta | Sí/No |
| Entregado | Sí/No |
| FechaPreparacion | Fecha y hora |
| FechaInicioRuta | Fecha y hora |
| FechaEntrega | Fecha y hora |

> ❓ La selección entre ambos modelos queda pendiente de confirmar la estructura real y las reglas del negocio.

---

# Reglas Iniciales

| Código | Estado | Regla |
|---|---|---|
| RV-EST-001 | 🎧 | En Preparación, En Ruta y Entregado utilizan una misma entidad operacional. |
| RV-EST-002 | 🎧 | Las opciones del menú aplican filtros diferentes sobre la misma lista. |
| RV-EST-003 | ✅ | Los estados se muestran mediante indicadores visuales. |
| RV-EST-004 | ✅ | El estado Entregado aparece en los registros `Inicio Inline`. |
| RV-EST-005 | ✅ | El vehículo posee además un estado general independiente. |
| RV-EST-006 | ⚠️ | El cambio de vista no debe perder el registro maestro del vehículo. |
| RV-EST-007 | ⚠️ | La selección debe limpiarse si deja de cumplir el filtro activo. |
| RV-EST-008 | ⚠️ | Las tres vistas deben reutilizar la misma galería y componentes. |
| RV-EST-009 | ❓ | Confirmar si los estados son mutuamente excluyentes. |
| RV-EST-010 | ❓ | Confirmar las condiciones de transición. |
| RV-EST-011 | ❓ | Confirmar si los estados se actualizan manual o automáticamente. |

---

# Riesgos de Implementación

| Riesgo | Consecuencia |
|---|---|
| Crear tres listas independientes | Duplicación e inconsistencia de información. |
| Confundir estado del vehículo con estado operacional | Modificación incorrecta de la disponibilidad del equipo. |
| Asumir una secuencia no confirmada | Bloqueo de operaciones válidas. |
| Permitir cambios sin auditoría | Pérdida de trazabilidad. |
| Duplicar pantallas | Mayor costo de mantenimiento. |
| Utilizar fórmulas no delegables | Resultados incompletos con grandes volúmenes. |

---

# Pendientes de Confirmación

| Estado | Elemento | Observación |
|---|---|---|
| ❓ | Nombre de la entidad | Confirmar denominación de negocio para `Inicio`. |
| ❓ | Modelo del estado | Confirmar campo único o indicadores independientes. |
| ❓ | Estado inicial | Determinar valor asignado al crear una operación. |
| ❓ | Transiciones | Confirmar recorrido permitido entre estados. |
| ❓ | Reversión | Confirmar si un estado puede retroceder. |
| ❓ | Automatización | Confirmar si los documentos cambian estados. |
| ❓ | Fechas | Confirmar fechas obligatorias por etapa. |
| ❓ | Responsables | Confirmar usuarios autorizados para cada cambio. |
| ❓ | Notificaciones | Confirmar alertas asociadas a las transiciones. |
| ❓ | Auditoría actual | Confirmar si AppSheet registra historial. |
| ❓ | Contadores | Confirmar si deben mostrarse en el menú nuevo. |
| ❓ | Campos de cada vista | Obtener capturas completas de las tres opciones. |

---

# Resumen de Evidencia

| Funcionalidad | Estado |
|---|---|
| Menú En Preparación | ✅ Confirmado |
| Menú En Ruta | ✅ Confirmado |
| Menú Entregado | ✅ Confirmado |
| Misma entidad para las tres vistas | 🎧 Confirmado por audio |
| Filtro diferente por opción | 🎧 Confirmado por audio |
| Indicadores en el detalle | ✅ Confirmado |
| Estado Entregado en Inicio Inline | ✅ Confirmado |
| Estado general del vehículo | ✅ Confirmado |
| Secuencia obligatoria | ❓ No confirmada |
| Cambio automático | ❓ No confirmado |
| Reglas de transición | ❓ No confirmadas |
| Permisos de cambio | ❓ No confirmados |
| Historial de estados | ❓ No confirmado |

---

# Próxima Parte

**Parte 7 de 8**

Se documentará:

- Casos de uso completos del módulo Vehículos.
- Actores.
- Flujos principales.
- Flujos alternativos.
- Excepciones.
- Permisos funcionales.
- Mensajes esperados.
- Criterios de aceptación.

