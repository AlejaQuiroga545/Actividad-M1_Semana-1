#  Sistema de validación de productos

En este documento podremos encontrar una explicación sobre cómo crear un <b>sistema de validación de productos. 🛒</b>
## 1. Función para convertir entradas a número

```python
def convertir_a_numero(entrada):

    # 1. Elimina los puntos en los números
    entrada = entrada.replace(".", "")

    # 2. Intenta convertir el número a entero directamente
    try:
        return int(entrada)
    finally: print  ("") # Línea reservada para depuración o espaciado (se puede quitar)
```
Esta función toma una cadena de texto (entrada), le quita los puntos que suelen usarse como separadores de miles, e intenta convertirla a un número entero.

- Reemplazo de cadenas con `.replace()`
- Manejo de errores con `try...finally`
  
## 2. Datos de entrada
- Nombre del producto
  ```python
  print("Ingresa el nombre del producto:")
  producto = input()
  ```
  
- Precio por unidad
  ```python
  precio = None
  while precio is None or precio <= 0:
    entrada_precio = input("Ingresa el precio por unidad: ")
    precio = convertir_a_numero(entrada_precio)
    if precio is None or precio <= 0:
        print("El precio debe ser un número positivo.")
  ```
  Pide el precio por unidad y asegura que sea un número positivo usando un bucle `while`
  
  - Bucle `while`: Se repite hasta que se ingrese un número válido.
  - Condicionales `if`: Verifica si el número es válido.
  - `entrada_precio`: guarda el texto que escribe el usuario.
  - `precio`: almacena el número validado y convertido.


- Cantidad de productos
    ```python
    cantidad = None
    while cantidad is None or cantidad <= 0:
        entrada_cantidad = input("Ingresa la cantidad de productos que llevas: ")
        cantidad = convertir_a_numero(entrada_cantidad)
        if cantidad is None or cantidad <= 0:
            print("La cantidad debe ser un número positivo.")
    ```
  Solicita la cantidad de productos y repite la pregunta si el número no es válido.

  - Bucle `while` y validación con `if`, igual que en el precio.
  - `entrada_cantidad`: entrada del usuario en texto.
  - `cantidad`: número entero validado.


    

## 3. Procesamiento

- Cálculo de subtotal

    ```python
    subTotal = precio * cantidad
   ```
    
- Validación de descuento

  Permite ingresar un descuento opcional, lo convierte a número decimal y valida que esté entre 0% y 100%.
  
  ```python
  print("Ingresa el descuento (presiona Enter si NO aplica):")
  entrada_descuento = input()

  if entrada_descuento.strip() == "":
    desc = 0.0
  else:
    entrada_descuento = entrada_descuento.replace("%", "")
    try:
        desc = float(entrada_descuento)
        if not 0 <= desc <= 100:
            print("El descuento debe estar entre 0% y 100%. Se aplicará 0%.")
            desc = 0.0
    except ValueError:
        print("Descuento inválido. Se aplicará 0%.")
        desc = 0.0
  ```
  - Condicionales `if`, `else`, `try`, `except`
  - Limpieza de datos con `.strip()` y `.replace()`
  - `entrada_descuento`: texto original del usuario
  - `desc`: porcentaje de descuento final como número


- Calcular el total

  ```python
  total = subTotal - (subTotal * desc / 100)
  ```
  Aplica el descuento al subtotal para obtener el total final.


## 4. Datos de salida

Muestra un resumen detallado de la compra con los datos ingresados y calculados.

```python
print(f"\nResumen de compra:")
print(f"Producto: {producto}")
print(f"Cantidad: {cantidad}")
print(f"Precio por unidad: ${precio:,.2f}")
print(f"Subtotal: ${subTotal:,.2f}")
print(f"Descuento aplicado: {desc}%")
print(f"Total a pagar: ${total:,.2f}")
```
- Impresión con formato (`f-strings`) que permite insertar variables directamente dentro del texto usando llaves para mostrar números con comas y dos decimales.
- `,` agrega separadores de miles (por ejemplo, 1,000 en vez de 1000).
- `.2f` muestra el número con 2 cifras decimales, y lo redondea si es necesario.


## 🧾 Código Completo

```python
# CONVERTIR ENTRADA A NÚMEROS

def convertir_a_numero(entrada):

    # 1. Elimina los puntos en los números
    entrada = entrada.replace(".", "")

    # 2. Intenta convertir el número a entero directamente
    try:
        return int(entrada)
    finally: print  ("")


# DATOS DE ENTRADA

# Producto
print("Ingresa el nombre del producto:")
producto = input()

# Obtener precio
precio = None
while precio is None or precio <= 0:
    entrada_precio = input("Ingresa el precio por unidad: ")
    precio = convertir_a_numero(entrada_precio)
    if precio is None or precio <= 0:
        print("El precio debe ser un número positivo.")

# Obtener cantidad
cantidad = None
while cantidad is None or cantidad <= 0:
    entrada_cantidad = input("Ingresa la cantidad de productos que llevas: ")
    cantidad = convertir_a_numero(entrada_cantidad)
    if cantidad is None or cantidad <= 0:
        print("La cantidad debe ser un número positivo.")



# PROCESAMIENTO

# Cálculo de subtotal
subTotal = precio * cantidad

# Obtener descuento
print("Ingresa el descuento (presiona Enter si NO aplica):")
entrada_descuento = input()

if entrada_descuento.strip() == "":
    desc = 0.0
else:
    entrada_descuento = entrada_descuento.replace("%", "")
    try:
        desc = float(entrada_descuento)
        if not 0 <= desc <= 100:
            print("El descuento debe estar entre 0% y 100%. Se aplicará 0%.")
            desc = 0.0
    except ValueError:
        print("Descuento inválido. Se aplicará 0%.")
        desc = 0.0

# Calcular total
total = subTotal - (subTotal * desc / 100)


# DATOS DE SALIDA

print(f"\nResumen de compra:")
print(f"Producto: {producto}")
print(f"Cantidad: {cantidad}")
print(f"Precio por unidad: ${precio:,.2f}")
print(f"Subtotal: ${subTotal:,.2f}")
print(f"Descuento aplicado: {desc}%")
print(f"Total a pagar: ${total:,.2f}")

```

