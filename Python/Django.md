---
tags: web
---
# Django
---
# 安裝(windows)

首先安裝django
```python=
pip install Django
```
將django加入環境變數
```cmake=
\Python35\Lib\site-packages\Django-1.11-py3.5.egg\django\bin
```
最後運行一下確認一下有沒有安裝成果
```python=
python
>>>importd django
>>>print(django.VERSION)
>>>(1, 11, 0, 'alpha', 0)
```

---
## 創建初始專案
在cmd輸入
```cmake
django-admin startproject myblog .
```
你打tree會看到，這便是他底下資料夾的結構
![](https://i.imgur.com/EfraQlk.jpg)

---
## 接下來建立資料庫系統~
```cmake
python manage.py migrate
```
如果正確執行會跑出
```cmake=
Operations to perform:
  Apply all migrations: admin, auth, contenttypes, sessions
Running migrations:
  Applying contenttypes.0001_initial... OK
  Applying auth.0001_initial... OK
  Applying admin.0001_initial... OK
  Applying admin.0002_logentry_remove_auto_add... OK
  Applying admin.0003_logentry_add_action_flag_choices... OK
  Applying contenttypes.0002_remove_content_type_name... OK
  Applying auth.0002_alter_permission_name_max_length... OK
  Applying auth.0003_alter_user_email_max_length... OK
  Applying auth.0004_alter_user_username_opts... OK
  Applying auth.0005_alter_user_last_login_null... OK
  Applying auth.0006_require_contenttypes_0002... OK
  Applying auth.0007_alter_validators_add_error_messages... OK
  Applying auth.0008_alter_user_username_max_length... OK
  Applying auth.0009_alter_user_last_name_max_length... OK
  Applying sessions.0001_initial... OK
```

### 接下來運行伺服器
在cmd打出以下指令
```cmake
python manage.py runserver 0:8000
```
為了檢查是否運行成功，在瀏覽器網址輸入 http://localhost:8000/

---