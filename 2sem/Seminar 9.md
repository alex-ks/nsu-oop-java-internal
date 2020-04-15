# Семинар 2020.04.15

## Пятиминутка
- Какая типизация реализована в Groovy?
- Как объявить переменную в Groovy?
- Какой тип у выражения `[1, 2, 3]` в Groovy?
- Какой синтаксис у лямбда-выражений в Groovy?
- Какому Java-коду эквивалентен следующий код на Groovy: `class A { int a = 2 }`


*Ответы*
- Динамическая, неявная с опциональными типами
- Как в Java или через ключевое слово `def`
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
- Код выше выбросит `StackOverflowError`
