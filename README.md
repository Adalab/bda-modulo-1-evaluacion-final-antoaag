# bda-modulo-1-evaluacion-final-antoaag
bda-modulo-1-evaluacion-final-antoaag created by GitHub Classroom

# Ejercicio final de Módulo: Crea una clase Tienda Online

class TiendaOnline:
    def __init__(self, nombre):
        self.nombre = nombre
        self.inventario = {} 
        self.ventas = 0.0 

    def agregar_producto(self, nombre, precio, cantidad):
        # Si el producto ya existe incrementamos la cantidad
        for producto in self.inventario.values():           #producto es el valor asoaciado a cada value en diccionario self.inventario.values
            if producto["nombre"].lower() == nombre.lower():
                producto["cantidad"] += cantidad
                print(f"se actualizó la cantidad de {nombre}")
                return                                            #usamos return para no ejecutar más codigo en la funcion
            
        nuevo_producto = {
                "nombre": nombre,
                "precio": precio,
                "cantidad": cantidad
            }
        self.inventario[nombre] = nuevo_producto

    def ver_inventario(self):
        # Iterar sobre el inventario e imprimir detalles
        for producto in self.inventario.values():
            print(f"Nombre: {producto['nombre']}, Precio: ${producto['precio']}, Cantidad: {producto['cantidad']}")

    def buscar_producto(self, nombre):
        # Busca un producto por nombre y lo imprime si existe
        for producto in self.inventario.values():
            if producto['nombre'].lower() == nombre.lower():
                print(f"Nombre: {producto['nombre']}, Precio: ${producto['precio']}, Cantidad: {producto['cantidad']}")
                return
        print("El producto no existe en el inventario.")

    def actualizar_stock(self, nombre):
        # Aumenta o disminuye la cantidad de stock según entrada del usuario
        for producto in self.inventario.values():
            if producto['nombre'].lower() == nombre.lower():
                cantidad_str = input(f"Introduce la cantidad a agregar o quitar para '{nombre}': ")
                try:
                    cantidad = int(cantidad_str)
                    producto['cantidad'] += cantidad
                    print(f"Stock de {nombre} actualizado. Cantidad actual: {producto['cantidad']}")
                except ValueError:
                    print("Entrada inválida. Debes introducir un número entero.")
                return
        print(f"El producto '{nombre}' no está en el inventario.")

    def eliminar_producto(self, nombre):
        # Solicitar confirmación antes de eliminar
        opcion = input(f"¿Desea eliminar el producto '{nombre}'? Escriba 'salir' para no eliminar nada, pulse enter para eliminar producto: ")
        if opcion.lower() == "salir":
            print("Operación cancelada. No se eliminará el producto.")
            return

        # Procedemos a eliminar el producto solo si el usuario no escribió "salir"
        for producto_nombre, producto_info in list(self.inventario.items()):
            if producto_nombre.lower() == nombre.lower():
                del self.inventario[producto_nombre]
                print(f"Producto '{nombre}' eliminado correctamente.")
                return
        print(f"Producto '{nombre}' no está en el inventario.")

    def calcular_valor_inventario(self):
        valor_total = 0.0
        for producto in self.inventario.values():
            valor_total += producto["precio"] * producto["cantidad"]
        print(f"El valor total del inventario es: ${valor_total}")
        return valor_total


# Ejemplo de uso: Le damos nombre a nuestra clase en este caso nuestra tienda:
mi_tienda = TiendaOnline("TiendaPython")


# Procedo a ir llamando a las funciones 

# Agregamos productos al inventario

mi_tienda.agregar_producto("Mouse", 10, 80)
mi_tienda.agregar_producto("Ordenador", 700, 40)
mi_tienda.agregar_producto("Pantalla", 70, 50)



# Ver el inventario
mi_tienda.ver_inventario()


# Buscar un producto existente
mi_tienda.buscar_producto("Ordenador")


# Actualizar stock de un producto según entrada del usuario
mi_tienda.actualizar_stock("Ordenador")


# Podemos volver ver el inventario para comprobar que se han hecho los cambios 
mi_tienda.ver_inventario()


# Eliminar un producto pulsando enter o escribimos "Salir" para no eliminar nada
mi_tienda.eliminar_producto("Mouse")


# Volver a ver inventario para comprobar la eliminación
mi_tienda.ver_inventario()


# Calcular el valor total del inventario
mi_tienda.calcular_valor_inventario()