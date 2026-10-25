- чтобы исполнить java код нужна jvm на платформе исполнения
- в jvm поступает byte code

# JAVA code -> compile -> byte code -> JVM

В процессе компиляции код собирается эффективным образом под опрделенную арх-ру

### JDK - Java development kit


Семейство JVM языков
Java\Kotlin\Scala\Jython\...

эти языки компилируют в байт код

#### примитивы  
byte 1  
short 2  
int 4  
long 8  
char 2  
boolean 1  
float 4  
double 8  
#### ссылки  
  
Напротив примитивов есть одноимённая обёртка класса  
Integer <- int  
  
Integer. parseInt("123") -> 123