# Предисловие
Я написал данную дорожную карту в первую очередь для того, чтобы собрать все самые необходимые знания в одном месте, как для себя, так и для других программистов. Данная карта поможет новичкам построить свой путь в мире Flutter без лишней воды и путаницы.

# 1. Dart Basics - in process
В данном разделе рассказываются самые базовые вещи, которые необходимы для работы с Dart.
## Built-In Types
### Основные типы данных:<br>
**Numbers:** int (не больше 64 бит, в зависимости от платформы), double (64-бит числа с плавающей запятой (двойной точности)<br>
**Strings:** String (UTF-16)<br>
**Booleans:** bool<br>
**Records:** (v1, v2)<br>
**Lists:** List<br>
**Sets:** Set<br>
**Maps:** Map<br>
**Runes:** Runes<br>
**Symbols:** Symbol<br>
**Null**: Null<br>

### Другие типы, с которыми вы постоянно будете сталкиваться:<br>
**Object** - суперкласс всех других классов, кроме Null<br>
**Enum** - суперкласс для создания списков<br>
**Future, Stream** - используются для асинхронного программирования<br>
**Iterable** - используется для создания классов-списков, а также функций синхронной генерации<br>
**Never** - указывает, что выражение никогда не сможет успешно завершить вычисление. Чаще всего используется для функций, которые всегда генерируют исключение.<br>
**dynamic** - указывает, что тип переменной может меняться по ходу программы.<br>
**var** - указывает, что тип переменной будет определен позже.<br>

>**Object, Object?, Null, Never** имеют особенную роль в иерархии классов. Подробнее об этом в разделе "Null-safety"<br>
## Variables
### Переменные определяются следующим образом:
```dart
int i = 2;
double d = 2.3;
String s = 'Something';
bool b = false;
List l = [2, 5];
Set s = {3, 4, 5};
Map m = {'s': 3};
```

### Подробнее про List:
**List** - это перечисление какого-либо объекта. Список может перечислять, как определенный тип, так и разные.
```dart
List<int> integers = [2, 4, 1, 25]; // Данный список может работать только с данными типа int
List<String> strings = ['some', 'thing', 'never']; // Данный список может работать только с данными типа String
```
Если вы захотите добавить в массив определенного типа другой тип, то будет следующее:
```dart
List<int> integers = [2, 4, 1, 25]; // Данный список может работать только с данными типа int
integers.add('asd'); // Ошибка: аргумент типа "Строка" не может быть установлен параметром типа "Число"
integers.add(24); // Ошибки не будет
```
Если вы хотите, чтобы в массиве можно было хранить разные типы, то можно использовать dynamic:
```dart
List<dynamic> list = ['some', 124, false];
// или 
List listB = ['some', 124, false];
```
> По умолчанию массив имеет тип dynamic, поэтому можно не писать тип.
> 
> Работа с типизацией типа у Set, Map такая же, как и у List. Происходит это благодаря Generics, подробнее о которых в **5.2**.

**Подробнее про Set:**
**Set** - это перечисление уникальных значений.
```dart
Set<dynamic> set = {2, 5, 1, 2};
```

> ЗАДАЧКА!
> Вам нужно получить уникальные значения из списка, что можно сделать?
> Ответ:
```dart
List list = [2, 3, 3, 5, 6];
Set uniqueList = list.toSet();// {2, 3, 5, 6}
```
 
### Подробнее про Map:
Map - это перечисление ячеек ключ-значение. Каждое значение имеет свой уникальный ключ, который может любым типом.
```dart
Map map = {'s': 3, 'd': 55};
Map<int, int> intMap = {3: 24, 4: 45};
```
>По умолчанию у ключа и значения тип **dynamic**.

## Operators
|Description|Operator|Associativity|
|---|---|---|
|unary postfix|_`expr`_`++`    _`expr`_`--`    `()`    `[]`    `?[]`    `.`    `?.`    `!`|None|
|unary prefix|`-`_`expr`_    `!`_`expr`_    `~`_`expr`_    `++`_`expr`_    `--`_`expr`_      `await` _`expr`_|None|
|multiplicative|`*`    `/`    `%`  `~/`|Left|
|additive|`+`    `-`|Left|
|shift|`<<`    `>>`    `>>>`|Left|
|bitwise AND|`&`|Left|
|bitwise XOR|`^`|Left|
|bitwise OR|`\|`|Left|
|relational and type test|`>=`    `>`    `<=`    `<`    `as`    `is`    `is!`|None|
|equality|`==`    `!=`|None|
|logical AND|`&&`|Left|
|logical OR|`\|`|Left|
|if-null|`??`|Left|
|conditional|_`expr1`_    `?`    _`expr2`_    `:`    _`expr3`_|Right|
|cascade|`..`    `?..`|Left|
|assignment|`=`    `*=`    `/=`   `+=`   `-=`   `&=`   `^=`   _etc._|Right|
|spread|`...`    `...?`|None|
## Functions
### Описание конструкции:
```dart
[TYPE] [NAME]([PARAMS]) [ASYNC] {}
```

### Функция, которая ничего не возвращает:
```dart
void func() {
/*
	your logic
*/
}
```

### Функция, которая возвращает какой-то тип:
>В таких функциях вам в любом случае надо вернуть какое-то значение указанного типа.

```dart
int func() {
/* your logic*/
	return 2;
}
```

### Асинхронная функция:
> **async** - означает, что функция является асинхронной.
> 
> Такие функции часто используются для запросов к API или для "параллельного" выполнения функции, пока выполняется следующий код.

```dart
Future<String> getString() async {//объявляем асинхронную функцию, которая возвращает строку
	await Future.delayed(const Duration(seconds: 5));// имитируем деятельность через асинхронное ожидание
	return 'some';// возвращаем ответ
}
Future<int> func() async {//объявляем асинхронную функцию, которая возвращает число
	String string = await getString();// дожидаемся выполнения getString() и получаем строку
	return string.length;//возвращаем длину полученной строки
}
```

### Функция с параметрами:
```dart
Future<String> getString(int seconds) async {//объявляем асинхронную функцию, которая получает кол-во секунд возвращает строку
	await Future.delayed(const Duration(seconds: seconds));// имитируем деятельность через асинхронное ожидание столько, сколько сказали извне
	return 'some';// возвращаем ответ
}
Future<int> func() async {//объявляем асинхронную функцию, которая возвращает число
	String string = await getString(10);// дожидаемся выполнения getString(10) и получаем строку
	return string.length;//возвращаем длину полученной строки
}
```

## Control FLow Statements
### Conditions
Как и во многих языках для условий используются операторы сравнения:

|Operator|Meaning|
|---|---|
|`==`|Equal; see discussion below|
|`!=`|Not equal|
|`>`|Greater than|
|`<`|Less than|
|`>=`|Greater than or equal to|
|`<=`|Less than or equal to|

```dart
bool b = false;
if(b) {// первичная проверка на условие
	/* some logic */
} else if (b == 25) {// проверка на условие, если не прошла первая. Таких может быть бесконечное множество.
	/* some elseif logic*/
} else {// событие, если никакое условие не было удовлетворено
	/* some else logic */
}
```

### Cycles
Существует несколько циклов: for, for in, while, while do.

## Classes
> Класс простым языком - это коробка, которая имеет в себе какие-то **параметры** (условно карандаши) и **методы**, которые может делать класс (открыть, закрыть коробку или ещё собрать, разобрать).

### Объявление класса:
```dart
class SomeClass {
}
```
Именно так выглядит пустой класс, который ничего не имеет и не умеет.

### Параметры внутри класса:
```dart
class SomeClass {
	int i = 0;
	bool isSome = false;
}
```
В данном случае у класса существует два параметра, оба из которых имеют значение, но так бывает не всегда.
Есть случаи, когда параметры должны быть инициализированы только, когда создаётся объект класса. Для такой инициализации используются конструкторы.

> Объект класса - это экземпляр, который имеет и умеет все то, что имеет и умеет класс.

### Конструкторы:
У класса может быть множество конструкторов.
```dart
class SomeClass {
	SomeClass(this.i, this.isSome);// базовый конструктор
	SomeClass.second({required this.i, this.isSome = false});//именованный конструктор
	SomeClass.third([this.i = 5, this.isSome = false]);
	int i;
	bool isSome;
}

SomeClass object1 = SomeClass(2, true);
SomeClass object2 = SomeClass.second(i: 2, isSome: true);
SomeClass object3 = SomeClass.third(2);
```

>Конструктор и функции могут принимать параметры, как в привычном нам виде: **()**, так в качестве именованных параметров: **{}**, а ещё опциональные параметры: **[]**.
>
>Именованные параметры очень удобны, когда у нас есть возможность не определять какие-то параметры, а также легче понять какое значение на какой параметр устанавливается.

>**Пример:** SomeClass.second({required this.i, this.isSome});
>**Разберём:**
>**required** - означает, что этот параметр обязательно должен быть указан при создании объекта. 
>**this.i** - указывает, что установлена должны быть переменная **i**.
>**this.isSome** = false - указывает, что можно установить параметр isSome, но он необязателен, так как по умолчанию он имеет значение **false**.

### Константные конструкторы:
Конструктор может быть константным, если все параметры будут final.
```dart
class SomeClass {
	const SomeClass({required this.i, this.isSome = false});
	final int i;
	final bool isSome;
}
```
Преимущество константных конструкторов в том, что мы можем создать константный объект и в случае полного совпадения параметров объект будет находится в одной ячейки памяти

# 2. Widgets - in process
## 2.1 Stateless Widgets
## 2.2 Stateful Widgets
## 2.3 Inherited Widgets
## 2.4 Styled Widgets
# 3. Design Principies, Patterns - in process
## 3.1 OOP
## 3.2 SOLID
## 3.3 Clean Architecture
## 3.4 Dependency Injection
# 4. Packages - in process**
## 4.1 pub.dev
## 4.2 flutter pub / dart pub
## 4.3 Top packages
#### Storage
#### API
# 5. Advanced Dart - in process
## 5.1 Lambdas
## 5.2 Generics
## 5.3 Class modefiers
## 5.4 Futures
## 5.5 Streams
## 5.6 Isolates
## 5.7 Functional Programming
# 6. State Managment - in process
## 6.1 Provider
## 6.2 BLoC
# 7. Advanced Flutter - in process
## 7.1 Garbage Collector
## 7.2 App Render Tree
## 7.3 Frame Render
## 7.4 Flutter Architecture
## 7.4 Platform Channels
# 8. Advanced Flutter - Animations - in process
## 8.1 Animation Controller
## 8.2 Animated Builder
## 8.3 Animated Widget
## 8.4 Curved Animation
## 8.5 Hero
## 8.6 Opacity
# 9. Testing - in process
# 10. DevTools - in process


