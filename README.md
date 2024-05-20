这是一个基于 node 的 puppeter 环境，用于构建带 puppeter 环境的应用，以下是一个可使用参考 Dockerfile 文件，如果这里的 puppeter 无法安装下载，可以通过 ENV 配置代理使其可安装，需要注意的时，设置 ENV 代理后，需要清除。

```
FROM webape/puppeter:latest

WORKDIR /app

COPY package.json ./

# RUN npm config set registry 'https://registry.npmmirror.com/'
RUN npm install

COPY src /app/src
COPY http.js /app/http.js
COPY webpack.config.js /app/webpack.config.js
RUN npx webpack

EXPOSE 8000

CMD ["npm", "run", "main"]

```

以下是 package.json 的文件示例

```
{
  "dependencies": {
    "body-parser": "^1.20.2",
    "express": "^4.18.3",
    "multer": "^1.4.5-lts.1",
    "puppeteer": "^22.1.0",
    "qs": "^6.12.0",
    "socks-proxy-agent": "^8.0.2"
  },
  "name": "ceshi-proxy",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "main": "npx webpack && node http.js"
  },
  "type": "module",
  "author": "",
  "license": "ISC",
  "description": "",
  "devDependencies": {
    "@babel/core": "^7.24.4",
    "@babel/node": "^7.23.9",
    "@babel/preset-env": "^7.24.4",
    "axios": "^1.6.8",
    "babel-loader": "^9.1.3",
    "crypto-js": "^4.2.0",
    "gm": "^1.25.0",
    "memory-fs": "^0.5.0",
    "request": "^2.88.2",
    "tesseract.js": "^5.0.5",
    "tesseractocr": "^2.0.3",
    "vue": "^2.7.14",
    "vuex": "^3.6.2",
    "webpack": "^5.91.0",
    "webpack-cli": "^5.1.4"
  }
}

```
