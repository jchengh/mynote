# FastAPI 教程

---

## 第一章 简介与安装

### 什么是 FastAPI

FastAPI 是一个现代、快速（高性能）的 Python Web 框架，基于标准 Python 类型提示，支持：

- **快速**：非常高的性能，与 NodeJS 和 Go 相当
- **快速编码**：开发速度提升约 200% 至 300%
- **更少的 bug**：减少约 40% 的人类（开发者）引发的错误
- **智能**：极佳的编辑器支持，代码补全无处不在
- **简单**：易于使用和学习
- **简短**：减少代码重复
- **健壮**：生产级别的代码
- **基于标准**：基于（并完全兼容）OpenAPI 和 JSON Schema

### 安装 FastAPI

```bash
# 安装FastAPI及所有标准依赖
pip install "fastapi[standard]"

# 如果想安装基础版本
pip install fastapi

# 安装uvicorn作为ASGI服务器
pip install "uvicorn[standard]"
```

### 创建第一个应用

```python
# main.py
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
async def root():
    return {"message": "Hello World"}
```

### 运行应用

```bash
# 开发模式（自动重载）
fastapi dev main.py

# 生产模式
fastapi run main.py

# 或使用uvicorn
uvicorn main:app --reload
```

### 访问应用

- 首页：`http://127.0.0.1:8000` - 返回 JSON 响应
- 交互式文档：`http://127.0.0.1:8000/docs` - Swagger UI
- 备选文档：`http://127.0.0.1:8000/redoc` - ReDoc
- OpenAPI JSON：`http://127.0.0.1:8000/openapi.json`

---

## 第二章 路径参数

### 基本路径参数

路径参数用于捕获 URL 中的动态值。使用与 Python 字符串格式化相同的语法声明：

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/items/{item_id}")
async def read_item(item_id):
    return {"item_id": item_id}
```

访问 `http://127.0.0.1:8000/items/foo` 返回：
```json
{"item_id": "foo"}
```

### 声明参数类型

使用 Python 类型注解声明路径参数的类型：

```python
@app.get("/items/{item_id}")
async def read_item(item_id: int):
    return {"item_id": item_id}
```

访问 `http://127.0.0.1:8000/items/3` 返回：
```json
{"item_id": 3}
```

### 自动数据转换

FastAPI 会根据类型声明自动进行数据转换：

- URL 中的字符串 `"3"` 会自动转换为整数 `3`
- 如果类型不匹配（如访问 `/items/foo`），会返回清晰的错误信息

### 数据校验

当传入无效数据时，FastAPI 会返回详细的错误信息：

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

### 路径参数的类型声明

| 类型 | 说明 | 示例 |
|------|------|------|
| `int` | 整数 | `/items/{item_id}` |
| `float` | 浮点数 | `/pi/{value}` |
| `str` | 字符串 | `/users/{username}` |
| `path` | 路径（包含斜杠） | `/files/{file_path:path}` |

### 使用 Enum 限制预定义值

创建枚举类来限制路径参数的取值：

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

### 路径参数的顺序

路由匹配按定义顺序进行。固定的路径应该写在带有参数的路径之前：

```python
@app.get("/users/me")
async def read_user_me():
    return {"user_id": "the current user"}

@app.get("/users/{user_id}")
async def read_user(user_id: str):
    return {"user_id": user_id}
```

**注意**：必须先定义 `/users/me`，否则 FastAPI 会把 `"me"` 当作 `{user_id}` 的值。

### 包含路径的路径参数

使用 `:path` 声明包含斜杠的路径参数：

```python
@app.get("/files/{file_path:path}")
async def read_file(file_path: str):
    return {"file_path": file_path}
```

这样可以匹配 `/files/home/johndoe/myfile.txt`。

---

## 第三章 查询参数

### 基础查询参数

不是路径参数的参数会被自动识别为查询参数：

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

访问 `/items/?skip=0&limit=10` 返回：
```json
[
  {"item_name": "Foo"},
  {"item_name": "Bar"}
]
```

### 查询字符串

查询字符串是 URL 中 `?` 后的键值对，以 `&` 分隔：

```
http://127.0.0.1:8000/items/?skip=0&limit=10
```

| 参数 | 值 |
|------|-----|
| skip | 0 |
| limit | 10 |

### 默认值

查询参数支持默认值：

```python
@app.get("/items/")
async def read_item(skip: int = 0, limit: int = 10):
    # 如果不提供参数，使用默认值
    pass
```

### 可选参数

将默认值设为 `None` 使参数变为可选：

```python
@app.get("/items/{item_id}")
async def read_item(item_id: str, q: str | None = None):
    if q:
        return {"item_id": item_id, "q": q}
    return {"item_id": item_id}
```

### 类型转换

查询参数可以声明为 `bool` 类型，FastAPI 会自动转换：

```python
@app.get("/items/{item_id}")
async def read_item(item_id: str, short: bool = False):
    item = {"item_id": item_id}
    if not short:
        item.update({"description": "This is an amazing item..."})
    return item
```

以下 URL 都会被转换为 `True`：
- `/items/foo?short=1`
- `/items/foo?short=True`
- `/items/foo?short=true`
- `/items/foo?short=on`

### 必选查询参数

没有默认值的参数是必选的：

```python
@app.get("/items/{item_id}")
async def read_user_item(item_id: str, needy: str):
    return {"item_id": item_id, "needy": needy}
```

访问 `/items/foo` 而不提供 `needy` 参数会返回错误。

### 混合使用

可以同时使用必选参数、默认值参数和可选参数：

```python
@app.get("/items/{item_id}")
async def read_user_item(
    item_id: str,
    needy: str,                          # 必选
    skip: int = 0,                       # 默认值
    limit: int | None = None             # 可选
):
    return {
        "item_id": item_id,
        "needy": needy,
        "skip": skip,
        "limit": limit
    }
```

---

## 第四章 请求体

### 什么是请求体

**请求体**是客户端发送给 API 的数据。使用 Pydantic 模型来声明请求体可以充分利用类型检查和验证功能。

### 创建 Pydantic 模型

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

### 请求体示例

发送的 JSON 数据：
```json
{
    "name": "Foo",
    "description": "An optional description",
    "price": 45.2,
    "tax": 3.5
}
```

或者省略可选字段：
```json
{
    "name": "Foo",
    "price": 45.2
}
```

### 自动功能

仅使用 Python 类型声明，FastAPI 就能：

1. **读取 JSON 数据**：自动解析请求体
2. **类型转换**：在需要时转换数据类型
3. **数据验证**：数据无效时返回清晰错误信息
4. **生成 OpenAPI Schema**：为自动文档提供支持
5. **编辑器支持**：代码补全和类型检查

### 使用模型

在路径操作函数中直接访问模型的所有属性：

```python
@app.post("/items/")
async def create_item(item: Item):
    item_dict = item.model_dump()
    if item.tax is not None:
        price_with_tax = item.price + item.tax
        item_dict.update({"price_with_tax": price_with_tax})
    return item_dict
```

### 混合使用

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
        result.update({"q": q})
    return result
```

### 参数识别规则

FastAPI 按以下规则识别参数：

| 参数类型 | 识别方式 |
|----------|----------|
| 路径参数 | 在路径中声明的参数 |
| 查询参数 | 单一类型参数（如 `int`, `str`） |
| 请求体 | Pydantic 模型类型的参数 |

---

## 第五章 Pydantic 模型高级特性

### 字段验证

使用 `Field` 添加额外验证：

```python
from pydantic import BaseModel, Field

class Item(BaseModel):
    name: str = Field(..., min_length=1, max_length=50)
    price: float = Field(..., gt=0)
    description: str | None = Field(default=None, max_length=200)
```

### 嵌套模型

可以创建嵌套的 Pydantic 模型：

```python
class Image(BaseModel):
    url: str
    name: str

class Item(BaseModel):
    name: str
    description: str | None = None
    image: Image | None = None

class User(BaseModel):
    name: str
    items: list[Item] = []
```

### 列表字段

```python
class Item(BaseModel):
    name: str
    tags: list[str] = []
    price: list[float] = []
```

### 字典字段

```python
class Item(BaseModel):
    metadata: dict[str, str] = {}
    prices: dict[str, float] = {}
```

### 联合类型

```python
class Item(BaseModel):
    value: int | float
    status: "pending" | "processing" | "done"
```

### 日期和时间

```python
from datetime import datetime, time, date
from pydantic import BaseModel

class Event(BaseModel):
    name: str
    start_datetime: datetime
    end_datetime: datetime
    start_time: time
    start_date: date
```

### UUID 和 URL

```python
from uuid import UUID
from pydantic import BaseModel, HttpUrl

class Link(BaseModel):
    id: UUID
    url: HttpUrl
```

### 别名

```python
from pydantic import BaseModel, Field

class Item(BaseModel):
    name: str = Field(..., alias="itemName")
    price: float = Field(..., alias="itemPrice")
```

### 排除字段

```python
class Item(BaseModel):
    name: str
    price: float
    
    # 排除某些字段不输出
    class Config:
        exclude = {"description"}
```

### 必选字段

使用 `...`（Ellipsis）表示必填：

```python
from pydantic import BaseModel, Field

class Item(BaseModel):
    name: str = Field(...)
    price: float = Field(...)
```

---

## 第六章 响应模型

### 声明响应类型

使用 `response_model` 参数声明返回数据的类型：

```python
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class Item(BaseModel):
    name: str
    description: str | None = None
    price: float
    tax: float | None = None

@app.get("/items/{item_id}", response_model=Item)
async def read_item(item_id: int):
    return {
        "name": "Foo",
        "description": "A very nice Item",
        "price": 35.4,
        "tax": 3.2
    }
```

### 响应模型的作用

1. **数据转换**：将返回值转换为声明的类型
2. **数据过滤**：自动排除额外字段
3. **文档生成**：在 OpenAPI 模式中记录响应格式
4. **编辑器支持**：提供代码补全

### 返回列表

```python
@app.get("/items/", response_model=list[Item])
async def read_items():
    return [
        {"name": "Foo", "price": 35.4},
        {"name": "Bar", "price": 42.0}
    ]
```

### 使用枚举作为响应

```python
from enum import Enum

class ModelName(str, Enum):
    alexnet = "alexnet"
    resnet = "resnet"

@app.get("/model/{model_name}", response_model=ModelName)
async def get_model(model_name: ModelName):
    return model_name
```

### 响应状态码

使用 `status_code` 参数设置响应状态码：

```python
@app.post("/items/", status_code=201)
async def create_item(item: Item):
    return item
```

常用状态码：

| 状态码 | 说明 | 用途 |
|--------|------|------|
| 200 | OK | 默认，成功响应 |
| 201 | Created | 资源创建成功 |
| 204 | No Content | 成功但无返回内容 |
| 400 | Bad Request | 请求错误 |
| 401 | Unauthorized | 未认证 |
| 403 | Forbidden | 无权限 |
| 404 | Not Found | 资源不存在 |
| 422 | Unprocessable Entity | 验证错误 |

---

## 第七章 依赖注入

### 什么是依赖注入

依赖注入是一种设计模式，允许声明函数运行所需的依赖，FastAPI 会自动解析并注入这些依赖。

### 基础用法

```python
from typing import Annotated
from fastapi import Depends, FastAPI

app = FastAPI()

async def common_parameters(q: str | None = None, skip: int = 0, limit: int = 100):
    return {"q": q, "skip": skip, "limit": limit}

@app.get("/items/")
async def read_items(commons: Annotated[dict, Depends(common_parameters)]):
    return commons

@app.get("/users/")
async def read_users(commons: Annotated[dict, Depends(common_parameters)]):
    return commons
```

### 类作为依赖

依赖可以是类：

```python
class CommonParams:
    def __init__(self, q: str | None = None, skip: int = 0, limit: int = 100):
        self.q = q
        self.skip = skip
        self.limit = limit

@app.get("/items/")
async def read_items(params: Annotated[CommonParams, Depends(CommonParams)]):
    return {"q": params.q, "skip": params.skip, "limit": params.limit}
```

### 子依赖

依赖可以依赖其他依赖：

```python
from typing import Annotated
from fastapi import Depends, FastAPI

app = FastAPI()

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
    query_or_default: Annotated[str, Depends(query_or_cookie_extractor)]
):
    return {"q_or_cookie": query_or_default}
```

### 带 yield 的依赖

用于清理资源（如关闭数据库连接）：

```python
async def get_db():
    db = DBSession()
    try:
        yield db
    finally:
        db.close()

@app.get("/items/")
async def read_items(db: Annotated[DBSession, Depends(get_db)]):
    return db.query(Item).all()
```

### 全局依赖

使用 `app.dependency_overrides` 覆盖依赖（用于测试）：

```python
async def override_dependency():
    return {"override": True}

app.dependency_overrides[common_parameters] = override_dependency
```

---

## 第八章 安全性

### OAuth2 密码模式

最常见的认证方式：

```python
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

async def get_user(username: str):
    if username in fake_users_db:
        user_dict = fake_users_db[username]
        return user_dict

async def authenticate_user(username: str, password: str):
    user = await get_user(username)
    if not user:
        return False
    if not fake_hash_password(password) == user["hashed_password"]:
        return False
    return user

@app.post("/token")
async def login(form_data: Annotated[OAuth2PasswordRequestForm, Depends()]):
    user = await authenticate_user(form_data.username, form_data.password)
    if not user:
        raise HTTPException(
            status_code=status.HTTP_401_UNAUTHORIZED,
            detail="Incorrect username or password",
        )
    return {"access_token": user["username"], "token_type": "bearer"}

@app.get("/users/me")
async def read_users_me(
    current_user: Annotated[dict, Depends(get_current_user)]
):
    return current_user
```

### 获取当前用户

```python
async def get_current_user(token: Annotated[str, Depends(oauth2_scheme)]):
    user = await get_user(token)
    if not user:
        raise HTTPException(
            status_code=status.HTTP_401_UNAUTHORIZED,
            detail="Could not validate credentials",
        )
    return user
```

### JWT Token（生产级别）

```python
from datetime import datetime, timedelta
from jose import JWTError, jwt
from passlib.context import CryptContext

SECRET_KEY = "your-secret-key"
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

@app.post("/token")
async def login_for_access_token(
    form_data: Annotated[OAuth2PasswordRequestForm, Depends()]
):
    user = await authenticate_user(form_data.username, form_data.password)
    if not user:
        raise HTTPException(
            status_code=status.HTTP_401_UNAUTHORIZED,
            detail="Incorrect username or password",
        )
    access_token_expires = timedelta(minutes=ACCESS_TOKEN_EXPIRE_MINUTES)
    access_token = create_access_token(
        data={"sub": user["username"]}, expires_delta=access_token_expires
    )
    return {"access_token": access_token, "token_type": "bearer"}
```

---

## 第九章 中间件

### 添加中间件

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

### CORS 跨域资源共享

```python
from fastapi import FastAPI
from fastapi.middleware.cors import CORSMiddleware

app = FastAPI()

origins = [
    "http://localhost.tiangolo.com",
    "https://localhost.tiangolo.com",
    "http://localhost",
    "http://localhost:8080",
]

app.add_middleware(
    CORSMiddleware,
    allow_origins=origins,
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)
```

### 可用的中间件参数

| 参数 | 说明 |
|------|------|
| `allow_origins` | 允许的源列表 |
| `allow_credentials` | 是否允许发送 cookies |
| `allow_methods` | 允许的 HTTP 方法 |
| `allow_headers` | 允许的 HTTP 头 |

---

## 第十章 数据库操作

### SQLAlchemy 集成

```python
from sqlalchemy import create_engine, Column, Integer, String
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker, Session
from typing import Annotated
from fastapi import FastAPI, Depends

SQLALCHEMY_DATABASE_URL = "sqlite:///./sql_app.db"

engine = create_engine(SQLALCHEMY_DATABASE_URL, connect_args={"check_same_thread": False})
SessionLocal = sessionmaker(autocommit=False, autoflush=False, bind=engine)
Base = declarative_base()

class Item(Base):
    __tablename__ = "items"
    
    id = Column(Integer, primary_key=True, index=True)
    name = Column(String, index=True)
    description = Column(String, index=True)
    price = Column(Integer)

Base.metadata.create_all(bind=engine)

def get_db():
    db = SessionLocal()
    try:
        yield db
    finally:
        db.close()

app = FastAPI()

@app.post("/items/", response_model=Item)
async def create_item(item: Item, db: Annotated[Session, Depends(get_db)]):
    db_item = Item(**item.dict())
    db.add(db_item)
    db.commit()
    db.refresh(db_item)
    return db_item

@app.get("/items/", response_model=list[Item])
async def read_items(
    skip: int = 0,
    limit: int = 100,
    db: Annotated[Session, Depends(get_db)]
):
    return db.query(Item).offset(skip).limit(limit).all()
```

---

## 第十一章 错误处理

### HTTPException

```python
from fastapi import FastAPI, HTTPException

app = FastAPI()

items = {"foo": "The Foo Wrestlers"}

@app.get("/items/{item_id}")
async def read_item(item_id: str):
    if item_id not in items:
        raise HTTPException(status_code=404, detail="Item not found")
    return {"item": items[item_id]}
```

### 自定义异常处理器

```python
from fastapi import FastAPI, Request
from fastapi.responses import JSONResponse

class UnicornException(Exception):
    def __init__(self, name: str):
        self.name = name

app = FastAPI()

@app.exception_handler(UnicornException)
async def unicorn_exception_handler(request: Request, exc: UnicornException):
    return JSONResponse(
        status_code=418,
        content={"message": f"Oops! {exc.name} did something. \
                  There's a rainbow!"},
    )

@app.get("/unicorns/{name}")
async def read_unicorn(name: str):
    if name == "yolo":
        raise UnicornException(name=name)
    return {"unicorn_name": name}
```

---

## 第十二章 测试

### 使用 TestClient

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

### 运行测试

```bash
# 使用 pytest
pytest

# 或指定文件
pytest test_main.py

# 带详细输出
pytest -v
```

---

## 第十三章 部署

### 使用 Gunicorn + Uvicorn Workers

```bash
pip install uvicorn[standard] gunicorn

# 运行
gunicorn main:app -w 4 -k uvicorn.workers.UvicornWorker
```

### Docker 部署

```dockerfile
FROM python:3.10

WORKDIR /code

COPY ./requirements.txt /code/requirements.txt

RUN pip install --no-cache-dir --upgrade -r /code/requirements.txt

COPY ./app /code/app

CMD ["fastapi", "run", "app/main.py", "--host", "0.0.0.0", "--port", "80"]
```

### Dockerfile 多阶段构建（优化体积）

```dockerfile
FROM python:3.10-slim as builder

WORKDIR /build
COPY requirements.txt .
RUN pip install --target=/lib -r requirements.txt

FROM python:3.10-slim
WORKDIR /app
COPY --from=builder /lib /usr/local/lib/python3.10/site-packages
COPY ./app /app
CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "80"]
```

### 环境变量配置

```python
from pydantic_settings import BaseSettings

class Settings(BaseSettings):
    app_name: str = "Awesome API"
    admin_email: str
    database_url: str

    class Config:
        env_file = ".env"

settings = Settings()
```

---

## 附录：常用命令速查表

| 命令 | 说明 |
|------|------|
| `fastapi dev main.py` | 开发模式运行 |
| `fastapi run main.py` | 生产模式运行 |
| `uvicorn main:app --reload` | 使用 uvicorn 开发模式 |
| `uvicorn main:app --workers 4` | 多工作进程模式 |
| `pip install "fastapi[standard]"` | 安装 FastAPI 及依赖 |
| `pytest` | 运行测试 |
| `pytest -v` | 详细测试输出 |

## 附录：常见 HTTP 状态码

| 状态码 | 名称 | 用途 |
|--------|------|------|
| 200 | OK | 成功 |
| 201 | Created | 创建成功 |
| 204 | No Content | 成功无内容 |
| 400 | Bad Request | 请求错误 |
| 401 | Unauthorized | 未认证 |
| 403 | Forbidden | 无权限 |
| 404 | Not Found | 未找到 |
| 422 | Unprocessable Entity | 验证错误 |
| 500 | Internal Server Error | 服务器错误 |

## 附录：FastAPI vs 其他框架对比

| 特性 | FastAPI | Flask | Django |
|------|---------|-------|--------|
| 性能 | 极高 | 中等 | 中等 |
| 类型提示 | 原生支持 | 需要插件 | 需要插件 |
| 自动文档 | Swagger/ReDoc | 需要插件 | DRF |
| 异步支持 | 原生 | 需要插件 | 部分支持 |
| 学习曲线 | 低 | 低 | 中等 |
| 适用场景 | API、微服务 | 小型应用 | 大型应用 |
