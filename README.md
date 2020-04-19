<p align="center">
  <img src="logo.png" alt="logo">
</p>

<p align="center">
  <img alt="Version" src="https://img.shields.io/npm/v/express-safe-async.svg">
  <img alt="travis" src="https://travis-ci.org/techbless/express-safe-async.svg?branch=master" />
  <img alt="Documentation" src="https://img.shields.io/badge/documentation-yes-brightgreen.svg" />
  <img alt="Maintenance" src="https://img.shields.io/badge/Maintained%3F-yes-green.svg" />
  <img alt="License: MIT" src="https://img.shields.io/github/license/techbless/express-safe-async" />
</p>

> Elegant async error handler with Decorator for async router function(controller) in express   

If you use `async` method for route handler and middleware, There must be some problem. When some error occured in `async` method, express can't handle your errors. So you should deal with it yourself. It is a pretty annoying task to handle this.   

This library provides a simple and elegant decorator `@AsyncHandled` to handle these errors from `async` method. this decorator handles occured errors from `async` method and bind `this` automatically.   

```
Nothing needs your attention anymore.
```

### 🏠 [Homepage](https://github.com/techbless/express-safe-async)

## Install

**Highly Recommend to use higher version than v2.0.1, If you are using lower version, You should update it.**

```sh
npm install express-safe-async
```

## Import

TypeScript
```typescript
import AsyncHandled, { safe } from 'express-safe-async';
```

JavaScript
```javascript
const safe = require('express-safe-async').safe;
```

## Usage

To use Decorator, Make sure the below line is in your tsconfig.json

**tsconfig.json**
```json
{
    "compilerOptions": {
        "target": "ES5",
        "experimentalDecorators": true
    }
}
```

**or**

```sh
tsc --target ES5 --experimentalDecorators
```

### Using Class Method

Just write `@AsyncHandled` on your async methods.

```typescript
import * as express from 'express';
import AsyncHandled from 'express-safe-async';

class ExampleController {
  @AsyncHandled // <- This is all you should do.
  public async asyncMethod(req: express.Request, res: express.Response) {
    // Your stuff here
    ...
  }
}

const app = express();
const example = new ExampleController();

app.get('/example', example.asyncMethod);
app.listen(PORT, (err) => {
  ...
});
```

### Not Using Class Method

Wrap your functions with `safe()` like below.

```typescript
import * as express from 'express';
import { safe } from 'express-safe-async';

const app = express();

app.use(safe( // <- This is all you should do
  async () => {
    // Your middleware here
    ...
  }
));

app.get('/example', safe( // <- This is all you should do
  async (req: express.Request, res: express.Response) => {
    // Your route handler here
    ...
  }
));

app.listen(1234, (err) => {
  ...
});
```

## Run tests when you contribute

```sh
npm run test
```

## Author

👤 **Yunbin Chang**

* Website: https://techbless.github.io
* Github: [@techbless](https://github.com/techbless)

## 🤝 Contributing

Contributions, issues and feature requests are welcome!<br />Feel free to check [issues page](https://github.com/techbless/express-safe-async/issues). You can also take a look at the [contributing guide](https://github.com/techbless/express-safe-async/blob/master/CONTRIBUTING.md).

## Show your support

Give a ⭐️ if this project helped you!

## 📝 License

Copyright © 2020 [Yunbin Chang](https://github.com/techbless).<br />
This project is [MIT](https://github.com/techbless/express-safe-async/blob/master/LICENSE) licensed.
