# FastAPI 教程讲义

---

## 目录

1. [FastAPI简介](#第一章-fastapi简介)
2. [环境搭建与安装](#第二章-环境搭建与安装)
3. [第一个FastAPI应用](#第三章-第一个fastapi应用)
4. [路径参数](#第四章-路径参数)
5. [查询参数](#第五章-查询参数)
6. [请求体](#第六章-请求体)
7. [Pydantic模型详解](#第七章-pydantic模型详解)
8. [响应模型](#第八章-响应模型)
9. [查询参数与字符串校验](#第九章-查询参数与字符串校验)
10. [路径参数与数值校验](#第十章-路径参数与数值校验)
11. [Cookie和Header参数](#第十一章-cookie和header参数)
12. [依赖注入系统](#第十二章-依赖注入系统)
13. [安全性与认证](#第十三章-安全性与认证)
14. [中间件](#第十四章-中间件)
15. [CORS跨域资源共享](#第十五章-cors跨域资源共享)
16. [数据库操作](#第十六章-数据库操作)
17. [错误处理](#第十七章-错误处理)
18. [后台任务](#第十八章-后台任务)
19. [测试](#第十九章-测试)
20. [部署](#第二十章-部署)

---

## 第一章 FastAPI简介

### 1.1 什么是FastAPI

FastAPI是一个现代、快速（高性能）的Python Web框架，用于构建API。它基于Python 3.7+的类型提示，充分利用了Python的现代特性。

**FastAPI的主要特点：**

| 特点 | 说明 |
|------|------|
| 快速 | 极高的性能，可与NodeJS和Go相媲美 |
| 快速开发 | 开发速度提升约200%至300% |
| 更少Bug | 减少约40%的开发者错误 |
| 智能支持 | 极佳的编辑器支持，代码补全无处不在 |
| 简单易用 | 易于使用和学习 |
| 代码简短 | 减少代码重复 |
| 健壮 | 生产级别的代码 |
| 标准兼容 | 基于并完全兼容OpenAPI和JSON Schema |

### 1.2 FastAPI的工作原理

FastAPI的架构可以简化为以下几个部分：

```
┌─────────────────────────────────────────────────────────┐
│                      FastAPI 应用                        │
├─────────────────────────────────────────────────────────┤
│  1. 接收HTTP请求                                       │
│  2. 验证请求数据（路径参数、查询参数、请求体等）          │
│  3. 使用Pydantic进行数据验证                           │
│  4. 调用相应的路径操作函数                              │
│  5. 使用Pydantic进行响应验证                           │
│  6. 返回HTTP响应                                       │
└─────────────────────────────────────────────────────────┘
```

### 1.3 FastAPI与其他框架对比

| 特性 | FastAPI | Flask | Django | Starlette |
|------|---------|-------|--------|-----------|
| 性能 | 极高 | 中等 | 中等 | 高 |
| 类型提示 | 原生支持 | 需插件 | 需插件 | 支持 |
| 自动文档 | Swagger/ReDoc | 需插件 | DRF | 需插件 |
| 异步支持 | 原生 | 需插件 | 部分 | 原生 |
| 学习曲线 | 低 | 低 | 中等 | 低 |
| 适用场景 | API、微服务 | 小型应用 | 大型应用 | 底层框架 |

### 1.4 FastAPI的技术栈

FastAPI构建在以下技术之上：

- **Starlette**：轻量级的ASGI框架/工具集
- **Pydantic**：数据验证库，使用Python类型提示
- **Uvicorn**：ASGI服务器实现
- **OpenAPI**：API文档规范

```
FastAPI
    │
    ├── Starlette (Web层)
    │       │
    │       ├── HTTP句柄
    │       ├── WebSocket支持
    │       └── 路由系统
    │
    └── Pydantic (数据验证层)
            │
            ├── 数据验证
            ├── 序列化
            └── JSON Schema生成
```

---

## 第二章 环境搭建与安装

### 2.1 创建虚拟环境

在使用FastAPI之前，建议创建一个独立的虚拟环境，以避免依赖冲突。

**使用venv创建虚拟环境：**

```bash
# Windows
python -m venv venv

# Linux/macOS
python3 -m venv venv
```

**激活虚拟环境：**

```bash
# Windows PowerShell
.\venv\Scripts\activate

# Windows CMD
venv\Scripts\activate.bat

# Linux/macOS
source venv/bin/activate
```

**使用conda创建虚拟环境：**

```bash
conda create -n fastapi-env python=3.11
conda activate fastapi-env
```

### 2.2 安装FastAPI

**基本安装：**

```bash
# 安装FastAPI基础版本
pip install fastapi

# 安装FastAPI及所有标准依赖（推荐）
pip install "fastapi[standard]"
```

**安装开发依赖：**

```bash
# 安装uvicorn作为开发服务器
pip install "uvicorn[standard]"

# 安装email-validator（用于Pydantic的EmailStr）
pip install email-validator

# 安装SQLModel（用于数据库操作）
pip install sqlmodel

# 安装所有常用依赖
pip install fastapi uvicorn pydantic sqlmodel email-validator python-multipart
```

### 2.3 安装的依赖说明

| 依赖包 | 说明 | 何时需要 |
|--------|------|----------|
| fastapi | 核心框架 | 必须 |
| uvicorn | ASGI服务器 | 必须 |
| pydantic | 数据验证 | 自动包含 |
| python-multipart | 表单数据解析 | 使用表单数据时 |
| email-validator | 邮箱验证 | 使用EmailStr时 |
| sqlmodel | SQL数据库ORM | 使用SQL数据库时 |
| jinja2 | 模板引擎 | 使用模板时 |

### 2.4 验证安装

```python
import fastapi
import uvicorn
import pydantic

print(f"FastAPI version: {fastapi.__version__}")
print(f"Uvicorn version: {uvicorn.__version__}")
print(f"Pydantic version: {pydantic.__version__}")
```

---

## 第三章 第一个FastAPI应用

### 3.1 最简单的应用

创建一个文件 `main.py`：

```python
from fastapi import FastAPI

# 创建FastAPI实例
app = FastAPI()

# 定义路径操作装饰器
@app.get("/")
async def root():
    return {"message": "Hello World"}
```

### 3.2 运行应用

**方法一：使用fastapi命令（推荐）**

```bash
# 开发模式（自动重载）
fastapi dev main.py

# 生产模式
fastapi run main.py
```

**方法二：使用uvicorn命令**

```bash
# 基本运行
uvicorn main:app --reload

# 指定主机和端口
uvicorn main:app --host 127.0.0.1 --port 8000 --reload

# 多工作进程
uvicorn main:app --workers 4
```

**方法三：使用Python运行**

```python
import uvicorn

if __name__ == "__main__":
    uvicorn.run("main:app", host="127.0.0.1", port=8000, reload=True)
```

### 3.3 访问应用

运行应用后，可以访问以下地址：

| 地址 | 说明 |
|------|------|
| http://127.0.0.1:8000 | 首页，返回JSON |
| http://127.0.0.1:8000/docs | Swagger UI交互式文档 |
| http://127.0.0.1:8000/redoc | ReDoc备选文档 |
| http://127.0.0.1:8000/openapi.json | OpenAPI规范JSON |

### 3.4 代码解析

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")  # 路径操作装饰器
async def root():  # 路径操作函数
    return {"message": "Hello World"}
```

**代码解析：**

1. **导入FastAPI类**：`from fastapi import FastAPI`

2. **创建FastAPI实例**：`app = FastAPI()`
   - 这个实例是创建所有API的主要交互对象

3. **定义路径操作装饰器**：`@app.get("/")`
   - `@app` 是FastAPI实例
   - `.get()` 是HTTP方法
   - `"/"` 是URL路径

4. **定义路径操作函数**：`async def root()`
   - 函数名可以自定义
   - 可以是 `async def` 或普通 `def`

### 3.5 交互式API文档

FastAPI自动生成两个交互式API文档：

**Swagger UI (http://127.0.0.1:8000/docs)**

```
┌─────────────────────────────────────────────┐
│  Swagger UI                                 │
├─────────────────────────────────────────────┤
│  [Authorize]                    [close]     │
│                                             │
│  /                                           │
│    GET /                                     │
│    ────────────────────────                 │
│    Responses                                  │
│    200: successful response                   │
│    [Try it out]                              │
│    [Generate Example]                        │
└─────────────────────────────────────────────┘
```

**ReDoc (http://127.0.0.1:8000/redoc)**

```
┌─────────────────────────────────────────────┐
│  FastAPI                              [≡]  │
├─────────────────────────────────────────────┤
│  GET /                                      │
│                                             │
│  ────────────────────────────────────────   │
│  Description: ...                            │
│  Responses: 200                             │
│                                             │
│  Request Body    Response Schema             │
│  ────────────────────────────────────────   │
│  {                                          │
│    "message": "string"                      │
│  }                                          │
└─────────────────────────────────────────────┘
```

---

## 第四章 路径参数

### 4.1 基本路径参数

路径参数用于捕获URL中的动态值：

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/items/{item_id}")
async def read_item(item_id):
    return {"item_id": item_id}
```

**URL示例：**
- `/items/1` → `item_id = "1"`
- `/items/foo` → `item_id = "foo"`
- `/items/abc123` → `item_id = "abc123"`

### 4.2 声明参数类型

使用类型注解声明路径参数的类型：

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/items/{item_id}")
async def read_item(item_id: int):
    return {"item_id": item_id}
```

**类型声明的作用：**

| 功能 | 说明 |
|------|------|
| 自动数据转换 | URL字符串自动转换为指定类型 |
| 数据验证 | 类型不匹配时返回清晰的错误信息 |
| 编辑器支持 | 代码补全和类型检查 |
| 文档生成 | 自动在OpenAPI中记录参数类型 |

### 4.3 数据转换示例

```python
@app.get("/items/{item_id}")
async def read_item(item_id: int):
    return {"item_id": item_id, "type": type(item_id).__name__}
```

**访问测试：**

| URL | 返回值 | 说明 |
|-----|--------|------|
| `/items/5` | `{"item_id": 5, "type": "int"}` | 字符串"5"转换为整数5 |
| `/items/3.14` | 错误 | 浮点数不能转换为整数 |

### 4.4 数据验证错误

当传入无效数据时，FastAPI返回详细的错误信息：

```json
{
  "detail": [
    {
      "type": "int_parsing",
      "loc": ["path", "item_id"],
      "msg": "Input should be a valid integer, unable to parse string as an integer",
      "input": "foo"
    }
  ]
}
```

**错误信息解析：**

| 字段 | 说明 |
|------|------|
| type | 错误类型（int_parsing表示整数解析失败） |
| loc | 错误位置（path表示在路径参数中） |
| msg | 人类可读的错误描述 |
| input | 导致错误的输入值 |

### 4.5 使用Enum限制取值

创建枚举类限制路径参数的取值：

```python
from enum import Enum
from fastapi import FastAPI

class ModelName(str, Enum):
    alexnet = "alexnet"
    resnet = "resnet"
    lenet = "lenet"

app = FastAPI()

@app.get("/models/{model_name}")
async def get_model(model_name: ModelName):
    if model_name is ModelName.alexnet:
        return {"model_name": model_name, "message": "Deep Learning FTW!"}
    if model_name.value == "lenet":
        return {"model_name": model_name, "message": "LeCNN all the images"}
    return {"model_name": model_name, "message": "Have some residuals"}
```

**枚举类说明：**

```python
class ModelName(str, Enum):
    alexnet = "alexnet"
    resnet = "resnet"
    lenet = "lenet"
```

| 属性 | 值 | 说明 |
|------|-----|------|
| ModelName.alexnet | "alexnet" | 枚举成员 |
| ModelName.alexnet.value | "alexnet" | 实际字符串值 |
| ModelName.alexnet.name | "alexnet" | 成员名称 |

### 4.6 路径参数顺序

路径匹配按定义顺序进行，固定的路径必须写在带参数的路径之前：

**正确示例：**

```python
@app.get("/users/me")
async def read_user_me():
    return {"user_id": "the current user"}

@app.get("/users/{user_id}")
async def read_user(user_id: str):
    return {"user_id": user_id}
```

**错误示例：**

```python
# 错误！如果这样定义，/users/me会被匹配为/user/{user_id}，user_id="me"
@app.get("/users/{user_id}")
async def read_user(user_id: str):
    return {"user_id": user_id}

@app.get("/users/me")  # 这行永远不会执行
async def read_user_me():
    return {"user_id": "the current user"}
```

### 4.7 包含路径的参数

使用 `:path` 声明包含斜杠的路径参数：

```python
@app.get("/files/{file_path:path}")
async def read_file(file_path: str):
    return {"file_path": file_path}
```

**URL示例：**
- `/files/home/user/doc.txt` → `file_path = "home/user/doc.txt"`

### 4.8 路径参数类型速查表

```python
from fastapi import FastAPI

app = FastAPI()

# 整数类型
@app.get("/items/{item_id}")
async def read_item(item_id: int):
    pass

# 浮点数类型
@app.get("/pi/{value}")
async def read_pi(value: float):
    pass

# 字符串类型（默认）
@app.get("/users/{username}")
async def read_user(username: str):
    pass

# UUID类型
@app.get("/users/{user_id}")
async def read_user(user_id: uuid.UUID):
    pass

# 路径类型（包含斜杠）
@app.get("/files/{file_path:path}")
async def read_file(file_path: str):
    pass
```

---

## 第五章 查询参数

### 5.1 基本查询参数

不是路径参数的函数参数会被自动识别为查询参数：

```python
from fastapi import FastAPI

app = FastAPI()

fake_items_db = [
    {"item_name": "Foo"},
    {"item_name": "Bar"},
    {"item_name": "Baz"}
]

@app.get("/items/")
async def read_item(skip: int = 0, limit: int = 10):
    return fake_items_db[skip : skip + limit]
```

**查询字符串格式：**

```
URL: http://127.0.0.1:8000/items/?skip=0&limit=10
         ─────────────────────────────────────
         路径    查询字符串（?后的部分）
```

| 参数 | 值 | 说明 |
|------|-----|------|
| skip | 0 | 起始偏移 |
| limit | 10 | 返回数量限制 |

### 5.2 默认值

查询参数支持默认值：

```python
@app.get("/items/")
async def read_item(skip: int = 0, limit: int = 10):
    # skip默认为0，limit默认为10
    pass
```

**访问方式对比：**

| URL | 实际参数 |
|-----|----------|
| `/items/` | `skip=0, limit=10`（使用默认值） |
| `/items/?skip=5` | `skip=5, limit=10` |
| `/items/?limit=5` | `skip=0, limit=5` |
| `/items/?skip=2&limit=3` | `skip=2, limit=3` |

### 5.3 可选参数

将默认值设为 `None` 使参数变为可选：

```python
from typing import Optional
from fastapi import FastAPI

app = FastAPI()

@app.get("/items/{item_id}")
async def read_item(item_id: str, q: Optional[str] = None):
    if q:
        return {"item_id": item_id, "q": q}
    return {"item_id": item_id}
```

**Python 3.10+ 简化写法：**

```python
@app.get("/items/{item_id}")
async def read_item(item_id: str, q: str | None = None):
    if q:
        return {"item_id": item_id, "q": q}
    return {"item_id": item_id}
```

### 5.4 必选查询参数

没有默认值的参数是必选的：

```python
@app.get("/items/{item_id}")
async def read_item(item_id: str, needy: str):
    return {"item_id": item_id, "needy": needy}
```

**错误示例：** 访问 `/items/foo` 而不提供 `needy` 参数会返回错误。

### 5.5 bool类型转换

查询参数可以声明为 `bool` 类型：

```python
@app.get("/items/{item_id}")
async def read_item(item_id: str, short: bool = False):
    item = {"item_id": item_id}
    if not short:
        item["description"] = "This is an amazing item that has a long description"
    return item
```

**bool值转换表：**

| URL中的值 | 转换为 |
|-----------|--------|
| `1`, `true`, `True`, `TRUE` | `True` |
| `0`, `false`, `False`, `FALSE` | `False` |
| `on`, `yes`, `y`, `Y` | `True` |

### 5.6 混合使用

可以同时使用路径参数和多个查询参数：

```python
@app.get("/users/{user_id}/items/{item_id}")
async def read_user_item(
    user_id: int,
    item_id: str,
    q: str | None = None,
    short: bool = False
):
    item = {"item_id": item_id, "owner_id": user_id}
    if q:
        item["q"] = q
    if not short:
        item["description"] = "This is an amazing item..."
    return item
```

### 5.7 查询参数参数类型速查表

```python
from fastapi import FastAPI
import uuid
from datetime import datetime, date

app = FastAPI()

# 整数
@app.get("/items/")
async def read_items(skip: int = 0, limit: int = 10):
    pass

# 浮点数
@app.get("/prices/")
async def read_prices(min_price: float = 0.0, max_price: float = 100.0):
    pass

# 布尔值
@app.get("/products/")
async def read_products(in_stock: bool = True):
    pass

# 日期时间
@app.get("/events/")
async def read_events(start_date: date = None, start_time: datetime = None):
    pass

# UUID
@app.get("/resources/")
async def read_resources(resource_id: uuid.UUID):
    pass
```

---

## 第六章 请求体

### 6.1 什么是请求体

**请求体**是客户端发送给API的数据，通常用于POST、PUT、PATCH请求。

**请求体与响应体：**

| 类型 | 说明 | 方向 |
|------|------|------|
| 请求体 | 客户端发送给API的数据 | 客户端 → API |
| 响应体 | API返回给客户端的数据 | API → 客户端 |

### 6.2 基本请求体

使用Pydantic模型声明请求体：

```python
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class Item(BaseModel):
    name: str
    description: str | None = None
    price: float
    tax: float | None = None

@app.post("/items/")
async def create_item(item: Item):
    return item
```

**请求示例：**

```json
POST /items/
{
    "name": "Foo",
    "description": "A very nice Item",
    "price": 35.4,
    "tax": 3.2
}
```

### 6.3 Pydantic模型说明

```python
class Item(BaseModel):
    name: str                    # 必选字段
    description: str | None = None  # 可选字段，默认None
    price: float                 # 必选字段
    tax: float | None = None    # 可选字段，默认None
```

**字段规则：**

| 声明方式 | 含义 |
|----------|------|
| `name: str` | 必选字段，必须提供 |
| `name: str \| None = None` | 可选字段，可以不提供 |
| `name: str = "default"` | 有默认值的字段 |

### 6.4 请求体自动功能

仅使用Python类型声明，FastAPI就能：

1. **读取JSON数据**：自动解析请求体
2. **类型转换**：在需要时转换数据类型
3. **数据验证**：数据无效时返回清晰错误信息
4. **生成OpenAPI Schema**：为自动文档提供支持
5. **编辑器支持**：代码补全和类型检查

### 6.5 使用模型

在路径操作函数中直接访问模型属性：

```python
@app.post("/items/")
async def create_item(item: Item):
    item_dict = item.model_dump()
    if item.tax:
        price_with_tax = item.price + item.tax
        item_dict["price_with_tax"] = price_with_tax
    return item_dict
```

### 6.6 混合使用多种参数

#### 请求体 + 路径参数

```python
@app.put("/items/{item_id}")
async def update_item(item_id: int, item: Item):
    return {"item_id": item_id, **item.model_dump()}
```

#### 请求体 + 路径参数 + 查询参数

```python
@app.put("/items/{item_id}")
async def update_item(
    item_id: int,
    item: Item,
    q: str | None = None
):
    result = {"item_id": item_id, **item.model_dump()}
    if q:
        result["q"] = q
    return result
```

### 6.7 参数识别规则

FastAPI按以下规则识别参数：

| 参数类型 | 识别方式 |
|----------|----------|
| 路径参数 | 在路径中声明的参数（如 `{item_id}`） |
| 查询参数 | 单一类型的参数（如 `int`, `str`） |
| 请求体 | Pydantic模型类型的参数 |
| Cookie参数 | 使用 `Cookie[...]` 声明 |
| Header参数 | 使用 `Header[...]` 声明 |

---

## 第七章 Pydantic模型详解

### 7.1 字段验证

使用 `Field` 添加额外验证：

```python
from pydantic import BaseModel, Field

class Item(BaseModel):
    name: str = Field(..., min_length=1, max_length=50)
    price: float = Field(..., gt=0, le=1000)
    quantity: int = Field(..., ge=0, le=100)
    description: str | None = Field(default=None, max_length=200)
```

**Field验证参数：**

| 参数 | 说明 | 示例 |
|------|------|------|
| `...` (Ellipsis) | 表示必选 | `Field(...)` |
| `gt` | 大于 | `gt=0` |
| `ge` | 大于等于 | `ge=0` |
| `lt` | 小于 | `lt=100` |
| `le` | 小于等于 | `le=100` |
| `min_length` | 最小长度 | `min_length=1` |
| `max_length` | 最大长度 | `max_length=50` |
| `regex` | 正则表达式 | `regex="^[a-z]+$"` |

### 7.2 嵌套模型

可以创建嵌套的Pydantic模型：

```python
class Image(BaseModel):
    url: str
    name: str

class Item(BaseModel):
    name: str
    description: str | None = None
    price: float
    image: Image | None = None
```

**嵌套请求示例：**

```json
{
    "name": "Item Name",
    "price": 35.4,
    "image": {
        "url": "https://example.com/image.jpg",
        "name": "item_image"
    }
}
```

### 7.3 列表和字典字段

```python
from typing import List, Dict
from pydantic import BaseModel

class Item(BaseModel):
    tags: List[str] = []
    prices: Dict[str, float] = {}
    dimensions: List[int] = []
```

**Python 3.9+简化写法：**

```python
class Item(BaseModel):
    tags: list[str] = []
    prices: dict[str, float] = {}
```

### 7.4 联合类型

```python
from typing import Union
from pydantic import BaseModel

class Item(BaseModel):
    value: Union[int, float]  # 整数或浮点数
    status: Literal["pending", "processing", "done"]  # 枚举值
```

### 7.5 日期和时间类型

```python
from datetime import datetime, time, date
from pydantic import BaseModel

class Event(BaseModel):
    name: str
    start_datetime: datetime
    end_datetime: datetime
    start_time: time
    start_date: date
    duration_seconds: int
```

**JSON格式：**

```json
{
    "name": "Event Name",
    "start_datetime": "2024-01-15T09:00:00",
    "end_datetime": "2024-01-15T17:00:00",
    "start_time": "09:00:00",
    "start_date": "2024-01-15",
    "duration_seconds": 28800
}
```

### 7.6 特殊类型

```python
from pydantic import BaseModel, HttpUrl, EmailStr
import uuid

class User(BaseModel):
    id: uuid.UUID
    username: str
    email: EmailStr
    website: HttpUrl
```

| 类型 | 说明 | 示例 |
|------|------|------|
| `EmailStr` | 邮箱地址 | "user@example.com" |
| `HttpUrl` | URL地址 | "https://example.com" |
| `UUID` | 通用唯一标识符 | "123e4567-e89b-12d3-a456-426614174000" |

### 7.7 别名

使用 `alias` 为字段指定JSON中的键名：

```python
from pydantic import BaseModel, Field

class Item(BaseModel):
    name: str = Field(..., alias="itemName")
    price: float = Field(..., alias="itemPrice")
```

**请求格式：**

```json
{
    "itemName": "Foo",
    "itemPrice": 35.4
}
```

### 7.8 模型配置类

```python
from pydantic import BaseModel, ConfigDict

class Item(BaseModel):
    model_config = ConfigDict(
        str_strip_whitespace=True,  # 自动去除空白字符
        validate_assignment=True,    # 赋值时验证
        extra='forbid'               # 禁止额外字段
    )
    
    name: str
    price: float
```

### 7.9 计算字段和验证器

```python
from pydantic import BaseModel, field_validator

class User(BaseModel):
    username: str
    password: str
    
    @field_validator('password')
    @classmethod
    def validate_password(cls, v):
        if len(v) < 8:
            raise ValueError('Password must be at least 8 characters')
        if not any(c.isupper() for c in v):
            raise ValueError('Password must contain uppercase letter')
        return v
```

---

## 第八章 响应模型

### 8.1 使用response_model参数

使用 `response_model` 参数声明返回数据的类型：

```python
from typing import List
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class Item(BaseModel):
    name: str
    price: float

@app.get("/items/", response_model=List[Item])
async def read_items():
    return [
        {"name": "Foo", "price": 35.4},
        {"name": "Bar", "price": 42.0}
    ]
```

### 8.2 响应模型的作用

| 功能 | 说明 |
|------|------|
| 数据转换 | 将返回值转换为声明的类型 |
| 数据过滤 | 自动排除额外字段 |
| 数据验证 | 确保返回数据符合模型 |
| 文档生成 | 在OpenAPI中记录响应格式 |

### 8.3 输入输出模型分离

创建单独的输入和输出模型以保护敏感数据：

```python
from pydantic import BaseModel, EmailStr

# 输入模型（包含密码）
class UserIn(BaseModel):
    username: str
    password: str
    email: EmailStr
    full_name: str | None = None

# 输出模型（不包含密码）
class UserOut(BaseModel):
    username: str
    email: EmailStr
    full_name: str | None = None

@app.post("/user/", response_model=UserOut)
async def create_user(user: UserIn):
    # 保存用户等逻辑...
    return user
```

### 8.4 使用类继承

```python
class BaseUser(BaseModel):
    username: str
    email: EmailStr
    full_name: str | None = None

class UserIn(BaseUser):
    password: str  # 新增password字段

@app.post("/user/")
async def create_user(user: UserIn) -> BaseUser:
    return user
```

### 8.5 响应状态码

使用 `status_code` 参数设置响应状态码：

```python
@app.post("/items/", status_code=201)
async def create_item(item: Item):
    return item
```

**常用HTTP状态码：**

| 状态码 | 名称 | 说明 |
|--------|------|------|
| 200 | OK | 默认，成功响应 |
| 201 | Created | 资源创建成功 |
| 204 | No Content | 成功但无返回内容 |
| 400 | Bad Request | 请求错误 |
| 401 | Unauthorized | 未认证 |
| 403 | Forbidden | 无权限 |
| 404 | Not Found | 资源不存在 |
| 422 | Unprocessable Entity | 验证错误 |
| 500 | Internal Server Error | 服务器错误 |

### 8.6 响应模型参数

```python
@app.get(
    "/items/{item_id}",
    response_model=Item,
    response_model_exclude_unset=True,  # 排除未设置的字段
    response_model_include={"name", "price"},  # 只包含这些字段
    response_model_exclude={"description"}  # 排除这些字段
)
async def read_item(item_id: int):
    pass
```

| 参数 | 说明 |
|------|------|
| `response_model_exclude_unset` | 不包含使用默认值的字段 |
| `response_model_include` | 只包含指定的字段 |
| `response_model_exclude` | 排除指定的字段 |

---

## 第九章 查询参数与字符串校验

### 9.1 使用Query参数

使用 `Query` 类添加验证和元数据：

```python
from fastapi import FastAPI, Query

app = FastAPI()

@app.get("/items/")
async def read_items(
    q: str | None = Query(None, min_length=3, max_length=50)
):
    results = {"items": [{"item_id": "Foo"}, {"item_id": "Bar"}]}
    if q:
        results["q"] = q
    return results
```

### 9.2 Query验证参数

```python
from fastapi import Query

@app.get("/items/")
async def read_items(
    q: str | None = Query(
        None,  # 默认值
        min_length=3,  # 最小长度
        max_length=50,  # 最大长度
        pattern="^fixedprefix",  # 正则表达式
        title="查询字符串",  # 用于文档
        description="要搜索的查询字符串"  # 用于文档
    )
):
    pass
```

### 9.3 必选查询参数

使用 `Query(..., min_length=1)` 使查询参数成为必选：

```python
@app.get("/items/")
async def read_items(
    q: str = Query(..., min_length=1)  # ...表示必选
):
    return {"q": q}
```

### 9.4 列表查询参数

```python
from typing import List

@app.get("/items/")
async def read_items(
    q: List[str] = Query(["foo", "bar"])  # 多个值
):
    return {"q": q}
```

**URL格式：**

```
GET /items/?q=foo&q=bar&q=baz
```

### 9.5 字符串校验速查表

```python
from fastapi import Query
import re

# 最小长度
q: str = Query(None, min_length=3)

# 最大长度
q: str = Query(None, max_length=50)

# 长度范围
q: str = Query(None, min_length=3, max_length=50)

# 正则表达式
q: str = Query(None, pattern=r"^\d{3}-\d{4}$")  # 格式：123-4567

# 包含特定前缀
q: str = Query(None, pattern=r"^prefix-.*")
```

---

## 第十章 路径参数与数值校验

### 10.1 使用Path参数

使用 `Path` 类为路径参数添加验证：

```python
from fastapi import FastAPI, Path

app = FastAPI()

@app.get("/items/{item_id}")
async def read_item(
    item_id: int = Path(..., ge=1, le=1000),
    q: str | None = None
):
    return {"item_id": item_id, "q": q}
```

### 10.2 Path验证参数

```python
from fastapi import Path

@app.get("/items/{item_id}")
async def read_item(
    item_id: int = Path(
        ...,  # 必选参数
        ge=1,  # 大于等于
        le=1000,  # 小于等于
        title="商品ID",  # 用于文档
        description="商品的唯一标识符"  # 用于文档
    )
):
    pass
```

### 10.3 数值类型验证

```python
from fastapi import Path

# 整数验证
item_id: int = Path(..., ge=1)

# 浮点数验证
price: float = Path(..., gt=0.0, le=1000.0)

# 多重验证
quantity: int = Path(..., ge=0, le=100, multiple_of=5)
```

### 10.4 数值验证参数速查表

| 参数 | 说明 | 示例 |
|------|------|------|
| `ge` | 大于等于 | `ge=0` |
| `gt` | 大于 | `gt=0` |
| `le` | 小于等于 | `le=100` |
| `lt` | 小于 | `lt=100` |
| `multiple_of` | 倍数 | `multiple_of=5` |

### 10.5 数值校验示例

```python
from fastapi import FastAPI, Path, Query

app = FastAPI()

@app.get("/users/{user_id}/items/{item_id}")
async def read_user_item(
    user_id: int = Path(..., ge=1, description="用户ID"),
    item_id: int = Path(..., ge=1, description="商品ID"),
    q: str | None = Query(None, min_length=3),
    skip: int = Query(0, ge=0),
    limit: int = Query(100, ge=1, le=100)
):
    return {
        "user_id": user_id,
        "item_id": item_id,
        "q": q,
        "skip": skip,
        "limit": limit
    }
```

---

## 第十一章 Cookie和Header参数

### 11.1 Cookie参数

使用 `Cookie` 类声明Cookie参数：

```python
from fastapi import FastAPI, Cookie

app = FastAPI()

@app.get("/items/")
async def read_items(
    session_id: str | None = Cookie(None)
):
    return {"session_id": session_id}
```

### 11.2 Header参数

使用 `Header` 类声明Header参数：

```python
from fastapi import FastAPI, Header

app = FastAPI()

@app.get("/items/")
async def read_items(
    user_agent: str | None = Header(None)
):
    return {"user_agent": user_agent}
```

### 11.3 自动转换

Header参数会自动转换下划线为连字符：

```python
from fastapi import FastAPI, Header

app = FastAPI()

@app.get("/items/")
async def read_items(
    x_token: list[str] | None = Header(None)  # 对应 X-Token header
):
    return {"x_token": x_token}
```

**自动转换规则：**

| 函数参数名 | HTTP Header名 |
|------------|--------------|
| `user_agent` | `User-Agent` |
| `x_token` | `X-Token` |
| `content_type` | `Content-Type` |

### 11.4 多个Header值

```python
from fastapi import Header

@app.get("/items/")
async def read_items(
    x_token: list[str] = Header(...)
):
    return {"x_token": x_token}
```

**请求格式：**

```
X-Token: value1
X-Token: value2
X-Token: value3
```

### 11.5 Cookie和Header速查表

```python
from fastapi import FastAPI, Cookie, Header

app = FastAPI()

# Cookie参数
@app.get("/profile/")
async def get_profile(
    user_id: str = Cookie(None)
):
    pass

# Header参数（必选）
@app.get("/secure/")
async def get_secure(
    authorization: str = Header(...)
):
    pass

# 多个Header值
@app.get("/multi/")
async def get_multi(
    x_custom: list[str] = Header(None)
):
    pass

# 自定义Header名称
@app.get("/custom/")
async def get_custom(
    custom_header: str = Header(..., alias="X-Custom-Header")
):
    pass
```

---

## 第十二章 依赖注入系统

### 12.1 什么是依赖注入

依赖注入是一种设计模式，允许声明函数运行所需的依赖，FastAPI会自动解析并注入这些依赖。

**依赖注入的优势：**

| 优势 | 说明 |
|------|------|
| 代码复用 | 共享业务逻辑 |
| 数据库连接 | 共享数据库连接 |
| 认证授权 | 统一的安全检查 |
| 配置管理 | 集中管理配置 |

### 12.2 基础依赖注入

```python
from typing import Annotated
from fastapi import Depends, FastAPI

app = FastAPI()

async def common_parameters(
    q: str | None = None,
    skip: int = 0,
    limit: int = 100
):
    return {"q": q, "skip": skip, "limit": limit}

@app.get("/items/")
async def read_items(
    commons: Annotated[dict, Depends(common_parameters)]
):
    return commons

@app.get("/users/")
async def read_users(
    commons: Annotated[dict, Depends(common_parameters)]
):
    return commons
```

### 12.3 类作为依赖

依赖可以是类：

```python
class CommonParams:
    def __init__(
        self,
        q: str | None = None,
        skip: int = 0,
        limit: int = 100
    ):
        self.q = q
        self.skip = skip
        self.limit = limit

@app.get("/items/")
async def read_items(
    params: Annotated[CommonParams, Depends(CommonParams)]
):
    return {"q": params.q, "skip": params.skip, "limit": params.limit}
```

### 12.4 子依赖

依赖可以依赖其他依赖：

```python
async def query_extractor(q: str | None = None):
    return q

async def query_or_cookie_extractor(
    q: Annotated[str, Depends(query_extractor)],
    last_query: str | None = None
):
    if not q:
        return last_query
    return q

@app.get("/read/")
async def read_query(
    query: Annotated[str, Depends(query_or_cookie_extractor)]
):
    return {"q": query}
```

### 12.5 带yield的依赖

用于清理资源：

```python
async def get_db():
    db = DBSession()
    try:
        yield db
    finally:
        db.close()

@app.get("/items/")
async def read_items(
    db: Annotated[DBSession, Depends(get_db)]
):
    return db.query(Item).all()
```

### 12.6 依赖注入层级图

```
┌────────────────────────────────────────────────────┐
│                 依赖注入层级                        │
├────────────────────────────────────────────────────┤
│                                                    │
│    current_user                                    │
│         │                                          │
│         ├── admin_user ── 管理员权限检查            │
│         │                                          │
│         └── active_user ── 用户激活状态检查        │
│                   │                                 │
│                   ├── verified_email ── 邮箱验证   │
│                   │                                 │
│                   └── valid_subscription ── 订阅验证│
│                                                    │
└────────────────────────────────────────────────────┘
```

### 12.7 全局依赖

使用 `app.dependency_overrides` 覆盖依赖（用于测试）：

```python
async def override_dependency():
    return {"override": True}

app.dependency_overrides[common_parameters] = override_dependency
```

---

## 第十三章 安全性与认证

### 13.1 OAuth2密码模式

使用OAuth2的Password Bearer流程实现认证：

```python
from typing import Annotated
from fastapi import Depends, FastAPI, HTTPException, status
from fastapi.security import OAuth2PasswordBearer, OAuth2PasswordRequestForm

app = FastAPI()

oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token")

# 模拟用户数据库
fake_users_db = {
    "johndoe": {
        "username": "johndoe",
        "full_name": "John Doe",
        "email": "johndoe@example.com",
        "hashed_password": "fakehashedsecret",
        "disabled": False,
    },
}

def fake_hash_password(password: str):
    return "fakehashed" + password

async def authenticate_user(username: str, password: str):
    user = fake_users_db.get(username)
    if not user:
        return False
    if not fake_hash_password(password) == user["hashed_password"]:
        return False
    return user

@app.post("/token")
async def login(form_data: Annotated[OAuth2PasswordRequestForm, Depends()]):
    user = authenticate_user(form_data.username, form_data.password)
    if not user:
        raise HTTPException(
            status_code=status.HTTP_401_UNAUTHORIZED,
            detail="Incorrect username or password",
        )
    return {"access_token": user["username"], "token_type": "bearer"}

async def get_current_user(token: Annotated[str, Depends(oauth2_scheme)]):
    user = fake_users_db.get(token)
    if not user:
        raise HTTPException(
            status_code=status.HTTP_401_UNAUTHORIZED,
            detail="Could not validate credentials",
        )
    return user

@app.get("/users/me")
async def read_users_me(
    current_user: Annotated[dict, Depends(get_current_user)]
):
    return current_user
```

### 13.2 获取当前用户

```python
from typing import Annotated
from fastapi import Depends, HTTPException, status
from fastapi.security import OAuth2PasswordBearer

oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token")

async def get_current_user(
    token: Annotated[str, Depends(oauth2_scheme)]
):
    credentials_exception = HTTPException(
        status_code=status.HTTP_401_UNAUTHORIZED,
        detail="Could not validate credentials",
        headers={"WWW-Authenticate": "Bearer"},
    )
    # 验证token并返回用户
    user = verify_token(token)
    if user is None:
        raise credentials_exception
    return user
```

### 13.3 JWT Token认证

```python
from datetime import datetime, timedelta
from jose import JWTError, jwt
from passlib.context import CryptContext

SECRET_KEY = "your-secret-key-here"
ALGORITHM = "HS256"
ACCESS_TOKEN_EXPIRE_MINUTES = 30

pwd_context = CryptContext(schemes=["bcrypt"], deprecated="auto")

def create_access_token(data: dict, expires_delta: timedelta | None = None):
    to_encode = data.copy()
    if expires_delta:
        expire = datetime.utcnow() + expires_delta
    else:
        expire = datetime.utcnow() + timedelta(minutes=15)
    to_encode.update({"exp": expire})
    encoded_jwt = jwt.encode(to_encode, SECRET_KEY, algorithm=ALGORITHM)
    return encoded_jwt

def verify_password(plain_password: str, hashed_password: str) -> bool:
    return pwd_context.verify(plain_password, hashed_password)

def get_password_hash(password: str) -> str:
    return pwd_context.hash(password)
```

### 13.4 密码哈希

```python
from passlib.context import CryptContext

pwd_context = CryptContext(schemes=["bcrypt"], deprecated="auto")

# 哈希密码
def hash_password(password: str) -> str:
    return pwd_context.hash(password)

# 验证密码
def verify_password(plain_password: str, hashed_password: str) -> bool:
    return pwd_context.verify(plain_password, hashed_password)
```

### 13.5 HTTPBearer

```python
from fastapi import HTTPBearer, Depends

security = HTTPBearer()

@app.get("/items/")
async def read_items(
    credentials: Annotated[HTTPAuthorizationCredentials, Depends(security)]
):
    token = credentials.credentials
    # 验证token
    return {"token": token}
```

### 13.6 安全方案速查表

```python
from fastapi import Depends
from fastapi.security import (
    OAuth2PasswordBearer,
    OAuth2PasswordRequestForm,
    HTTPBearer,
    HTTPBasic,
    HTTPBasicCredentials
)

# OAuth2 with Password Bearer (最常用)
oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token")

# HTTP Basic Auth
security = HTTPBasic()

# HTTP Bearer
security = HTTPBearer()

# 使用
@app.get("/protected")
async def protected(
    token: Annotated[str, Depends(oauth2_scheme)]
):
    pass
```

---

## 第十四章 中间件

### 14.1 添加中间件

中间件是在每个请求处理前后执行的函数：

```python
from fastapi import FastAPI
from time import time

app = FastAPI()

@app.middleware("http")
async def add_process_time_header(request, call_next):
    start_time = time()
    response = await call_next(request)
    process_time = time() - start_time
    response.headers["X-Process-Time"] = str(process_time)
    return response
```

### 14.2 中间件流程图

```
┌─────────────────────────────────────────────────────────────┐
│                        请求流程                              │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│    客户端请求                                               │
│         │                                                   │
│         ▼                                                   │
│    ┌─────────────┐                                        │
│    │  中间件1     │ ◄── 执行前置逻辑                       │
│    └──────┬──────┘                                        │
│           │                                                 │
│           ▼                                                 │
│    ┌─────────────┐                                        │
│    │  中间件2     │ ◄── 执行前置逻辑                       │
│    └──────┬──────┘                                        │
│           │                                                 │
│           ▼                                                 │
│    ┌─────────────┐                                        │
│    │  路径操作函数 │ ◄── 处理业务逻辑                      │
│    └──────┬──────┘                                        │
│           │                                                 │
│           ▼                                                 │
│    ┌─────────────┐                                        │
│    │  响应处理    │ ◄── 收集响应                          │
│    └──────┬──────┘                                        │
│           │                                                 │
│           ▼                                                 │
│    ┌─────────────┐                                        │
│    │  中间件2     │ ◄── 执行后置逻辑                       │
│    └──────┬──────┘                                        │
│           │                                                 │
│           ▼                                                 │
│    ┌─────────────┐                                        │
│    │  中间件1     │ ◄── 执行后置逻辑                       │
│    └──────┬──────┘                                        │
│           │                                                 │
│           ▼                                                 │
│    客户端响应                                               │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### 14.3 日志记录中间件

```python
import logging

logging.basicConfig(level=logging.INFO)
logger = logging.getLogger(__name__)

@app.middleware("http")
async def log_requests(request: Request, call_next):
    logger.info(f"Request: {request.method} {request.url}")
    response = await call_next(request)
    logger.info(f"Response: {response.status_code}")
    return response
```

### 14.4 CORS中间件

见下一章详细说明。

---

## 第十五章 CORS跨域资源共享

### 15.1 什么是CORS

CORS（Cross-Origin Resource Sharing）是一种W3C规范，允许Web服务器放宽同源策略，使得一个域名的网页可以请求另一个域名的资源。

**同源定义：**

| 属性 | 相同 | 不同 |
|------|------|------|
| 协议 | http | https |
| 域名 | example.com | api.example.com |
| 端口 | 8000 | 8001 |

### 15.2 配置CORS

```python
from fastapi import FastAPI
from fastapi.middleware.cors import CORSMiddleware

app = FastAPI()

# 配置CORS中间件
app.add_middleware(
    CORSMiddleware,
    allow_origins=["http://localhost:3000"],  # 允许的源
    allow_credentials=True,  # 是否允许发送cookies
    allow_methods=["*"],  # 允许的HTTP方法
    allow_headers=["*"],  # 允许的HTTP头
)
```

### 15.3 CORS配置参数详解

| 参数 | 说明 | 示例 |
|------|------|------|
| allow_origins | 允许的源列表 | ["http://example.com"] |
| allow_origin_regex | 源的regex模式 | "^https://.*\\.example\\.com$" |
| allow_credentials | 是否允许cookies | True/False |
| allow_methods | 允许的HTTP方法 | ["GET", "POST"] 或 ["*"] |
| allow_headers | 允许的HTTP头 | ["*"] 或 ["Content-Type"] |
| expose_headers | 暴露给浏览器的头 | ["X-Custom-Header"] |
| max_age | 预检请求缓存时间 | 600（秒） |

### 15.4 CORS响应头

| 响应头 | 说明 |
|--------|------|
| Access-Control-Allow-Origin | 允许的源 |
| Access-Control-Allow-Credentials | 是否允许credentials |
| Access-Control-Allow-Methods | 允许的方法 |
| Access-Control-Allow-Headers | 允许的头 |
| Access-Control-Max-Age | 预检请求缓存时间 |

### 15.5 常见CORS配置场景

**开发环境（允许所有源）：**

```python
app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)
```

**生产环境（指定源）：**

```python
app.add_middleware(
    CORSMiddleware,
    allow_origins=[
        "https://example.com",
        "https://www.example.com",
    ],
    allow_credentials=True,
    allow_methods=["GET", "POST", "PUT", "DELETE"],
    allow_headers=["Authorization", "Content-Type"],
)
```

---

## 第十六章 数据库操作

### 16.1 使用SQLModel

SQLModel是FastAPI作者创建的ORM，基于SQLAlchemy和Pydantic构建：

```python
from typing import Optional
from fastapi import Depends, FastAPI, HTTPException
from sqlmodel import Field, Session, SQLModel, create_engine, select

app = FastAPI()

# 定义模型
class Hero(SQLModel, table=True):
    id: Optional[int] = Field(default=None, primary_key=True)
    name: str = Field(index=True)
    age: Optional[int] = Field(default=None, index=True)
    secret_name: str

# 创建数据库引擎
sqlite_file_name = "database.db"
sqlite_url = f"sqlite:///{sqlite_file_name}"
connect_args = {"check_same_thread": False}
engine = create_engine(sqlite_url, connect_args=connect_args)

# 创建表
def create_db_and_tables():
    SQLModel.metadata.create_all(engine)

# Session依赖
def get_session():
    with Session(engine) as session:
        yield session

SessionDep = Annotated[Session, Depends(get_session)]

@app.on_event("startup")
def on_startup():
    create_db_and_tables()
```

### 16.2 CRUD操作

**创建（Create）：**

```python
@app.post("/heroes/", response_model=Hero)
async def create_hero(hero: Hero, session: SessionDep):
    session.add(hero)
    session.commit()
    session.refresh(hero)
    return hero
```

**读取（Read）：**

```python
@app.get("/heroes/", response_model=list[Hero])
async def read_heroes(
    session: SessionDep,
    offset: int = 0,
    limit: int = 100
):
    heroes = session.exec(select(Hero).offset(offset).limit(limit)).all()
    return heroes

@app.get("/heroes/{hero_id}", response_model=Hero)
async def read_hero(hero_id: int, session: SessionDep):
    hero = session.get(Hero, hero_id)
    if not hero:
        raise HTTPException(status_code=404, detail="Hero not found")
    return hero
```

**更新（Update）：**

```python
@app.patch("/heroes/{hero_id}", response_model=Hero)
async def update_hero(
    hero_id: int,
    hero: Hero,
    session: SessionDep
):
    db_hero = session.get(Hero, hero_id)
    if not db_hero:
        raise HTTPException(status_code=404, detail="Hero not found")
    
    hero_data = hero.model_dump(exclude_unset=True)
    for key, value in hero_data.items():
        setattr(db_hero, key, value)
    
    session.add(db_hero)
    session.commit()
    session.refresh(db_hero)
    return db_hero
```

**删除（Delete）：**

```python
@app.delete("/heroes/{hero_id}")
async def delete_hero(hero_id: int, session: SessionDep):
    hero = session.get(Hero, hero_id)
    if not hero:
        raise HTTPException(status_code=404, detail="Hero not found")
    session.delete(hero)
    session.commit()
    return {"ok": True}
```

### 16.3 分离输入输出模型

```python
class HeroBase(SQLModel):
    name: str
    age: int | None = None

class Hero(HeroBase, table=True):
    id: int | None = None
    secret_name: str

class HeroCreate(HeroBase):
    secret_name: str

class HeroPublic(HeroBase):
    id: int

class HeroUpdate(SQLModel):
    name: str | None = None
    age: int | None = None
    secret_name: str | None = None
```

### 16.4 关系模型

```python
class Team(SQLModel, table=True):
    id: Optional[int] = Field(default=None, primary_key=True)
    name: str = Field(index=True)
    
    # 关系
    heroes: list["Hero"] = Relationship(back_populates="team")

class Hero(SQLModel, table=True):
    id: Optional[int] = Field(default=None, primary_key=True)
    name: str = Field(index=True)
    
    # 外键
    team_id: Optional[int] = Field(default=None, foreign_key="team.id")
    
    # 关系
    team: Optional[Team] = Relationship(back_populates="heroes")
```

---

## 第十七章 错误处理

### 17.1 HTTPException

使用 `HTTPException` 返回HTTP错误：

```python
from fastapi import FastAPI, HTTPException

app = FastAPI()

items = {"foo": "The Foo Wrestlers"}

@app.get("/items/{item_id}")
async def read_item(item_id: str):
    if item_id not in items:
        raise HTTPException(
            status_code=404,
            detail="Item not found",
            headers={"X-Error": "Item not found"}
        )
    return {"item": items[item_id]}
```

### 17.2 自定义异常处理器

```python
from fastapi import FastAPI, Request
from fastapi.responses import JSONResponse

app = FastAPI()

class UnicornException(Exception):
    def __init__(self, name: str):
        self.name = name

@app.exception_handler(UnicornException)
async def unicorn_exception_handler(
    request: Request,
    exc: UnicornException
):
    return JSONResponse(
        status_code=418,
        content={
            "message": f"Oops! {exc.name} did something. "
                      f"There's a rainbow!"
        },
    )

@app.get("/unicorns/{name}")
async def read_unicorn(name: str):
    if name == "yolo":
        raise UnicornException(name=name)
    return {"unicorn_name": name}
```

### 17.3 错误响应格式

```json
{
  "detail": "Error message here"
}
```

**带额外信息的错误：**

```json
{
  "detail": [
    {
      "loc": ["body", "name"],
      "msg": "field required",
      "type": "value_error.missing"
    }
  ]
}
```

### 17.4 常见错误处理场景

```python
from fastapi import HTTPException, status

# 404 Not Found
raise HTTPException(status_code=404, detail="Resource not found")

# 401 Unauthorized
raise HTTPException(
    status_code=status.HTTP_401_UNAUTHORIZED,
    detail="Could not validate credentials",
    headers={"WWW-Authenticate": "Bearer"},
)

# 403 Forbidden
raise HTTPException(
    status_code=status.HTTP_403_FORBIDDEN,
    detail="Not enough permissions"
)

# 400 Bad Request
raise HTTPException(
    status_code=status.HTTP_400_BAD_REQUEST,
    detail="Invalid input data"
)
```

---

## 第十八章 后台任务

### 18.1 使用BackgroundTasks

```python
from fastapi import FastAPI, BackgroundTasks

app = FastAPI()

def send_email(email: str, message: str):
    # 发送邮件的逻辑
    print(f"Sending email to {email}: {message}")

@app.post("/send-notification/{email}")
async def send_notification(
    email: str,
    background_tasks: BackgroundTasks
):
    background_tasks.add_task(send_email, email, message)
    return {"message": "Notification sent in the background"}
```

### 18.2 后台任务流程

```
┌─────────────────────────────────────────────────────────────┐
│                    后台任务流程                              │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  1. 客户端发送请求                                          │
│  2. FastAPI处理请求并返回响应（立即）                        │
│  3. 后台任务在独立的线程/进程中执行                           │
│  4. 任务完成后自动清理                                       │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### 18.3 带依赖的依赖注入

```python
from fastapi import Depends

def send_email(email: str, message: str):
    print(f"Sending email to {email}: {message}")

@app.post("/send-notification/{email}")
async def send_notification(
    email: str,
    background_tasks: BackgroundTasks,
    current_user: Annotated[User, Depends(get_current_user)]
):
    background_tasks.add_task(
        send_email,
        email,
        f"Hello {current_user.username}!"
    )
    return {"message": "Notification queued"}
```

---

## 第十九章 测试

### 19.1 使用TestClient

```python
from fastapi.testclient import TestClient
from main import app

client = TestClient(app)

def test_read_item():
    response = client.get("/items/foo")
    assert response.status_code == 200
    assert response.json() == {"item_id": "foo", "name": "Foo"}

def test_read_item_not_found():
    response = client.get("/items/bar")
    assert response.status_code == 404
```

### 19.2 测试POST请求

```python
from pydantic import BaseModel

class Item(BaseModel):
    name: str
    price: float
    description: str | None = None

def test_create_item():
    response = client.post(
        "/items/",
        json={"name": "Test Item", "price": 10.0}
    )
    assert response.status_code == 200
    data = response.json()
    assert data["name"] == "Test Item"
    assert data["price"] == 10.0
    assert "id" in data
```

### 19.3 测试认证

```python
def test_read_items_auth():
    # 获取token
    response = client.post(
        "/token",
        data={"username": "johndoe", "password": "secret"}
    )
    assert response.status_code == 200
    token = response.json()["access_token"]
    
    # 使用token访问受保护资源
    response = client.get(
        "/users/me",
        headers={"Authorization": f"Bearer {token}"}
    )
    assert response.status_code == 200
    assert response.json()["username"] == "johndoe"
```

### 19.4 异步测试

```python
from httpx import AsyncClient, ASGITransport

@pytest.mark.asyncio
async def test_read_items_async():
    async with AsyncClient(
        transport=ASGITransport(app=app),
        base_url="http://test"
    ) as client:
        response = await client.get("/items/")
        assert response.status_code == 200
```

### 19.5 测试依赖覆盖

```python
from main import app
from main import get_current_user

app.dependency_overrides[get_current_user] = lambda: {"username": "testuser"}

def test_with_override():
    response = client.get("/users/me")
    assert response.status_code == 200
    assert response.json()["username"] == "testuser"

# 清理
def test_cleanup():
    app.dependency_overrides.clear()
```

---

## 第二十章 部署

### 20.1 使用Gunicorn + Uvicorn Workers

```bash
# 安装
pip install gunicorn uvicorn[standard]

# 运行（4个工作进程）
gunicorn main:app -w 4 -k uvicorn.workers.UvicornWorker
```

### 20.2 Docker部署

**Dockerfile：**

```dockerfile
FROM python:3.11-slim

WORKDIR /app

# 安装依赖
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# 复制应用代码
COPY ./app /app/app

# 运行
CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "80"]
```

**requirements.txt：**

```
fastapi
uvicorn[standard]
pydantic
sqlmodel
python-multipart
email-validator
```

**构建和运行：**

```bash
# 构建镜像
docker build -t myfastapi .

# 运行容器
docker run -d -p 8000:80 myfastapi
```

### 20.3 Docker多阶段构建

```dockerfile
# 构建阶段
FROM python:3.11-slim as builder

WORKDIR /build
COPY requirements.txt .
RUN pip install --target=/lib -r requirements.txt

# 运行阶段
FROM python:3.11-slim

WORKDIR /app
COPY --from=builder /lib /usr/local/lib/python3.11/site-packages
COPY ./app /app/app

CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "80"]
```

### 20.4 Docker Compose

```yaml
version: '3.8'

services:
  api:
    build: .
    ports:
      - "8000:80"
    environment:
      - DATABASE_URL=postgresql://user:pass@db:5432/mydb
    depends_on:
      - db

  db:
    image: postgres:15
    environment:
      - POSTGRES_USER=user
      - POSTGRES_PASSWORD=pass
      - POSTGRES_DB=mydb
    volumes:
      - postgres_data:/var/lib/postgresql/data

volumes:
  postgres_data:
```

### 20.5 环境变量配置

```python
from pydantic_settings import BaseSettings
from functools import lru_cache

class Settings(BaseSettings):
    app_name: str = "FastAPI Application"
    database_url: str
    secret_key: str
    
    class Config:
        env_file = ".env"
        env_file_encoding = "utf-8"

@lru_cache()
def get_settings():
    return Settings()

settings = get_settings()
```

### 20.6 常用部署平台

| 平台 | 说明 |
|------|------|
| Railway | 简单部署，支持多种语言 |
| Render | 托管服务，免费层可用 |
| Heroku | 老牌PaaS平台 |
| AWS ECS/EC2 | AWS云服务 |
| Google Cloud Run | GCP容器服务 |
| Azure Container Instances | Azure云服务 |

---

## 附录A：常用命令速查表

| 命令 | 说明 |
|------|------|
| `fastapi dev main.py` | 开发模式运行 |
| `fastapi run main.py` | 生产模式运行 |
| `uvicorn main:app --reload` | 使用uvicorn开发模式 |
| `uvicorn main:app --workers 4` | 多工作进程模式 |
| `pip install "fastapi[standard]"` | 安装FastAPI及依赖 |
| `pytest` | 运行测试 |
| `pytest -v` | 详细测试输出 |

---

## 附录B：常见HTTP状态码

| 状态码 | 名称 | 说明 |
|--------|------|------|
| 200 | OK | 成功 |
| 201 | Created | 创建成功 |
| 204 | No Content | 成功无内容 |
| 400 | Bad Request | 请求错误 |
| 401 | Unauthorized | 未认证 |
| 403 | Forbidden | 无权限 |
| 404 | Not Found | 未找到 |
| 405 | Method Not Allowed | 方法不允许 |
| 422 | Unprocessable Entity | 验证错误 |
| 500 | Internal Server Error | 服务器错误 |
| 503 | Service Unavailable | 服务不可用 |

---

## 附录C：OpenAPI安全方案类型

| 类型 | 说明 |
|------|------|
| apiKey | API密钥（查询/Header/Cookie） |
| http | HTTP认证（Basic/Bearer） |
| oauth2 | OAuth2认证 |
| openIdConnect | OpenID Connect认证 |

---

**本教程基于FastAPI官方文档编写**

**参考链接：**
- FastAPI官网：https://fastapi.tiangolo.com/
- FastAPI GitHub：https://github.com/fastapi/fastapi
- SQLModel文档：https://sqlmodel.tiangolo.com/
