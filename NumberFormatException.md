# ⚠️ NumberFormatException: ошибка преобразования строки в число

**NumberFormatException** возникает, когда мы пытаемся превратить строку в число, но в строке есть нецифровые символы (буквы, пробелы, знаки).  
В этом материале я разбираю обработку этой ошибки.

---

### Что такое NumberFormatException?

Методы типа `Integer.parseInt()` или `Double.parseDouble()` ожидают, что в строке будет число.  
Если там буквы или другие символы:

```java
String str = "abc";
int num = Integer.parseInt(str);  // ❌ NumberFormatException
```
Программа падает. Чтобы этого избежать — используем `try-catch`.

## Пример 1: обрабатываем NumberFormatException
**Код:**

```java
public static void main(String[] args) {
    String str = "abc";

    try {
        System.out.println(Integer.parseInt(str));
    } catch (NumberFormatException e) {
        System.out.println("Не число");
    }
}
```
**Что происходит:**
1. `try` — пытаемся превратить строку `abc` в число
2. В строке буквы, а не цифры → возникает `NumberFormatException`
3. `catch (NumberFormatException e)` — ловим именно эту ошибку

**Вывод:**
```
Не число
```

---

### Мои заметки:
- `Integer.parseInt()` — превращает строку в `int`
- Если строка не число → `NumberFormatException`
- Обработка этой ошибки полезна при вводе данных от пользователя

---

### Какие строки вызовут NumberFormatException

| Строка | Можно преобразовать в число? |
|--------|------------------------------|
| "123" | ✅ Да |
| "-456" | ✅ Да |
| "abc" | ❌ Нет (буквы) |
| "12.3" | ❌ Нет (точка — для `parseInt`; для `parseDouble` - подойдёт) |
| "12 3" | ❌ Нет (пробел) |
| "" | ❌ Нет (пустая строка) |

### Что я запомнила
- `NumberFormatException` — при ошибке преобразования строки в число
- `Integer.parseInt()` — для целых чисел
- `Double.parseDouble()` — для дробных чисел
- Обработка этой ошибки обязательна, если данные приходят от пользователя

---

⭐ Когда моя программа падает с `NumberFormatException`, я открываю этот файл и вспоминаю,  
что перед преобразованием нужно проверить строку или обработать исключение.
