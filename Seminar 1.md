# Семинар 1

## Вводная часть
- Представление семинариста
  - Контакты
- Страница курса
  - http://ccfit.nsu.ru/~vlasov/OOP/
- Правила игры
  - Сдаём задачи на GitHub
    - Приём только на ноутбуке преподавателя
  - 16 задач
    - 6 - на тройку
    - 11 - на четвёрку
    - 14 - на пятёрку
  - За каждый месяц без сдачи - штраф в одну задачу
  - В начале каждого семинара - пятиминутки по предыдущей лекции (нет штрафов, есть бонусы)
  - Необходимо соблюдать Code Style: https://google.github.io/styleguide/javaguide.html

## Hello, world!

Создаём файлик `App.java`:

```Java
public class App {                                // В Java нет свободных функций, поэтому сначала нужен класс.
    public static void main(String[] args) {      // Объявляем точку входа a la int main(). Обязана быть public.
        System.out.println("Hello, world!");
    }
}
```

Компилируем:

```bash
javac App.java
```

Здесь `javac` - компилятор. Видим, что появился файл `App.class`. Запускаем:

```bash
java -classpath . App
```

Здесь:
- `java` - виртуальная машина
- `-classpath .` - указываем путь к директории, из которой будут загружаться классы
- `App` - имя одного из загруженных классов, который содержит точку входа

Если всё пошло хорошо, то в консоли мы увидим `Hello, world!`.

Горюем, что как-то сложна по сравнению с C. Радуемся, что больше делать этого не придётся.

## Знакомство с IDE

Скачиваем [JetBrains Toolbox](https://www.jetbrains.com/toolbox/app/), устанавливаем, через него загружаем IntelliJ IDEA Community.

*Можно скачать установщик IDEA напрямую, но тогда развлекаться с обновлениями будете сами.*

При первом запуске нас попросят настроить плагины - можно смело оставлять всё по умолчанию. Создаём пустой Java-проект.

Время рассказать про структуру проекта:

```
src - папка со всеми исходниками
| main - содержит исходники непосредственно приложения (могут быть тесты, но это потом)
  | java - содержит исходники на языке Java. Выносится в отдельную папку, т.к. для JVM есть и другие языки.
    | ru.nsu.fit.komissarov.myproject - имя вашего пакета. Именуется вот так витеевато.
                                        точки здесь на самом деле образуют вложенные директории.
      | utils - вложенный пакет. Полностью именуется ru.nsu.fit.komissarov.myproject.utils
      | App.java
```

Из коробки IDEA может сгенерировать только папку src и все её поддиректории считать пакетами - нужно это дело скорректировать: `File | Project Structure | Modules` - и выстраиваем там нужную нам иерархию.

Создаём корневой пакет, создаём в нём `App.java` со знакомым нам Hello, world. Запускаем через `Run | Run 'App'` или через контекстные иконки в коде - видим, что в консоль нам выплюнули `Hello, world!`. Успех!

Оставшуюся часть семинара пишем генератор чисел Фибоначчи:

```Java
public class FibonacciGenerator {
    private long[] cache;

    public FibonacciGenerator(int elementsCount) {
        if (elementsCount <= 0) {
            return;
        }
        cache = new long[elementsCount];  // by default all values are zero.
        // Initialize our sequence cache with first two values.
        cache[0] = 1;
        if (elementsCount > 1) {
            cache[1] = 1;
        }
    }

    public long getNthNumber(int n) {
        if (cache == null || n < 0 || n >= cache.length) {
            return -1;
        }
        if (cache[n] != 0) {
            return cache[n];
        } else {
            cache[n] = getNthNumber(n - 1) + getNthNumber(n - 2);
            return cache[n];
        }
    }
}
```

Ради развлечения можно посчитать сложность по времени метода `getNthNumber`.