# Reto-1-POO
## Punto 1
Crear una función que realice operaciones básicas (suma, resta, multiplicación, división) entre dos números, según la elección del usuario, la forma de entrada de la función será los dos operandos y el caracter usado para la operación. *entrada:* `(1,2,"+")`, *salida* `(3)`.
### solución
Se implementó una función con tres parámetros:

- `first_number`: un número entero.
- `second_number`: otro número entero.
- `sign`: una cadena que representa una operación matemática (+, -, *, /).

A través del uso de la estructura `match`, se gestionan diferentes casos para realizar operaciones básicas:
```python
def basic_operation(first_number: int,  second_number: int, sign: str):
    match sign:
        case  "+":
            return first_number + second_number
        case  "-":
            return first_number - second_number
        case  "*":
            return first_number * second_number
        case  "/":
            return first_number / second_number
```

## Punto 2
Realice una función que permita validar si una palabra es un palíndromo. **Condición:** No se vale hacer slicing para invertir la palabra y verificar que sea igual a la original.
### solución
La función para verificar si una palabra es un palíndromo sigue los siguientes pasos:
1. **Verificación de paridad:**
   - Se determina si la longitud de la palabra es par o impar.
   
2. **Comprobación para palabras pares:**
   - Si la palabra es par, se recorre cada carácter de la palabra y se compara con su correspondiente de orden inverso.
   - Si en algún punto estos caracteres difieren, se establece una bandera como falsa, indicando que la palabra no es un palíndromo.

3. **Comprobación para palabras impares:**
   - Si la palabra es impar, se realiza una comprobación similar, pero se omite el carácter central ya que no tiene un equivalente en el otro extremo.
   - Se comparan los caracteres en ambos lados de la palabra
   - Si en algún punto estos caracteres difieren, se establece la bandera como falsa.

Esta función retorna True si la palabra es un palíndromo y False en caso contrario, aplicando el enfoque mencionado.
```python
def is_palindrome(word: str) -> bool:
    flag = True
    if len(word) % 2 != 0:
        for char in range(len(word)):
            if char != (len(word)//2)+1:
                if word[char] != word[-char-1]:
                    flag = False
                    break
    else:
        for char in range(len(word)):
            if word[char] != word[-char-1]:
                flag = False
                break
    return flag
```
## Punto 3
Escribir una función que reciba una lista de números y devuelva solo aquellos que son primos. La función debe recibir una lista de enteros y retornar solo aquellos que sean primos.
### solución
La función prime_numbers toma como entrada una lista de números y devuelve una lista que contiene únicamente los números primos de la lista original.

**Función Interna is_prime:**

Dentro de la función principal, se encuentra una función interna llamada is_prime. Esta función se encarga de verificar si un número dado es primo o no. Se sigue una serie de condiciones:

  Si el número es menor o igual a 1, se considera que no es primo y la función devuelve False.
  - Si el número es igual a 2, se considera primo y la función devuelve True.
  - Si el número es divisible por 2, excluyendo el propio 2, se descarta como primo y la función devuelve False.
  - Para el caso de números impares mayores a 2, se realiza un bucle que itera desde 3 hasta el número, con un paso de 2 para evitar verificar divisibilidad por números pares. Si en algún momento el número es divisible por algún valor en este rango, la función retorna False. En caso contrario, se considera primo y se retorna True.

**Función Principal prime_numbers:**

Esta función utiliza list comprehension para crear una nueva lista que contiene solo los números primos de la lista de entrada, utilizando la función is_prime para determinar la primalidad de cada número.


```python
def prime_numbers(numbers: list) -> list:
    prime_numbers = []

    def is_prime(number):
        if number <= 1:
            return False
        if number == 2:
            return True
        if number % 2 == 0:
            return False
        for x in range(3, number, 2):
            if number % x == 0:
                return False
        return True
    for number in numbers:
        if is_prime(number) is True:
            prime_numbers.append(number)
    return prime_numbers


print(prime_numbers([1, 2, 3, 4, 5, 6, 7, 8, 9]))
```
## Punto 4
Se ha desarrollado una función diseñada para procesar una lista de números enteros y calcular la mayor suma entre dos elementos consecutivos en la lista. El procedimiento es el siguiente:

  - Se inicializa la variable sum_numbers para almacenar la suma máxima.

  - Se identifica el número máximo en la lista mediante la función max(), y se obtiene su índice en la lista.

  - Si el número máximo es el último elemento de la lista, se suma este número con su elemento consecutivo anterior.

  - Si el número máximo no es el último elemento, se suma con el elemento consecutivo mayor entre el siguiente y el anterior.

La función finalmente devuelve la mayor suma entre dos elementos consecutivos en la lista de números proporcionada.
```python
def max_consecutive_sum(numbers: list) -> int:
    sum_numbers: int = 0
    sum_numbers += max(numbers)
    if max(numbers) == numbers[-1]:
        sum_numbers += numbers[numbers.index(max(numbers))-1]
        return sum_numbers

    elif numbers[numbers.index(max(numbers))+1] > numbers[numbers.index(max(numbers))-1]:
        sum_numbers += numbers[numbers.index(max(numbers))+1]
        return sum_numbers

    else:
        sum_numbers += numbers[numbers.index(max(numbers))-1]
        return sum_numbers
```
## Punto 5
Escribir una función que reciba una lista de string y retorne unicamente aquellos elementos que tengan los mismos caracteres. e.j. entrada: `["amor", "roma", "perro"]`, salida `["amor", "roma"]`
### solución
1. **Creación de un Diccionario de Anagramas:**
- La función recorre cada palabra en la lista y la ordena alfabéticamente, creando así una forma estandarizada.
- Se utiliza un diccionario para almacenar estas palabras ordenadas y sus correspondientes palabras originales.

2. **Agrupación de Anagramas:**
- Si una palabra ordenada ya está en el diccionario, se agrega la palabra original a la lista de anagramas asociada.
- Si la palabra ordenada no está en el diccionario, se crea una nueva entrada con la palabra original como su primer elemento.

3. **Filtrado de Anagramas:**
    Al finalizar el proceso, la función filtra los resultados, excluyendo aquellas palabras que no tienen anagramas en la lista original.
```python
def find_anagrams(words: list) -> list:
    anagrams_dict = {}
    for word in words:
        sort_word = "".join(sorted(word))
        if sort_word in anagrams_dict:
            anagrams_dict[sort_word].append(word)
        else:
            anagrams_dict[sort_word] = [word]
    anagrams = [word for group in anagrams_dict.values() if len(group) > 1 for word in group]
    return anagrams
```

