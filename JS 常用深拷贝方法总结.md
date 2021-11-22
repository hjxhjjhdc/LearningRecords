# JS 常用深拷贝方法总结

拷贝：其实就是一个对象复制给另外一整个对象，让对象相互不影响。

所谓的浅拷贝，只是拷贝了基本类型的数据，对于引用的类型数据，复制后也是会发生引用，这种拷贝就叫做浅拷贝

浅拷贝和深拷贝之间的区别：

假设A复制了B，B发生了改变，A也跟着改变，就是浅拷贝，如果A没有变化，那就是深拷贝（深拷贝本质是两者数据的内存地址完全不同）

深拷贝常用方法：

1. Object.assign(target, ...sources)

Object.assign() 是ES6新增方法，也可以用于对象的合并。

但是在进行拷贝对象时，当对象中只有一级属性，没有二级属性的时候，此方法为深拷贝。

但是需要注意的是，当对象中有对象或数组复杂类型数据时，此方法，在二级属性以后就是浅拷贝，即为引用数据类型。

2. 通过 JSON 对象实现深拷贝

先将对象转成字符串，再转成 JSON，但是这个方法只有可以转成 JSON 格式的对象才可以这样用，像 function 无法转成 JSON，RegExp 对象也是无法通过这种方式深拷贝。

// 语法--
let deepObj = JSON.parse(JSON.stringify(obj))

// demo--
const obj1 = { a : 1, b : 2}
const obj2 = JSON.parse(JSON.stringify(obj1));
obj1.a = 2;
console.log(obj1); // { a:2, b:2 }
console.log(obj2); // { a:1, b:2 }
对于原对象中undefined、function、symbol 三种数据类型是无效的，因为这三种值会在转换过程中被忽略掉，所以对有这三种属性的对象使用这种方式会造成上述三种属性的数据丢失。但是对没有这三种属性的数据来说使用这种方式简单快捷。

3. 通过lodash函数库实现深拷贝

lodash是当前很热门的函数库，提供了 lodash.cloneDeep()可以快速实现对象或数组的深拷贝  loadsh中文网

// 引入loadsh函数库
import _ from 'loadsh'

// 使用cloneDeep实现深拷贝
var obj= [{ 'a': 1 }, { 'b': 2 }];
var deep = _.cloneDeep(obj);
console.log(deep[0] === objects[0]); // => false
4. 使用递归进行深拷贝

function deepClone(source) {
  if (!source) return
  let target;
  if (typeof source === 'object') {
    // 根据source类型判断是新建一个数组还是对象
    target = Array.isArray(source) ? [] : {}
    // 遍历source，并且判断是source的属性才拷贝
    for (let key in source) {
      if (source.hasOwnProperty(key)) {
        if (typeof source[key] !== 'object') {
          target[key] = source[key]
        } else {
          // 如果内部属性存在复杂数据类型，使用递归实现深拷贝
          target[key] = deepClone(source[key])
        }
      }
    }
  } else {
    target = source
  }
  return target
}

