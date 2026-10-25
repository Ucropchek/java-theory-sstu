```java
class A extends Object {
	
}
```

---
```java
String toString(); // Нужно знать где он нужен, но с помощью него не сформировать JSON (не надо точнее)
```

```java
boolean equals(Object); // если переопределили его, то ОБЯЗАНЫ переопределить hashCode(); Нужен для свравнение объектов по содержанию, а не по ссылке
```

```java
int hashCode(); // числовая свертка объекта
```
---
```java
protected Object clone(); //есть и можно переопределить, но он невеликий
```
---
```java
final Class getClass(); // возвращает полную информацию о методах полях класса
```

```java
final wait() notify() notifyAll(); // управление потоками
```

## Многопоточность

Многопоточность про выполнение одной большой задачи параллельными процессами

если для мытья пола надо убрать стол, то уборщик встает на wait()

если я убираю стол, то вызываю notify() для одного уборщика или notifyAll() для всех, чтобы кто-то помыл полы под ним и встал на wait() после

**==🔴с wait() никто не уходит автоматически. Надо где-то вызывать notify()==**

По-другому:
*Убран/не убран помыл пошел дальше* (проблема в том, что много ресурсов уходит на проверки)

==🟢Нормальное решение:==

```java
class MyController {
	Repository repo;
	String hello(String name) {
		return "hello" + repo.findFullName(name);
	}
}
```

Проблема многопоточности: если оба обращаются к одному и тому же
например: запись и чтение (пока читаем, кто-то записывает)

==🔵Собесы на senior забиты многопоточностью==

```java
public class Main() {
	static void main() {
		
	}
	
	static void change(B b) {
		synchronized(b) {
			b.x = 99;
			b.notify();
		}
	}
}

class B extends A {
	int x;
	synchronized void test() throws InterruptException {
		if (x == 0) {
			this.wait(); // - бросает Exception, но пока это неважно
		}
	}
}
```

synchronized(b) - метод который не может выполниться, пока открыт параллельный монитор

 Уровень изоляции и транзакции - место где в основном решаются проблемы многопоточности

*native - внутри плюсовый код из какой-то библиотеки*

```java
public class Main() {
	static void main() {
		Class clz = new B().getClass();
		Arrays.asList(clz.getMethodsDeclared()).forEach(System.out::println); // все кроме test()
		Arrays.asList(clz.getMethodsDeclared()).forEach(System.out::println); // только test()
	}
	
	static void change(B b) {
		synchronized(b) {
			b.x = 99;
			b.notify();
		}
	}
}

class B extends A {
	int x;
	synchronized void test() throws InterruptException {
		if (x == 0) {
			this.wait(); // - бросает Exception, но пока это неважно
		}
	}
}
```

---
## equals()

В большинстве случаев equals выглядит вот так:

```java
мы в классе B
@Override
public final boolean equals(Object o) {
	if (o == this) return true;
	if (o == null || !(o instanceof B b) return false;
	return x == b.x;
}
```

нельзя вызывать equals от неопределенной ссылки, если в сравнении есть определенная (делаем наоборот)

equals работает по правилам из дискретки:
==🟠a == a, a == b & b == c, a == b -> b == a, a == b b == a==

у родителей лучше делать final equals, чтобы сохранить симметричность, но тогда нельзя сравнить по состоянию наследников

---
## hashCode()

```java
public class Main() {
	static void main() {
		List<B> = new ArrayList<B>();
	}
}
```


| B(1) | B(2) | B(6) | B(3) |     |     |      |     |     | массив   |
| ---- | ---- | ---- | ---- | --- | --- | ---- | --- | --- | -------- |
|      |      |      |      |     |     | B(3) |     |     | **мапа** |
|      | B(1) | B(2) |      |     |     | B(6) |     |     |          |

int ограничен вместимостью, поэтому на основе хэш-кода мы вычисляем позицию массива в мапе

```java
мы в классе B
@Override
public int hashCode() {
	считаем число;
}
```