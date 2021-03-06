# 加载和切换场景

在 Cocos Creator 中，我们使用场景文件名（ 可以不包含扩展名）来索引指代场景。并通过以下接口进行加载和切换操作：

```js
cc.director.loadScene('MyScene');
```

## 通过常驻节点进行场景资源管理和参数传递

通常我们同时只会加载运行一个场景，当切换场景时，默认会将场景内所有节点和其他实例销毁。如果我们需要用一个组件控制所有场景的加载，或在场景之间传递参数数据，就需要将该组件所在节点标记为「常驻节点」，使它在场景切换时不被自动销毁，常驻内存。我们使用以下接口：

`cc.game.addPersistRootNode(myNode);`

上面的接口会将 `myNode` 变为常驻节点，这样挂在上面的组件都可以在场景之间持续作用，我们可以用这样的方法来储存玩家信息，或下一个场景初始化时需要的各种数据。

如果要取消一个节点的常驻属性：

`cc.game.removePersistRootNode(myNode)`

### 使用全局变量

除此之外，简单的数值类数据传递也可以使用全局变量的方式进行，详见[通过全局变量跨组件访问值](access-node-component.md#--9)。


## 场景加载回调

加载场景时，可以附加一个参数用来指定场景加载后的回调函数：

`cc.director.loadScene('MyScene', onSceneLaunched);`

上一行里 `onSceneLaunched` 就是声明在本脚本中的一个回调函数，在场景加载后可以用来进一步的进行初始化或数据传递的操作。

由于回调函数只能写在本脚本中，所以场景加载回调通常用来配合常驻节点，在常驻节点上挂载的脚本中使用。

## 预加载场景

`cc.director.loadScene` 会在加载场景之后自动切换运行新场景，有些时候我们需要在后台静默加载新场景，并在加载完成后手动进行切换。

可以预先使用 `preloadScene` 接口对场景进行预加载:

```js
cc.director.preloadScene('table', function () {
    cc.log('Next scene preloaded');
});
```

之后在合适的时间调用 `loadScene`, 就可以立即切换场景

```js
cc.director.loadScene('table');
```

实战例子可以参考 [21点演示项目](https://github.com/cocos-creator/tutorial-blackjack/blob/master/assets/scripts/Menu.js#L12-L14)

**注意** 使用预加载场景资源配合 `runScene` 的方式进行预加载场景的方法已被废除:

```js
// 请不要再使用下面的方法预加载场景!
cc.loader.loadRes('MyScene.fire', function(err, res) {
    cc.director.runScene(res.scene); 
});
```