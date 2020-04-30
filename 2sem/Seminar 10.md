# Семинар 2020.04.23

## Пятиминутка
- Как в Groovy объявить package-private поле?
- Будут ли сгенерированы getter/setter для поля в Groovy, если явно указать его видимость (`public`, `private`, ...)?
- Какого типа следующие выражения: `'1'`, `"2"`, `'34'`, `"56"`, `"7${8}"`, `'''90'''`?
- Как вызвать метод у объекта, если его имя и аргументы известны только в рантайме? (На примере `class A { void doSmth(int a, String b) {} }`)
- Когда вызывается метод `invokeMethod` у `GroovyObject`, а когда - у `GroovyInterceptable`?


*Ответы*
- С помощью аннотации `@PackageScope`
- Нет
- `String`, `String`, `String`, `String`, `GString`, `String`
- `a.invokeMethod("doSmth", [1, "arg2"])`
- У `GroovyObject` - когда его вызвали явно или если вызываемый метод отсутствует у объекта; у `GroovyInterceptable` - при любом вызове любого метода (в т.ч. самого `invokeMethod`)