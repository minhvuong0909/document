# Nhập môn Property trong C# - không có trong Java

- Kiến thức core, cốt lõi, must know

## I. Get / Set là gì???

- Get (lấy ra) là lấy thông tin đc lưu trữ trong biến
- Set (thay đổi đi) là chỉnh sửa thông tin đc lưu trữ trong biến

## II. MỖi biến bất kì đã bao hàm khái niệm GET và SET

- **Class**: là cái khuôn, template, biểu mẫu (form), blue-print chờ đổ info vào để clone ra 1 sản phẩm, 1 object.
- **Constructor**: hàm khởi tạo, phễu đổ vật liệu vào khuôn, có nhiều cách fill into vào khuôn, có nhiều constructor. => **để đúc ra 1 Object**
- **Phím nóng tạo constructor**:
  - `ctor tab tab`: tạo constructor default.
  - `ctrl .`: tạo constructor có members.
- Xét khai báo:

```java
int yob = 2005; // hay còn gọi là backing field
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

- named-argument | terms | terminology: tham số đưa vào có đính kèm tên tham số
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

---

**Property trong C# là kĩ thuật viết GET SET kiểu mới, thông qua biến public bao luôn sau đó, trong nó 2 hàm GET SET;**

- Xài Get Set kiểu mới y chang xài biến, tên biến - tên property là GET
  tên biến - tên property = ??? là set
- Giúp việc xài Get Set tự nhiên hơn kì nhiều, thay vì .GetYob() nay chỉ còn .Yob và thay vì .SetYob(2005) nay chỉ còn .Yob = 2005
- Tuy nhiên phía sau vẩn cần Field _yob _... mang ý nghĩa backing field thằng chống lưng lưu info cho hàm Get Set

---

### Có 2 loại cú pháp PROPERTY !!!

[1] **Full Property - dùng phím nóng `Propfull tab tab`**

- Prop dạng này đầy đủ cú pháp, gồm cả backing field và tên hàm Get Set Full Code
- Cú pháp này dùng khi mình muốn If Else trong các hàm Get Set check Validation khi gọi Get Set !!!

[2] **Auto Implemented Property - Auto Property - Phím nóng `prop tab tab`**

- Sử dụng này thì nó sẽ tư sinh backing field ẩn danh khi BUILD AND RUN
- Kĩ thuật viết prop kiểu ngắn gọn, tự sinh ngầm _\_ten-bien_ đc gọi là **auto implemented property**

---

# Kĩ thuật Nullable

- **null** trong database nghĩa là giá trị của cell - ô chưa xác định đc, chưa biết nó sẽ là gì đó trong tương lai | trạng thái chưa xác định rõ, ko là value đong đếm so sánh đc.

- **Giải pháp cho phép null:**

  - dấu _?_ mang ý nghĩa là bạn đc quyền gán giá trị là null.
  - Nếu 1 cột trong database là null, khi đọc vào biến tương ứng trong class, thì biến này cũng phải mang ý nghĩa null.
  - **Primitive data type - kiểu dữ liệu nguyên thủy** ko phép null, bắt buộc phải có giá trị gì đó và nếu bổ sung thêm dấu `?` ngay sau data type để cho phép biến primitive mang null !!!!

  ```java
  int? value;
    -Trường hợp value là field của class → mặc định nó sẽ là null.

    -Trường hợp value là biến cục bộ (local variable) trong hàm → bạn chưa khởi tạo nên sẽ báo lỗi compile:
        "Use of unassigned local variable 'value'."


    => fix lại:
     int? value = null;
     -Sẽ chạy đc và không hiển thị gì.
  ```

**Áp dụng trong method**

```java
-- ĐỐI VỚI PRIMITIVE
public static void PlayPrimitiveNullable()
{
    // int long float double bool char short byte
    int? yob; // những biến đc gán giá trị mặc định, những biến primitive nếu nó là backing field thì sẽ mang default nếu ko đc gán giá trị khi new object


    // biến local tức là khai báo trong method thì chưa gán giá trị, ko cho xài
    yob = null;
    Console.WriteLine(yob);
}

public static void PlayObjectNullable()
{
    Student? an = new Student() { Id = 123, Name = "Vương" };
    Console.WriteLine(an.ToString());

    an = null;
    Console.WriteLine(an.ToString());

    // biến primitive - value-type ko đc mang null, ráng gõ, lỗi cú pháp

    // biến primitive, value-type mún mang null thì phải là nullable ?
    // vẫn xài bình thường khi in, ko bị exception

    // biến object đc quyền gán = null mà ko cần ?
    // sẵn có null mà ko cần ?, có ? vào cũng đc, ko cũng ko sao !!!
    // nhưng nếu ráng xài hàm của biến object đang null => exception liền ngay và luôn !!!
    // NULL REFERENCE EXCEPTION !!!!!!!!!!!!!!!!!!
    // if (bien != null) đc quyền dùng nullable và biến object

}


public static void PlayObjectNullableV2()
{
    Student? an = new Student() { Id = 123, Name = "Vương" };
    Console.WriteLine(an.ToString());
    //an = null;

    Student? anClone = an; //2 chàng trỏ 1 nang
    //Console.WriteLine("an 2: " + anClone.ToString());
    anClone.Gpa = 8.8;
    //Console.WriteLine("an: " + an.ToString());
    an = null;
    Console.WriteLine("an: " + an.ToString());

    Console.WriteLine(anClone.ToString()); //null exception chắc luống. vì đây ram ko có object

    //nếu vùng ram ko có ai trỏ, ko có biến giữ lại, vùng ram mồ côi, con diều dứt dật, bộ gom rác - garabage collection định kì theo phần trăm giây sẽ clear vùng object để dành cho lệnh new khác. new tốn ram, con trỏ null là giải phóng vùng ram new
    //mặc định object dc xài null mà ko cần ?. có cx đc
    //2 biến obj = nhau, nghĩa là trỏ chung vùng ram
    //biến trong hàm mà chấm gọi hàm, bên ngoài đổi theo do cả 2 cùng trỏ 1 vùng new

}
```

- Lamda, Deligate
