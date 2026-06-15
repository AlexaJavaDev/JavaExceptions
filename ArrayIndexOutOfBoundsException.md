# ⚠️ ArrayIndexOutOfBoundsException: выход за границы массива

**ArrayIndexOutOfBoundsException** возникает, когда мы пытаемся обратиться к элементу массива по индексу, которого не существует.  
В этом материале я разбираю 3 способа обработки этой ошибки.

---

### Что такое ArrayIndexOutOfBoundsException?

В **Java** индексы массива начинаются с `0` и заканчиваются на `длина_массива - 1`.  
Если массив из 3 элементов (индексы 0, 1, 2), то обращение к индексу `5` вызовет ошибку:

```java
int[] arr = {1, 2, 3};
System.out.println(arr[5]);  // ❌ ArrayIndexOutOfBoundsException
```
Программа падает. Чтобы этого избежать — используем `try-catch`.

---

## Пример 1: обрабатываем только ArrayIndexOutOfBoundsException
**Код:**

```java
public static void main(String[] args) {
    int[] arr = {1, 2, 3};
    try {
        System.out.println(arr[5]);
    } catch (ArrayIndexOutOfBoundsException e) {
        System.out.println("Выход за границы массива");
    }
}
```
**Что происходит:**
1. `try` — пытаемся получить элемент по индексу `5`
2. Индекса `5` нет в массиве (максимальный индекс = 2)
3. Возникает `ArrayIndexOutOfBoundsException`
4. `catch` ловит именно эту ошибку и выводит сообщение

**Вывод:**
```
Выход за границы массива
```

---

### Мои заметки:
Этот `catch` поймает только ошибки выхода за границы массива. Другие ошибки (например `NullPointerException`) он не обработает.

---

## Пример 2: обрабатываем все исключения (Exception)
**Код:**

```java
public static void main(String[] args) {
    int[] arr = {1, 2, 3};

    try {
        System.out.println(arr[5]);
    } catch (Exception e) {
        System.out.println("Ошибка массива");
    }
}
```
**Что происходит:**
1. `catch (Exception e)` — ловит любое исключение
2. `ArrayIndexOutOfBoundsException` — это частный случай `Exception`, поэтому он тоже будет пойман

**Вывод:**
```
Ошибка массива
```

---

### Мои заметки:
`Exception` ловит всё. Удобно, если не важно, какая именно ошибка случилась.  
Но если нужно разное поведение для разных ошибок — лучше использовать несколько `catch` или конкретный тип.

---

## Пример 3: выбрасываем исключение вручную через throw
**Код:**

```java
public static void main(String[] args) {
    int[] arr = {1, 2, 3, 4, 5};

    try {
        System.out.println(getElement(arr, 10));
    } catch (Exception e) {
        System.out.println("Ошибка: " + e.getMessage());
    }
}

public static int getElement(int[] arr, int index) {
    if (index < 0 || index >= arr.length) {
        throw new ArrayIndexOutOfBoundsException("Выход за границы массива");
    }
    return arr[index];
}
```
**Что происходит:**
1. В методе `getElement` проверяем, существует ли индекс
2. Если индекс меньше `0` или `больше/равен длине` массива — сами создаём исключение через `throw new ArrayIndexOutOfBoundsException(...)`
3. В `main` ловим это исключение и выводим сообщение из исключения через `e.getMessage()`

**Вывод:**
```
Ошибка: Выход за границы массива
```

---

### Мои заметки:
- Условие `index >= arr.length` проверяет, что индекс не выходит за верхнюю границу
- Условие `index < 0` проверяет, что индекс не отрицательный
- `throw` — создаёт исключение вручную с понятным сообщением
- `e.getMessage()` — возвращает текст ошибки

---

### Что я запомнила
- Индексы массива: от `0` до `длина - 1`
- `ArrayIndexOutOfBoundsException` — при обращении к несуществующему индексу
- `catch (ArrayIndexOutOfBoundsException e)` — ловим только эту ошибку
- `catch (Exception e)` — ловит все ошибки (включая эту)
- `throw new ArrayIndexOutOfBoundsException("текст")` — создаём ошибку сами
- Всегда полезно проверять индекс перед обращением к массиву

--- 

⭐ Когда моя программа падает с `ArrayIndexOutOfBoundsException`, я открываю этот файл и вспоминаю, как правильно обрабатывать выход за границы массива.
