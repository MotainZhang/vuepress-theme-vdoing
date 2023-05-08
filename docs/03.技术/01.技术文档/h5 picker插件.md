# 介绍

用于angularJS h5页面 类似于小程序picker pickerView组件（城市级联选择，日期选择等等）

# 代码演示

## 城市级联选择 二级 三级都可以

```
 new IosSelect(2,
  [省份数据，市级数据.....],
  {
	title: '',
	headerHeight: 50,
	itemHeight: 40,
	itemShowCount: 7,
	relation: [1, 1],
	showAnimate: true,
	oneLevelId:,
	twoLevelId: ,
	callback: function (selectOneObj, selectTwoObj) {

	},
	fallback: function () {

	}
 });
```

# 日期选择 年月日 年月日时分秒都可以

```
new IosSelect(3,
  [年份数据，月份数据，日期数据],
  {
	title: '',
	headerHeight: 50,
	itemHeight: 40,
	itemShowCount: 7,
	showAnimate: true,
	showLoading: true,
	oneLevelId:,
	twoLevelId:,
	threeLevelId: ,
	callback: function (selectOneObj, selectTwoObj, selectThreeObj) {

	},
	fallback: function () {

	}
  });
```

# Props

| 参数 | 说明 | 类型 | 默认值 |
| --- | --- | --- | --- |
| level | 数据的层级，最多支持6层 | number | 1 |
| data | 层级数据，二维数组 | Array | - |
| title | 标题 | String | - |
| sureText | 确定 | String | 确定 |
| closeText | 取消 | String | 取消 |
| itemHeight | 每一项高度 | number | 35 |
| itemShowCount | 组件展示的项数，可选项，可选3,5,7,9 | number | 7 |
| headerHeight | 组件标题栏高度 | number | 44 |
| cssUnit | 元素css尺寸单位，可选项，可选px或者rem | String | px |
| addClassName | 组件额外类名，用于自定义样式，可选项 | String | - |
| relation | [oneTwoRelation, twoThreeRelation, threeFourRelation, fourFiveRelation, fiveSixRelation] 可选项。如果数据是数组(非方法)，各级选项之间通过parentId关联时，需要设置；如果是通过方法获取数据，不需要该参数。 | Array | [0, 0, 0, 0, 0] |
| oneLevelId - sixLevelId | 1-6级默认数据，用于默认选中 | String | - |
| showLoading | 展示加载动画 | boolean | false |
| showAnimate | 展示入场，退场动画 | boolean | false |

# Events

| 事件名 | 说明 | 参数 |
| --- | --- | --- |
| IosSelectCreated | 组件创建完毕事件 |  |
| IosSelectDestroyed | 组件销毁事件 |  |

```
window.addEventListener('IosSelectCreated', function(e) {
	console.log(e);
});
```

```
window.addEventListener('IosSelectDestroyed', function(e) {
	console.log(e);
});
```

#
