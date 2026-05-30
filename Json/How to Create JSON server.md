#### Install JSON in your project.

```
npm install json-server
```
[JSON Website](https://www.npmjs.com/package/json-server)

#### `package.json` File Structure

- Add custom `script` to run JSON server
```json
{
"scripts": {
    "server": "json-server --watch src/jobs.json --port 8000"
  },
}
```
`src/jobs.json` file location. `--port 8000` its localhost port.

#### Run JSON Server

- Open the Terminal of your code editor
```
npm run serve
```