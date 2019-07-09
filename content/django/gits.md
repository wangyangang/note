# Gist
<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Gist](#gist)
	- [向前端返回json格式的数据](#向前端返回json格式的数据)
	- [django中ajax的使用](#django中ajax的使用)
		- [关于ajax的csrf验证：](#关于ajax的csrf验证)

<!-- /TOC -->
## 向前端返回json格式的数据

```python
def get_house_index():
    try:
        ret = redis_store.get('home_page_data')
    except Exception as e:
        current_app.logger.error(e)
        ret = None

    if ret:
        current_app.logger.info('hit house index info redis')
        return '{"errno": 0, "errmsg": "OK", "data": %s}' % ret, 200, {"Content-Type": "application/json"}
```

## django中ajax的使用
    *post：*

```js
$('#btn2').click(function () {
      var new_session_value = $('#new_session_value').val();
      var csrf = $('input[name="csrfmiddlewaretoken"]').val();
      {#var args = {'name': new_session_value, 'csrfmiddlewaretoken': csrf};#}
      var args = {name: new_session_value};
      var json_args = JSON.stringify(args);
      console.log(json_args);
      $.ajax({
            url: '/app01/sessions/',
            type: 'post',
            data: json_args,
            {#contentType:'application/json',#}
            dataType: 'json',
            headers:{
              'X-CSRFTOKEN': csrf
            },
            success: function (data) {
                  var resno = data['resno'];
                  if(resno == 1){
                    var val = data['name'];
                    $('#session_value').val(val);
                  }else if(resno == 0){
                    $('#session_value').val(data['errmsg']);
                  }
            }
      })
})

```
- url地址前要有 "/"

```js
$.post('/order/pay', params, function (data), 'json')
  ...
// 以下是jquery中ajax post的部分定义：
// jQuery[ method ] = function( url, data, callback, type ) {}
```

### 关于ajax的csrf验证：
  - 传的数据不是json，那么可以把`csrfmiddlewaretoken`作为键放到参数里
  - 传的数据是json，不能把`csrfmiddlewaretoken`放到参数里，放进去也不起作用。只能用ajax的常规写法，把`csrf`放到请求头里。
  - 后台获取json数据，用
    ```python
    json_body = json.loads(request.body)
    ```
    获取单个数据也可以用
    ```python
    name = request.POST.get('name')
    ```
