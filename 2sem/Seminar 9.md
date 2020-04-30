# Семинар 2020.04.16

## Пятиминутка
- Какая типизация реализована в Groovy?
- Как объявить переменную в Groovy?
- Какой тип у выражения `[1, 2, 3]` в Groovy?
- Какой синтаксис у лямбда-выражений в Groovy?
- Какому Java-коду эквивалентен следующий код на Groovy: `class A { int a = 2 }`


*Ответы*
- Типизация:
  - динамическая (даже при указании типов они будут проверяться в runtime), но опционально можно включить статическую (`--compile-static`)
  - неявная с опциональными типами
  - слабая (не как в JS, но всё же). [Документация о преобразовании типов](https://docs.groovy-lang.org/latest/html/documentation/core-semantics.html#_promotion_and_coercion) и [блог с примерами](https://e.printstacktrace.blog/groovy-dynamic-types-coercion-and-promotion-you-have-been-warned/). Включение статической компиляции делает типизацию несколько сильнее, но всё равно код a la `Boolean flag = "false"` останется валидным (и при этом `flag == true`)
- Как в Java, через ключевое слово `def`, либо без ключевого слова (глобальная переменная всего скрипта)
- ArrayList
- `{ arg1, arg2 -> /* do smth */ }` или `{ doSmth(it) }` (где `it` - единственный аргумент лямбда-выражения)
- Код:
```Java
class A {
  private int a = 2;

  public int getA() {
    return a;
  }

  public void setA(int value) {
    a = value;
  }
}
```

Среди последствий ответа на вопрос 5:
- Геттер и/или сеттер свойства можно перегрузить отдельно:
```Groovy
class B extends A {
  @Override void setA(int val) {
    a = val + 1;
  }
}
```
- Код выше выбросит `StackOverflowError` (почему?)
