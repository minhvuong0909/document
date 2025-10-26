# DB trong c#

- Với ngôn ngữ lập trình nói chung, có 2 cách chơi với db

  - Code First: ta dùng code để tạo ra table, tạo ra data trong table, code này là code OOP
  - Database First: ta có table có sắn trong database rồi, từ db, từ table ta suy ngược lên thành code, thành các class OOP

  => style nào cũng giống nhau: cuối cùng là code OOP để CRUD table
  => ta dùng ORM - Object Relational Mapping: là kị thuật ánh xạ 1 class thành 1 table , 1 object thành 1 dòng trong table

  ko dùng câu SQL truyền thống mà chỉ là class, object, method là đã CRUD đc table, thì đó gọi là ORM
  ngầm phía sau vẫn là SQL truyền thống, nhưng đc che bởi .Method() .gọi hàm()

  => trong java, ORM đc hiện thực qua thư viện - FRAMEWORK: Hibernate, Eclipse-link,...
  =. trong C#, ORM đc hiện thực qua thư viện: EF core - Entity Framework Core (hàng chính hãng)
  dapper -> hàng open-source

  => trong nodejs: "ORM Framework For ... ngôn ngữ lập trình đang dùng

  I. chơi với EF Core

  - EF core là bộ thư viện giúp c#, .Net móc nối với database: truyền thống, dựa trên table, còn gọi là RDBMS - relational Database Management System

    - Hiện đại, ko dựa trên table và sql, còn gọi là NoSQL MongoDB, Redis, Casandra,...

  - EF core gồm 2 bộ công cụ ta cần tải về máy

  1.  .DLL dùng trong code, tức là những class cần đc import vào trong project để có class ta khai báo trong code, để crud data table
      -> dll dùng trong code đc gọi là dependency ( y chang java, nodejs, react,...) và ta tải về qua 1 tool riêng gọi là NuGet
      -> NuGet là 1 tool trong hệ sinh thái, .Net giúp tải, quản lí các thư viện, .Net nó y chang ( maven ) bên java, y chang ( npm ) bên nodejs, y chang ( pip ) bên python

  2.  Tool dùng để gõ lệnh ở cửa sở terminal để giúp đồng bộ cấu trúc code mapping xuống table, tức là nếu table thêm cột, thì code cũng đc update ngược lại code update field nào đó, table thêm cột

---

bài thi PE ko cần là mục 2. do tool đã cài bây h rồi thì vào phòng thi cứ thế mà dùng mục 1. thì phải cài lại

-- kiểm tra xem EF core, tool, đã cài chưa
`dotnet tool list --global`: kiểm tra đã cài hay chưa

-> gỡ tool để có thể cài lại, hoặc cài version mới hơ
dotnet tool uninstall dotnet-ef -g

-- lệnh cài tool ef-core bản mới nhất nhưng phải ứng với .Net sdk version

máy tính đang cài .Net 9.x nhưng trên mạng đang .Net 10.x

- EF Core mới nhất 9.X EF Core mới nhất 10.x

`dotnet tool install --global dotnet-ef --version 9.\*`

database first với EF CORE -> sinh ra class map với table !!! table có trước, class có sau

FA25_BookDB

WORKLOADS

**dotnet ef dbcontext scaffold "Server=(local);uid=sa;pwd=12345;database=PRN212_Bookstore;TrustServerCertificate=True" Microsoft.EntityFrameworkCore.SqlServer --output-dir Entities --context-dir ./** là câu lệnh dùng để tạo các entities trong project

Khi cần lưu nhìu thông tin, ta dùng collection framework - 1 nhóm các class dùng để chứa nhìu info trong nó: List, Map, Set (java)

- Java: List<Student> bag = new ArrayList<>();
  ArrayList<Student>bag = new ArrayList<>();

- C# List<Student> bag = new ArrayList<>(); // ko dùng ArrayList

-> nhét đồ vào balo đi du lịch
bag.add(món đồ); // Java // món đồ: biến object trỏ vùng new
bag.Add(món đồ); // C# // trong bag chứa con trỏ khác trỏ
// vùng new bự chứa object, chứa info thật
// nhét đồ vào túi thực ra là nhét tham chiếu. Ngoài đời chính là tờ giấy chứa danh sách đăng kí, danh sách kí tên, Khi đăng kí, ta ko ngồi lên tờ giấy, ta chỉ để lại số di động chính là tham chiếu
bag chứa danh sách obj đc add vào, vậy for/FOR trong bag tức là duyệt qua danh sách!!!!!
nhìn vào cái túi cái giỏ coi có gì, tức là FOR
for (Student x : bag) java for each toán tử A ngược
foreach (Student x in bag) C#
với mỗi, ovi71 mọi x thuộc tập hợp
-> quăng đồ ra khỏi balo:

scaffo là câu lệnh suy ngược lại

**tên namespace mặc định của app nhưng nó ko bắt buộc giống với tên project**

click vào file .json click F4 chọn copy to output chỉnh lại thành always

microsoft.extensions.Configuration
microsoft.extensions.Configuration.json

---

## DbContext

- DbContext là class cha, chứa những câu lệnh thao tác của câu lệnh CRUD của các table trong csdl

```java
public virtual DbSet<Book> Books { get; set; }
//              List<Book> _bag = new sẵn ròi, có data luôn rồi
//                         ._bag, .Books nghĩa là đã select * rồi
// muốn xóa 1 cuốn sách thì sao:
//                             ._bag.Remove()   .Books.Remove(...)
//      for each là đi qua hết các cuốn sách!!!!!!!!!!
//  OOP 100%, code first!!! chơi db mà toàn là object và chấm
//
```

- **Các bước thực hiện trong DbContext**

```java
1.  phải new DbContext
2.  sờ vào các DbSet<?> trong DbContext
3.  For each để lôi ra từng dòng của table, nay là từng object của class thuộc Entities\
     Prn212BookstoreContext ctx = new(); // móc vào db rồi chỉ sờ vào 3 cái túi
    ctx.Books // trả về \_bag chứa toàn sách đã đc select
    BookListDataGrid.ItemsSource = ctx.Books.Include("BookCategory").ToList(); // include nghĩa là join với bảng Category, lấy tên biến tham chiếu, ko lấy data type, vì đang chơi object, phải là tên biến
    DbSet<> rất giống List, nhưng ko là List, ta cần convert về List<>
    DbSet giúp mình hậu trường select \* from
    ==> List chỉ trong ram, nên cần convert
```

- **Các bước config connection trong DbContext**

```java
- Cài đặt 2 thư viện này microsoft.extensions.Configuration
                        microsoft.extensions.Configuration.json

- lấy chuỗi từ hàm nhét vào DbContext
- click vào file .json click F4 chọn copy to output chỉnh lại thành always.
```

## Đề thi PE bao gồm

- File .sql để tạo database

- File "Note.docx" có những ghi chú cần nhớ. trong đây chứa:

  - tên các thư viện Nuget cần tải về
  - các lệnh db scafford để generate class từ table
  - chứa lệnh kết nối csdl - connection string
  - chưa cấu trúc, nội dung file appsettings.json
  - chứa hàm đọc file json trả về chuỗi kết nối csdl

- File đề thi "EXAM PAPPER.docx"

* tải 3 file này về từ phần mềm PEA
* lưu ý: đọc kĩ các chỉ dẫn trong đề, trong file ghi chú, làm theo chính xác

2. chạy file .sql để có database để sẵn sàng cho việc generate entity class và dbContext class

- Database luôn cho 3 table, 1 table đứng 1 mình dành cho login, 2 table còn lại mối quan hệ 1 - N ( Major - Student, Category - Book)

* Table đúng 1 mình:
  chứa thông tin account để login, chứa thông tin role: admin, manager, staff, member
  thường login qua email/pass

role quyết định khi login thành công thì đc CRUD thế nào ?

- 2 table 1 - N
  Category có nhìu Book

- 3. tạo mới solution, chọn WPF là project chính - chứa GUI
- đặt tên solution như đề thi yêu cầu - có Mã số SV, tên SV
- đặt tên project WPF như đề thi yêu cầu - có Mã số SV, tên SV
- chú ý nơi lưu bài thường lưu ở khu vực deskstop

vd: deskstop PE_PRN212
PE_SWT301
PE_SWR302

<!-- 3.Create Solution in Visual Studio 2019/2022 named PE_PRN212_SU24TrialTest_StudentName.
Inside the Solution, Project WPF named: AirConditionerShop_StudentName. -->

3.1. Tạo lun 2 class entity library project để code theo kiến thức 3 layer

-- DAL: data access layer - project lo chơi với table
-- BLL: business logic layer - lo sử lý trong RAM - if else, List<>
--

3.2. add 1 lèo, 1 lúc 6 thư viện (4 cho database, 2 cho json)

- cần vào wifi trường để download thư viện -> khảo thí biết điều này, giám thị biết điều này (khiếu nại ở 117, 119 fix máy tính)
- click phải chuột DAL project (ko phải GUI project), add dependency -> nuget
- tên 6 thư viện có sẵn trong file note ko cần nhớ, nhưng nên nhớ cho nhanh

Microsoft.EntityFrameworkCore
Microsoft.EntityFrameworkCore.Design
Microsoft.EntityFrameworkCore.SqlServer
Microsoft.EntityFrameworkCore.Tools
Microsoft.Extentions.Configuration
Microsoft.Extentions.Configuration.Json

cấm quên quan trọng
**MENU BUILD | BUILD SOLUTION**

4. Generate Entities class và DbContext

- đứng ở DAL để làm, đúng chỗ khác thì toang, vì ko có thư viên để connect DB
- click phải chuột trên DAL, chọn open terminal
- copy câu lệnh đã chỉnh sửa pass từ file note.docx dán vào để tạo ra entities

5. di chyển chuỗi kết nối csdl ra khỏi dbContext

- tạo appsettings.json trên GUI vì GUI là app chính chạy từ app chính, cho nên json phải chạy ở WPF project
- copy content json từ file ghi chú, bỏ vào file json
- copy hàm đọc json từ file ghi chú, bỏ vào DbContext
- sửa hàm ON_Configuring để đọc file json

**Table đứng 1 mình**

```java
- chứa thông tin account để login, chứa thông tin role: admin, manager, staff, member
thường login qua email / pass
VD:
  ID  | email | pass | fulName | Role
  1     ad@     x                 1 (admin)
  2     st@     x                 2 (staff)
  3     mg@     x                 3

  - Role quyết định khi login thành công thì d9c CRUD thế nào?
```

- về nhà: tạo sẵn 3 màn hình
- LoginWindow có sẵn ô nhập Email, Pass, 2 nút Login, Quit
- MainWindow có sẵn: grid, dàn nút Create, Update, Delete, Quit
- Detail Window có sẵn: dàn 7 ô nhập và 1 comboBox ứng với table AirConditioner
  đặt tên sẵn lun
