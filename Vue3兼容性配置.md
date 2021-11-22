## 兼容性配置

### [#](https://v3.cn.vuejs.org/guide/migration/migration-build.html#全局配置)全局配置

兼容性特性可以进行单独禁用：

```js
import { configureCompat } from 'vue'

// 禁用某些兼容性特性
configureCompat({
  FEATURE_ID_A: false,
  FEATURE_ID_B: false
})
```

或者整个应用默认为 Vue 3 的行为，仅开启某些兼容性特性：

```js
import { configureCompat } from 'vue'

// 所有 Vue 3 的默认行为，并开启某些兼容性特性
configureCompat({
  MODE: 3,
  FEATURE_ID_A: true,
  FEATURE_ID_B: true
})
```

### [#](https://v3.cn.vuejs.org/guide/migration/migration-build.html#基于单个组件的配置)基于单个组件的配置

一个组件可以使用 `compatConfig` 选项，并支持与全局 `configureCompat` 方法相同的选项：

```js
export default {
  compatConfig: {
    MODE: 3, // 只为这个组件选择性启用 Vue 3 行为
    FEATURE_ID_A: true // 也可以在组件级别开启某些特性
  }
  // ...
}
```

### [#](https://v3.cn.vuejs.org/guide/migration/migration-build.html#针对编译器的配置)针对编译器的配置

以 `COMPILER_` 开头的特性是针对编译器的：如果你正在使用完整构建版本 (含浏览器内编译器)，它们可以在运行时中被配置。然而如果使用构建设置，它们必须换为通过在构建配置中的 `compilerOptions` 进行配置 (参阅上述的配置)。