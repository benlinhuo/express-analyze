###中间件总结
#####中间件定义及对应引用方式（两种）
1. 方式一
  ```javascript
  function middleware1(req, res, next) {
    req.count=21;//给每个请求加上属性count
    next();
  }
  ```
该方式的引用需要：app.use(middleware1);//如果定义的app与middleware1在一个文件中，可以直接引用。

2. 方式二
```javascript
function middleware2(){
    var i=0;
    return function(req, res, next){
        i++;
        req.count=i;
       next();
    }
}
```
该方式的引用：app.use(middleware2())。注意：我们是在执行函数middleware2的时候，return一个代表中间件的函数出来，该函数才是中间件的实体。