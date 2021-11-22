## vuex-persist 持久化存储vuex

![image-20211012161813608](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20211012161813608.png)

```js
import { createStore } from 'vuex'

import VuexPersistence from 'vuex-persist'

import state from './state'

import mutations from './mutations'

import getters from './getters'

import actions from './actions'

const vuexLocal = new VuexPersistence({

 storage: window.localStorage

})
export const store = createStore({

 state,mutations,getters,actions,

 plugins: [vuexLocal.plugin]

})
```

