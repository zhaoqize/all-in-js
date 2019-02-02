## 使用有意义的变量命名（Use searchable names）

Bad:
```js
// What the heck is 86400000 for?
setTimeout(blastOff, 86400000);
```

Good:
```js
// Declare them as capitalized named constants.
const MILLISECONDS_IN_A_DAY = 86400000;

setTimeout(blastOff, MILLISECONDS_IN_A_DAY);
```

## 使用有解释性的变量（Use explanatory variables）

Bad:
```js
const address = 'One Infinite Loop, Cupertino 95014';
const cityZipCodeRegex = /^[^,\\]+[,\\\s]+(.+?)\s*(\d{5})?$/;
saveCityZipCode(address.match(cityZipCodeRegex)[1], address.match(cityZipCodeRegex)[2]);
```

Good:
```js
const address = 'One Infinite Loop, Cupertino 95014';
const cityZipCodeRegex = /^[^,\\]+[,\\\s]+(.+?)\s*(\d{5})?$/;
const [, city, zipCode] = address.match(cityZipCodeRegex) || [];
saveCityZipCode(city, zipCode);
```

## 使用默认参数而不是短路或条件语法（Use default arguments instead of short circuiting or conditionals）

Bad:
```js
function createMicrobrewery(name) {
  const breweryName = name || 'Hipster Brew Co.';
  // ...
}
```

Good:
```js
function createMicrobrewery(name = 'Hipster Brew Co.') {
  // ...
}
```

## 函数参数不要超过2个（Function arguments (2 or fewer ideally)）

Bad:
```js
function createMenu(title, body, buttonText, cancellable) {
  // ...
}
```

Good:
```js
function createMenu({ title, body, buttonText, cancellable }) {
  // ...
}

createMenu({
  title: 'Foo',
  body: 'Bar',
  buttonText: 'Baz',
  cancellable: true
});
```

## 函数应该职责单一（Functions should do one thing）

Bad:
```js
function emailClients(clients) {
  clients.forEach((client) => {
    const clientRecord = database.lookup(client);
    if (clientRecord.isActive()) {
      email(client);
    }
  });
}
```

Good:
```js
function emailActiveClients(clients) {
  clients
    .filter(isActiveClient)
    .forEach(email);
}

function isActiveClient(client) {
  const clientRecord = database.lookup(client);
  return clientRecord.isActive();
}
```

## 使用 Object.assign 设置对象（Set default objects with Object.assign）

Bad:
```js
const menuConfig = {
  title: null,
  body: 'Bar',
  buttonText: null,
  cancellable: true
};

function createMenu(config) {
  config.title = config.title || 'Foo';
  config.body = config.body || 'Bar';
  config.buttonText = config.buttonText || 'Baz';
  config.cancellable = config.cancellable !== undefined ? config.cancellable : true;
}

createMenu(menuConfig);
```

Good:
```js
const menuConfig = {
  title: 'Order',
  // User did not include 'body' key
  buttonText: 'Send',
  cancellable: true
};

function createMenu(config) {
  config = Object.assign({
    title: 'Foo',
    body: 'Bar',
    buttonText: 'Baz',
    cancellable: true
  }, config);

  // config now equals: {title: "Order", body: "Bar", buttonText: "Send", cancellable: true}
  // ...
}

createMenu(menuConfig);
```

## 避免进行会产生副作用的操作（Avoid Side Effects）
> 避免引用值的混乱，一个好用的库[immutable-js](https://facebook.github.io/immutable-js/)

Bad:
```js
const addItemToCart = (cart, item) => {
  cart.push({ item, date: Date.now() });
};
```

Good:
```js
const addItemToCart = (cart, item) => {
  return [...cart, { item, date: Date.now() }];
};
```

## 善用函数式编程而不是命令式编程（Favor functional programming over imperative programming）

Bad:
```js
const programmerOutput = [
  {
    name: 'Uncle Bobby',
    linesOfCode: 500
  }, {
    name: 'Suzie Q',
    linesOfCode: 1500
  }, {
    name: 'Jimmy Gosling',
    linesOfCode: 150
  }, {
    name: 'Gracie Hopper',
    linesOfCode: 1000
  }
];

let totalOutput = 0;

for (let i = 0; i < programmerOutput.length; i++) {
  totalOutput += programmerOutput[i].linesOfCode;
}
```

Good:
```js
const programmerOutput = [
  {
    name: 'Uncle Bobby',
    linesOfCode: 500
  }, {
    name: 'Suzie Q',
    linesOfCode: 1500
  }, {
    name: 'Jimmy Gosling',
    linesOfCode: 150
  }, {
    name: 'Gracie Hopper',
    linesOfCode: 1000
  }
];

const totalOutput = programmerOutput
  .reduce((totalLines, output) => totalLines + output.linesOfCode, 0)
```

## 避免使用否定条件（Avoid negative conditionals）

Bad:
```js
function isDOMNodeNotPresent(node) {
  // ...
}

if (!isDOMNodeNotPresent(node)) {
  // ...
}
```

Good:
```js
function isDOMNodePresent(node) {
  // ...
}

if (isDOMNodePresent(node)) {
  // ...
}
```

## 避免使用多条件（Avoid conditionals）
> 当你看到这项优化的时候可能有点懵逼，心里想，‘老哥，你逗呢？’。没有if，还怎么写流程语句。答案是，你可以使用多态来实现。为什么要这么做？因为函数尽量职责单一，一个函数只做一件事。

Bad:
```js
class Airplane {
  // ...
  getCruisingAltitude() {
    switch (this.type) {
      case '777':
        return this.getMaxAltitude() - this.getPassengerCount();
      case 'Air Force One':
        return this.getMaxAltitude();
      case 'Cessna':
        return this.getMaxAltitude() - this.getFuelExpenditure();
    }
  }
}
```

Good:
```js
class Airplane {
  // ...
}

class Boeing777 extends Airplane {
  // ...
  getCruisingAltitude() {
    return this.getMaxAltitude() - this.getPassengerCount();
  }
}

class AirForceOne extends Airplane {
  // ...
  getCruisingAltitude() {
    return this.getMaxAltitude();
  }
}

class Cessna extends Airplane {
  // ...
  getCruisingAltitude() {
    return this.getMaxAltitude() - this.getFuelExpenditure();
  }
}
```

## 尽量使用get与set模式思维（Use getters and setters）

Bad:
```js
function makeBankAccount() {
  // ...

  return {
    balance: 0,
    // ...
  };
}

const account = makeBankAccount();
account.balance = 100;
```

Good:
```js
function makeBankAccount() {
  // this one is private
  let balance = 0;

  // a "getter", made public via the returned object below
  function getBalance() {
    return balance;
  }

  // a "setter", made public via the returned object below
  function setBalance(amount) {
    // ... validate before updating the balance
    balance = amount;
  }

  return {
    // ...
    getBalance,
    setBalance,
  };
}

const account = makeBankAccount();
account.setBalance(100);
```

## 仅在逻辑复杂的地方写上备注（Only comment things that have business logic complexity.）

Bad:
```js
function hashIt(data) {
  // The hash
  let hash = 0;

  // Length of string
  const length = data.length;

  // Loop through every character in data
  for (let i = 0; i < length; i++) {
    // Get character code.
    const char = data.charCodeAt(i);
    // Make the hash
    hash = ((hash << 5) - hash) + char;
    // Convert to 32-bit integer
    hash &= hash;
  }
}
```

Good:
```js
function hashIt(data) {
  let hash = 0;
  const length = data.length;

  for (let i = 0; i < length; i++) {
    const char = data.charCodeAt(i);
    hash = ((hash << 5) - hash) + char;

    // Convert to 32-bit integer
    hash &= hash;
  }
}
```


## 参考&拓展
- [clean-code-javascript](https://github.com/ryanmcdermott/clean-code-javascript)
- [clean-code-linters](https://github.com/collections/clean-code-linters)
- [standard](https://github.com/standard/standard/blob/master/docs/README-zhcn.md)
- [HTMLHint](https://github.com/htmlhint/HTMLHint)
- [csslint](https://github.com/CSSLint/csslint)
- [jshint](https://github.com/jshint/jshint)