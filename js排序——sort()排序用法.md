# js排序——sort()排序用法 

### sort() 方法用于对数组的元素进行排序,并返回数组。默认排序顺序是根据字符串Unicode码点。

```
语法：array.sort(fun)；参数fun可选。规定排序顺序。必须是函数。
注：如果调用该方法时没有使用参数，将按字母顺序对数组中的元素进行排序，说得更精确点，是按照字符编码的顺序进行排序。

如果想按照其他规则进行排序，就需要提供比较函数，该函数要比较两个值，然后返回一个用于说明这两个值的相对顺序的数字。比较函数应该具有两个参数 a 和 b，其返回值如下：
若 a 小于 b，在排序后的数组中 a 应该出现在 b 之前，则返回一个小于 0 的值。
若 a 等于b，则返回 0。
若 a 大于 b，则返回一个大于 0 的值。
简单点就是：比较函数两个参数a和b，返回a-b 升序，返回b-a 降序
//注：原数组发生改变
```

#### 例：

##### 1.不传参数，将不会按照数值大小排序，按照字符编码的顺序进行排序；

		var arr = ['General','Tom','Bob','John','Army'];
		var resArr = arr.sort();
		console.log(resArr);//输出   ["Army", "Bob", "General", "John", "Tom"]
		
		var arr2 = [30,10,111,35,1899,50,45];
		var resArr2 = arr2.sort();
		console.log(resArr2);//输出   [10, 111, 1899, 30, 35, 45, 50]
2. ##### 传入参数，实现升序，降序；

		var arr3 = [30,10,111,35,1899,50,45];
		arr3.sort(function(a,b){
			return a - b;
		})
		console.log(arr3);//输出  [10, 30, 35, 45, 50, 111, 1899]
		
		var arr4 = [30,10,111,35,1899,50,45];
		arr4.sort(function(a,b){
			return b - a;
		})
		console.log(arr4);//输出 [1899, 111, 50, 45, 35, 30, 10]


3. ##### 根据数组中的对象的某个属性值排序；

		var arr5 = [{id:10},{id:5},{id:6},{id:9},{id:2},{id:3}];
		arr5.sort(function(a,b){
			return a.id - b.id
		})
		console.log(arr5);
		//输出新的排序
		//		{id: 2}
		//		{id: 3}
		//		{id: 5}
		//		{id: 6}
		//		{id: 9}
		//		{id: 10}


4. ##### 根据数组中的对象的多个属性值排序，多条件排序；

		var arr6 = [{id:10,age:2},{id:5,age:4},{id:6,age:10},{id:9,age:6},{id:2,age:8},{id:10,age:9}];
		arr6.sort(function(a,b){
			if(a.id === b.id){//如果id相同，按照age的降序
				return b.age - a.age
			}else{
				return a.id - b.id
			}
		})
		console.log(arr6);
		//输出新的排序
		//		{id: 2, age: 8}
		//		{id: 5, age: 4}
		//		{id: 6, age: 10}
		//		{id: 9, age: 6}
		//		{id: 10, age: 9}
		//		{id: 10, age: 2}