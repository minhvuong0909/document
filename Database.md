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

**dotnet ef dbcontext scaffold "Server=(local);uid=sa;pwd=12345;database= FA25_BookDB;TrustServerCertificate=True" Microsoft.EntityFrameworkCore.SqlServer --output-dir Entities --context-dir ./** là câu lệnh dùng để tạo các entities trong project
