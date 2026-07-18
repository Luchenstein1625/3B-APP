# 3B APP
# Navegación de la Aplicación

**Versión:** 1.0

**Documento:** 02_Menu_Navegacion.md

**Estado:** En construcción

---

# Objetivo

Este documento describe el funcionamiento del sistema de navegación de la aplicación 3B APP.

El propósito es documentar cómo el usuario se desplaza entre los distintos módulos, cuál es la estructura del menú y cómo deberá implementarse posteriormente en Power Apps.

---

# Descripción General

La aplicación utiliza una navegación lateral permanente.

El menú permanece visible durante toda la utilización de la aplicación mientras que el contenido cambia dinámicamente según el módulo seleccionado.

Visualmente la aplicación se divide en dos grandes zonas.

```text
+-------------------------------------------------------------+

 HEADER

+------------+------------------------------------------------+

|            |                                                |
|            |                                                |
|            |                                                |
|  MENÚ      |           CONTENIDO                            |
|            |                                                |
|            |                                                |
|            |                                                |
|            |                                                |

+------------+------------------------------------------------+

 FOOTER
```

Esta arquitectura evita abrir múltiples pantallas y permite una experiencia consistente para el usuario.

---

# Principios de Navegación

La navegación cumple las siguientes reglas.

- Existe un único menú lateral.
- Siempre existe un módulo activo.
- El contenido cambia sin abandonar la aplicación.
- La navegación mantiene el contexto del usuario.
- Los controles principales permanecen siempre visibles.

---

# Componentes de Navegación

La navegación está compuesta por cuatro componentes principales.

```text
Header

↓

Menú

↓

Contenido

↓

Footer
```

---

# Header

El encabezado contiene los elementos globales de la aplicación.

Ejemplo observado.

```text
Logo

Nombre aplicación

Usuario

Botón menú

Otros accesos rápidos
```

---

# Menú Lateral

El menú constituye el principal mecanismo de navegación.

Cada opción representa un módulo funcional independiente.

Visualmente cada opción se comporta como un botón.

```text
Inicio

Vehículos

Cotización

...

```

El módulo activo permanece resaltado.

---

# Contenido Principal

La zona de contenido muestra únicamente un módulo a la vez.

```text
Menú

↓

Vehículos

↓

Lista

↓

Detalle
```

o bien

```text
Menú

↓

Cotización

↓

Formulario

↓

Resultado
```

---

# Flujo General

```text
Usuario

↓

Selecciona opción

↓

Sistema actualiza módulo activo

↓

Se ocultan módulos anteriores

↓

Se muestra nuevo módulo

↓

Usuario continúa trabajando
```

---

# Arquitectura Propuesta para Power Apps

En la migración se propone utilizar una única variable de navegación.

```powerapps
Set(varModulo;"Vehiculos")
```

Posteriormente cada container decidirá si debe mostrarse.

```powerapps
Visible =
varModulo="Vehiculos"
```

---

# Modelo de Navegación

```text
                     Aplicación

                          │

        ┌─────────────────┴─────────────────┐

        ▼                                   ▼

      Menú                             Contenido

                                           │

        ┌──────────────────────────────────┴────────────────────────────────┐

        ▼                 ▼                ▼                ▼

    Inicio           Vehículos       Cotización       Otros módulos
```

---

# Estados del Menú

Cada opción del menú puede encontrarse en alguno de los siguientes estados.

## Inactivo

No seleccionado.

Color normal.

---

## Activo

Módulo actualmente visible.

Debe resaltarse mediante:

- color
- fondo
- borde
- iconografía

---

## Deshabilitado

Opción disponible pero no accesible.

Ejemplo:

Permisos insuficientes.

---

# Navegación entre Módulos

La navegación debe ser inmediata.

No deberán abrirse nuevas pantallas para cambiar de módulo.

Se recomienda utilizar únicamente:

```powerapps
Set(varModulo,"NombreModulo")
```

---

# Comportamiento Esperado

Al seleccionar una opción.

```text
Click

↓

Guardar módulo seleccionado

↓

Actualizar menú

↓

Actualizar contenido

↓

Mantener scroll si corresponde

↓

Actualizar detalle
```

---

# Menú Responsive

En dispositivos pequeños el menú podrá contraerse.

```text
Expandido

+----------------+

Vehículos

Cotización

Ruta

...

+----------------+
```

↓

```text
Contraído

+

🚗

📄

🚚

...
```

---

# Variables de Navegación

Se propone utilizar las siguientes variables.

```text
varModulo

varMenuAbierto

varRegistroSeleccionado

varModoFormulario
```

---

# Colección del Menú

En Power Apps el menú podrá construirse mediante una colección.

```powerapps
ClearCollect(

colMenu,

{
    Id:1,
    Nombre:"Inicio",
    Icono:Icon.Home
},

{
    Id:2,
    Nombre:"Vehículos",
    Icono:Icon.Car
},

{
    Id:3,
    Nombre:"Cotización",
    Icono:Icon.Document
}

)
```

La colección podrá crecer sin modificar la estructura de la aplicación.

---

# Componente Recomendado

Se recomienda encapsular el menú como componente.

```text
cmpMenu
```

Entradas.

```text
Módulo activo

Colección menú
```

Salidas.

```text
Módulo seleccionado
```

---

# Seguridad

La navegación deberá respetar los permisos del usuario.

Ejemplos.

```text
Administrador

↓

Todos los módulos
```

```text
Operador

↓

Sólo módulos operacionales
```

```text
Consulta

↓

Sólo lectura
```

---

# Consideraciones para la Migración

Durante la migración deberán validarse los siguientes aspectos.

- Módulos visibles según perfil.
- Navegación entre formularios.
- Acciones automáticas del menú.
- Accesos rápidos.
- Atajos disponibles.
- Estado seleccionado al iniciar la aplicación.

---

# Pendientes de Confirmación

Los siguientes elementos deberán verificarse durante el análisis detallado del video y la aplicación original.

| Estado | Elemento | Observación |
|---------|----------|-------------|
| ❓ | Orden completo del menú | Confirmar la secuencia exacta de todos los módulos. |
| ❓ | Iconografía | Identificar todos los íconos utilizados. |
| ❓ | Menús secundarios | Verificar si existen submenús desplegables. |
| ❓ | Reglas por perfil | Confirmar diferencias de navegación según permisos. |
| ❓ | Accesos rápidos | Identificar accesos directos adicionales en el encabezado. |

---

# Próximo Documento

El siguiente documento abordará el primer módulo funcional de la aplicación.

```text
03_Modulo_Inicio.md
```

Se documentará:

- Objetivo del módulo.
- Componentes visibles.
- Flujo funcional.
- Acciones disponibles.
- Reglas de negocio.
- Propuesta de implementación en Power Apps.