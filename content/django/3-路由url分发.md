# django路由url分发

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
