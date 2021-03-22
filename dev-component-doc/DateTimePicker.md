# Refactor DateTimePicker Component

## Target

- 兼容旧版本 API
- 使用 TDD 方案
- 组件高复用
- TS

## Component

> 这里列出了所有 DateTimePicker 的所有组件

### Public Component

> 向用户公开的组件

- TimeSelect
  - 时间列表
- TimePicker
  - 两种选择波动条
  - 通过模式来选择
    - time
    - timerange
- DatePicker
  - 通过模式来改变现实效果
    - year
    - month
    - date
    - week
    - datetime
    - datetimerange
    - daterange

### Private Component

> 内部调用的组件

- Picker
  - 文本框
  - 弹出框
  - 通过模式来修改弹窗风格
    - single
    - range
- InputRange
  - 两个文本框
  - 实现区间的效果
- Time
  - 时间波选器
  - 有两种模式选择
    - 通过滚动方式
    - 通过上下按钮方式
- TimeModelRolling
  - Time 的 rolling 模式
- TimeModelButton
  - Time 的 Button 模式
- TimeRange
  - 时间区间选择器
- Year
  - 年的选择组件
- Mouth
  - 月的选择组件
- Day
  - 日的选择组件
- Date
  - 年月日的复合组件
- DateTime
  - 年月日时间的复合组件
- DateTimeRange
  - 可以选择一个区间的 DateTime
- DateRange
  - 可以选择一个区间的 Time

## Dependence

> 这里是组件之间的依赖关系的描述，如：Picker 组件必须在 Input、InputRange、Popover 完成后才能开发

- Picker
  - Input
  - InputRange
  - Popover
- Time
  - TimeModelRolling
  - TImeModelButton
- TimeRange
  - Time
  - Button
- Date
  - Year
  - Mouth
  - Day
- DateTime
  - Date
  - Time
- DateRange
  - Date
- **TimeSelect**
  - Select
- **TimePicker**
  - Time
  - TimeRange
- **DatePicker**
  - Date
  - DateTime
  - DateRange

## Tasking

### Entity DateTime

> 该实体类实现，日期时间的控制、转换、格式化输出等方法

- 实现输入一个日期时间字符串来实例化
  - [ ] constance(datetime:string|Date, template)
- 实现 年/月/日/时/分/秒 单独控制
  - [ ] setDateTime(datetime:string|number|Date|DateTime|DateTimeMeta):boolean 设置日期时间，返回是否成功
    - DateTimeMeta:{ year:number,mouth:number, date:number, hour:number, minute:number, second:number }
- 实现格式化输出
  - [ ] format(template:string):string 输入字符串模版，来格式化输出
    - 模版占位符请参考https://element.eleme.cn/#/zh-CN/component/date-picker日期格式
- 获取时间
  - [ ] getTime():string
- 获取日期
  - [ ] getDate():string
- 转为Date类型
  - [ ] toDate():Date

### Entity DateTimeMulti（待定）

> 实现多 DateTime 处理

- 实现装入 DateTime
- 实现移除 DateTime
- 实现格式化输出 DateTime 数组

### Entity DateTimeRange

> 该实体实现绑定两个 DateTime 对象，来实现时间区间的功能

- 实现使用两个 DateTime 来实例化对象
- 实现通过分隔符模版输出开始时间和结束时间
- 实现设置开始时间和结束时间

### Entity DateTimeUtils

> 该实体类要实现一些数据生成的方法

- 实现生成指定范围内的年的数据列表
  - static generateYearRange(currentYear, size):[number, number]
    - 返回一个区间[2021,2022]包含2021也包含2022
- 实现生成月的区间
  - static generateMouth():[number, number]
- 实现生成某一年的某一月的个数
  - static generateDay(year, mouth):[number, number]
- 实现生成时
  - static generateHour():[number, number]
- 实现生成分
  - static generateMinute():[number,number]
- 实现生成秒
  - static generateSecond():[number,number]
- 格式化时间
  - static format(date, template):string

### InputRange

- 实现两个文本框的输入
  - [ ] 基于`modelValue`进行数据双向绑定，实现两个文本框的输入modelValue[0]是开始的输入框内容，modelValue[1]是结束的输入框内容
    - modelValue
      - Type: string[]
  - [ ] 当 input 失去焦点的时候触发`blur`事件
  - [ ] 当 input 获得焦点后触发`focus`事件
- 实现文本选择
  - [ ] 通过`select(inputID, start, length)`方法对选中的文本框进行文本选择
    - inputID
      - Type: 'start'|'end' 分别表示开始输入框和结束输入框
- 实现手动聚焦
  - [ ] 通过`focus(inputID)`对输入框进行聚焦
- 实现自定义图标及是否显示
  - [ ] 基于`prefix-icon`实现自定义文本框前的图标
  - [ ] 基于`clear-icon`实现自定义移除图标
  - [ ] 基于`clearable`实现是否显示移除图标
- 实现输入框状态的控制
  - [ ] 基于`readonly`实现只读
  - [ ] 基于`disabled`实现禁用
  - [ ] 基于`editable`实现是否可编辑
- 实现输入框的样式控制
  - [ ] 基于`size`实现大小变更
    - size
      - Type: 'medium' | 'small' | 'mini'
  - [ ] 基于`align`实现对齐效果
    - align
      - Type: 'left' | 'center' | 'right'
- 实现空输入的时候显示的占位文本
  - [ ] 基于`start-placeholder`实现文本框 1 的内容显示
  - [ ] 基于`end-placeholder`实现文本框 2 的内容显示

### Picker

- 实现不同模式下文本框
  - [ ] 基于`model`实现文本框控制
    - mode
      - Type: 'input' | 'input-range'
- 实现自定义弹窗
  - [ ] 在点击 input 的时候弹出框
  - [ ] 基于`#default`实现自定义弹框内容

### Time/TimeModelRolling/TimeModeButton

- 实现时分秒的选择
  - [ ] 基于`modelValue`实现时间的双向绑定
    - modelValue
      - Type: string
- 实现不同模式的选择方式
  - [ ] 基于`model`实现不同模式的选择方式
    - model
      - Type: 'rolling' | 'button'
- 实现通过回撤方法来取消输入
  - [ ] 通过`undo()`方法回到保存的值
  - [ ] 通过`save()`方法来保存一个值
- 实现鼠标放到 Time 上触发的事件
  - [ ] 当鼠标放到列表上触发`hover(pos)`事件
    - pos 表示当前所在的列表位置
      - Type: 'hour' | 'minute' | 'second'
        - hour 时
        - minute 分
        - second 秒
  - [ ] 当鼠标移开之后触发`leave(pos)`事件
- 实现可选时间段控制
  - [ ] 基于selectableRange实现可以选时间段控制
    - selectableRange
      - Type: string[]
        - eg: ['11:22:00-12:33:00'] or ['11:22:00']

### TimeRange

- 实现时间区间的选择功能
  - [ ] 基于`modelValue`来双向绑定两个DateTime类型的数据
    - modelValue
      - Type: [DateTime, DateTime]
- 实现不同模式的选择方式
  - [ ] 基于`model`实现不同模式的选择方式
    - model
      - Type: 'rolling' | 'button'
- 实现通过回撤方法来取消输入
  - [ ] 通过`undo(timeID)`方法回到初始的值
    - timeID
      - Type: 'start' | 'end'
- 实现鼠标放到 Time 上触发的事件
  - [ ] 当鼠标放到列表上触发`hover(timeID, pos)`事件
    - pos 表示当前所在的列表位置
      - Type: 'hour' | 'minute' | 'second'
        - hour 时
        - minute 分
        - second 秒
  - [ ] 当鼠标移开之后触发`leave(timeID, pos)`事件

- 实现可选时间段控制
  - [ ] 基于selectableRange实现可以选时间段控制
    - selectableRange
      - Type: {start:string[],end:string[]}
        - eg: ['11:22:00-12:33:00'] or ['11:22:00']

### TimePicker

- 实现输入框的编辑状态的控制
  - [ ] 基于 `readonly` 控制是否可读
  - [ ] 基于`disabled`控制是否禁用
  - [ ] 基于`editable`控制是否可编辑
- 实现对输入框的图标控制
  - [ ] 基于`clearable` 是否显示清空图标
  - [ ] 基于`prefix-icon`实现自定义头部图标
  - [ ] 基于`clear-icon`实现自定义清空图标
- 实现输入框为空的时候占位信息
  - [ ] 基于`placeholder`实现在is-range为false的时候的输入框的占位信息
  - [ ] 基于`start-placeholder`实现在is-range为true的时候开始输入框的占位信息
  - [ ] 基于`end-placeholder`实现在is-range为true的时候结束输入框的占位信息
- 实现样式控制
  - [ ] 基于`size`实现组件大小的设置
  - [ ] 基于`align`实现对齐控制
  - [ ] 基于`arrow-control`实现时间选择弹窗的样式控制
  - [ ] 基于`popper-class`实现弹窗的样式控制
- 实现输入框的焦点控制
  - [ ] 暴露`focus`方法来聚焦
  - [ ] 基于`is-auto-focus`来实现是否自动聚焦
  - [ ] 当输入框失去焦点触发`blur`事件
  - [ ] 当输入框得到焦点触发`focus`事件
- 实现是否为时间范围选择的模式
  - [ ] 基于`is-range`来实现是否为范围选择
  - [ ] 基于`range-separator` 实现分隔符的控制
- 实现指定时间选择
  - [ ] 基于`modelValue`来数据点双向绑定
  - [ ] 选择后触发`change`事件
- 实现格式化输入与输出
  - [ ] 基于`value-format`实现格式化输入
  - [ ] 基于`picker-options`实现格式化输出并且实现可选区间的控制
    - picker-options.selectableRange 可选时间段，例如`'18:30:00 - 20:30:00'`或者传入数组`['09:30:00 - 12:00:00', '14:30:00 - 18:30:00']`
    - picker-options.format 时间格式化(TimePicker)

### 待定

## Directory

- src/components
  - ...
  - InputRange
  - Picker
  - Time
  - ...
  - TimeSelect
  - TimePicker
  - DatePicker
    - src
      - entity
        - DateTime.ts
        - DateTimeRange.ts
      - tools
        - DateTimeUtils.ts
      - DatePicker.vue
    - tests
      - entity
        - DateTime.spec.ts
        - ...
      - ...
    - types.ts
    - props.ts
    - index.js

