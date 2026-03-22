# Setup Source Code With `C#` By Architecture Microservice

---

### 1. Cài đặt môi trường

- download tool:
  `.NET SDK 8^  `
  `Docker Desktop`
  `Visual Studio 2022 ^`

### 2. Tạo project || solution

- Tạo solution

```
dotnet new sln -n `ten_solution`
```

- Tạo project Gateway

```
dotnet new webapi -n GatewayAPI
```

- Tạo các services

```
dotnet new webapi -n AuthAPI
dotnet new webapi -n EmailAPI
```

- Tạo Class Libraries

```
dotnet new classlib -n MessageBus
``dùng để giao tiếp giữa các service
VD: request và response model
``
```

```
dotnet new classlib -n Contracts
`dùng để định nghĩa dữ liệu và quy ước chung cho các project giao tiếp nhau`
```

```
dotnet new classlib -n Common
 ``dùng để chứa các đồ dùng chung cho hệ thống
VD: ApiResponse<>
    BusinessExpception
```

```
dotnet new classlib -n Extensions
``chứa extension methods để cấu hình DI, middleware, configuration
VD: IConfiguration
    WebApplication
``
```

### 4. Thêm các project vào solution

```
dotnet sln add GatewayAPI
dotnet sln add AuthAPI
dotnet sln add EmailAPI
dotnet sln add ServiceAPI

dotnet sln add MessageBus
dotnet sln add Contracts
dotnet sln add Common
dotnet sln add Extensions
```

---

Solution
│
├── GatewayAPI
│
├── Services
│ ├── AuthAPI
│ ├── EmailAPI
│ └── ServiceAPI
│
├── BuildingBlocks
│ ├── MessageBus
│ ├── Contracts
│ ├── Common
│ └── Extensions
│
└── docker

### 5. Setup API Gateway (YARP)

```
dotnet add GatewayAPI package Yarp.ReverseProxy
```

Program.cs

```dotnet
using Yarp.ReverseProxy;

var builder = WebApplication.CreateBuilder(args);

builder.Services
    .AddReverseProxy()
    .LoadFromConfig(builder.Configuration.GetSection("ReverseProxy"));

var app = builder.Build();

app.MapReverseProxy();

app.Run();
```

appsettings.json

```json
{
  "ReverseProxy": {
    "Routes": [
      {
        "RouteId": "auth",
        "ClusterId": "authCluster",
        "Match": {
          "Path": "/auth/{**catch-all}"
        }
      },
      {
        "RouteId": "email",
        "ClusterId": "emailCluster",
        "Match": {
          "Path": "/email/{**catch-all}"
        }
      }
    ],
    "Clusters": {
      "authCluster": {
        "Destinations": {
          "d1": {
            "Address": "http://authapi:5000/"
          }
        }
      },
      "emailCluster": {
        "Destinations": {
          "d1": {
            "Address": "http://emailapi:5000/"
          }
        }
      }
    }
  }
}
```

`Lưu ý:` port nội bộ 5000 phải đồng bộ với docker file

### 6. Cấu trúc của 1 Service

`có thể dùng clean architecture trong này`
ServiceAPI
│
├── Controllers
├── Services
├── Repositories
├── Entities
└── DTO

### 7. Setup MessageBus (Kafka | RabbitMQ)

==> Dùng để xử lý giao tiếp bất đồng bộ giữa các service qua RabbitMQ/Kafka.

MessageBus.cs

```dotnet
public interface IMessageBus
{
    Task Publish<T>(T message);
    Task Subscribe<T>();
}
```

### 8. setup docker

```
docker-compose.yml : chạy toàn bộ của hệ thống

lệnh chạy hệ thống
docker-compose up --build
```

- phải tạo Dockerfile cho mỗi services
