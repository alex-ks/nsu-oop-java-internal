# Семинар 2020.04.15

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
  - слабая ([документация о преобразовании типов](https://docs.groovy-lang.org/latest/html/documentation/core-semantics.html#_promotion_and_coercion) и [блог с примерами](https://e.printstacktrace.blog/groovy-dynamic-types-coercion-and-promotion-you-have-been-warned/)), но сильная при статической компиляции (поскольку определение сильной/слабой типизации и так довольно размыто, этот пункт я не буду учитывать при оценке)
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

  public int setA(int value) {
    a = value;
  }
}
```

Среди последствий ответа на вопрос 5:
- Геттер и/или сеттер свойства можно перегрузить:
```Groovy
class B extends A {
  @Override void setA(int val) {
    a = val + 1;
  }
}
```
- Код выше выбросит `StackOverflowError` (почему?)
