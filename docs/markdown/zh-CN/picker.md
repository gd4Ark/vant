## Picker 选择器

### 使用指南
``` javascript
import { Picker } from 'vant';

Vue.component(Picker.name, Picker);
```

### 代码演示


#### 基础用法

```html
<van-picker :columns="columns" @change="onChange" />
```

```javascript
export default {
  data() {
    return {
      columns: ['杭州', '宁波', '温州', '嘉兴', '湖州']
    };
  },
  onChange(picker, value, index) {
    Toast(`当前值：${value}, 当前索引：${index}`);
  }
};
```

#### 禁用选项
选项可以为对象结构，通过设置 disabled 来禁用该选项

```html
<van-picker :columns="columns" />
```

```javascript
export default {
  data() {
    return {
      columns: [
        { text: '杭州', disabled: true },
        { text: '宁波' },
        { text: '温州' }
      ]
    };
  }
};
```

#### 展示顶部栏

```html
<van-picker
  showToolbar
  :title="标题"
  :columns="columns"
  @cancel="onCancel"
  @confirm="onConfirm"
/>
```

```javascript
export default {
  data() {
    return {
      columns: ['杭州', '宁波', '温州', '嘉兴', '湖州']
    }
  },
  methods: {
    onConfirm(value, index) {
      Toast(`当前值：${value}, 当前索引：${index}`);
    },
    onCancel() {
      Toast('取消');
    }
  }
};
```

#### 多列联动

```html
<van-picker :columns="columns" @change="onChange" />
```

```javascript
const citys = {
  '浙江': ['杭州', '宁波', '温州', '嘉兴', '湖州'],
  '福建': ['福州', '厦门', '莆田', '三明', '泉州']
};

export default {
  data() {
    return {
      columns: [
        {
          values: Object.keys(citys),
          className: 'column1'
        },
        {
          values: citys['浙江'],
          className: 'column2',
          defaultIndex: 2
        }
      ]
    };
  },
  methods: {
    onChange(picker, values) {
      picker.setColumnValues(1, citys[values[0]]);
    }
  }
};
```

### API

| 参数 | 说明 | 类型 | 默认值 | 可选值 |
|-----------|-----------|-----------|-------------|-------------|
| columns | 对象数组，配置每一列显示的数据 | `Array` | `[]` | - |
| showToolbar | 是否显示顶部栏 | `Boolean` | `false` | - |
| title | 顶部栏标题 | `String` | `''` | - |
| itemHeight | 选项高度 | `Number` | `44` | - |
| visibileColumnCount | 可见的选项个数 | `Number` | `5` | - |
| valueKey | 选项对象中，文字对应的 key | `String` | `text` | - |

### Columns 数据结构
当传入多列数据时，`columns`为一个对象数组，数组中的每一个对象配置每一列，每一列有以下`key`

| key | 说明 |
|-----------|-----------|
| values | 列中对应的备选值 |
| defaultIndex | 初始选中项的索引，默认为 0 |
| className | 为对应列添加额外的`class` |

### Picker 实例
在`change`事件中，可以获取到`picker`实例，通过实例方法可以灵活控制 Picker 内容

| 函数 | 说明 |
|-----------|-----------|
| getValues() | 获取所有列选中的值，返回一个数组 |
| setValues(values) | 设置所有列选中的值 |
| getIndexes() | 获取所有列选中值对应的索引，返回一个数组 |
| setIndexes(indexes) | 设置所有列选中值对应的索引 |
| getColumnValue(columnIndex) | 获取对应列选中的值 |
| setColumnValue(columnIndex, value) | 设置对应列选中的值 |
| getColumnIndex(columnIndex) | 获取对应列选中项的索引 |
| setColumnIndex(columnIndex, optionIndex) | 设置对应列选中项的索引 |
| getColumnValues(columnIndex) | 获取对应列中所有选项 |
| setColumnValues(columnIndex, values) | 设置对应列中所有选项 |