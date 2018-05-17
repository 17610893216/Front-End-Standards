# 目录

- <a href='#embeddingRule'>嵌入规则</a>
- <a href='#alignIndentLine'>对齐缩进与换行</a>
- <a href='#name'>命名</a>
- <a href='#type'>类型</a>
- <a href='#object'>对象</a>
- <a href='#array'>数组</a>
- <a href='#string'>字符串</a>
- <a href='#function'>函数</a>
- <a href='#attr'>属性</a>
- <a href='#let'>变量</a>
- <a href='#expression'>条件表达式和等号</a>
- <a href='#block'>块</a>
- <a href='#notes'>注释</a>
- <a href='#whitespace'>空白</a>
- <a href='#commas'>逗号</a>
- <a href='#semicolons'>分号</a>
- <a href='#type-coercion'>类型转换</a>
- <a href='#naming-conventions'>命名约定</a>
- <a href='#accessors'>存取器</a>
- <a href='#constructors'>构造器</a>
- <a href='#events'>事件</a>
- <a href='#modules'>模块</a>
- <a href='#jquery'>jQuery</a>

# <a id='embeddingRule'>嵌入规则</a>

Javascript程序应该尽量放在.js的文件中，需要调用的时候在页面中以```<script src="filename.js">```的形式包含进来。Javascript代码若不是该页面专用的，则应尽量避免在页面中直接编写Javascript代码。

# <a id='alignIndentLine'>对齐缩进与换行</a>

- 缩进
    - 在同一系统中应采用同一种缩进标准，本文提倡缩进大小为4个空格。各编译器对Tab键所代替的空白大小定义不同。建议在设置开发环境时，将编辑器里的Tab快捷键重新设置成4个空格。多数编译器提供了此功能。否则建议按4次空格来进行缩进。
- 换行
    - > 在以下位置必须换行：
    - 每个独立语句结束后；
    - if、else、catch、finally、while等关键字前；
    - 运算符处换行时，运算符必须在新行的行首。 
    - 对于因为单行长度超过限制时产生的换行，参考行长度中的策略进行分隔。
1. 字符串过长截断

每行代码应小于80个字符。若代码较长应尽量换行，换行应选择在操作符和标点符号之后，最好是在分号“;”或逗号“,”之后。下一行代码相对上一行缩进4个空格。这样可以有效防止复制粘贴引起的代码缺失等错误并增强可读性。

2. 三元运算符过长

三元运算符由3部分组成，因此其换行应当根据每个部分的长度不同，形成3种不同的情况：
```javascript
<script>
    // good
    // 无需换行
    let result = condition ? resultA : resultB;
    // 条件超长的情况
    let result = thisIsAVeryVeryLongCondition ? resultA : resultB;
    //  结果分支超长的情况
    let result = condition
        ? thisIsAVeryVeryLongCondition
        :resultB;
    let result = condition
        ? resultA
        : thisIsAVeryVeryLongCondition;
</script>
```
不得出现以下情况：
```javascript
<script>
    // 最后一个结果很长，但不建议合并条件和第一个分支
    // bad
    let result = condition ? resultA
        : thisIsAVeryVeryLongCondition;
</script>
```
3. 过长的逻辑条件组合

当因为较复杂的逻辑条件组合导致80个字符无法满足需求时，应当将每个条件独立一行，逻辑运算符放置在行首进行分隔，或将部分逻辑按逻辑组合进行分隔。最终将右括号)与左大括号{放在独立一行，保证与if内语句块能容易视觉辨识。如：

```javascript
<script>
    // 注意逻辑运算符前的缩进
    if (user.isAuthenticated()
        && user.isInRole('admin')
        && user.hasAuthority('add-admin')
        || user.hasAuthority('delete-admin')
    ) {
        // code
    }
</script>
```
4. 过长的JSON和数组

如果对象属性较多导致每个属性一行占用空间过大，可以按语义或逻辑进行分组的组织，如：
```javascript
<script>
    // 引文-数字的映射
    let mapping = {
        one: 1, two: 2, three: 3, four: 4, five: 5,
        six: 6, seven: 7, eight:8, nine: 9, ten: 10,
        eleven: 11
    }
</script>
```
通过5个一组的分组，将每一行控制在合理的范围内，并且按逻辑进行了切分。 对于项目较多的数组，也可以采用相同的方法

5. return语句

return如果用表达式的执行作为返回值，请把表达式和 return 放在同一行中，以免换行符被误解析为语句的结束而引起返回错误。return 关键字后若没有返回表达式，则返回 undefined。构造器的默认返回值为 this。

# <a id='name'>命名</a>
> 命名的方法通常有以下几类：

1. 命名法说明
    - 1).camel命名法，形如thisIsAnApple 
    - 2).pascal命名法，形如ThisIsAnApple
    - 3).下划线命名法，形如this_is_an_apple · 
    - 4).中划线命名法，形如this-is-an-apple 
    > 根据不同类型的内容，必须严格采用如下的命名法：

2. 变量名：必须使用camel命名法
3. 参数名：必须使用camel命名法 
4. 函数名：必须使用camel命名法
5. 方法/属性：必须使用camel命名法
6. 私有（保护）成员：必须以下划线_开头
7. 常量名：必须使用pascal命名法
8. 类名：必须使用pascal命名法
9. 枚举名：必须使用pascal命名法 
10. 枚举的属性：必须使用全部大写的下划线命名法
11. 命名空间：必须使用camel命名法 
12. 语义：命名同时还需要关注语义，如： 
    - 变量名应当使用名词
    - boolean类型的应当使用is、has等起头，表示其类型
    - 函数名应当用动宾短语
    - 类名应当用名词

# <a id='type'>类型</a>

- 原始值: 相当于传值
    - string
    - number
    - boolean
    - null
    - undefined

```javascript
<script>
    let foo = 1,
        bar = foo;
    bar = 9;
console.log(foo, bar); // => 1, 9
</script>
```

- 复杂类型: 相当于传引用
    - object
    - array
    - function

```javascript
<script>
    let foo = [1, 2],
        bar = foo;
    bar[0] = 9;
    console.log(foo[0], bar[0]); // => 9, 9
</script>
```

# <a id='object'>对象</a>

- 使用字面值创建对象

```javascript
<script>
// bad
let item = new Object();

// good
let item = {};
</script>
```

- 不要使用保留字 reserved words 作为键

```javascript
<script>
// bad
let superman = {
  class: 'superhero',
  default: { clark: 'kent' },
  private: true
};

// good
let superman = {
  klass: 'superhero',
  defaults: { clark: 'kent' },
  hidden: true
};
</script>
```

# <a id='array'>数组</a>

- 使用字面值创建数组

```javascript
<script>
// bad
let items = new Array();

// good
let items = [];
</script>
```

- 如果你不知道数组的长度，使用push

```javascript
<script>
let someStack = [];

// bad
someStack[someStack.length] = 'abracadabra';

// good
someStack.push('abracadabra');
</script>
```

- 当你需要拷贝数组时使用slice

```javascript
<script>
let len = items.length,
    itemsCopy = [],
    i;

// bad
for (i = 0; i < len; i++) {
  itemsCopy[i] = items[i];
}

// good
itemsCopy = items.slice();
</script>
```

- 使用slice将类数组的对象转成数组

```javascript
<script>
function trigger() {
  let args = Array.prototype.slice.call(arguments);
  ...
}
</script>
```

# <a id='string'>字符串</a>

- 对字符串使用单引号 ''

```javascript
<script>
// bad
let name = "Bob Parr";

// good
let name = 'Bob Parr';

// bad
let fullName = "Bob " + this.lastName;

// good
let fullName = 'Bob ' + this.lastName;
</script>
```

- 超过80个字符的字符串应该使用字符串连接换行
- 注: 如果过度使用，长字符串连接可能会对性能有影响

```javascript
<script>
// bad
let errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';

// bad
let errorMessage = 'This is a super long error that \
was thrown because of Batman. \
When you stop to think about \
how Batman had anything to do \
with this, you would get nowhere \
fast.';


// good
let errorMessage = 'This is a super long error that ' +
  'was thrown because of Batman.' +
  'When you stop to think about ' +
  'how Batman had anything to do ' +
  'with this, you would get nowhere ' +
  'fast.';
</script>
```

- 编程时使用join而不是字符串连接来构建字符串，特别是IE

```javascript
<script>
let items,
    messages,
    length, i;

messages = [{
    state: 'success',
    message: 'This one worked.'
},{
    state: 'success',
    message: 'This one worked as well.'
},{
    state: 'error',
    message: 'This one did not work.'
}];

length = messages.length;

// bad
function inbox(messages) {
  items = '<ul>';

  for (i = 0; i < length; i++) {
    items += '<li>' + messages[i].message + '</li>';
  }

  return items + '</ul>';
}

// good
function inbox(messages) {
  items = [];

  for (i = 0; i < length; i++) {
    items[i] = messages[i].message;
  }

  return '<ul><li>' + items.join('</li><li>') + '</li></ul>';
}
</script>
```

# <a id='function'>函数</a>

- 函数表达式:

```javascript
<script>
// 匿名函数表达式
let anonymous = function() {
  return true;
};

// 有名函数表达式
let named = function named() {
  return true;
};

// 立即调用函数表达式
(function() {
  console.log('Welcome to the Internet. Please follow me.');
})();

</script>
```

- 绝对不要在一个非函数块里声明一个函数，把那个函数赋给一个变量。浏览器允许你这么做，但是它们解析不同。
- 注: ECMA-262定义把块定义为一组语句，函数声明不是一个语句.

```javascript
<script>
// bad
if (currentUser) {
  function test() {
    console.log('Nope.');
  }
}

// good
if (currentUser) {
  let test = function test() {
    console.log('Yup.');
  };
}

</script>
```

- 绝对不要把参数命名为 arguments, 这将会逾越函数作用域内传过来的 arguments 对象.

```javascript
<script>
// bad
function nope(name, options, arguments) {
  // ...stuff...
}

// good
function yup(name, options, args) {
  // ...stuff...
}
</script>
```

# <a id='attr'>属性</a>

- 当使用变量访问属性时使用中括号.

```javascript
<script>
let luke = {
  jedi: true,
  age: 28
};

function getProp(prop) {
  return luke[prop];
}

let isJedi = getProp('jedi');
</script>
```

# <a id='let'>变量</a>

- 总是使用 let 来声明变量，如果不这么做将导致产生全局变量，我们要避免污染全局命名空间。

```javascript
<script>
// bad
superPower = new SuperPower();

// good
let superPower = new SuperPower();
</script>
```

- 使用一个 let 以及新行声明多个变量，缩进4个空格。

```javascript
<script>
// bad
let items = getItems();
let goSportsTeam = true;
let dragonball = 'z';

// good
let items = getItems(),
    goSportsTeam = true,
    dragonball = 'z';
</script>
```

- 最后再声明未赋值的变量，当你想引用之前已赋值变量的时候很有用。

```javascript
<script>
// bad
let i, len, dragonball,
    items = getItems(),
    goSportsTeam = true;

// bad
let i, items = getItems(),
    dragonball,
    goSportsTeam = true,
    len;

// good
let items = getItems(),
    goSportsTeam = true,
    dragonball,
    length,
    i;

</script>
```

- 在作用域顶部声明变量，避免变量声明和赋值引起的相关问题。

```javascript
<script>
// bad
function() {
  test();
  console.log('doing stuff..');

  //..other stuff..

  let name = getName();

  if (name === 'test') {
    return false;
  }

  return name;
}

// good
function() {
  let name = getName();

  test();
  console.log('doing stuff..');

  //..other stuff..

  if (name === 'test') {
    return false;
  }

  return name;
}

// bad
function() {
  let name = getName();

  if (!arguments.length) {
    return false;
  }

  return true;
}

// good
function() {
  if (!arguments.length) {
    return false;
  }

  let name = getName();

  return true;
}
</script>
```

# <a id='expression'>条件表达式和等号</a>

- 适当使用 === 和 !== 以及 == 和 !=
- 条件表达式的强制类型转换遵循以下规则：
    - 对象 被计算为 true
    - Undefined 被计算为 false
    - Null 被计算为 false
    - 布尔值 被计算为 布尔的值
    - 数字 如果是 +0, -0, or NaN 被计算为 false , 否则为 true
    - 字符串 如果是空字符串 '' 则被计算为 false, 否则为 true

    ```javascript
    <script>
        if ([0]) {
        // true
        // An array is an object, objects evaluate to true
        }
    </script>
    ```

- 使用快捷方式

```javascript
<script>
// bad
if (name !== '') {
  // ...stuff...
}

// good
if (name) {
  // ...stuff...
}

// bad
if (collection.length > 0) {
  // ...stuff...
}

// good
if (collection.length) {
  // ...stuff...
}
</script>
```

# <a id='block'>块</a>

- 给所有多行的块使用大括号

```javascript
<script>
// bad
if (test)
  return false;

// good
if (test) return false;

// good
if (test) {
  return false;
}

// bad
function() { return false; }

// good
function() {
  return false;
}
</script>
```

# <a id='notes'>注释</a>

> 注释要尽量简单，清晰明了。着重注释的意思，对不太直观的部分进行注解

> JavaScript 的注释有两种"//" 和"/* .... */"

- 建议"//"用作代码行注释
- "/* .... */"形式用作对整个代码段的注销，或较正式的声明中，如函数参数、功能、文件功能等的描述中
- >另：复制粘贴应注意注释是否与代码对应。

- 使用 /** ... */ 进行多行注释，包括描述，指定类型以及参数值和返回值

```javascript
<script>
// bad
// make() returns a new element
// based on the passed in tag name
//
// @param <String> tag
// @return <Element> element
function make(tag) {

  // ...stuff...

  return element;
}

// good
/**
 * make() returns a new element
 * based on the passed in tag name
 *
 * @param <String> tag
 * @return <Element> element
 */
function make(tag) {

  // ...stuff...

  return element;
}
</script>
```

- 使用 // 进行单行注释，在评论对象的上面进行单行注释，注释前放一个空行.

```javascript
<script>
// bad
let active = true;  // is current tab

// good
// is current tab
let active = true;

// bad
function getType() {
  console.log('fetching type...');
  // set the default type to 'no type'
  let type = this._type || 'no type';

  return type;
}

// good
function getType() {
  console.log('fetching type...');

  // set the default type to 'no type'
  let type = this._type || 'no type';

  return type;
}
</script>
```

- 如果你有一个问题需要重新来看一下或如果你建议一个需要被实现的解决方法的话需要在你的注释前面加上 FIXME 或 TODO 帮助其他人迅速理解

```javascript
<script>
function Calculator() {

  // FIXME: shouldn't use a global here
  total = 0;

  return this;
}

function Calculator() {

  // TODO: total should be configurable by an options param
  this.total = 0;

  return this;
}
</script>
```

# <a id='whitespace'>空白</a>

- 将tab设为4个空格

  ```javascript
  // bad
  function() {
  ∙∙let name;
  }

  // bad
  function() {
  ∙let name;
  }

  // good
  function() {
  ∙∙∙∙let name;
  }
  ```

- 大括号前放一个空格

  ```javascript
  // bad
  function test(){
    console.log('test');
  }

  // good
  function test() {
    console.log('test');
  }

  // bad
  dog.set('attr',{
    age: '1 year',
    breed: 'Bernese Mountain Dog'
  });

  // good
  dog.set('attr', {
    age: '1 year',
    breed: 'Bernese Mountain Dog'
  });
  ```

- 在做长方法链时使用缩进.

  ```javascript
  // bad
  $('#items').find('.selected').highlight().end().find('.open').updateCount();

  // good
  $('#items')
    .find('.selected')
      .highlight()
      .end()
    .find('.open')
      .updateCount();

  // bad
  let leds = stage.selectAll('.led').data(data).enter().append('svg:svg').class('led', true)
      .attr('width',  (radius + margin) * 2).append('svg:g')
      .attr('transform', 'translate(' + (radius + margin) + ',' + (radius + margin) + ')')
      .call(tron.led);

  // good
  let leds = stage.selectAll('.led')
      .data(data)
    .enter().append('svg:svg')
      .class('led', true)
      .attr('width',  (radius + margin) * 2)
    .append('svg:g')
      .attr('transform', 'translate(' + (radius + margin) + ',' + (radius + margin) + ')')
      .call(tron.led);
  ```

# <a id='commas'>逗号</a>

- 不要将逗号放前面

  ```javascript
  // bad
  let once
    , upon
    , aTime;

  // good
  let once,
      upon,
      aTime;

  // bad
  let hero = {
      firstName: 'Bob'
    , lastName: 'Parr'
    , heroName: 'Mr. Incredible'
    , superPower: 'strength'
  };

  // good
  let hero = {
    firstName: 'Bob',
    lastName: 'Parr',
    heroName: 'Mr. Incredible',
    superPower: 'strength'
  };
  ```

- 不要加多余的逗号，这可能会在IE下引起错误，同时如果多一个逗号某些ES3的实现会计算多数组的长度。

  ```javascript
  // bad
  let hero = {
    firstName: 'Kevin',
    lastName: 'Flynn',
  };

  let heroes = [
    'Batman',
    'Superman',
  ];

  // good
  let hero = {
    firstName: 'Kevin',
    lastName: 'Flynn'
  };

  let heroes = [
    'Batman',
    'Superman'
  ];
  ```

# <a id='semicolons'>分号</a>

- 语句结束一定要加分号

  ```javascript
  // bad
  (function() {
    let name = 'Skywalker'
    return name
  })()

  // good
  (function() {
    let name = 'Skywalker';
    return name;
  })();

  // good
  ;(function() {
    let name = 'Skywalker';
    return name;
  })();
  ```

# <a id='type-coercion'>类型转换</a>

- 在语句的开始执行类型转换.
- 字符串:

  ```javascript
  //  => this.reviewScore = 9;

  // bad
  let totalScore = this.reviewScore + '';

  // good
  let totalScore = '' + this.reviewScore;

  // bad
  let totalScore = '' + this.reviewScore + ' total score';

  // good
  let totalScore = this.reviewScore + ' total score';
  ```

- 对数字使用 `parseInt` 并且总是带上类型转换的基数.

  ```javascript
  let inputValue = '4';

  // bad
  let val = new Number(inputValue);

  // bad
  let val = +inputValue;

  // bad
  let val = inputValue >> 0;

  // bad
  let val = parseInt(inputValue);

  // good
  let val = Number(inputValue);

  // good
  let val = parseInt(inputValue, 10);

  // good
  /**
   * parseInt was the reason my code was slow.
   * Bitshifting the String to coerce it to a
   * Number made it a lot faster.
   */
  let val = inputValue >> 0;
  ```

- 布尔值:

  ```javascript
  let age = 0;

  // bad
  let hasAge = new Boolean(age);

  // good
  let hasAge = Boolean(age);

  // good
  let hasAge = !!age;
  ```

# <a id='naming-conventions'>命名约定</a>

- 避免单个字符名，让你的变量名有描述意义。

  ```javascript
  // bad
  function q() {
    // ...stuff...
  }

  // good
  function query() {
    // ..stuff..
  }
  ```

- 当命名对象、函数和实例时使用驼峰命名规则

  ```javascript
  // bad
  let OBJEcttsssss = {};
  let this_is_my_object = {};
  let this-is-my-object = {};
  function c() {};
  let u = new user({
    name: 'Bob Parr'
  });

  // good
  let thisIsMyObject = {};
  function thisIsMyFunction() {};
  let user = new User({
    name: 'Bob Parr'
  });
  ```

- 当命名构造函数或类时使用驼峰式大写

  ```javascript
  // bad
  function user(options) {
    this.name = options.name;
  }

  let bad = new user({
    name: 'nope'
  });

  // good
  function User(options) {
    this.name = options.name;
  }

  let good = new User({
    name: 'yup'
  });
  ```

- 命名私有属性时前面加个下划线 `_`

  ```javascript
  // bad
  this.__firstName__ = 'Panda';
  this.firstName_ = 'Panda';

  // good
  this._firstName = 'Panda';
  ```

- 当保存对 `this` 的引用时使用 `_this`.

  ```javascript
  // bad
  function() {
    let self = this;
    return function() {
      console.log(self);
    };
  }

  // bad
  function() {
    let that = this;
    return function() {
      console.log(that);
    };
  }

  // good
  function() {
    let _this = this;
    return function() {
      console.log(_this);
    };
  }
  ```

# <a id='accessors'>存取器</a>

- 属性的存取器函数不是必需的
- 如果你确实有存取器函数的话使用getVal() 和 setVal('hello')

  ```javascript
  // bad
  dragon.age();

  // good
  dragon.getAge();

  // bad
  dragon.age(25);

  // good
  dragon.setAge(25);
  ```

- 如果属性是布尔值，使用isVal() 或 hasVal()

  ```javascript
  // bad
  if (!dragon.age()) {
    return false;
  }

  // good
  if (!dragon.hasAge()) {
    return false;
  }
  ```

- 可以创建get()和set()函数，但是要保持一致

  ```javascript
  function Jedi(options) {
    options || (options = {});
    let lightsaber = options.lightsaber || 'blue';
    this.set('lightsaber', lightsaber);
  }

  Jedi.prototype.set = function(key, val) {
    this[key] = val;
  };

  Jedi.prototype.get = function(key) {
    return this[key];
  };
  ```

# <a id='constructors'>构造器</a>

- 给对象原型分配方法，而不是用一个新的对象覆盖原型，覆盖原型会使继承出现问题。

  ```javascript
  function Jedi() {
    console.log('new jedi');
  }

  // bad
  Jedi.prototype = {
    fight: function fight() {
      console.log('fighting');
    },

    block: function block() {
      console.log('blocking');
    }
  };

  // good
  Jedi.prototype.fight = function fight() {
    console.log('fighting');
  };

  Jedi.prototype.block = function block() {
    console.log('blocking');
  };
  ```

- 方法可以返回 `this` 帮助方法可链。

  ```javascript
  // bad
  Jedi.prototype.jump = function() {
    this.jumping = true;
    return true;
  };

  Jedi.prototype.setHeight = function(height) {
    this.height = height;
  };

  let luke = new Jedi();
  luke.jump(); // => true
  luke.setHeight(20) // => undefined

  // good
  Jedi.prototype.jump = function() {
    this.jumping = true;
    return this;
  };

  Jedi.prototype.setHeight = function(height) {
    this.height = height;
    return this;
  };

  let luke = new Jedi();

  luke.jump()
    .setHeight(20);
  ```

- 可以写一个自定义的toString()方法，但是确保它工作正常并且不会有副作用。

  ```javascript
  function Jedi(options) {
    options || (options = {});
    this.name = options.name || 'no name';
  }

  Jedi.prototype.getName = function getName() {
    return this.name;
  };

  Jedi.prototype.toString = function toString() {
    return 'Jedi - ' + this.getName();
  };
  ```

# <a id='events'>事件</a>

- 当给事件附加数据时，传入一个哈希而不是原始值，这可以让后面的贡献者加入更多数据到事件数据里而不用找出并更新那个事件的事件处理器

  ```js
  // bad
  $(this).trigger('listingUpdated', listing.id);

  ...

  $(this).on('listingUpdated', function(e, listingId) {
    // do something with listingId
  });
  ```

  更好:

  ```js
  // good
  $(this).trigger('listingUpdated', { listingId : listing.id });

  ...

  $(this).on('listingUpdated', function(e, data) {
    // do something with data.listingId
  });
  ```

# <a id='modules'>模块</a>

- 模块应该以 `!` 开始，这保证了如果一个有问题的模块忘记包含最后的分号在合并后不会出现错误
- 这个文件应该以驼峰命名，并在同名文件夹下，同时导出的时候名字一致
- 加入一个名为noConflict()的方法来设置导出的模块为之前的版本并返回它
- 总是在模块顶部声明 `'use strict';`

  ```javascript
  // fancyInput/fancyInput.js

  !function(global) {
    'use strict';

    let previousFancyInput = global.FancyInput;

    function FancyInput(options) {
      this.options = options || {};
    }

    FancyInput.noConflict = function noConflict() {
      global.FancyInput = previousFancyInput;
      return FancyInput;
    };

    global.FancyInput = FancyInput;
  }(this);
  ```
  
# <a id='jquery'>jQuery</a>

- 缓存jQuery查询

  ```javascript
  // bad
  function setSidebar() {
    $('.sidebar').hide();

    // ...stuff...

    $('.sidebar').css({
      'background-color': 'pink'
    });
  }

  // good
  function setSidebar() {
    let $sidebar = $('.sidebar');
    $sidebar.hide();

    // ...stuff...

    $sidebar.css({
      'background-color': 'pink'
    });
  }
  ```

- 对DOM查询使用级联的 `$('.sidebar ul')` 或 `$('.sidebar ul')`，[jsPerf](http://jsperf.com/jquery-find-vs-context-sel/16)
- 对有作用域的jQuery对象查询使用 `find`

  ```javascript
  // bad
  $('.sidebar', 'ul').hide();

  // bad
  $('.sidebar').find('ul').hide();

  // good
  $('.sidebar ul').hide();

  // good
  $('.sidebar > ul').hide();

  // good (slower)
  $sidebar.find('ul');

  // good (faster)
  $($sidebar[0]).find('ul');
  ```
