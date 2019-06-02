# ReactNative

## 环境搭建

### Node

Node 的版本必须高于 8.3

```
npm config set registry https://registry.npm.taobao.org --global
npm config set disturl https://npm.taobao.org/dist --global
```

### Python

Python 的版本必须为 2.x（不支持 3.x）

### JDK

JDK 的版本必须是 1.8

### react-native-cli

```
npm install -g react-native-cli
npm config set registry https://registry.npm.taobao.org --global
npm config set disturl https://npm.taobao.org/dist --global
```

### Yarn

Yarn 是 Facebook 提供的替代 npm 的工具，可以加速 node 模块的下载。安装完 yarn 之后就可以用 yarn 代替 npm 了，例如用yarn代替npm install命令，用yarn add 某第三方库名代替npm install 某第三方库名。

```
npm install -g yarn
```

### Android Studio

主要使用gradle，gradle版本要匹配，不要更新

### Android SDK

目前编译 React Native v0.57应用需要的是Android 8.1 (Oreo)版本的 SDK。

展开"Android SDK Build-Tools"选项，确保选中了 React Native 所必须的27.0.3版本。

### 配置系统环境变量

```
//新建下面两个环境变量
ANDROID_HOME
C:\Users\Administrator\AppData\Local\Android\Sdk
JAVA_HOME
C:\Program Files\Java\jdk1.8.0_161
//添加下面两行到Path变量
%ANDROID_HOME%\platform-tools
%ANDROID_HOME%\tools
```

## 创建工程

```
react-native init AwesomeProject
cd AwesomeProject
react-native run-android
```

再次运行

```
adb reverse tcp:8081 tcp:8081
react-android start
```

## 组件的生命周期

![2019-01-03_133114](image\reactnative\2019-01-03_133114.png)

## 父子组件

## ReactNative中ES5和ES6语法的不同

### 引用

```js
//ES5
var ReactNative = require('react-native')
var React = require('react')
var Component = React.Component
var AppRegistry = ReactNative.AppRegistry
var StyleSheet = ReactNative.StyleSheet
var Text = ReactNative.Text
var View = ReactNative.View

//ES6
import React,{Component} from 'react'
import {
    AppRegistry,
    StyleSheet,
    Text,
    View
} from 'react-native'
```

### 导出

```js
//ES5
var MyComponent = React.createClass({
    ...
});
module.exports = MyComponent;

//ES6
export default class MyComponent extends Component{
    ...
}

```

### 定义组件

```js
//ES5
var Photo = React.createClass({
    render: function() {
        return (
            <Image source={this.props.source} />
        );
    },
});

//ES6
class Photo extends React.Component {
    render() {
        return (
            <Image source={this.props.source} />
        );
    }
}

```

### 定义方法

```js
//ES5
var Photo = React.createClass({
    componentWillMount: function(){
 
    },
    render: function() {
        return (
            <Image source={this.props.source} />
        );
    }
});

//ES6
class Photo extends React.Component {
    componentWillMount() {
 
    }
    render() {
        return (
            <Image source={this.props.source} />
        );
    }
}

```

### 定义组件的属性

```js
//ES5 
var Video = React.createClass({
    getDefaultProps: function() {
        return {
            autoPlay: false,
            maxLoops: 10,
        };
    },
    propTypes: {
        autoPlay: React.PropTypes.bool.isRequired,
        maxLoops: React.PropTypes.number.isRequired,
        posterFrameSrc: React.PropTypes.string.isRequired,
        videoSrc: React.PropTypes.string.isRequired,
    },
    render: function() {
        return (
            <View />
        );
    },
});

//ES6
class Video extends React.Component {
    static defaultProps = {
        autoPlay: false,
        maxLoops: 10,
    };  // 注意这里有分号
    static propTypes = {
        autoPlay: React.PropTypes.bool.isRequired,
        maxLoops: React.PropTypes.number.isRequired,
        posterFrameSrc: React.PropTypes.string.isRequired,
        videoSrc: React.PropTypes.string.isRequired,
    };  // 注意这里有分号
    render() {
        return (
            <View />
        );
    } // 注意这里既没有分号也没有逗号
}

```

### 初始化State

```js
//ES5
var Video = React.createClass({
    getInitialState: function() {
        return {
            loopsRemaining: this.props.maxLoops,
        };
    },
})

//ES6
class Video extends React.Component {
    constructor(props){
        super(props);
        this.state = {
            loopsRemaining: this.props.maxLoops,
        };
    }
}

```

### 方法绑定回调

```js
//ES5
var PostInfo = React.createClass({
    handleOptionsButtonClick: function(e) {
        // Here, 'this' refers to the component instance.
        this.setState({showOptionsModal: true});
    },
    render: function(){
        return (
            <TouchableHighlight onPress={this.handleOptionsButtonClick}>
                <Text>{this.props.label}</Text>
            </TouchableHighlight>
        )
    },
});

//ES6
class PostInfo extends React.Component
{
    handleOptionsButtonClick(e){
        this.setState({showOptionsModal: true});
    }
    render(){
        return (
            <TouchableHighlight 
                onPress={this.handleOptionsButtonClick.bind(this)}
                onPress={e=>this.handleOptionsButtonClick(e)}
                >
                <Text>{this.props.label}</Text>
            </TouchableHighlight>
        )
    },
}

```

### 其他

```js
//ES5


//ES6

```

## 组件-安卓

### ActivityIndicator

显示一个圆形的 loading 提示符号。

![ActivityIndicator](image\reactnative\ActivityIndicator.gif)

- animating

  是否要显示指示器动画，默认为 true 表示显示，false 则隐藏。

- color

- size

  指示器的大小，默认为'small'。目前只能在 Android 上设定具体的数值。具体的数值指的是直径大小，单位默认为px

### Button

按钮的属性，其中下划线为必填属性

- <u>onPress</u>

  用户点击此按钮时所调用的处理函数

- <u>title</u>

  按钮内显示的文本

- accessibilityLabel

  用于给残障人士显示的文本

- color

  按钮的背景色

- disabled

  设置为 true 时此按钮将不可点击。

- testID

  用来在端到端测试中定位此视图。

### DrawerLayoutAndroid

抽屉式导航栏，封装了 Android 平台的DrawerLayout，通常用于导航切换。推荐使用跨平台的react-navigation中的 DrawerNavigation 来代替此组件。

![DrawLayout](image\reactnative\DrawLayout.gif)

### FlatList

高性能的简单列表组件，支持下面这些常用的功能：

- 完全跨平台。
- 支持水平布局模式。
- 行组件显示或隐藏时可配置回调事件。
- 支持单独的头部组件。
- 支持单独的尾部组件。
- 支持自定义行间分隔线。
- 支持下拉刷新。
- 支持上拉加载。
- 支持跳转到指定行（ScrollToIndex）。

#### 属性

- <u>renderItem</u>: function

  从data中挨个取出数据并渲染到列表中

- <u>data</u>: array

  数据源，只支持普通数组

- ItemSeparatorComponent: component

  行与行之间的分割线组件，不会出现第一行之前和最后一行之后

- ListEmptyComponent: component, funtion, element

  列表为空时渲染该组件

- ListFooterComponent: component, funtion, element

  尾部组件，在所有item的底部呈现

- ListHeaderComponent: component, funtion, element

  头部组件，在所有item的顶部呈现

- columWrapperStyle: style object

  如果设置了多列布局，即numColums大于1的情况，指定此样式作用在每行容器上

- extraData: any

  如果有除data以外的数据，在此属性中指定，告诉列表重新渲染

- getItemLayout: function

  如果提前知道内容的高度或者行高是固定的，可以使用次属性避免动态测量内容尺寸的开销

- horizontal: boolean

  设置为true是则变为水平布局模式

- initialNumToRender: number

  初始渲染的元素数量，最好刚刚够填满一个屏幕

- initialScrollIndex: number

  初始顶端元素为列表中次属性索引元素，而不是第一个元素

- inverted: boolean

  翻转滚动方向

- keyExtractor: function

  用于为给定的 item 生成一个不重复的 key

- numColums: number

  在非水平布局模式下使用，组件内元素会从左到右从上到下按 Z 字形排列

- onEndReached: function

  当列表被滚动到距离内容最底部不足`onEndReachedThreshold`的距离时调用。

- onEndReachedThreshold

  设置距离底部多少距离触发`onEndReached`。注意此参数是一个比值而非像素单位。比如，0.5 表示距离内容最底部的距离为当前列表可见长度的一半时触发。

- onRefresh: funtion

  如果设置了此选项，则会在列表头部添加一个标准的RefreshControl控件，以便实现“下拉刷新”的功能。

- onViewableItemsChanged: function

  在可见行元素变化时调用

- progressViewOffset: number

  当需要在指定的偏移处显示加载指示器的时候，就可以设置这个值。

- legacyImplementation: boolean

  用于调试和性能比较

- refreshing: boolean

  在等待加载新数据时将此属性设为 true，列表就会显示出一个正在加载的符号。

- removeClippedSubviews

  对于大列表启用本属性可能可以提高性能。

- viewabilityConfig

- viewabilityConfigCallbackPairs

#### 方法

- scrollToEnd

  滚动到底部。如果不设置`getItemLayout`属性的话，可能会比较卡。

- scrollToIndex

  将位于指定位置的元素滚动到可视区的指定位置，当`viewPosition` 为 0 时将它滚动到屏幕顶部，为 1 时将它滚动到屏幕底部，为 0.5 时将它滚动到屏幕中央。

- scrollToItem

  这个方法会顺序遍历元素。尽可能使用`scrollToIndex`代替。

- scrollToOffset

  滚动列表到指定的偏移（以像素为单位）

- recordInteraction

  主动通知列表发生了一个事件，以使列表重新计算可视区域。比如说当`waitForInteractions`为 true 并且用户没有滚动列表时。一般在用户点击了列表项或发生了导航动作时调用。

- flashScrollIndicators

  短暂地显示滚动指示器。

### Image

用于显示多种不同类型图片的 React 组件，包括网络图片、静态资源、临时的本地图片、以及本地磁盘上的图片（如相册）等。

#### 属性

- style

  图片样式

- blurRadius

  模糊半径，为图片添加指定半径的模糊滤镜

- onLayout

  当元素加载或者布局改变的时候调用

- onLoad

  加载成功完成时调用

- onLoadEnd

  加载结束后，不论成功还是失败都调用

- onLoadStart

  加载开始时调用

- resizeMode

  当容器尺寸和图片不成比例的时候如何调整图片的大小

- source

  图片源数据

- loadingIndicatorSource

  图片还未加载时的指示图片源数据

- onError

  加载错误时回调

- testID

- resizeMethod

  当图片实际尺寸和容器尺寸不一致时，如何调整图片大小

- accessibilityLabel

  ios，读屏

- accessible

  ios，无障碍

- capInsets

  ios，当图片被缩放的时候，capInsets 指定的角上的尺寸会被固定而不进行缩放，而中间和边上其他的部分则会被拉伸

- defaultSource

  读取图片时默认显示的图片，在Android的debug版本上本属性不会生效（但在release版本中会生效）。

- onPartialLoad

  ios，如果图片本身支持逐步加载，则逐步加载的过程中会调用此方法。

- onProgress

  在加载过程中不断调用

- fadeDuration

  淡出时间

- progressiveRenderingEnabled

  启用渐进式jpeg流传输

#### 方法

- getSize

  在显示图片前获取图片的宽高

- prefetch

  预加载一个远程图片(将其下载到本地磁盘缓存)。

- abortPrefetch

  中断预加载操作。仅 Android 可用。

- queryCache

  查询图片缓存状态

- resolveAssetSource

  将资源引用解析为拥有uri、width和height属性对象

### ImageBackground

图片背景

- Image

  指定图片数据源

- style

- imageStyle

- imageRef

### KeyboardAvoidingView

手机上弹出的键盘常常会挡住当前的视图。本组件可以自动根据键盘的位置，调整自身的 position 或底部的 padding，以避免被遮挡。

![KeyboardAvoidingView](image\reactnative\KeyboardAvoidingView.gif)

- keyboardVerticalOffset: number

- behavior: enum('height', 'position', 'padding')

   Android 可能不指定此属性更好，而 iOS 可能相反

- contentContainerStyle

- enabled: boolean

  是否启用KeyboardAvoidingView。默认为true。

### ListView

弃用

### Modal

Modal 组件是一种简单的覆盖在其他视图之上显示内容的方式。

- visible: boolean

  visible属性决定modal是否显示

- supportedOrientations

- <u>onRequestClose</u>: function

  在安卓平台上为必填，在用户按下 Android 设备上的后退按键或是 Apple TV 上的菜单键时触发。

- onShow: function

  在 modal 显示时调用。

- transparent: boolean

  指背景是否透明，默认为白色，将这个属性设为：true 的时候弹出一个透明背景层的modal。

- animationType: enum('none','slide','fade')

  指定了 modal 的动画类型。

  - slide 从底部滑入滑出
  - fade 淡入淡出
  - none 没有动画

- hardwareAccelerated: boolean

  决定是否强制启用硬件加速来绘制弹出层。

- onDismiss

- onOrientationChange

- presentationStyle

### Picker

本组件渲染原生的选择器（Picker）

- onValueChange: function

  某一项被选中时执行,调用时带有如下参数：

  - `itemValue`: 被选中项的`value`属性
  - `itemPosition`: 被选中项在picker中的索引位置

- selectedValue: any

  默认选中的值。可以是字符串或整数。

- style

- testID

- enabled: boolean

  如果设为false，则会禁用此选择器。

- mode: enum('dialog', 'dropdown')

  在Android上，可以指定在用户点击选择器时，以怎样的形式呈现选项：

  - 'dialog': 显示一个模态对话框。默认选项。
  - 'dropdown': 以选择器所在位置为锚点展开一个下拉框。

- prompt: string

  设置选择器的提示字符串

- itemStyle

  指定应用在每项标签上的样式。

### ProgressBarAndroid

封装了Android平台上的ProgressBar的React组件。这个组件可以用来表示应用正在加载或者有些事情正在进行中。

- animating: boolean

  是否显示进度条（默认为true显示）。

- color: color

  进度条的颜色。

- indeterminate

  决定进度条是否要显示一个不确定的进度。

- progress: number

  当前的进度值（在0到1之间）。

- styleAttr: enum('Horizontal', 'Normal', 'Small', 'Large', 'Inverse', 'SmallInverse', 'LargeInverse')

  进度条的样式

- testID

### RefreshControl

这一组件可以用在ScrollView或FlatList内部，为其添加下拉刷新的功能。当ScrollView处于竖直方向的起点位置（scrollY: 0），此时下拉会触发一个onRefresh事件。

- <u>refreshing</u>: boolean

  视图是否应该在刷新时显示指示器。

- onRefresh: function

  在视图开始刷新时调用。

- colors

  指定至少一种颜色用来绘制刷新指示器。

- enabled: boolean

  指定是否要启用刷新指示器。

- progressBackgroundColor

  指定刷新指示器的背景色。

- progressViewOffset

  指定刷新指示器的垂直起始位置(top offset)。

- size: RefreshControl.SIZE

  指定刷新指示器的大小

- tintColor

- title: string

- titleColor

### SafeAreaView

SafeAreaView会自动根据系统的各种导航栏、工具栏等预留出空间来渲染内部内容。更重要的是，它还会考虑到设备屏幕的局限，比如屏幕四周的圆角或是顶部中间不可显示的“刘海”区域。

只需简单地把你原有的视图用`SafeAreaView`包起来，同时设置一个`flex: 1`的样式。

### ScrollView

滚动视图，必须有一个确定的高度才能正常工作。一般来说我们会给ScrollView设置`flex: 1`以使其自动填充父容器的空余空间。

ScrollView会简单粗暴地把所有子元素一次性全部渲染出来。

`FlatList`会惰性渲染子元素，只在它们将要出现在屏幕中时开始渲染。

#### 属性

- alwaysBounceVertical

- contentContainerStyle

  这些样式会应用到一个内层的内容容器上，所有的子视图都会包裹在内容容器内。

- keyboardDismissMode: enum

  用户拖拽滚动视图的时候，是否要隐藏软键盘。

  - `none`（默认值），拖拽时不隐藏软键盘。
  - `on-drag`当拖拽开始的时候隐藏软键盘。
  - `interactive`

- keyboardShouldPersistTaps

  如果当前界面有软键盘，那么点击scrollview后是否收起键盘

  - `never`（默认值），点击TextInput以外的子组件会使当前的软键盘收起
  - `always`键盘不会自动收起，ScrollView也不会捕捉点击事件，但子组件可以捕获。
  - `handled`当点击事件被子组件捕获时，键盘不会自动收起。

- onContentSizeChange: function

  在ScrollView内部可滚动内容的视图发生变化时调用。

- onMomentumScrollBegin: function

  滚动动画开始时调用

- onMomentumScrollEnd: function

  滚动动画结束时调用此函数。

- onScroll: function

  在滚动的过程中，每帧最多调用一次此回调函数

- onScrollBeginDrag: function

  当用户开始拖动此视图时调用此函数。

- onScrollEndDrag: function

  当用户停止拖动此视图时调用此函数。

- pagingEnabled: boolean

  当值为true时，滚动条会停在滚动视图的尺寸的整数倍位置。这个可以用在水平分页上。默认值为false。

  注意：垂直分页在Android上不支持。

- refreshControl: element

  用于为ScrollView提供下拉刷新功能。只能用于垂直视图

- removeClippedSubviews: boolean

  当此属性为true时，屏幕之外的子视图会被移除。这个可以提升大列表的滚动性能。默认值为true。

- scrollEnabled: boolean

  当值为false的时候，内容不能滚动，默认值为true。

- showsHorizontalScrollIndicator: boolean

  当此属性为true的时候，显示一个水平方向的滚动条。

- showsVerticalScrollIndicator: boolean

  当此属性为true的时候，显示一个垂直方向的滚动条。

- stickyHeaderIndices: array of number

  一个子视图下标的数组，用于决定哪些成员会在滚动之后固定在屏幕顶端。

- endFillColor

  有时候滚动视图会占据比实际内容更多的空间。这种情况下可以使用此属性，指定以某种颜色来填充多余的空间，以避免设置背景和创建不必要的绘制开销。一般情况下并不需要这种高级优化技巧。

- overScrollMode

  覆盖默认的overScroll模式，可选的值有：

  - `auto` - 默认值，允许用户在内容超出视图高度之后可以滚动视图。
  - `always` - 无论内容尺寸，用户始终可以滚动视图。
  - `never` - 始终不允许用户滚动视图。

- scrollPerfTag

- DEPRECATED_sendUpdatedChildFrames

- alwaysBounceHorizontal

- horizontal: boolean

  当此属性为true的时候，所有的子视图会在水平方向上排成一行，而不是默认的在垂直方向上排成一列。默认值为false。

- automaticallyAdjustContentInsets

- bounces

- bouncesZoom

- canCancelContentTouches

- centerContent

- contentInset

- contentInsetAdjustmentBehavior

- contentOffset

- decelerationRate

  一个浮点数，用于决定当用户抬起手指之后，滚动视图减速停下的速度

- directionalLockEnabled

- indicatorStyle

- maximumZoomScale

- minimumZoomScale

- pinchGestureEnabled

- scrollEventThrottle

- scrollIndicatorInsets

- scrollsToTop

- snapToAlignment

  当设置了`snapToInterval`，`snapToAlignment`会定义停驻点与滚动视图之间的关系。

  - `start` (默认) 会将停驻点对齐在左侧（水平）或顶部（垂直）
  - `center` 会将停驻点对齐到中间
  - `end` 会将停驻点对齐到右侧（水平）或底部（垂直）

- snapToInterval: number

  当设置了此属性时，会让滚动视图滚动停止后，停止在`snapToInterval`的倍数的位置。这可以在一些子视图比滚动视图本身小的时候用于实现分页显示。

- snapToOffsets: array of number

- snapToStart: boolean

- snapToEnd: boolean

- zoomScale

- nestedScrollEnabled: boolean

  在Android API level 21（5.0）以上启用嵌套滚动。

#### 方法

- scrollTo

  滚动到指定的x, y偏移处。第三个参数为是否启用平滑滚动动画。

- scrollToEnd

  滚动到视图底部（水平方向的视图则滚动到最右边）。

- scrollWithoutAnimationTo

- flashScrollIndicators

  短暂地显示滚动指示器。

### SectionList

高性能的分组(section)列表组件

- 完全跨平台。
- 行组件显示或隐藏时可配置回调事件。
- 支持单独的头部组件。
- 支持单独的尾部组件。
- 支持自定义行间分隔线。
- 支持分组的头部组件。
- 支持分组的分隔线。
- 支持多种数据源结构
- 支持下拉刷新。
- 支持上拉加载。

### Slider

滑动选择，用于选择一个范围值的组件。

### StatusBar

控制应用状态栏的组件。

### Switch

开关组件。

你必须使用`onValueChange`回调来更新`value`属性以响应用户的操作。如果不更新`value`属性，组件只会按一开始给定的`value`值来渲染且保持不变，看上去就像完全点不动。

### Text

文本

### TextInput

文本输入

### ToolbarAndroid

工具栏

一个Toolbar可以显示一个徽标，一个导航图标（譬如汉堡形状的菜单按钮），一个标题与副标题，以及一个功能列表。标题和副标题会在中间显示，徽标和导航图标会在左侧显示，而功能列表则在右侧显示。

### TouchableHighlight

本组件用于封装视图，使其可以正确响应触摸操作。当按下的时候，封装的视图的不透明度会降低，同时会有一个底层的颜色透过而被用户看到，使得视图变暗或变亮。

### TouchableNativeFeedback

本组件用于封装视图，使其可以正确响应触摸操作（仅限Android平台）。在Android设备上，这个组件利用原生状态来渲染触摸的反馈。

目前它只支持一个单独的View实例作为子节点。

### TouchableOpacity

本组件用于封装视图，使其可以正确响应触摸操作。当按下的时候，封装的视图的不透明度会降低。

此组件与TouchableHighlight的区别在于并没有额外的颜色变化，更适于一般场景。

### TouchableWithoutFeedback

本组件没有任何视觉反馈

### View

作为创建 UI 时最基础的组件

### ViewPagerAndroid

一个允许在子视图之间左右翻页的容器。每一个 ViewPagerAndroid 的子容器会被视作一个单独的页，并且会被拉伸填满 ViewPagerAndroid。

注意所有的子视图都必须是纯 View，而不能是自定义的复合容器。

### VirtualizedList

FlatList和SectionList的底层实现。仅当想获得比 FlatList 更高的灵活性（比如说在使用 immutable data 而不是 普通数组）的时候，你才应该考虑使用 VirtualizedList。极大的改善了内存消耗以及在有大量数据情况下的使用性能

### WebView

Web视图，建议使用react-native-community/react-native-webview代替它

## 接口-安卓

### AccessibilityInfo

用户的设备是否正在运行读屏应用。

### Alert

启动一个提示对话框，包含对应的标题和信息。

### Animated

动画

### AppRegistry

AppRegistry所有 React Native 应用的 JS 入口。应用的根组件应当通过AppRegistry.registerComponent方法注册自己，然后原生系统才可以加载应用的代码包并且在启动完成之后通过调用AppRegistry.runApplication来真正运行应用。

### AppState

`AppState`能告诉你应用当前是在前台还是在后台，并且能在状态变化的时候通知你。

AppState 通常在处理推送通知的时候用来决定内容和对应的行为。

### AsyncStorage

`AsyncStorage`是一个简单的、异步的、持久化的 Key-Value 存储系统，它对于 App 来说是全局性的。可用来代替 LocalStorage。

我们推荐您在 AsyncStorage 的基础上做一层抽象封装，而不是直接使用 AsyncStorage。

### BackHandler

监听设备上的后退按钮事件。

Android：监听后退按钮事件。如果没有添加任何监听函数，或者所有的监听函数都返回 false，则会执行默认行为，退出应用。

### CameraRoll

`CameraRoll`模块提供了访问本地相册的功能。

### Clipboard

`Clipboard`组件可以在 剪贴板中读写内容。

### DatePickerAndroid

本组件会打开一个标准的 Android 日期选择器的对话框。

### Dimensions

本模块用于获取设备屏幕的宽高。

### Easing

`Easing`模块实现了常见的动画缓动函数。**缓动函数**指定动画效果在执行时的速度，使其看起来更加真实。

### Geolocation

地理定位

本 API 在安卓上需要谷歌框架支持，因而无法在国内使用，请在 github 上搜索百度或高德等国内第三方封装替代库。

地理定位只用于返回经纬度数据，无法得出具体地名。如果需要通过经纬度数据查询具体地名，则需要额外的“逆地理编码”（即通过经纬度查询地图数据库得到地名）。一般第三方的地图封装带有此功能。

### ImageEditor

- cropImage

剪裁对应的图片

### ImageStore

存储删除内存图片

### InteractionManager

Interactionmanager 可以将一些耗时较长的工作安排到所有互动或动画完成之后再进行。这样可以保证 JavaScript 动画的流畅运行。

### Keyboard

`Keyboard`模块用来控制键盘相关的事件。

### LayoutAnimation

布局动画

### Linking

`Linking`提供了一个通用的接口来与传入和传出的 App 链接进行交互

### NetInfo

通过NetInfo模块可以获取设备当前的联网状态。

### PanResponder

`PanResponder`类可以将多点触摸操作协调成一个手势。它使得一个单点触摸可以接受更多的触摸操作，也可以用于识别简单的多点触摸手势。

### PermissionAndroid

`PermissionsAndroid` 可以访问Android M(也就是6.0)开始提供的权限模型。有一些权限写在`AndroidManifest.xml`就可以在安装时自动获得，但有一些“危险”的权限则需要弹出提示框供用户选择。本API即用于后一种情形。

### PixelRatio

PixelRatio 类提供了访问设备的像素密度的方法。

### Share

分享

### StyleSheet

StyleSheet 提供了一种类似 CSS 样式表的抽象。

### Systrace

- installReactHook
- setEnabled
- isEnabled
- beginEvent
- endEvent
- beginAsyncEvent
- endAsyncEvent
- counterEvent
- attachToRelayProfiler
- swizzleJSON
- measureMethods
- measure

### TimePickerAndroid

本组件会打开一个标准的 Android 时间选择器的对话框。

### ToastAndroid

用于在 Android 设备上显示一个悬浮的提示信息。

### Transforms

- decomposedMatrix
- rotation
- scaleX
- scaleY
- transform
- transformMatrix
- translateX
- translateY

### Vibration

用于控制设备震动。震动触发是异步的，也就是说这个函数会立即返回而非等待震动结束。

### View Style Props

## 第三方

### react-navigation

```
npm install --save react-navigation
//If you’re using Expo you don’t need to do anything here,otherwise
npm install --save react-native-gesture-handler
//运行之后无法识别 link、run-android等，为什么？然后需要使用npm install才可以使用
//npm存在安装新库时会删除其他库的问题,尽量使用yarn代替npm操作
react-native link react-native-gesture-handler

yarn add react-navigation
yarn add react-native-gesture-handler
```

### react-native-vector-icons

```
yarn add react-native-vector-icons
//link的目的是什么
react-native link react-native-vector-icons
```

### react-native-gesture-handler

```java
yarn add react-native-gesture-handler
react-native link react-native-gesture-handler
```

安卓需要更新MainActivity文件，不然ReactButton的onPress函数没有反应

![gesturehandle](image\reactnative\gesturehandle.png)