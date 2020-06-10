### 框架说明
#### 架构： npm/npx + capacitor + vue
本框架是native开发版本，可打包生成apk，建议 Android Studios 4.0 版本
本机 node = v10.15.3， npm = 6.9.0
#### 以下是框架的构建方式（vue/react/angular等框架基本相同）
1. 构建完框架后，先安装capacitor
```
npm install --save @capacitor/core @capacitor/cli
```
2. 然后初始化 capacitor，App name 和 App Package ID 根据你自己的项目去进行填写
```
npx cap init
```
初始化之后我们需要改一下 capacitor.config.json 里的 webDir，改成 dist，dist是打包生成的静态文件目录，里面必须要有入口index.html，这样可以省的我们去复制代码到 www 目录（并且我们也没有创建 www 目录）。
```
"webDir": "dist"
```
3. 接下来我们构建项目
```
//一般是这个，具体可以查看package.json
npm run build
```
4. 然后我们使用 capacitor 添加对Android平台的支持
```
npx cap add android
```
这是在项目里创建一个android项目（android文件夹），这个项目可以直接用Android Studios打开
5. 将构建的代码拷贝到Android项目库里
```
npx cap copy android
```
6. 直接使用 capacitor启动Android Studio
```
npx cap open android
```
不建议执行上面的命令启动Android Studios，通过手动启动，然后导入项目（就是上面第4步生成的文件夹），这样有时会提示gradle，可以手动设置，自动配置的时候如果遇到版本不一致就无法编译。
7. 针对于Android Studio导入项目后报错的解决方案
一般正常直接导入项目不会报错，但如果Android Studio的默认的gradle和项目里的版本不一致就会报错。 解决方式： 更新最新的Android Studio，我目前用的是4.0，最好不要用3.6以下的版本。 在File->Settings->Build,Execution,Deployment->Gradle 里的 Use Gradle from这栏重新选择Gradle，提交。 然后关闭项目，从新导入（注意导入import，不是打开open），导入后项目自行构建build，结束后就可以运行了。
8. 对于ionic和capacitor、npx的一些误解
ionic在这里仅仅是组件库，不用也行。但capacitor是必须要安装的，capacitor是用来打包和构建hybrid和的工具，和angular版ionic一样（ionic cordova ...），这里需要用npx调用capacitor进行android打包（npx cap ...）。 npx也是nodejs附带的工具。

#### 初始化vue对装饰器的支持
需要安装下面两个依赖
```
"vue-class-component": "^7.0.2"
"vue-property-decorator": "^8.1.0"
```