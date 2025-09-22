### Data Type: kiểu, hình thái của dữ liệu

1. Dữ liệu đơn giản - còn gọi là **primitive data**, **value-type data**

- là 1 thứ đơn giản, nó có sao là vậy. không có nhiều lời để nói về nó
- ĐƠN GIẢN: 5, 10, 15, 20, True, False
  **JAVA**: những thứ đơn giản như trên gọi là Primitive data
  **C#**: gọi là value-type data, em chỉ có value như vậy, that's all !!!
  _int, long, float, double, char, bool/boolean, short: primitive data type_
  value-type data

2. Dữ liệu phức tạp - còn gọi là

### Chuyền Đề: " Truyền Giá Trị " vào trong hàm, pass something into the method via paramters

1. Truyền tham trị - **Pass By Value**

- với kiểu dữ liệu primitive datatype, mặc định giá trị truyền vào hàm qua tham số, là truyền tham trị (pass by value)
- trong hàm thay đổi, bền ngoài giữ nguyên
  // hàm chỉ xin value của biến bên ngoài, copy value, tự chơi riêng
- C, JAVA, C# giống nhau 100% với primitive datatype, value type
- Nhưng C# còn làm hơn thế với primitive datatype !!!
  _C# có biến tấu thêm trên value-type, primitive data type với 2 từ khóa: out, ref_

2. Truyền tham chiếu - **Pass By Reference**

- từ khóa "out" trong C# xuất hiện ở tham số hàm mang ý nghĩa truyền tham chiếu biến tham số móc thẳng vào biến gốc ở nơi gọi hàm
- Biến "out" thay đổi value của biến gốc luôn
- trong hàm thay đổi, bên ngoài đổi theo, trong hàm biến out trỏ thẳng, Refer (v), Reference (N) tham chiếu gọi thẳng vào biến gốc ngoài hàm truyền thống: primitive / value - type chỉ truyền tham trị vào hàm nhưng trong c# thêm out lập tức thành tham chiếu !!!
- truyền thống: tham chiếu là đặc quyền của biến object, nay với C# primitive đc luôn nếu chơi out
  ==> out mang nghĩa là trong hàm em hứa, sẽ có 1 value đc trả về bên ngoài biến gốc em hứa có value return qua OUT !!!!
  chắc kèo là có value return ra ngoài !!!!
  phải có câu lệnh biến out = value nào đó trong hàm; để đảm bảo lời có value vứt ra

```C#
internal class Program
{
    static void Main(string[] args)
    {
        int n = 10;
        Console.WriteLine("Before calling method, n = " + n); // 10
        PowerByTwo(out n);
        Console.WriteLine("after calling method, x now is " + n); // 100
    }
    public static void PowerByTwo(out int x)
    {
        x = 100;
    }
}
```

==> **out** chính là hình thức return trong hàm qua tham số

> > Ứng dụng của sài OUT

- Hàm truyền thống trả về 1 value qua lệnh return và tên hàm
- Sử dụng out, hàm có thể trả về nhiều value qua tham số
- Ngạc nhiên chưa: hàm void cũng return đc value, qua out, và nhiều out
- Hàm trả về nhiều value: khi tiện ta đang for trên tập data, dùng 1 lượt for làm nhiều việc luôn!!!

_có 3 cách sài out_

```javascript
public static void PowerByTwo(out int x)
{
    int a = 10;
    int b = a;
    x = 100; // bên ngoài đổi theo đó em
    //int c;
}

 static void Main(string[] args)
 {
     // cách sài out kiểu 1
     //int n = 10;
     //Console.WriteLine("Before calling method, n = " + n);
     //PowerByTwo(out n);
     //Console.WriteLine("after calling method, x now is " + n);

     // cach sài out kiểu 2
     int n;
     PowerByTwo(out n); // biến đưa vào hàm out ko gán value
     // vì đằng nào hàm cũng out ra !!!
     Console.WriteLine("after calling method, x now is " + n);

     // cach sài out kiểu 3
     //PowerByTwo(out int n); // kĩ thuật khai báo inline
     // inline: khai báo biến ngay trong lời gọi hàm, ngay lúc đưa tham số
     //Console.WriteLine("after calling method, x now is " + n);
 }

```

- _Từ khóa ref_: cũng là nguyên lý truyền tham chiếu: trong hàm thay đổi, bên ngoài đổi theo nhưng mạnh như out, có thể trong hàm ko chỉnh sửa value đưa vào, ko cam kết có value mới đc kết quả !!!
- Thực chiến nếu hàm muốn hàm trả về nhiều giá trị -> ta nên là sự lựa chọn **out** hàng đầu!!!
  **ref**: !!!
- _Từ khóa in_: tham số đầu vào trở thành readonly, nghĩa là cầm thay đổi giá trị của biến đầu vào trong hàm, xài thì cứ xài, dùng value cứ dùng, cấm đổi value!!!
