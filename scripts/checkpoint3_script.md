# Checkpoint 3 - Scripts Utilizados

## 1. Script del Diagrama de Clases (PlantUML)
Este es el código fuente utilizado para generar el modelo UML del Checkpoint 1 en Lucidchart.

```plantuml
@startuml
skinparam classAttributeIconSize 0
skinparam monochrome true
skinparam shadowing false
skinparam defaultFontName Arial
skinparam class {
    BackgroundColor White
    BorderColor Black
    ArrowColor Black
}

interface IVendible <<Interface>> {
    + calcularPrecioVenta(): Double
    + obtenerResumen(): String
}

abstract class Producto <<Abstract>> {
    - codigo: String
    - titulo: String
    - precioBase: Double
    - stock: Int
    - categoria: String
    + actualizarStock(cantidad: Int): void
    + verificarDisponibilidad(): Boolean
    + calcularPrecioVenta(): Double {abstract}
    + obtenerResumen(): String {abstract}
}

class Libro {
    - autor: String
    - isbn: String
    - numeroPaginas: Int
    - genero: String
    - esTapaDura: Boolean
    + calcularPrecioVenta(): Double
    + obtenerResumen(): String
}

class Revista {
    - numeroEdicion: Int
    - mesPublicacion: String
    - tematica: String
    + calcularPrecioVenta(): Double
    + obtenerResumen(): String
}

class ArticuloPapeleria {
    - marca: String
    - material: String
    + calcularPrecioVenta(): Double
    + obtenerResumen(): String
}

class Cliente {
    - idCliente: String
    - nombre: String
    - correo: String
    - esSocio: Boolean
    + obtenerDatosCliente(): String
}

class DetalleVenta {
    - cantidad: Int
    - subtotal: Double
    + calcularSubtotal(): Double
}

class Venta {
    - idVenta: String
    - fecha: String
    - totalVenta: Double
    + agregarProducto(producto: Producto, cantidad: Int): void
    + calcularTotal(): Double
    + generarTicket(): String
}

class Inventario {
    - listaProductos: List<Producto>
    + agregarProducto(producto: Producto): void
    + buscarProductoPorCodigo(codigo: String): Producto
    + obtenerProductosConBajoStock(limite: Int): List<Producto>
}

Producto <|-- Libro
Producto <|-- Revista
Producto <|-- ArticuloPapeleria
IVendible <|.. Producto

Inventario "1" *-- "0..*" Producto : contiene >
Venta "1" *-- "1..*" DetalleVenta : contiene >
DetalleVenta "1" --> "1" Producto : referencia >
Venta "1" --> "1" Cliente : pertenece a >
@enduml