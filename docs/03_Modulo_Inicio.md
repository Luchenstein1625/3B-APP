# 3B APP
# Módulo Inicio

**Versión:** 1.0

**Documento:** 03_Modulo_Inicio.md

**Estado:** En construcción

---

# Objetivo

El módulo **Inicio** constituye el punto de entrada de la aplicación 3B APP.

Su propósito es entregar al usuario un acceso centralizado a los distintos módulos operacionales del sistema, manteniendo una navegación consistente y permitiendo continuar el trabajo sin abandonar la aplicación.

Desde este módulo el usuario podrá acceder rápidamente a las funcionalidades disponibles según su perfil.

---

# Objetivos Funcionales

El módulo Inicio debe permitir:

- Acceder a los distintos módulos del sistema.
- Visualizar el estado general de la aplicación.
- Mantener una navegación uniforme.
- Mostrar información inicial al usuario.
- Actuar como punto de retorno desde cualquier módulo.

---

# Alcance

El módulo Inicio no administra información de negocio directamente.

Su responsabilidad principal es servir como punto de navegación y acceso a las funcionalidades de la aplicación.

---

# Flujo General

```text
Usuario

↓

Abre aplicación

↓

Carga Inicio

↓

Carga menú

↓

Carga información inicial

↓

Usuario selecciona un módulo

↓

Sistema navega al módulo seleccionado
```

---

# Layout General

```text
+-----------------------------------------------------------------------+

HEADER

+---------------+-------------------------------------------------------+

|               |                                                       |
|               |                                                       |
|               |                                                       |
|               |                 ÁREA PRINCIPAL                        |
|               |                                                       |
|    MENÚ       |                                                       |
|               |                                                       |
|               |                                                       |
|               |                                                       |
|               |                                                       |
|               |                                                       |

+---------------+-------------------------------------------------------+

FOOTER
```

---

# Componentes Principales

El módulo se compone de cuatro zonas principales.

## Header

Información global de la aplicación.

Ejemplos.

- Logo.
- Nombre sistema.
- Usuario.
- Acciones globales.

---

## Menú

Permite acceder a todos los módulos disponibles.

Ejemplo.

```text
Inicio

Vehículos

Cotización

...

```

---

## Área Principal

Zona donde se muestra el contenido correspondiente al módulo Inicio.

Dependiendo de la evolución del sistema podrá contener:

- Mensajes.
- Indicadores.
- Accesos rápidos.
- Información relevante.

---

## Footer

Zona reservada para información institucional o técnica.

---

# Diagrama Funcional

```text
               Inicio

                  │

      ┌───────────┴────────────┐

      ▼                        ▼

 Menú lateral             Área principal

      │

      ▼

 Selección módulo

      │

      ▼

 Cambio contenido
```

---

# Casos de Uso

## CU-001

Ingresar a la aplicación.

### Actor

Usuario.

### Flujo

1. El usuario abre la aplicación.
2. Se inicializa el sistema.
3. Se muestra el módulo Inicio.
4. Se carga el menú.
5. El usuario selecciona una opción.

Resultado esperado.

El usuario puede comenzar a trabajar.

---

## CU-002

Seleccionar un módulo.

### Actor

Usuario.

### Flujo

1. Usuario presiona una opción del menú.
2. El sistema actualiza el módulo activo.
3. Se refresca el contenido.
4. Se mantiene el menú disponible.

Resultado esperado.

El usuario continúa trabajando en el nuevo módulo.

---

# Componentes Power Apps

## Screen

```text
scrPrincipal
```

---

## Containers

```text
conHeader

conBody

conMenu

conInicio

conFooter
```

---

## Controles

```text
Gallery

Container

Label

Image

Icon

Button

Rectangle
```

---

# Variables

```powerapps
varModulo

varMenuAbierto

varUsuario

varPantallaActual
```

---

# Inicialización

Durante la carga de la aplicación se propone ejecutar.

```powerapps
Set(
    varModulo,
    "Inicio"
);

Set(
    varMenuAbierto,
    true
);
```

---

# Navegación

La navegación se controla mediante la variable.

```powerapps
varModulo
```

Cuando el valor sea:

```text
Inicio
```

el container correspondiente deberá permanecer visible.

```powerapps
Visible =
varModulo="Inicio"
```

---

# Menú

El menú permanecerá disponible durante toda la sesión.

Se recomienda implementarlo mediante una Gallery.

```powerapps
galMenu
```

Su origen será una colección.

```powerapps
colMenu
```

---

# Información Inicial

El contenido del Inicio podrá utilizarse para mostrar información relevante al usuario.

Ejemplos.

```text
Bienvenida

Noticias

Indicadores

Accesos rápidos

Recordatorios

Últimas actividades
```

La incorporación de estos elementos dependerá de los requerimientos del negocio.

---

# Seguridad

Al ingresar a la aplicación deberán aplicarse las reglas correspondientes al perfil del usuario.

Ejemplos.

```text
Administrador

Operador

Consulta
```

Estas reglas determinarán los módulos visibles y las acciones permitidas.

---

# Experiencia de Usuario

El módulo Inicio debe cumplir los siguientes objetivos.

- Carga rápida.
- Navegación intuitiva.
- Bajo número de clics.
- Consistencia visual.
- Acceso inmediato al menú.

---

# Recomendaciones Power Apps

Se recomienda evitar múltiples pantallas.

La navegación deberá implementarse utilizando Containers.

```text
scrPrincipal

↓

conInicio

↓

conVehiculos

↓

conCotizacion

↓

...
```

Cada módulo será mostrado u ocultado según la variable global.

---

# Dependencias

El módulo Inicio depende de:

- Autenticación.
- Menú.
- Variables globales.
- Componentes reutilizables.

No depende de ninguna entidad funcional específica.

---

# Pendientes

Durante el levantamiento funcional deberán verificarse los siguientes aspectos.

| Estado | Elemento | Observación |
|---------|----------|-------------|
| ❓ | Contenido exacto del Inicio | Confirmar la información mostrada al ingresar. |
| ❓ | Accesos rápidos | Validar si existen botones directos a funcionalidades frecuentes. |
| ❓ | Indicadores | Confirmar si se presentan métricas o resúmenes. |
| ❓ | Mensajes al usuario | Identificar alertas o notificaciones visibles. |
| ❓ | Personalización | Verificar si el contenido cambia según el perfil del usuario. |

---

# Resumen Técnico

| Elemento | Implementación propuesta |
|----------|--------------------------|
| Pantalla | `scrPrincipal` |
| Container | `conInicio` |
| Variable principal | `varModulo` |
| Menú | `galMenu` |
| Visible | `varModulo="Inicio"` |
| Componentes | Header, Menú, Contenido, Footer |

---

# Próximo Documento

```
04_Modulo_Vehiculos.md
```

Este documento abordará el primer módulo operativo de la aplicación e incluirá:

- Objetivo funcional.
- Pantallas.
- Flujo de trabajo.
- Listado de vehículos.
- Formularios.
- Acciones CRUD.
- Modelo de datos.
- Reglas de negocio.
- Diseño SharePoint.
- Implementación detallada en Power Apps.