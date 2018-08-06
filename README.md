## ct-adc-list-editor

列表编辑组件，适用于项目中的列表类编辑，如添加多个时间段等

## 组件示例图

[!img](https://github.com/ct-adc/ct-adc-list-editor/blob/master/block.png)
[!img](https://github.com/ct-adc/ct-adc-list-editor/blob/master/inline.png)


## 在线demo

暂无

## 功能点

1. 支持行内列表编辑和块级列表编辑
2. 编辑区域可通过slot方式定义

## 使用

从npm安装ct-adc-list-editor

```
npm install ct-adc-list-editor --save
```
在代码中使用

```
import {Inline, Block} from 'index.js';

new Vue({
    components: {
        Inline,
        Block
    },
    ...
});

```

## props

### 公共props

参数 | 说明 | 类型 | 默认值 | 可选值 | 描述 |
--- | --- | --- | --- | ---- | ---
removeButtonText | 删除按钮的文字 | String | 删除 | 任意字符串 | 删除按钮上显示的文字 |
addButtonText | 添加按钮的文字 | String | 添加 | 任意字符串 | 添加按钮上显示的文字 |
minCount | 至少几项 | Number | 0 | 任意正整数 / 0 | 列表至少要配几项 |
maxCount | 最多几项 | Number | -1(即不限制) | 任意正整数 / 0 / -1 | 列表最多可以配几项 |
initialCount | 起始有几项 | Number | 0 | 任意正整数 / 0 | 初始化时显示几项 |
step | 步长 | Number | 1 | 任意正整数 | 点一次添加按钮添加几项 |
emptyText | 为空文字 | String | 暂无数据 | 任意字符串 | 列表数量为0时显示的文字 |
removable | 是否可删 | Boolean Array | [] | 和外部数据length相同的数组，其中每一项为一个Boolean类型的值，表示该项是否可删除 | 每项是否可被删除 |

### props for Block 

针对Block类型有以下几个属性：

参数 | 说明 | 类型 | 默认值 | 可选值 | 描述 |
--- | --- | --- | --- | ---- | ---
visible | 是否可见 | Boolean Array | [] | 和外部数据length相同的数组，其中每一项为一个Boolean类型的值，表示该项是否可见 | 每项是否可见 |
maxHeight | 内容区域的最大高度 | Number | 200 | 任意正整数，请根据项目决定，设置一个内容区域的保险高度 | 单位 px |
duration | 动画持续时长 | Number | 500 | 任意正整数 | 动画持续时长 单位 ms |

### props for Inline

针对Inline类型有以下几个属性：

参数 | 说明 | 类型 | 默认值 | 可选值 | 描述 |
--- | --- | --- | --- | ---- | ---
hasHead | 是否需要头部 | Boolean | true | false/true | 是否需要头部 |


## slot

### Inline类型 

slot名称 | 说明 | 是否有默认内容 | scope |
--- | --- | --- | --- | 
head | 头部slot | 是 | index(当前项的索引)
head-form | 头部的form部分，即title的位置 | 是 | index(当前项的索引)
head-remove | 头部的删除按钮所在部分，一般不会配置相关的内容 | 是 | index(当前项的索引)
list | 列表slot | 是 | index(当前项的索引)
list-form | 列表的form部分，用来放置编辑的内容 | 是 | index(当前项的索引)
list-remove | 列表的删除按钮所在部分，一般是一个删除按钮 | 是 | index(当前项的索引)

### Block类型

slot名称 | 说明 | 是否有默认内容 | scope |
--- | --- | --- | --- | 
list | 列表slot | 是 | index(当前项的索引)
list-head | 标题栏 | 是 | index(当前项的索引)
list-head-title | 标题栏title | 是 | index(当前项的索引)
list-head-remove | 标题栏删除按钮部分 | 是 | index(当前项的索引)
list-form | 列表的form部分，用来放置编辑的内容 | 是 | index(当前项的索引)

## 方法

### add

添加项

#### 参数列表

无

返回值

无

### remove

删除项

#### 参数列表

参数 | 说明 | 类型 | 默认值 | 可选值 | 描述 |
--- | --- | --- | --- | ---- | ----
index | 删除项的索引 | Number | 无 | 数据的索引  | 数据的索引

#### 返回值

返回值 | 说明 | 类型 |
--- | --- | --- |
删除是否成功 | 删除是否成功 | Boolean


## 事件列表

事件名称 | 说明 | 回调参数 | 描述
add | 添加事件 | count：新增的条数 | 点击添加按钮时触发的事件
remove | 删除事件 | index: 删除的项的索引 | 删除数据时触发的事件

## 更新日志

[更新日志]({https://github.com/ct-adc/ct-adc-list-editor/blob/master/CHANGELOG.md})

## 外部资源依赖列表

无

