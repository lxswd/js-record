## 字符串

js为字符串提供了一些方法，调用这些方法不会改变字符串，会返回一个新的字符串

#### toUpperCase

toUpperCase() 把一个字符串全部变为大写

```js
var s = 'hello';
s.toUpperCase();	//返回'HELLO'
```

#### toLowerCase

toLowerCase() 把一个字符串全部变为小写

```js
var s = 'Hello, World';
s.toLowerCase();	//返回'hello, world'
```

#### indexOf

indexOf() 会搜索指定字符串出现的位置

```js
var s = 'hello, world';
s.indexOf('world');	//返回7
s.indexOf('World');	//没有找到指定字符串，返回-1
```

#### subString

subString() 返回指定索引区间的子串

```js
var s = 'hello, world';
s.subString(0, 5);	//从索引0开始到5（不包括5），返回'hello'
s.subString(7);	//从索引7开始到结束，返回'world'
```

## 数组

#### slice

slice() 就是对应String的subString()版本，它截取Array的部分元素，然后返回一个新的Array；

```js
var arr = ['a', 'b', 'c', 'd', 'e', 'f', 'g'];
arr.slice(0, 3);	//从索引0开始，到索引3结束，但不包括3：['a', 'b', 'c']
arr.slice(3);	//从索引3到结束：['d', 'e', 'f', 'g']
var copy = arr.slice();	//如果不给slice()传递任何参数，就会截取所有元素，利用这一点，可以复制一个Array
copy;	// ['a', 'b', 'c', 'd', 'e', 'f', 'g']
copy === arr;	//false
```

注意slice() 的起止参数包括开始索引，不包括结束索引；

#### push和pop

push() 向Array的末尾添加若干元素，pop()则把Array的最后一个元素删掉

```js
var arr = [1, 2];
arr.push('a', 'b')	//返回Array新的长度：4
arr;	//[1, 2, 'a', 'b']
arr.pop();	//返回'b'
arr;	//[1, 2, 'a']
arr.pop(); arr.pop(); arr.pop();	//连续pop()3次
arr;	//[]
arr.pop();	//空数组继续pop()不会报错，而是返回undefined
arr;	//[]
```

#### unshift和shift

unshift()向Array头部添加若干元素，shift()删除Array的第一个元素

```js
var arr = [1, 2];
arr.unshift('a', 'b');	//返回Array新的长度：4
arr;	//['a', 'b', 1, 2]
arr.shift();	//['b', 1, 2]
//和pop类似，空数组继续shift也不会报错，返回undefined
```

#### sort

sort()可以对当前Array进行排序，直接调用时，按照默认顺序排序

```js
var arr = ['b', 'c', 'a'];
arr.sort();
arr;	//['a', 'b', 'c']
```

可以按照指定的顺序排序

#### reverse

reverse()把整个Array的元素顺序反转

```js
var arr = ['a', 'b', 'c']
arr.reverse();
arr;	//['c', 'b', 'a']
```

#### splice

splice()可以从指定的索引开始删除若干元素，然后再从该位置添加若干元素

```js
var arr = ['a', 'b', 'c', 'd', 'e', 'f'];
//从索引2开始删除3个元素，然后再添加2个元素
arr.splice(2, 3, 'aa', 'cc')	//返回删除的元素['c', 'd', 'e']
arr;	//['a', 'b', 'aa', 'cc', 'f']
//从索引2开始删除2个元素
arr.splice(2, 2);	//['aa', 'cc']
arr;	//['a', 'b', 'f']
//只添加，不删除
arr.splice(2, 0, 'aa', 'cc')	//返回为[],因为为没有删除任何元素
arr;	//['a', 'b', 'aa', 'cc', 'f']
```

#### concat

concat()把当前的Array和另一个Array连接起来，并返回一个新的Array，并没有修改当前Array

```js
var arr = ['a', 'b', 'c']
var added = arr.concat(['e', 'f'])
added;	//['a', 'b', 'c', 'e', 'f']
arr;	//['a', 'b', 'c']
//concat()可以接受任意元素和Array，并且自动把Array拆开，然后添加到新的Array中
arr.concat(1, 2, [3, 4]);	//['a', 'b', 'c', 1, 2, 3, 4]
```

#### join

join()把当前Array的每一个元素都用指定的字符串连接起来，然后返回连接后的字符串

```js
var arr = ['a', 'b', 'c', 1, 2, 3];
arr.join('-');	//'a-b-c-1-2-3'
```

如果Array的元素不是字符串，将自动转换为字符串后再连接

## Map和Set

#### Map

Map是一组键值对的结构，具有快速的查找速度

举个例子，假设根据同学的名字查找对应成绩，如果用Array实现，需要两个Array

```js
var names = ['a', 'b', 'c'];
var scores = [90, 91, 100];
```

给定一个名字要查找对应的成绩，就要先在names中找到对应位置，再从scroes取出对应的成绩，Array越长，耗时越长

如果用Map实现，只需要一个“名字”-“成绩”的对照表，直接根据名字查找成绩，无论这个表有多大，查找速度都不会变慢

```js
var m = new Map(['a', 99], ['b', 89], ['c', 90]);
m.get('a');	//99
```

初始化Map需要一个二维数组，或者直接初始化一个空Map

```js
var m = new Map();
m.set('a', 90);	//添加新的key-value
m.set('b', 88);
m.has('a');	//是否存在key 'a': true
m.get('a');	//90
m.delete('a');	//删除key 'a'
m.get('a');	//undefined
```

由于一个key只能对应一个value，所以多次对一个key放入value，后面的值会把前面的值替换掉

```js
var m = new Map();
m.set('a', 90);
m.set('a', 99);
m.get('a');	//99
```

#### Set

Set是一组key的集合，但是不存储value。由于key不能重复，所以在Set中，没有重复的key

要创建一个Set，需要提供一个Array作为输入，或者直接创建一个空Set

```js
var s1 = new Set();
var s2 = new Set([1, 2, 3])
```

重复元素在Set中会自动被过滤

```js
var s = new Set([1, 2, 3, 3, '3']);
s;	//Set [1, 2, 3, '3']
```

数字3和字符串‘3’是不同的元素

通过add(key)方法可以添加元素到Set中，可以重复添加，但是不会有效果

```js
s.add(4);
s;	//Set [1, 2, 3, 4]
s.add(4);
s;	//仍然是Set [1, 2, 3, 4]
```

通过delete(key)可以删除元素

```js
var s = new Set([1, 2, 3]);
s;	//Set [1, 2, 3]
s.delete(3);
s;	//Set [1, 2]
```

