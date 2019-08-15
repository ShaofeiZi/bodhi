# 菩提

An implementation of [Micro Frontends](https://micro-frontends.org/)
## document
XXX
## Usage

```shell
npm i @alipay/bodhi -S
```
## Warning
子应用 请打开CSS隔离 例如 [css modules](http://www.ruanyifeng.com/blog/2016/06/css_modules.html)
不要污染全局 样式

子应用请使用 `umd`模块化
例如 webpack
```javascript
output:{
    library : 'charComponent',
    libraryTarget : 'umd'
}
```

## Examples

```shell
npm i
npm run install:examples
npm start
npm run start:main
```

Visit `http://localhost:3000`

![](./examples/example.gif)

```javascript
        Bodhi({
            container: this.props.id,  // 位置ID 用来确定DOM位置
            entry: this.props.url // 加载地址
        }).then((app) => {
            const { bootstrap, mount, unmount ,appContent} = app;
            bootstrap();
            this.mount = mount;
            this.unmount = unmount;
            const content = appContent;
            this.setState({
                content,
            });
        });
```
另外值得一提的是。这里的HTML 充当的是应用静态资源表的角色。如果我们可以对组件进行强管制。也可以采用直接加载静态资源的模式，从而减少一次请求
```javascript
   Bodhi({
            container: this.props.id,
            entry: {
                html: `<div id="root"></div>`,
                scripts: [
                    this.props.jsurl,
                ],
                styles:[
                    this.props.cssurl,
                ]
            },
        }).then((app: App) => {
            const { bootstrap, mount, unmount,appContent } = app;
            bootstrap();
            this.mount = mount;
            this.unmount = unmount;
            const content = appContent;
            this.setState({
                content,
            });
        });
```