### type

1. type可以声明基本类型别名、联合类型、元祖等类型
```js
// 基本类型别名
type Name = string;

// 联合类型
interface Dog {
  wong()
}
interface Cat {
  miao();
}

type Pet = Dog | Cat;

// 具体定义数组每个位置的类型
type PetList = [Dog, Pet];

```

2. type语句中还可以使用typeof获取实例的类型进行赋值
```js
// 当你想要获取一个变量的类型时，使用typeof
let div = document.createElement('div');
type B = typeof div;
```  

3. 其他骚操作
```js
type StringOrNumber = string | number;
type Text = string | { text: string };
type NameLookup = Dictionary<string, Person>;
type Callback<T> = (data: T) => void;
type Pair<T> = [T, T];
type Coordinates = Pair<number>;
type Tree<T> = T | { left: Tree<T>, right: Tree<T> };
```

### interface

### 泛型