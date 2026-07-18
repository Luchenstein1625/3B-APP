# 🚀 Guía de Desarrollo
# Agregar un Nuevo Módulo a la Aplicación Power Apps

---

# Arquitectura General

La aplicación fue diseñada utilizando **una sola pantalla**.

Toda la navegación ocurre mediante:

- Variables globales
- Contenedores
- Componentes reutilizables

La estructura es la siguiente:

App

└── Pantalla 3B

    ├── HeaderInicio
    │
    ├── Cuerpo
    │
    │    ├── conMenu
    │    │
    │    │    └── galMenu
    │    │
    │    └── conContenido
    │
    │         ├── conModuloVehiculos
    │         ├── conModuloCotizacion
    │         ├── conModuloMOP
    │         ├── conModuloOC
    │         ├── conModuloOT
    │         ├── conModuloPackingList
    │         ├── conModuloPlanAmarre
    │         └── ...
    │
    └── Footer

---

# Regla Principal

NUNCA crear una nueva pantalla.

Todos los mantenedores deben vivir dentro de:

```
conContenido
```

Esto permite:

- Navegación instantánea
- Mejor rendimiento
- Reutilizar Header
- Reutilizar Menú
- Mantener una sola arquitectura

---

# Paso 1
## Crear el nuevo módulo

Dentro de

```
conContenido
```

crear un nuevo Container.

Nombre:

```
conModuloXXXX
```

Ejemplo

```
conModuloVehiculos

conModuloMOP

conModuloCotizacion

conModuloPackingList
```

---

# Paso 2
## Estructura del módulo

Cada módulo SIEMPRE debe tener esta estructura.

```
conModuloXXXX

│

├── conXXXXHeader

│     │

│     ├── Label Título

│     ├── Buscar

│     ├── Botón Agregar

│     └── Botón Filtro

│

└── conXXXXBody

      │

      └── Gallery Principal
```

No agregar controles directamente sobre el módulo.

Siempre deben ir dentro del Header o del Body.

---

# Paso 3
## Configurar Visible

Cada módulo se muestra únicamente cuando corresponde.

Ejemplo

```
conModuloVehiculos

Visible

=

varModulo = "Vehiculos"
```

Otro ejemplo

```
conModuloCotizacion

Visible

=

varModulo = "Cotizacion"
```

---

# Paso 4
## Agregar el menú

Ir a

```
galMenu

Items
```

Agregar un nuevo registro.

Ejemplo

```powerapps
{
    Id:15;
    Titulo:"Clientes";
    Icono:Icon.Person;
    Modulo:"Clientes"
}
```

---

# Paso 5
## Navegación

El OnSelect del Item debe permanecer siempre igual.

```powerapps
Set(
    varModulo;
    ThisItem.Modulo
)
```

No modificar esta lógica.

---

# Paso 6
## Crear el módulo correspondiente

Dentro de

```
conContenido
```

crear

```
conModuloClientes
```

---

# Paso 7
## Configurar Visible

```powerapps
Visible

=

varModulo="Clientes"
```

Listo.

La navegación ya funcionará automáticamente.

---

# Paso 8
## Crear Header

Dentro del módulo

```
conClientesHeader
```

Agregar:

✔ Label

✔ Buscar

✔ Botón Agregar

✔ Botón Filtro

---

# Paso 9
## Crear Body

Dentro

```
conClientesBody
```

Agregar

Gallery Vertical

Esta Gallery contendrá los registros.

---

# Paso 10
## Fuente de datos

Mientras la aplicación esté en POC utilizar

```powerapps
Table(...)
```

Ejemplo

```powerapps
Table(
    {
        Nombre:"Cliente 1";
        Estado:"Activo"
    },
    {
        Nombre:"Cliente 2";
        Estado:"Inactivo"
    }
)
```

NO conectar SharePoint todavía.

---

# Paso 11
## Cuando llegue SharePoint

Solo reemplazar

```powerapps
Table(...)
```

por

```powerapps
ListaClientes
```

Toda la interfaz seguirá funcionando.

---

# Convención de nombres

Módulos

```
conModuloVehiculos
conModuloClientes
conModuloMOP
```

Headers

```
conVehiculosHeader
conClientesHeader
```

Body

```
conVehiculosBody
conClientesBody
```

Galerías

```
galVehiculos
galClientes
```

Botones

```
btnAgregar

btnBuscar

btnFiltro
```

Variables

```
varModulo

varMenuAbierto

varRegistroSeleccionado
```

---

# Flujo de Navegación

```
Usuario

↓

Selecciona menú

↓

galMenu

↓

Set(varModulo)

↓

Visible

↓

Muestra únicamente

conModuloSeleccionado
```

---

# Buenas prácticas

✔ Nunca crear otra Screen.

✔ Todo módulo vive dentro de conContenido.

✔ Todos los módulos tienen Header + Body.

✔ El Header nunca contiene datos.

✔ El Body contiene Gallery y Formularios.

✔ Todas las galerías tienen la misma estructura.

✔ Todos los mantenedores reutilizan el mismo diseño.

✔ La fuente de datos siempre puede cambiar sin modificar la interfaz.

---

# Objetivo Final

```
App

↓

Header

↓

Menú

↓

conContenido

├── Vehículos

├── Cotización

├── MOP

├── OC

├── OT

├── Packing List

├── Plan de Amarre

├── Clientes

├── Usuarios

└── Configuración
```

La aplicación completa reutiliza la misma arquitectura, haciendo que agregar un nuevo módulo tome solo unos minutos.