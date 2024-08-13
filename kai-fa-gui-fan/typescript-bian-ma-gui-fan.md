# 👕 TypeScript编码规范

## TypeScript编码规范

## 1 命名及约定

### 1.1 类

使用 PascalCase 进行命名。

**Bad**

```typescript
class foo {}
```

**Good**

```typescript
class Foo {}
```

### 1.2 类成员（变量、方法）

使用 camelCase 进行命名。

**Bad**

```typescript
class Foo {
  Bar: number;
  Baz(): number {}
}
```

**Good**

```typescript
class Foo {
  bar: number;
  baz(): number {}
}
```

### 1.3 接口

使用 PascalCase 进行命名，不要在接口名前加“I”。

接口成员使用 camelCase 进行命名。

**Bad**

```typescript
interface IFoo {
  Bar: number;
  Baz(): number;
}
```

**Good**

```typescript
interface Foo {
  bar: number;
  baz(): number;
}
```

### 1.4 命名空间

使用 PascalCase 进行命名。

**Bad**

```typescript
namespace foo {}
```

**Good**

```typescript
namespace Foo {}
```

### 1.5 枚举

*   使用 PascalCase 进行命名。

    **\*Bad\***

    ```typescript
    enum color {}
    ```

    **\*Good\***

    ```typescript
    enum Color {}
    ```
*   枚举成员使用 PascalCase 进行命名。

    **\*Bad\***

    ```typescript
    enum Color {
      red,
    }
    ```

    **\*Good\***

    ```typescript
    enum Color {
      Red,
    }
    ```

### 1.6 文件名

* 使用破折号分隔描述性单词，比如：hero-list.ts。
* 使用点将描述性名称与类型分开，比如：user-info.page.ts。
* 尽量使用常规的几种类型名，包括.page,.service,.component,.pipe,.module,.directive,.controller 和.middleware。当然也可以自己创建其他类型，但不宜太多。
* 类名与文件名匹配，并遵循类命名规范。

| 类名                                  | 文件名                     |
| ----------------------------------- | ----------------------- |
| export class AppComponent { }       | app.component.ts        |
| export class HeroListComponent { }  | hero-list.component.ts  |
| export class UserProfileService { } | user-profile.service.ts |

## 2 类型

*   需显式地为变量、数组和方法编写类型（类型推论能够推断出类型的不需要声明类型）。

    **\*Bad\***

    ```typescript
    class Bar {
      bar(input) {
        let isZero;
        const foo: number = 5;
        if (input === 5) {
          isZero = false;
        }
        const resultObject = {
          fo: foo,
          isZeroRes: isZero,
        };
        return resultObject;
      }
    }
    ```

    **\*Good\***

    ```typescript
    class Bar {
      bar(input: number): BarResult {
        let isZero: boolean;
        const foo = 5;
        if (input === 0) {
          isZero = true;
        }
        const resultObject = {
          fo: foo,
          isZeroRes: isZero,
        };
        return resultObject;
      }
    }
    ​
    interface BarResult {
      fo: number;
      isZeroRes: boolean;
    }
    ```
*   不要使用 Number、String、Boolean、Object 为变量、数组和方法设置类型。

    **\*Bad\***

    ```typescript
    baz(foo: String): String {
    ​
    }
    ```

    **\*Good\***

    ```typescript
    baz(foo: string): string {
    ​
    }
    ```

## 3 声明变量

* 如果变量在其生命周期可能发生改变，尽量使用 let。
*   如果一个值在程序生命周期内不会改变，尽量使用 const。

    **\*Bad\***

    ```typescript
    var bar = "bar";
    var count;
    if (true) {
      console.log(bar);
      count += 1;
    }
    ```

    **\*Good\***

    ```typescript
    const bar = "bar";
    let count: number;
    if (true) {
      console.log(bar);
      count += 1;
    }
    ```

## 4 对象

*   使用{}进行对象创建。

    **\*Bad\***

    ```typescript
    const  item  =  new  Object（）;
    ```

    **\*Good\***

    ```typescript
    const item = {};
    ```
*   在对象字面量里使用属性简写。

    **\*Bad\***

    ```typescript
    const lukeSkywalker = "Luke Skywalker";
    const obj = {
      lukeSkywalker: lukeSkywalker,
    };
    ```

    **\*Good\***

    ```typescript
    const lukeSkywalker = "Luke Skywalker";
    const obj = {
      lukeSkywalker,
    };
    ```
*   仅使用引号用于属于无效标识符的属性。

    **\*Bad\***

    ```typescript
    const bad = {
      foo: 3,
      bar: 4,
      "data-blah": 5,
    };
    ```

    **\*Good\***

    ```typescript
    const good = {
      foo: 3,
      bar: 4,
      "data-blah": 5,
    };
    ```

## 5 字符串

*   使用单引号声明字符串。

    **\*Bad\***

    ```typescript
    const bar = "bar";
    ```

    **\*Good\***

    ```typescript
    const bar = 'bar'；
    ```

## 6 解构

*   访问和使用对象的多个属性时，使用对象解构。

    **\*Bad\***

    ```typescript
    const foo = user.firstName;
    const bar = user.lastName;
    ```

    **\*Good\***

    ```typescript
    const { foo, bar } = user;
    ```
*   访问数组中的多个数据时，使用解构。

    **\*Bad\***

    ```typescript
    const arr = [1, 2, 3, 4];
    const first = arr[0];
    const second = arr[1];
    ```

    **\*Good\***

    ```typescript
    const arr = [1, 2, 3, 4];
    const [first, second] = arr;
    ```

## 7 空格

* 在定义类型前面加上空格。
* 赋值等号两边加上空格。
* 方法、类大括号前空格。
* 对象冒号后空格。

**\*Bad\***

```typescript
class Foo {
  openDetail(item: string): void {
    let foo: string;
    foo = "";
    const foa = {
      name: "foo",
    };
    console.log(item);
  }
}
```

**\*Good\***

```typescript
class Foo {
  openDetail(item: string): void {
    let foo: string;
    foo = "";
    const foa = {
      name: "foo",
    };
    console.log(item);
  }
}
```

## 8 缩进

使用两个空格缩进。

## 9 分号

语句结尾添加分号。

**\*Bad\***

```typescript
const foo = "foo";
```

**\*Good\***

```typescript
const foo = "foo";
```

## 10 数组

*   使用\[]定义数组。

    **\*Bad\***

    ```typescript
    let foos: Array<Foo>;
    ```

    **\*Good\***

    ```typescript
    let foos: Foo[];
    ```
*   使用 push 添加数据

    **\*Bad\***

    ```typescript
    const foos = [];
    foos[foos.length] = "abracadabra";
    ```

    **\*Good\***

    ```typescript
    const foos = [];
    foos.push("abracadabra");
    ```

TypeScript编码规范

[https://ths-fe.github.io/2020/05/24/TypeScript%E7%BC%96%E7%A0%81%E8%A7%84%E8%8C%83/](https://ths-fe.github.io/2020/05/24/TypeScript%E7%BC%96%E7%A0%81%E8%A7%84%E8%8C%83/)

**作者**

刘莹鑫

**发布于**

2020-05-24

**更新于**

2023-08-05

**许可协议**

[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)
