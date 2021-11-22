#  JS日期格式化转换方法

## 可以为Date原型添加如下的方法：

```
Date.prototype.format = function(fmt) { 
     var o = { 
        "M+" : this.getMonth()+1,                 //月份 
        "d+" : this.getDate(),                    //日 
        "h+" : this.getHours(),                   //小时 
        "m+" : this.getMinutes(),                 //分 
        "s+" : this.getSeconds(),                 //秒 
        "q+" : Math.floor((this.getMonth()+3)/3), //季度 
        "S"  : this.getMilliseconds()             //毫秒 
    }; 
    if(/(y+)/.test(fmt)) {
            fmt=fmt.replace(RegExp.$1, (this.getFullYear()+"").substr(4 - RegExp.$1.length)); 
    }
     for(var k in o) {
        if(new RegExp("("+ k +")").test(fmt)){
             fmt = fmt.replace(RegExp.$1, (RegExp.$1.length==1) ? (o[k]) : (("00"+ o[k]).substr((""+ o[k]).length)));
         }
     }
    return fmt; 
}        
```

var time1 = new Date().format("yyyy-MM-dd hh:mm:ss");
console.log(time1);

运行如下：

  ![img](https://images0.cnblogs.com/i/561794/201406/082121235999016.png)

也可以转换成 ”年月日”的格式 

var time2 = new Date().format("yyyy-MM-dd");
console.log(time2);

运行如下：

 ![img](https://images0.cnblogs.com/i/561794/201406/082122201143518.png)

