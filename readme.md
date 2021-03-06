# 原生 JavaScript 实现扫雷游戏

学习了一段时间之后，使用原始 JS 实现的一个扫雷游戏，未使用 canvas，所以性能方面有些问题。


## 效果图
![demo1](https://github.com/CaiJinyc/game-mineSweepinng/blob/master/img/demo1.gif)![demo2](https://github.com/CaiJinyc/game-mineSweepinng/blob/master/img/demo2.png)![demo3](https://github.com/CaiJinyc/game-mineSweepinng/blob/master/img/demo3.png)![demo4](https://github.com/CaiJinyc/game-mineSweepinng/blob/master/img/demo4.png)

## 功能
#### 实现的功能
基本扫雷的功能都实现了，例如：
* 计时
* 选择游戏难度
* 标记地雷（插旗子标记地雷，标记之后不能点击）
* 剩余雷数（总的雷数减去插旗的数量）
* 自动连锁点开（当点开某个区块后，如果该区块的数字为 0，也就是九宫格内没有雷，那么将自动点开九宫格内的所有区块）

还做了点小彩蛋，例如：踩到地雷时，地雷会逐步显示，还有成功扫到所有雷之后，地图逐渐被彩色方块覆盖，然后提示扫雷成功。


#### 生成一张扫雷地图
这里当然用的是数组啦，会玩扫雷的应该都懂，如果一个方块块有雷，那么边上的值都加 1。

1. 根据行数和列数创建一个多维数组（使用 for 循环嵌套实现）
2. 然后使用 Math 随机 map[x][x] 来写入雷的位置（再次使用 for 循环，写入 9（9 就代表雷）），如果位置已经有雷了就重写随机然后写入
3. 然后我们就会得到一个这样的数组，这个时候我们只需要让 9 的四周加上 1
   [ [0, 9, 0, 0],
     [0, 0, 9, 0],
     [9, 0, 9, 0],
     [0, 9, 0, 0] ]
4. 得到这样的数组，这样就大功告成啦。
  [  [1, 9, 2, 1],
     [2, 4, 9, 2],
     [9, 4, 9, 2],
     [2, 9, 2, 1]  ]


#### 将地图写入页面
使用 doucument.querySelector 获取到元素节点，然后使用 innerHTML 就行了。

#### 自动连锁点开
1. 点击到为 0 的位置，就自动显示周围一圈的位置。
2. 然后周围一圈的还有为 0 的位置，就继续显示周围一圈，然后循环到没有为止。
