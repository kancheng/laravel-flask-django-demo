# Laravel + Flask + Django Demo

此專案目標：快速建立三個環境，並各自輸出 `Hello world`。

## 1) Laravel (PHP)

### 建立專案

```powershell
cd f:\xampp\htdocs\laravel-flask-django-demo
composer create-project laravel/laravel laravel-app
```

> 若下載過程超時，可先設定：
>
> ```powershell
> $env:COMPOSER_PROCESS_TIMEOUT=1800
> composer create-project laravel/laravel laravel-app
> ```

### 下載過慢時（Laravel/Composer）

XAMPP，請先打開：

`F:\xampp\php\php.ini`

找到這行（可用 Ctrl+F 搜尋）：

```ini
;extension=zip
```

把前面的 `;` 拿掉，改成：

```ini
extension=zip
```

完成後請重新開啟終端機，再重新執行：

```powershell
composer create-project laravel/laravel laravel-app
```

### 修改路由為 Hello world

編輯 `laravel-app\routes\web.php`：

```php
<?php

use Illuminate\Support\Facades\Route;

Route::get('/', function () {
    return 'Hello world from Laravel!';
});
```

### 啟動

```powershell
cd laravel-app
php artisan serve
```

開啟：`http://127.0.0.1:8000`

若要改埠號：

```powershell
php artisan serve --port=8001
```

開啟：`http://127.0.0.1:8001`

---

## 2) Flask (Python)

### 建立專案與虛擬環境

```powershell
cd f:\xampp\htdocs\laravel-flask-django-demo
mkdir flask-app
cd flask-app
python -m venv .venv
.\.venv\Scripts\activate
pip install flask
```

### 建立 `app.py`

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello():
    return "Hello world from Flask!"

if __name__ == "__main__":
    app.run(debug=True)
```

### 啟動

```powershell
cd f:\xampp\htdocs\laravel-flask-django-demo\flask-app
.\.venv\Scripts\activate
python app.py
```

開啟：`http://127.0.0.1:5000`

若要改埠號（擇一）：

```powershell
flask run --port 5001
```

或修改 `app.py`：

```python
if __name__ == "__main__":
    app.run(debug=True, port=5001)
```

開啟：`http://127.0.0.1:5001`

---

## 3) Django (Python)

### 建立專案與虛擬環境

```powershell
cd f:\xampp\htdocs\laravel-flask-django-demo
mkdir django-app
cd django-app
python -m venv .venv
.\.venv\Scripts\activate
pip install django
django-admin startproject config .
```

### 設定 Hello world 路由

編輯 `django-app\config\views.py`：

```python
from django.http import HttpResponse

def hello(request):
    return HttpResponse("Hello world from Django!")
```

編輯 `django-app\config\urls.py`：

```python
from django.contrib import admin
from django.urls import path
from .views import hello

urlpatterns = [
    path("admin/", admin.site.urls),
    path("", hello),
]
```

### 啟動

```powershell
cd f:\xampp\htdocs\laravel-flask-django-demo\django-app
.\.venv\Scripts\activate
python manage.py runserver
```

開啟：`http://127.0.0.1:8000`

若要改埠號：

```powershell
python manage.py runserver 8002
```

開啟：`http://127.0.0.1:8002`

---

## 建議目錄結構

```text
laravel-flask-django-demo/
  ├─ laravel-app/
  ├─ flask-app/
  ├─ django-app/
  └─ README.md
```

## 備註

- Laravel 與 Django 預設都可能使用 `8000` 連接埠，請避免同時啟動或改埠號。
- 改埠號範例：
  - Laravel：`php artisan serve --port=8001`
  - Flask：`flask run --port 5001`（或 `app.run(port=5001)`）
  - Django：`python manage.py runserver 8002`
