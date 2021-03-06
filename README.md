# react-native-wheel-picker
[![npm version](http://img.shields.io/npm/v/@yz1311/react-native-wheel-picker.svg?style=flat-square)](https://npmjs.org/package/@yz1311/react-native-wheel-picker "View this project on npm")
[![npm version](http://img.shields.io/npm/dm/@yz1311/react-native-wheel-picker.svg?style=flat-square)](https://npmjs.org/package/@yz1311/react-native-wheel-picker "View this project on npm")

# 前言

该库最开始基于[react-native-wheel-picker](https://github.com/lesliesam/react-native-wheel-picker)，修改和拓展了很多功能

> android端基于[WheelPicker](https://github.com/AigeStudio/WheelPicker) 1.1.2版本(注意不要手动升级到1.1.3)进行封装

> ios端基于RN自带的PickerIOS进行封装

在原库的基础上面，进行了下面的修改:

* <span style="color: #006AB1;">修复几处严重bug，支持RN新版本</span>
* <span style="color: #006AB1;">添加typescript定义文件</span>
* <span style="color: #006AB1;">封装多Wheel支持(支持普通和级联模式)</span>
* <span style="color: #006AB1;">封装常用的DatePicker、RegionPicker、DateRangePicker组件</span>

由于两端均是原生组件，性能较好，所有的其他组件均是单个wheel在js端实现，后面bug修复可以直接修改js，方便热更新。


# 集成


```
npm i @yz1311/react-native-wheel-picker@0.2.0-beta14 --save
```

## 自动集成

RN>=0.60,由于auto linking，无需操作

RN<0.60

```
react-native link @yz1311/react-native-wheel-picker
```

## 手动集成

```
Add in settings.gradle 

include ':react-native-wheel-picker'
project(':react-native-wheel-picker').projectDir = new File(settingsDir, '../node_modules/@yz1311/react-native-wheel-picker/android')

Add in app/build.gradle

compile project(':react-native-wheel-picker')

Modify MainApplication

    import com.zyu.ReactNativeWheelPickerPackage;
    ......
    
    protected List<ReactPackage> getPackages() {
        return Arrays.<ReactPackage>asList(
            new MainReactPackage(), new ReactNativeWheelPickerPackage()
        );
    }
```

# 介绍
该库(>=0.2.0)提供了多种Picker，全部均是view，相比直接提供Modal+picker的模式，单纯的picker view更加灵活,想怎么组合都行

```javascript
import WheelPicker ,{CommonPicker,DateRangePicker,DatePicker,RegionPicker} from "@yz1311/react-native-wheel-picker";
```

## 基础Picker

* <font color='red'>WheelPicker</font>: 单个的wheel，是所有其他picker的基础控件，基于原生封装(iOS是RN自带的PickerIOS，android封装自`cn.aigestudio.wheelpicker:WheelPicker`)

* <font color='red'>CommonPicker</font>: 基于`WheelPicker`封装的多Wheel picker组件，支持`parallel`(wheel间不关联)和`cascade`(wheel间关联)两种模式,基本所有单、多wheel组件均可以直接使用该组件或者在该组件上封装


## 常用Picker

* <font color='red'>DatePicker</font>: 基于`CommonPicker`封装的日期选择组件，支持日期/时间/日期+时间 三种模式

* <font color='red'>DateRangePicker</font>: 基于`CommonPicker`封装的日期段选择组件，可以选择一个时间段

* <font color='red'>RegionPicker</font>: 基于`CommonPicker`封装的地址选择组件，支持选择省市区，封装了2019/01月的省市区数据，支持自定义数据源


各组件的属性，请查看[index.d.ts](./index.d.ts)

## 例子

引用
```
import WheelPicker ,{CommonPicker,DateRangePicker,DatePicker,RegionPicker} from "@yz1311/react-native-wheel-picker";
```

* ### 单wheel

```javascript
<CommonPicker
      pickerData={['刘备', '张飞', '关羽', '赵云', '黄忠', '马超', '魏延', '诸葛亮']}
      selectedValue={['']} />
```
![](https://tva1.sinaimg.cn/large/006tNbRwgy1ga6p3v0gwpj30bz082q33.jpg)


* ### 多wheel(parallel模式)

```javascript
<CommonPicker
        pickerData={[['男','女'],['0~20岁','21~40岁','40~60岁','60岁以上']]}
        selectedValue={['']} />
```
![](https://tva1.sinaimg.cn/large/006tNbRwgy1ga6p6tuax5j30bx0860sy.jpg)


* ### 多wheel(cascade模式)
  
```javascript
<CommonPicker
        pickerData={{
            '男': ['打游戏', '电子产品', '看球'],
            '女': ['买衣服', '买鞋子', '美妆', '自拍']
        }}
        selectedValue={['男','电子产品']} />
```
![](https://tva1.sinaimg.cn/large/006tNbRwgy1ga6pbbo92bj30c0085aa9.jpg)


* ### 日期选择(默认date模式，支持date/time/datetime)

```
<DatePicker
        mode={'date'}
        />
```
![](https://tva1.sinaimg.cn/large/006tNbRwgy1ga6pgdtf5aj30bx08474n.jpg)
![](https://tva1.sinaimg.cn/large/006tNbRwgy1ga6pfdoeusj30bw081jrh.jpg)
![](https://tva1.sinaimg.cn/large/006tNbRwgy1ga6pftwfmwj30bx082t98.jpg)

* ### 日期段选择

```
<DateRangePicker

       />
```

![](https://tva1.sinaimg.cn/large/006tNbRwgy1ga6pq1oyjhj30by0ay3yu.jpg)

* ### 地址选择

```
<RegionPicker
        onPickerConfirm={(names, codes)=>{
            //names: ["上海市", "市辖区", "黄浦区"]
            //codes: ["31", "3101", "310101"]
        }}
        selectedValue={['']} />
```

![](https://tva1.sinaimg.cn/large/006tNbRwgy1ga6pskjshtj30c0084aaj.jpg)

## 截图(android/iOS)

### datePicker

![](https://tva1.sinaimg.cn/large/006tNbRwgy1ga6o9nw0lxj30u01uo762.jpg)
![](https://tva1.sinaimg.cn/large/006tNbRwgy1ga6o9xu78pj30c00lx3za.jpg)


### dateRangePicker

![](https://tva1.sinaimg.cn/large/006tNbRwgy1ga6ob3ycfcj30u01uomzf.jpg)
![](https://tva1.sinaimg.cn/large/006tNbRwgy1ga6obajcubj30c00lxaau.jpg)

### regionPicker

![](https://tva1.sinaimg.cn/large/006tNbRwgy1ga6obnr8ykj30u01uowgk.jpg)
![](https://tva1.sinaimg.cn/large/006tNbRwgy1ga6obrmhndj30c00lxaaq.jpg)