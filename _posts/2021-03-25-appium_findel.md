---
layout: post
title:  "Appium元素定位"
date:   2021-03-25 13:01:03
categories: Appium
tags: tingyun.com
excerpt: 
---
* content
{:toc}

## appium元素定位（js语法）

### 通过id定位

resource-id也称为id，resource-id是唯一的

```
let elementsOne = await driver.elementById("SomeID");
let elementsTwo = await driver.elements("id", "SomeID");
```

### 通过className定位

```
let elementsOne = await driver.elementsByClassName("SomeID");
```

### 通过AccessibilityID定位

AccessibilityId也称为content-desc

```
let elementsOne = await driver.elementsByAccessibilityId("SomeAccessibilityID");
```

### 通过xpath定位

1.层级定位

fullIndexXpath：全路径的形式

2.text定位

```
let elementsOne = await driver.elementsByXpath("//*[@text='查找的文本']");
```

3.contains模糊定位

```
let elementsOne = await driver.elementsByXpath("//<class_name>[contains(@text, '查找的文本')]");
```

4.组合定位

同时包含class和text两个属性

```
let elementsOne = await driver.elementsByXpath("//*[@text='查找的文本' and @class='<class_name>']");
```

5.通过UIAutomator定位

android uiautomator原理是通过android 自带的android uiautomator的类库去查找元素，其实和appium的定位一样，或者说他比appium的定位方式更佳多以及更佳适用，它也支持id、className、text、模糊匹配等进行定位。

5.1.text定位

```
let el = await driver.elementByAndroidUIAutomator("new UiSelector().text('查找的文本')");
```

5.2.text模糊定位

```
let el = await driver.elementByAndroidUIAutomator("new UiSelector().textContains('查找的文本')");
```

5.3.textStartsWith定位

以text开始

```
let el = await driver.elementByAndroidUIAutomator("new UiSelector().textStartsWith('查找的文本')");
```

5.4.textMatches正则匹配查找

```
let el = await driver.elementByAndroidUIAutomator("new UiSelector().textMatches('^查找的文本.*')");
```

5.5.resourceID定位

```
let el = await driver.elementByAndroidUIAutomator("new UiSelector().resourceID('id')");
```

5.6.resourceIDMatches定位

通过id进行正则匹配定位

```
let el = await driver.elementByAndroidUIAutomator("new UiSelector().resourceIdMatches('.+id')");
```

5.7.className定位

```
let el = await driver.elementByAndroidUIAutomator("new UiSelector().className('<class_name>')");
```

5.8.classNameMatches定位

通过className正则匹配进行定位

```
let el = await driver.elementByAndroidUIAutomator("new UiSelector().classNameMatches('.+<class_name>')");
```

5.9.组合定位

```
let el = await driver.elementByAndroidUIAutomator("new UiSelector().resourceId('id').text('查找的文本')");
```

5.10.父子关系、兄弟关系定位

```
//父子关系
let el = await driver.elementByAndroidUIAutomator("new UiSelector().resourceId('id').childSelector(text('查找的文本'))");
```

```
//兄弟关系
let el = await driver.elementByAndroidUIAutomator("new UiSelector().resourceId('id').fromParent(text('查找的文本'))");
```

5.11.滚动查找

```
let el = await driver.elementByAndroidUIAutomator("new UiScrollable(new UiSelector().scrollable(true).instance(0)).scrollIntoView(new UiSelector().text('查找的元素文本').instance(0));");
```

## 常用api及属性

1.获取页面源码（xml层级结构）

```
let pageSource = await driver.source();
```

2.隐式等待

```
await driver.setImplicitWaitTimeout(20000);
```

3.强制等待

```
await driver.sleep(5000);
```

4.允许授权

```
await driver.passPermission();
```

5.click

元素点击方法

```
let element = await driver.elementByAccessibilityId('id', 'SomeId');
await element.click();
```

6.sendKeys

向元素输入一连串的按键

```
let element = await driver.elementByAccessibilityId("SomeAccessibilityID");
await element.type("Hello world!")
```
或

```
let element = await driver.elementByAccessibilityId("SomeAccessibilityID");
await element.sendKeys("Hello world!");
```

7.clear

清除某一元素值

```
let element = await driver.elementByAccessibilityId("SomeAccessibilityID");
await element.clear();
```

8.text

返回元素可见的文本

```
let element = await driver.elementByAccessibilityId("SomeAccessibilityID");
await element.text();
```

9.Name

获得元素标签名

```
let element = await driver.elementByAccessibilityId("SomeAccessibilityID");
let tagName = await element.getTagName();
```

10.Attribute

获得元素属性值

```
let element = await driver.elementByAccessibilityId("SomeAccessibilityID");
let tagName = await element.getAttribute("content-desc");
```

返回类型string

11.selected

确定表单元素被选中

```
let element = await driver.elementByAccessibilityId("SomeAccessibilityID");
let isSelected = await element.isSelected();
```

返回布尔值

12.Enable

判断一个元素当前是否可操作

```
let element = await driver.elementByAccessibilityId("SomeAccessibilityID");
let isEnabled = await element.isEnabled();
```

返回布尔值

13.Location

确定元素在页面或屏幕上的位置

```
let element = await driver.elementByAccessibilityId("SomeAccessibilityID");
let location = await element.getLocation();
```

点 (0, 0) 指的是页面的左上角. 元素的坐标以具有x和y属性的JSON对象返回

14.size

获取元素大小

```
let element = await driver.elementByAccessibilityId("SomeAccessibilityID");
let size = await element.getSize();
```

尺寸将作为具有宽度和高度属性的对象返回,width:元素的宽度,height:元素的高度

15.Rect

获取元素的维度和坐标

```
let element = await driver.elementByAccessibilityId("SomeAccessibilityID");
let rect = await element.getRect();
```

响应
|名称|类型|描述|
|x|数值类型|X坐标|
|y|数值类型|Y坐标|
|height|数值类型|矩形框高度|
|width|数值类型|矩形框宽度|

16.Submit

提交表单

```
let element = await driver.elementByAccessibilityId("SomeAccessibilityID");
await element.submit();
```

该提交命令也适用于表单元素的子类（Web网页适用)

17.Equals Element

判断元素是否相等(判断两个元素的ID是否指向同一元素)

```
let elementOne = await driver.elementByClassName("someClass");
let elementTwo = await driver.elementByClassName("someOtherClass");
let isEqual = await elementOne.equalsElement(elementTwo);
```

18.Move to

将鼠标移动指定元素的偏移量

```
await driver.moveTo(element, 10, 10);
```

如果未指定任何元素，则移动是相对于当前鼠标光标的。 如果提供了元素但没有偏移，则鼠标将移动到元素的中心。 如果该元素不可见，则将其滚动到视图中。


19.双击

双击鼠标

```
await driver.moveTo(element);
await driver.doubleclick();
```

20.Button Down

单机当前鼠标坐标处，并按住鼠标左键

```
await driver.moveTo(element);
await driver.buttonDown();
```

21.Button Up

释放之前按住的鼠标按钮

```
await driver.moveTo(element);
await driver.buttonDown();
await driver.moveTo(element, 10, 10);
await driver.buttonUp();
```

22.touch

22.1.single tap

轻按屏幕启用设备

```
await driver.tapElement(elementOne);
```
或
```
let action = new wd.TouchAction();
action.tap({el: element});
await action.perform();
```

eg:
```
let el1 = await driver.elementById('com.yt.hxmb50.launcher:id/custom_input');
        let size = await el1.getSize();
        let location = await el1.getLocation();

        let keyJson = '{"0":[9,0],"1":[0,0],"2":[1,0],"3":[2,0],"4":[3,0],"5":[4,0],"6":[5,0],"q":[0,1],"w":[1,1],"e":[2,1],"r":[3,1],"t":[4,1],"y":[5,1]}';
        console.debug('keyJson= ' + keyJson);
        var keyObj = JSON.parse(keyJson);
        console.debug('keyJson= ' + keyJson);
        let btnWidth = size.width / 10;
        let btnheight = size.height / 4;
        let password = 'qwerty123';
        for (let i of password) {
            console.debug('keyObj = ' + keyObj[i]);
            console.log(i);
            let btn1X = location.x + keyObj[i][0] * btnWidth + btnWidth / 2;
            let btn1y = location.y + keyObj[i][1] * btnheight + btnheight / 2;
            console.debug('btn1X= ' + btn1X);
            console.debug('btn1y = ' + btn1y);
            const wd = require('wd');
            await (new wd.TouchAction(driver))
                .tap({ x: btn1X, y: btn1y })
                .perform()
        }
```

22.2.Move

手指在屏幕上移动

```
let action = new wd.TouchAction(driver);
action.press({x: 10, y: 10})
      .wait(1000)
      .moveTo({x: 50, y: 50})
      .release();
await action.perform();
```

22.3.Long Tap

长按

```
let action = new wd.TouchAction();
action.longPress({el: element});
await action.perform();
```

22.4.Scroll

滚动事件

```
await driver.scroll(10, 100);
```

22.5.Flick

滑动事件

```
//以像素为单位的x方向的偏移量,以像素为单位的y方向的偏移量,速度，单位为“像素/秒”
await element.flick(1, 10, 10);
```

