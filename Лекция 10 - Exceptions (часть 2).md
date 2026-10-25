```java
public Main {  
    static void main() {  
        System.out.println(test());  
    }  
  
    static void test() {  
        System.out.println("start");  
        try {  
            sum(2, 3);  
        } catch (IOException e) {  
            System.out.println("catch");  
        } finally {  
            System.out.println("fnially");  
        }  
        System.out.println("end");  
    }  
    public static int sum(int x, int y) throws IOException{  
        if (x < 0) throw new IOException();  
        return x + y;  
    }  
}
```

```
start
cat
```