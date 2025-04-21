## Map和Object的区别
作为es6新增的类型，map和object有很多相似的地方，在一些实际使用情况下两者也可以互相替代，但是map仍然有一些普通对象不具有的新特性。

1. 键的类型的要求：`Object`只能以`string`、`symbol`类型作为键（`number`类型会被自动转换为字符串），而`Map`支持任意类型作为键。
2. 对顺序的维护：ES6 规范明确了普通对象属性的遍历顺序：数字键（正整数字符串）按数值升序排列；字符串键按插入顺序排列（在数字键之后）；Symbol 键按插入顺序排列（在字符串键之后）。可以看出当存在数字键的时候object并不是有序的；而map对有序性时有强制要求的，map会主动维护插入的顺序。
3. 内存与扩展性：object因为原型链的影响，内存占用稍高；map可以通过.size属性直接获取大小，object需要用`Object.keys(obj).length`这样的方法来获取
4. 效率：在频繁增删方面，map做过特别优化，效率比普通object更高。
5. 迭代与工具方法：
- 迭代方面：map内置迭代方法，自带foreach，entrires，keys，values；object需转换为数组：`Object.keys()`/`entries()`。
- 序列化方面：`Map`不支持直接使用`JSON.stringify`，需要先转换为普通对象或数组，例如：
  ```javascript
  const map = new Map([['key1', 'value1'], ['key2', 'value2']]);
  const serialized = JSON.stringify(Object.fromEntries(map));
  console.log(serialized); // {"key1":"value1","key2":"value2"}
  ```


## Map常用的方法
- has():查询某个键是否存在
- get():获取某个键的值
- set():键不存在的时候加入键值对，存在的时候更新对应键的值
- delete():删除对应键值对，键存在返回true，键不存在返回false
- clear(): 清空所有键值对
- entries(): 返回一个包含所有键值对的迭代器
- keys(): 返回一个包含所有键的迭代器
- values(): 返回一个包含所有值的迭代器