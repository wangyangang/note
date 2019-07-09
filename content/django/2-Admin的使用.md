# django-admin的使用

> django-admin是一个用来管理django站点后台数据库的应用，是django自带的。
我们用pycharm创建django应用的时候，默认就把admin这个应用加入到settngs.py的installed app里了。

## 几个注意点

1. 更改admin页面的语言和时区,在setting.py里更改如下内容：

```python
TIME_ZONE = 'Asia/Shanghai'
LANGUAGE_CODE = 'zh-hans`
```

2. 更改admin页面显示的app的名称,在应用的apps.py里加上verbose_name

```python
from django.apps import AppConfig

class App01Config(AppConfig):
    name = 'app01'
    verbose_name = '博客'
```

在app目录下的__init__.py里加上default_app_config
```python
default_app_config = 'app01.apps.App01Config'
```

3. 利用model的Meta类，改变模型在admin界面的显示

```python
class Meta:
   db_table = 'book_info'
   verbose_name = '书籍'
   verbose_name_plural = '许多书籍'
   ```

4. 要想在admin界面管理哪个model，就要把它注册到admin里。也可以继承admin.ModelAdmin进行自定义.在admin.py里：

```python
class BookInfoAdmin(admin.ModelAdmin):
    list_display = ['name', 'price', 'comment'] # BookInfo类在后台显示哪几个字段

admin.site.register(BookInfo, BookInfoAdmin)
```
