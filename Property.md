# Nhập môn Property trong C# - không có trong Java

- Kiến thức core, cốt lõi, must know

## I. Get / Set là gì???

- Get (lấy ra) là lấy thông tin đc lưu trữ trong biến
- Set (thay đổi đi) là chỉnh sửa thông tin đc lưu trữ trong biến

## II. MỖi biến bất kì đã bao hàm khái niệm GET và SET

- Xét khai báo:

```java
int yob = 2005;
- Tên biến chính là value, chính là Get rồi
sout(yob) -> màn hình in 2005; get giá trị ròi mới in đc cw(yob);
- Ta viết hàm Get:
public int GetYob () {
    return yob;
}
- Tên biến đã bao hàm sẵn value để GET, dùng tên biến đã là GET rồi, khỏi cần 1 cái hàm bên ngoài, rồi cuối cùng cũng return tên biến mà thôi
```

```java
Set -> tên biến = ???, chính là set rồi
int yob = 2005;
yob = 2007; // set giá trị mới ròi

public void SetYob (int value) {
    this.yob = value;
}
- Tên biến đã bao hàm sẵn value để SET, dùng tên biến = VALUE đã là SET rồi, khỏi cần 1 cái hàm bên ngoài
```

=> Hàm Get() và Set() bản chất vẫn là thao tác trên biến liên quan !!! dùng trực tiếp tên biến đã bao hàm Get và Set

- Vậy cái đoạn code Get() và Set() đang viết nó cần thiết, nhưng nhàm chán, ko mới mẻ, nhưng phải viết để object nó tự nhiên khi giao tiếp: lấy thông tin ra, thay đổi thông tin
  Đoạn code nhàm chán nhưng phải làm gọi là Boiler-Plate !!!
  **->** C# ko hỗ trợ generate đám boiler-plate, làm bằng tay
  -> C# cung cấp cách thức để thay thế đoạn code Get / Set chán đời tức là tận dụng ngay tên biến làm Get và Set
  vì tên biến đã bao hàm sẵn Get và Set !!!
  -> C# lợi dụng biến đã có Get Set, chế thêm 1 biến trai bao, biến tiếp tân, biến bồi bàn, bao bên ngoài biến \_
  đóng 2 vai Get Set
  Yob đóng vai get nếu .Yob
  Yob đóng vai set nếu .Yob = ??? value gì đó
  thằng \_yob đúng phía sau phục vụ -> gọi tên mới: Biến chống lưng
  (backing field)
  **Property - là 1 đặc tính của 1 object**

## Có 5 cách khai báo 1 Object

```javascript
- Khai báo đầy đủ
        public static void CreateObject()
        {
           Student stu = new Student("SE1", "vuong", "2005", 8.6);
           Console.WriteLine(stu);
        }

- Bỏ vế phải
        public static void CreateObjectV2() {
            Student stu = new("SE1", "vuong", "2005", 8.6);
            Console.WriteLine(stu);
        }

- Bỏ vế trái và thẹm datatype `var`
        public static void CreateObjectV3() {
            var stu = new Student("SE1", "vuong", "2005", 8.6); // type infference: tự suy luận kiểu !!!
            Console.WriteLine(stu);
        }

- named-argument: tham số đưa vào có đính kèm tên tham số
        public static void CreateObjectV4()
        {
            var stu = new Student(gpa: 8.6,yob: "2005",name: "vuong",id: "SE1"); // cho phép truyền lộn xộn thứ tự tham số miễn là ghi tên tham số kèm dấu: phía trước giá trị đưa vào!!
            Console.WriteLine(stu);
        }

- object initializer: tạo object và khởi động luôn set theo ý muốn
        public static void CreateStudentNewStyle()
        {
            //Student stu = new Student(); // mang default value bên trong
            // muốn sửa bên trong thì gọi hàm set

            Student an = new Student()
            {
                Id = "SE1",
                Name = "An",
                Yob = 2007,
                Gpa = 8.0
                // object initializer - tạo object và khởi động luôn hàm set theo ý muốn !!!
                // 1 ctor rỗng vô số cách đổ vào !!!
            };
            Console.WriteLine($"|{an.Id}|{an.Name}|{an.Gpa}|{an.Yob}|");
        }
```
