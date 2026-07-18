# 3B APP
# Especificación Funcional
## Módulo Vehículos

**Versión:** 0.1

**Estado:** En elaboración

---

# 1. Objetivo

Documentar el comportamiento funcional del módulo Vehículos para reconstruirlo en Microsoft Power Apps manteniendo la experiencia de usuario de la aplicación actual.

---

# 2. Arquitectura General

La aplicación utiliza una navegación mediante menú lateral.

Cada opción abre un módulo especializado.

La pantalla mantiene una estructura consistente:

+------------------------------------------------------+
| Header                                               |
|------------------------------------------------------|
| Menú | Listado | Panel de Detalle                    |
|      |         |                                     |
|      |         |                                     |
+------------------------------------------------------+

---

# 3. Componentes observados

## Header

Contiene:

- Logo 3B APP
- Buscador
- Usuario
- Acciones generales

Estado:

✅ Confirmado

---

## Menú lateral

Módulos observados:

- Inicio
- En Ruta
- Entregado
- Cotización
- Vehículos
- Módulos
- DC
- MP
- OT
- Parking Lot
- Planeo Hardware
- About
- AppSheet

Estado:

✅ Confirmado

---

# 4. Módulo Vehículos

Al ingresar se observa:

- listado de vehículos
- búsqueda
- botón Agregar
- acciones por registro
- panel derecho con detalle

Estado:

✅ Confirmado

---

# 5. Distribución

## Panel izquierdo

Listado de vehículos.

Cada fila contiene información resumida.

Se puede seleccionar un vehículo.

---

## Panel derecho

Muestra el detalle del vehículo seleccionado.

Dependiendo del contexto se visualizan:

- imagen
- información técnica
- cotización
- documentos
- botones de acción

---

# 6. Funcionalidades

## 6.1 Buscar

Existe una caja de búsqueda superior.

Estado:

✅ Confirmado

---

## 6.2 Agregar

Existe botón "Agregar".

Estado:

✅ Confirmado

Detalle del formulario:

⚠️ Pendiente documentar completamente.

---

## 6.3 Seleccionar

Al seleccionar un vehículo cambia el panel derecho.

Estado:

✅ Confirmado

---

## 6.4 Visualizar detalle

Se muestran datos completos del vehículo.

Estado:

✅ Confirmado

---

## 6.5 Cotización

Existe una sección Cotización.

Estado:

✅ Confirmado

Reglas:

⚠️ Pendientes.

---

## 6.6 Documentos

El detalle contiene documentos asociados.

Estado:

✅ Confirmado

---

# 7. Tipos de Vehículo observados

Durante el recorrido aparecen distintas categorías.

Ejemplos:

- Camión
- Contenedor
- Módulos
- Equipos especializados

Estado:

✅ Confirmado visualmente.

Modelo propuesto:

Vehículo
    ↓
Tipo

---

# 8. Estados

Confirmado por conversaciones.

No son mantenedores distintos.

Corresponden a filtros.

Estados:

- En preparación
- En ruta
- Entregado

Modelo:

Vehículos
      ↓
Estado
      ↓
Preparación
Ruta
Entregado

Estado:

✅ Confirmado por audio.

---

# 9. Modelo Funcional

Vehículos

↓

Listado

↓

Detalle

↓

Acciones

↓

Actualizar vista

---

# 10. Componentes Power Apps

## Pantalla

scrVehiculos

---

## Containers

conHeader

conMenu

conListado

conDetalle

conFooter

---

## Galerías

galVehiculos

---

## Formularios

frmVehiculo

frmCotizacion

---

# 11. Colecciones

colVehiculos

colCategorias

colEstados

colCotizaciones

---

# 12. SharePoint

Vehiculos

Categorias

Estados

Cotizaciones

Documentos

---

# 13. Reglas de negocio confirmadas

✔ Existe un único mantenedor reutilizable.

✔ En preparación, En Ruta y Entregado reutilizan la misma entidad.

✔ El cambio corresponde a un filtro.

✔ El resto de módulos debe reutilizar la misma estructura.

---

# 14. Pendientes

Documentar:

- todos los campos
- validaciones
- botones
- reglas
- mensajes
- formularios
- relaciones
- permisos