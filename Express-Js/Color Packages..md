you can set color on terminal using color package.

1. Install Colors library.

```
npm install colors
```

2. How to use in http request.
    - `logger` page structure.

```js
import colors from "colors";
  
const logger = (req, res, next) => {
  const methodColor = {
    GET: 'green',
    POST: 'blue',
    PUT: 'yellow',
    DELETE: 'red',
  }
  const color = methodColor[req.method] || white;

  console.log(
    `${req.method} ${req.protocol}://${req.get("host")}${req.originalUrl}`[color]
  );
  next();
};

export default logger;
```