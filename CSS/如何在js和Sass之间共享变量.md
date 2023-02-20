# 如何在js和Sass之间共享变量

环境之间共享变量是神圣的。以下是如何在JavaScript和Sass（或CSS）之间共享变量。随着大型单页应用程序的兴起，Javascript和CSS变得越来越紧密。通常会在两者之间复制值（例如，与React的CSSTransitionGroup一起使用的动画持续时间或将主题颜色传递到图形库中）。然而，维护两个相同值的副本不可避免地导致只更新一个副本，并最终导致bug的出现。幸运的是，有了webpack和CSS模块，还有更好的方法。在这篇博文中，我们将通过前面提到的为CSSTransitionGroup共享动画持续时间的示例，探讨如何在脚本和样式之间共享变量。

第一步安装我们的依赖:

```shell
npm install sass-loader node-sass webpack --save-dev
```

接下来，我们需要将webpack配置为使用sass加载器，以便我们可以从Javascript访问sass代码。

```shell
// webpack.config.js
module.exports = {
  module: {
    rules: [
      {
        test: /\.css$/,
        use: ['style-loader', 'css-loader', 'sass-loader']
      }
    ]
  }
}
```

现在是有趣的部分。我们在Sass中定义实际变量值，并将其导出到Javascript。CSS模块有一个整洁的实用程序，名为：export。export指令的工作原理与ES6的export关键字基本相同。Sass代码将导出一个包含要在Javascript中使用的变量名及其关联值的对象。这些值都导出为字符串。

```scss
// styles/animation.scss
$animation-length: 250;
$animation-length-ms: $animation-length + 0ms;

:export {
  animationMillis: $animation-length-ms;
}

.component-enter {
  ...

  transition: all $animation-length-ms ease-in;
}
```

您会注意到，我们首先在一个变量中声明整数值，然后在另一个变量中将其添加0ms。这使得我们只能导出“250”，而不是“250ms”，这在Javascript端更容易解析（将0ms添加到数字会将其“类型”强制转换为ms）。

现在，在Javascript中，我们只需要从样式表中导入样式，并从导出的变量中解析一个整数。

```javascript
// js/animation.js
import styles from '../styles/animation.scss'
import CSSTransitionGroup from 'react-transition-group/CSSTransitionGroup'

const millis = parseInt(styles.animationMillis)

...

<CSSTransitionGroup
  transitionName="component"
  transitionEnterTimeout={millis}
  transitionLeaveTimeout={millis}
/>

...
```

这种方法非常简单，但如果您避免了在Javascript和Sass之间同步更改的麻烦，它会有很大的回报。