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
- Convierte una entrada de texto en un número entero.
- Elimina puntos de miles y maneja errores de conversión.
  
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
  
- Cantidad de productos
    ```python
    cantidad = None
    while cantidad is None or cantidad <= 0:
        entrada_cantidad = input("Ingresa la cantidad de productos que llevas: ")
        cantidad = convertir_a_numero(entrada_cantidad)
        if cantidad is None or cantidad <= 0:
            print("La cantidad debe ser un número positivo.")
    ```
    

## 3. Procesamiento

- Cálculo de subtotal

    ```python
    subTotal = precio * cantidad
   ```
    
- Validación de descuento
  
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

- Calcular el total

  ```python
  total = subTotal - (subTotal * desc / 100)
  ```

## 4. Datos de salida

```python
print(f"\nResumen de compra:")
print(f"Producto: {producto}")
print(f"Cantidad: {cantidad}")
print(f"Precio por unidad: ${precio:,.2f}")
print(f"Subtotal: ${subTotal:,.2f}")
print(f"Descuento aplicado: {desc}%")
print(f"Total a pagar: ${total:,.2f}")
```

## 🧾 Código Completo

```python
def convertir_a_numero(entrada):
    entrada = entrada.replace(".", "")
    try:
        return int(entrada)
    finally:
        print("")

print("Ingresa el nombre del producto:")
producto = input()

precio = None
while precio is None or precio <= 0:
    entrada_precio = input("Ingresa el precio por unidad: ")
    precio = convertir_a_numero(entrada_precio)
    if precio is None or precio <= 0:
        print("El precio debe ser un número positivo.")

cantidad = None
while cantidad is None or cantidad <= 0:
    entrada_cantidad = input("Ingresa la cantidad de productos que llevas: ")
    cantidad = convertir_a_numero(entrada_cantidad)
    if cantidad is None or cantidad <= 0:
        print("La cantidad debe ser un número positivo.")

subTotal = precio * cantidad

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

total = subTotal - (subTotal * desc / 100)

print(f"\nResumen de compra:")
print(f"Producto: {producto}")
print(f"Cantidad: {cantidad}")
print(f"Precio por unidad: ${precio:,.2f}")
print(f"Subtotal: ${subTotal:,.2f}")
print(f"Descuento aplicado: {desc}%")
print(f"Total a pagar: ${total:,.2f}")

```

