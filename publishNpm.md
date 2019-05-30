## 发布npm包

## install package
``` bash
# if your computer does not has 'vue-cli' , do it ...
npm install -g vue-cli

# we use simple vue-cli ,It is  'webpack-simple' ,so ...
vue init webpack-simple <project-name>

```
## run project
``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build
```
## set webpack
``` bash
# set webpack.config.js
entry: './src/index.js',
output: {
    path: path.resolve(__dirname, './dist'),
    publicPath: '/dist/',
    filename: '<project-name>.js',
    library : '<project-name>', 
    libraryTarget : 'umd', 
    umdNamedDefine : true, 
},
```
## set package.json
``` bash
# set package.json 
{
  "private": false,//must set false
  "main": "dist/vue-transfer-box.js",//set builded file path
}
```
## connent NPM
you must login in NPM website		
```
### login NPM 
``` bash
# if you have NPM account , you can do next step ...
# your computer npm origin is 'https://registry.npmjs.org/',You can use 'nrm' to set it.
cd <project>
npm login
npm adduser //first login npm
npm publish //Not the first publish your project , you must notice 'version' in package.json.
```

**study form [HERE](https://juejin.im/post/5c8ced235188257de6634efe)**
