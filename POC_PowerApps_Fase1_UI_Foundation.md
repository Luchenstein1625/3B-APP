# 🚀 POC Power Apps -- Migración desde AppSheet

## Estado del Proyecto -- Fase 1 (UI Foundation)

### Objetivo

Construir una Proof of Concept (POC) que replique visualmente la
aplicación desarrollada en AppSheet utilizando Power Apps Canvas,
desacoplando completamente la interfaz de la fuente de datos.

Durante esta fase se utilizarán tablas locales (`Table()`), dejando la
integración con SharePoint para una segunda etapa.

------------------------------------------------------------------------

## Arquitectura

``` text
App
│
├── Header
│   ├── Logo
│   ├── Nombre Aplicación
│   ├── Buscador
│   └── Menú Hamburguesa
│
├── Body
│   ├── Menú Lateral
│   └── Área de Contenido
│
└── Footer
```

## Navegación

Se utilizará una única pantalla con módulos visibles mediante:

``` powerapps
Set(varModulo;"Vehiculos")
```

Cada módulo utiliza:

``` powerapps
Visible = varModulo = "Vehiculos"
```

## Variables Globales

-   varMenuAbierto
-   varModulo

## Estado actual

### Header

-   Logo
-   Nombre aplicación
-   Buscador
-   Colores corporativos

### Menú lateral

-   Galería dinámica
-   Navegación entre módulos
-   Iconos
-   Estado seleccionado

### Módulo Vehículos

``` text
conModuloVehiculos
├── Header
│   ├── Buscar
│   ├── Agregar
│   └── Filtro
└── Body
    └── Gallery
```

## Estrategia de desarrollo

Mientras se construye la aplicación se utilizarán datos simulados:

``` powerapps
Table(...)
```

Ventajas:

-   Desarrollo rápido.
-   No depende de SharePoint.
-   Validación temprana de UX.
-   Fácil migración posterior.

## Arquitectura objetivo

``` text
Power Apps
      ↓
Componentes UI
      ↓
Tablas Locales (POC)
      ↓
SharePoint Lists
```

## Próximos módulos

1.  Vehículos
2.  Cotización
3.  Inicio 3B
4.  MOP
5.  OC
6.  OT
7.  Packing List
8.  Plan de Amarre
9.  Inicio

## Fase 2

-   Crear SharePoint Lists.
-   Reemplazar Table() por listas.
-   Conectar formularios.
-   Carga de documentos.
-   Seguridad y permisos.

## Conclusión

Primero se finalizará toda la interfaz y navegación utilizando tablas
locales. Una vez aprobada la POC, la integración con SharePoint
consistirá principalmente en sustituir el origen de datos, reduciendo el
riesgo y acelerando la implementación.
