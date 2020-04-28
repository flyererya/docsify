> https://www.npmjs.com/package/axios

## axios是基于XMLHttpRequest和Promise封装的，但是fetch不是

## 常用api
- axios(config)
- axios(url[, config])  `默认是get方法`  
- axios.get(url[, config])
- axios.post(url[, data[, config]])

## params和data的区别
- `params`是即将与请求一起发送的 URL 参数
- `data` 是作为请求主体被发送的数据


## 错误处理
```javascript
axios.get('/user/12345')
  .catch(function (error) {
    if (error.response) {
      // 服务器返回了结果，但结果不是我们想要的
      // 请求已发出，但服务器响应的状态码不在 2xx 范围内
      // axios会默认只有2开头的算请求成功
      // 即使请求过去，返回过来成功，但不是2开头的都算失败
      console.log(error.response.data);
      console.log(error.response.status);
      console.log(error.response.headers);
    } else {
      // 服务器连结果都没有返回
      // Something happened in setting up the request that triggered an Error
      console.log('Error', error.message);
    }
    console.log(error.config);
  });
```

## 配置响应状态码的验证(axios会默认只有2开头的算请求成功)
```javascript
axios.defaults.validateStatus = status =>{
    return /^(2|3)\d{2}$/.test(status);
}
```