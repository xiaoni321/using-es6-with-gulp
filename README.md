# 在gulp中使用ES6

gulp在3.9版本里面增加了对babel的支持，因此我们可以直接在gulpfile里面使用ES6(ES2015)了。

## 升级gulp版本

首先要检测一下我们的gulp版本，确保CLI版本及Local版本都在3.9之上:

```
gulp -v
```

版本如下：
```
CLI version 3.9.0
Local version 3.9.0
```

若版本过低，我们可以通过以下方式进行升级，这里将同时升级CLI版本和Local版本：

```
npm install gulp -g && npm install gulp --save-dev
```

## 安装babel

我们需要安装[babel-core](https://github.com/babel/babel/tree/master/packages/babel-core)及[babel-preset-es2015](https://github.com/babel/babel/tree/master/packages/babel-preset-es2015)来转换ES6代码：

```
npm install babel-core babel-preset-es2015 --save-dev
```

然后，创建一个`.babelrc`文件来使用es2015 preset：

```
touch .babelrc
```

写入如下内容：

```
{
  "presets": ["es2015"]
}
```

> 或者是不创建.babelrc，直接在package.json里面添加`babel`字段，如：
> ```
"babel": {
  "presets": [
    "es2015"
  ]
}
> ```


接下来就是使用ES6语法重写gulpfile了。

## 使用ES6语法重写gulpfile

首先，重命名gulpfile.js为gulpfile.babel.js，这样gulp执行前会自动调用babel转换文件。

```
mv gulpfile.js gulpfile.babel.js
```

然后在gulpfile.babel.js里面用ES6语法写些内容，如下：

```
'use strict';

import gulp from 'gulp';
import less from 'gulp-less';

const PATHS = {
  less: 'less/',
  dest: 'build/'
};

gulp.task('less', () => {
  gulp.src(`${PATHS.less}**/*.less`)
    .pipe(less())
    .pipe(gulp.dest(`${PATHS.dest}css/`));
});
```

然后执行gulp命令：

```
gulp less
```

这里和原来一样，以前的命令怎么用现在还是怎么用!

参考资料：

[https://github.com/yeoman/generator-gulp-webapp/issues/356](https://github.com/yeoman/generator-gulp-webapp/issues/356)

[es6-features.org](es6-features.org)

---

[MIT License](./LICENSE)