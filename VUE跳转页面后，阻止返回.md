# VUE种跳转页面后，阻止返回
### 在跳转到的页面内加上下面的代码：

created() { 
    history.pushState(null, null, document.URL);
    window.addEventListener("popstate", function () {
      history.pushState(null, null, document.URL);
    });
  },

