# django路由url分发

## 1. 基本使用
- 项目的urls.py文件

```python
from django.contrib import admin
from django.urls import path, re_path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    re_path(r'^app01/', include(('app01.urls', 'app01'), namespace='app01'))
]
```

- 应用的urls.py文件

```python
from django.urls import path, re_path
from app01.views import IndexView, BookInfoListView

urlpatterns = [
    re_path(r'^index', IndexView.as_view(), name='index'),
    re_path(r'^books', BookInfoListView.as_view(template_name='books.html'), name='books'),
]
```

## 2. 获取参数

- 位置参数
```python
url(r'^delete(\d+)/$',views.show_arg),

def show_arg(request,id):
    return HttpResponse('show arg %s'%id)
```
- 关键字参数
```python
url(r'^delete(?P<id1>\d+)/$',views.show_arg),

def show_arg(request,id1):
    return HttpResponse('show %s'%id1)
```
> 注意：视图show_arg此时必须要有一个参数名为id1，否则报错。
