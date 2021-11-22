# nuxt.js SSR 渲染  

## =>window is not defined

```
 import E from 'wangeditor'  // 通过npm 下载并引入wangeditor
 替换为
 const E = process.browser ? require('wangeditor') : undefined;
```

