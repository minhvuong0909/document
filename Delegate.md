# Delegate: ủy quyền, ủy nhiệm

- Mối quan hệ tay ba:
  Dữ liệu - Kiểu dữ liệu - Biến
  Data DataType Variable

- Truyền hàm như 1 tham số

## I. Dữ liệu là gì ?

- Những thứ quanh ta được mô tả, đc viết ra dưới 2 hình dạng: đơn giản và phức tạp

**1. Dữ liệu đơn giản, trạng thái đúng sai**

- con số, con chữ, trạng thái đúng sai
- 5, 10, 15, 20, 3000
- A, B, C, $, #

2. Dữ liệu phức tạp - Object Data - gồm nhiều dữ liệu đơn giản hợp thành, tạo thành

- là 1 object, 1 chủ thể

## II. Data Type - kiểu dữ liệu

- là tên gọi chung (danh từ chung) cho 1 đám data đồng dạng, cùng hình dạng, cùng hình thức
- 5 10 15 20 -> đồng dạng: con số, nguyên con, ko lẻ miếng

---

- 3.14
  > > > từ những dữ liệu cụ thể đồng dạng (data), ta gom chung thành 1 tên gọi là data type

## III. Biến - Variable

- Biến là tên gọi riêng cho 1 data cụ thể nào đó
- Biến là tên gọi chi 1 data trong đám data type

```java
--- khai báo 1 deligate dựa với đầu vào là 2 tham số, đầu ra là int
public delegate int Calculate(int a, int b);

-- khởi tạo hàm
public int Add(int a, int b) => a + b;
public int Sub(int a, int b) => a - b;

--- sử dụng delegate
Calculate calc = Add;
int result = calc(5, 3); // Output: 8
result += cal(3, 2) // nó sẽ cộng vào cho kết quả tiếp theo

result.invoke(); // call method thông qua delegate
```

## Delegate với Anonymous method và Lamda, Event

```java
* Anonymous method
Calculate calc = delegate(int a, int b) { return a + b; };
calc();
```

```java
* Lamda
Calculate calc = (a, b) => a + b;
calc();
```

```java
* Lamda
Calculate calc = (a, b) => a + b;
calc();
```

```java
* Event chia các sự kiện dể dễ xử lý và tái sử dụng
public delegate void ProcessCompletedHandler();

public class Processor
{
    public event ProcessCompletedHandler OnCompleted;

    public void Run()
    {
        // Logic...
        OnCompleted?.Invoke();
    }
}
```

## Delegate tích hợp sẵn với Action, Func, Predicate

```java
- Action<String>: lun trả về string đối với Action
Action<string> log = msg =>
{
    Console.WriteLine("Thông báo " + msg);
};
log("Học C# cơ bản");
```

```java
- Func<int, int, int>: lun trả về int | double | float | number đối với Func
Func<int, int, int> sum = (x, y) => x + y;
int result = sum(5, 10);
Console.WriteLine("Kết quả: " + result);
```

```java
- Predicate<int>: input vào có thể là String Number return của sẽ trả về true | false
Predicate<int> isEven = x => x % 2 == 0;
Console.WriteLine("True | False: " + isEven(2));
```

### Name convention - nguyên tắc đặt tên

- `Động từ + Delegate`
  VD: CalculateDelegate
- `Danh từ + Handler`
  VD: NotificationHandler
- `Danh từ + EventHandler`
