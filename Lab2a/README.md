# **Лабораторна робота №2А**
---
## Послідовність виконання лабораторної роботи:
#### 1. Переглянув офіційну документацію для ***Python***.
#### 2. Створюю файл ***test.py*** для виконання базових прикладів.
1. Виводжу вбудованні константи за допомогою команд:

    ```python
    print("Перша константа: ", True)
    print("Друга константа: ", False)
    print("Третя константа: ", NotImplemented)
    ```
1. Виводжу результат роботи вбудованих функцій за допомогою команд:
   ```python
    print("Число 20 в 16-ві системі числення дорівнює: ", hex(20))
    print("2 в 10 степені дорівнює: ", pow(2,10))
    print("Максимальне число з чисел 5,6,9,3,45 :",max(5,6,9,3,45))
    ```
1. Виводжу результат роботи циклу і розгалужень за допомогою команд:
    ```python
    x= [1 for i in range(10)]
    print("Виведення 10 одиниць з масиву: ",x)

    b=5
    print("Змінна B дорівнює 5" if b == 5 else "Змінна B не дорівнює 5")
    ```
1. Виводжу результат роботи конструкції `try`->`except`->`finally` при помилці за допомогою команд:
    ```python
    y=[5,2]
    print("Що буде якщо вивести 10 елемент масиву y[]?: ")
    try:
        print(y[10])
    except Exception as e:
        print(e)
    finally:
        print("То ось що буде!")
    ```
1. Виводжу результат роботи контекст-менеджера `with` за допомогою команд:
    ```python
    i=1
    with open("README.md", "r") as file:
        for line in file:
            print("Рядок " + str(i) + ": " + line)
            i=i+1
    ```
1. Виводжу результат роботи з `lambdas` за допомогою команд:
    ```python
    new_lambda = lambda first_number, second_number: f'Сума першого і другого числа дорівнює {first_number + second_number}'
    print("Розташування функції в памяті: ", new_lambda)
    print("Виклик лямбди: ", new_lambda(5, 6))
    ```
#### 3. Створив у власному рипозеторії такі файли:
   ```text
   lab2a/
   ├── modules/
   │   └── common.py
   ├── __init__.py
   └── __main__.py
   ```