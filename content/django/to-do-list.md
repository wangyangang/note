- 验证码复习
- FDFS复习
- 分页的url

```python
re_path(r'^paginator([0-9]*)/$', PaginatorView.as_view(), name='paginator')
```
> paginator后别跟“/”，不然如果页码参数缺少，url会变成以两个反斜线结尾

- celery深入
- django 自定义tag里面的include_tags()
