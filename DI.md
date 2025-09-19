# Giải ngồ về Dependency Injection

### Dependency là gì ?

- Nếu Class A khai báo biến thuộc class B, cần B để giúp công việc gì đó cho A, mà B chyên trách, B giỏi thì B gọi là dependency của A hoặc A phụ thuộc vào B.

```Java
    public class A {
        B objB; // objB là obj, thuộc, được clone từ class B
                // B đc gọi là dependency của A, A phụ thuộc vào B để làm gì đó
    }

    public class B { // giỏi việc nào đó, chyên việc nào đó
        // ...
        void doSomething() {...}
    }
```

- Dependency còn là các **thư viện** lập trình ( chẳng qua gồm bên trong nhiều class làm việc gì đó rất giỏi), ta có JDBC Dependency, Hibernate, JPA Dependency,...

- A phụ thuộc vào B, B là dependency của A, tức là 2 class có gắn kết, cần nhau (A cần B đúng hơn) gọi là **COUPLING**

### Tight coupling, Loose coupling - chắc chắn phải dính dáng dependency, class này cần class kia

1. **Tight coupling - gắn kết, phụ thuộc chặt chẽ**

- Class A cần Class B, quản lí luôn vòng đời object class B (tạo, hủy) trong lòng class A

```java
    public static void main() {
        A objA = new A(); // khi new A đã có ngay B bên trong lòng
                          // có A là đã có B
    }
    public  class A {
        B objB = new B(); // tight coupling
    }

    public class B { // giỏi việc nào đó, chyên việc nào đó
        // ...
        void doSomething() {...}
    }
```

    **Vấn đề của tight coupling**
    - A chỉ chơi với B mà thôi
    - Khi B chưa code xong, thì khó có thể run A
    - Nếu muốn thay thế B bằng B' tương đương về khả năng giải quyết vấn đề ( thay hibernate bằng EclipseLink ??? ), thì chắc chắn phải sửa code của A !!!
