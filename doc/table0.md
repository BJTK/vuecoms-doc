# 表格说明

## 基本用法

vuecoms表格是集：表格、查询条件、分页等控件于一体的控件，你可以根据需要进行设置，以决定某些特性是否启用。

```
<Grid :data="data" :value="value"></Grid>
```

表格的主要参数都放在 data(Object)中，value(Array)为对应的双向绑定的数据。

## data参数说明

| 属性参数名 | 说明 | 类型 | 缺省值 |
|----------|-----|------|------|
| columns | 表头定义，详情请参见《表头列定义说明》 | Array | 必填 |
| rowHeight | 行高 | Number | 34 |
| minColWidth | 最小列宽度 | Number | 5 |
| defaultColWidth | 缺省列宽度 | Number | 100 |
| nowrap | 是否自动换行 | Boolean | false |
| width | 表格宽度。如果为 'auto' 时， 会根据父元素宽度自动调整 | Number\|'auto'| 'auto' |
| height | 表格高度。如果为 'auto' 时，会根据内容高度自动调整 | Number\|'auto' | 'auto' |
| theme | 显示样式。目前支持： 'default', 'simple'。simple 则没有列的竖线。 | Enum | 'default' |
| checkCol | 是否显示checkbox列 | Boolean | false |
| checkColWidth | checkbox列的宽度 | Number | 30 |
| checkColTitle | checkbox列的标题 | String | '' |
| indexCol | 是否显示序号列 | Boolean | false |
| indexColWidth | 序号列的宽度 | Number | 40 |
| indexColTitle | 序号列的标题 | String | '#' |
| cellTitle | 是否将单元格内容作为title属性，这样当鼠标放上时，可以显示Tip | Boolean | true |
| idField | 表格数据名唯一字段的字段名。用于定位某一行，比如删除 | String | 'id' |
| orderField | 排序字段名 | String | 'order' |
| multiSelect | 是否多选 | Boolean | false |
| clickSelect | 点击时是否选中。如果为 false ，则只能通过checkbox来选中，所以要把 checkCol 设为 true | Boolean | false |
| selectedRowClass | 选中时的class属性，缺省为 'selected', 如果设置为空，则选中行不显示对应的class | String | selected |
| resizable | 是否可以设置表头列的宽度 | Boolean | true |
| draggable | 是否支持行拖拽 | Boolean | false |
| loadingText | 装入数据中显示的文本,支持HTML格式。 | String | '&lt;i class="icon-loading ivu-icon ivu-icon-load-c"&gt;&lt;/i&gt; Loading...' |
| url | 从后台装入数据的地址 | String | '' |
| autoLoad | 是否自动从后台装入数据 | Boolean | true |
| parseUrl | 是否自动从浏览器的URL上分析查询条件的参数 | Boolean | true |
| buttons | 表格头的按钮定义。将显示在表格左上角。具体定义格式详情参见下面的 按钮定义 | Array | [] |
| rightButtons | 表格头的按钮定义。将显示在表格右上角。具体定义格式详情参见下面的 按钮定义 | Array | [] |
| bottomButtons | 表格底的按钮定义。将显示在表格左下角。具体定义格式详情参见下面的 按钮定义 | Array | [] |
| combineCols | 单元格合并设置。它是一个二维数组。每一个数组定义了连续的表格列，当上下列的值相同时，会将上下单元格合并成一个。 | Array | [] |
| noData | 无数据时缺省显示的文本 | String | 暂无数据 |
| editMode | 编辑表格的模式。目前只支持行编辑，可以设为 'row' | String | '' |
| actionColumn | 当处于行编辑状态时，指定某列显示编辑按钮，如 "编辑", "删除" | String | '' |
| deleteRowConfirm | 当删除时，并且使用内置的删除处理时，是否在删除时要确认 | Boolean | true |
| query | 查询参数，详情参见 查询说明 | Object | {} |
| pagination | 分页展示切换 | Boolean | false |
| prev | 上一页按钮显示的文本 | String | '上一页' |
| next | 下一页按钮显示的文本 | String | '下一页' |
| first | 首页按钮显示的文本。为空时不显示 | String | '' |
| last | 最后一页按钮显示的文本。为空时不显示 | String | '' |
| start | 起始序号 | Number | 1 |
| total | 总条数。它将在后台加载数据后，由应用来根据具体值进行调整 | Number | 0 |
| pageSizeOpts | 每页显示条数设置 | Array | [10, 20, 30, 40, 50] |
| pageSize | 每页显示条数 | Number | 10 |
| tree | 是否按treegrid来显示 | Boolean | false |
| defaultExpanded | 缺省是否展表父结点 | Boolean | false |
| treeField | 显示树型结构的列名 | String | '' |
| expandField | 用于标识父结点展开状态的字段名 | String | '_expand' |
| openedIcon | 父结点打开时显示的图标类名  | String | 'ivu-icon ivu-icon-arrow-down-b' |
| closedIcon | 父结点关闭时显示的图标类名  | String | 'ivu-icon ivu-icon-arrow-right-b' |
| indentWidth | 子结点缩近的宽度 | Number | 20 |
| iconWidth | 折叠图标的宽度 | Number | 14 |
| choices | 表格中editor中type为select对应的choices值，可以直接更新它让column的editor的choices更新 | Object | {} |
| headerShow | 是否显示表头 | Boolean | true |
| multiHeaderSep | 多行表头分隔符 | String | '/' |
| hoverShow | 当鼠标移动时，是否显示hover的样式 | Boolean | true |
| checkStrictly | 当Grid为树型结构时，设置为 true 时，选择父结点不会自动选择子结点。为 false 时，选择父结点会自动联动选择子结点 | Boolean | true |


| 回调函数名 | 说明 |
|----------|-----|
| onLoadData | 装入数据回调函数，将传入 function (url, param, callback)，当树型结构时，会变为(parent(idField), row(当前结点))。其中param会包含：<br/>分页变量: pageSize(每页条数), page(当前页)<br/>排序字段: sortField(排序字段名), sortDir(排序方向asc, desc))<br/>查询变量: 这个是和query对应的。<br/><br/>callback(rows, param) callback用于在处理后返回数据。例如：callback(rows, {total: 总条数}) |
| onSelect | 在选择行前执行，返回为true，则允许选中。传入参数为 (row, flag) flag 为true表示选中，为false表示取消选中|
| onDeselect | 在取消选择行前执行，返回为true，则允许取消选中。如果不提供，则当onSelect存在时会调用onSelect。传入参数为 row |
| onCheckable | 是否显示checkbox |
| onSaveRow | 保存行时调用 function (row, callback)。当执行完毕时，需调用 callback ，格式为 callback(flag, data)。其中 flag 为 'ok' 表示成功，则data为最后的数据。 'error' 表示有错误， 则data为出错信息。 |
| onSaveCol | 保存单元格时调用 function (row, callback)。当执行完毕时，需调用 callback ，格式为 callback(flag, data)。其中 flag 为 'ok' 表示成功，则data为最后的数据。 'error' 表示有错误， 则data为出错信息。 |
| onDeleteRow | 删除行的确认 function (row, callback), callback(flag, data) |
| onRowEditRender | 行编辑对应的编辑按钮列的自定义渲染回调函数 function (h, row) h 为create函数，row为数据行。当返回 null 时，使用缺省的渲染函数，需要自行渲染时，应返回一个render调用结果，如： render('div', '本行不可编辑') |

## 表头列定义说明

| 属性参数名 | 说明 | 数据类型 | 缺省值 |
|----------|-----|------|------|
| name | 列名。不可为空。 | String |  |
| width | 列宽度。当不提供时，表示自适应宽度。 | Number | 0 |
| sortable | 是否显示排度指示。为 true 时，在字段标题右侧会显示一个图标，可以用来控制排序值。 | Boolean | false |
| align | 列的文字对齐。可选值为: 'left', 'right', 'center' | Enum | 'center' |
| hidden | 是否隐藏。可以控制某列是否显示。 | Boolean | false |
| fixed | 浮动位置。可选值为: 'left', 'right', '' | Enum | '' |
| html | 是否对内容进行转义。render不受此控制。format的结果受控制。 | Boolean | true |
| resizable | 是否可以拖拽改变宽度。| Boolean | true |
| editor | 如果可以编辑，则为编辑器的定义对象。它符合Build的字段定义规则。详情参见 Build的字段定义说明。| Object | {} |
| render | 自定义渲染函数。形式为 render: function(h, param)，其中h 为createElement函数。param为上下文参数，其值为：<br/>{<br/>value: 单元格的值<br/>column: 单元格定义对象<br/>row: 单元格所在行的数据对象<br/>grid: 所属grid对象<br/>}| Function | null |
| format | 自定义格式化函数。与render不同。render可以生成新的控件，而format只输出HTML。所以只要需要对单元格内容做文本加工的，可以使用format，如：加颜色，链接之类的。调用形式为：format: function(value, column, row)。 <br/>新增字符串形式，如 `'<a href="/view/${row.id}">${row.title}</a>'`| Function\|String | null |

## 表格按钮定义说明

表格按钮的定义和Build中的按钮定义是相同的。它是一个二维数组。每一个子数组通过 ButtonGroup 组织在一起。

每个按钮的定义说明如下：

| 属性参数名 | 说明 | 数据类型 | 缺省值 |
|----------|-----|------|------|
| label | 按钮标签 | String | 必填 |
| type | 按钮样式，可以选择：'primary', 'ghost', 'dashed', 'text', 'info', 'success', 'warning', 'error'| Enum | '' |
| shape | 形状。可以选择：'' 或 'circle' | Enum | '' |
| size | 大小。可以选择：'large', '', 'small' | Enum | '' |
| disabled | 是否禁用。 | Boolean | false |
| long | 是否长按钮 | Boolean | false |
| loading | 是否显示装入效果，为装入效果时禁用。 | Boolean | false |
| icon | 图标类型名。使用iview的图标名称 | String | '' |
| onClick | 点击时的回调函数。函数原型为 onClick: function (target, data), 其中target为表格控件本身。data为表格底层的store对象。 | Function | null |

## 表格查询配置说明

Grid支持内置的查询展示，通过定义 `query` 属性，具体格式为：

```
query: {
  fields: [
    {name: "str1", type: "string", label: "字符串1", placeholder: "请输入字符串1"},
  ],
  layout: [
    ['str1']
  ]
}
```

属性说明：

| 属性参数名 | 说明 | 数据类型 | 缺省值 |
|----------|-----|------|------|
| fields | 查询字段定义。具体的形式和Build中的字段定义一致。 | Array | 必填 |
| labelWidth | 标签宽度。 | Number | 80 |
| layout | 布局。为二维数组，如 `[['str1', 'str2'], ['str3', 'str4']]` <br/>其中每个字段是对应fields中字段的name值。除字符串类型外，还可以定义为对象，如 `{name: 'str1', colspan: 8}`，其中 `colspan` 用于定义字段的宽度。按24列计算，如果按2列按，colspan应为 12.| Array[Array] | 必填 |
| firstLineLayout | 当布局为多行时，缺省只显示第一行，则第一行展示的内容是根据layout属性的第一行来决定的。你也可以自定义第一行的布局，它将显示为紧凑模式。并且可以单独设置某个字段的宽度. | Array | 非必填 |
| showLine | 缺省显示几行条件。在布局有多行时有意义。 | Number | 1 |
| choices | 对于字段为下拉列表时，当choices为异步处理时，可以通过设置这个值来异步修改对应字段的下拉值。如：<br/>`choices: {select1: []}`| Object | 非必填 |
| submitText | 提交查询的按钮名称 | String | `'查询'` | 
| resetText | 重置查询的按钮名称。如果为空，则不显示 | String | `'重置'` | 
| parseUrl | 是否自动根据URL来解析查询字段的值。| Boolean | true |

## 表格Store方法说明

在表格底层有store对象，其中states保存了Grid所需要的变量，store本身则保存了一些常用方法，通过在Grid上定义ref，然后 this.$refs.grid.store可以调用相应的方法。下面分别进行说明：

| 方法名 | 说明 | 返回值 |
|----------|-----|------|
| selected | selected(row) <br/>判断一行是否被选中, row为要判断的行。 | true / false |
| toggle | toggle(row, force=false) <br/>切换选中/不选中状态。force为强制切换。 | 无 |
| select | select(row, force=false) <br/>选中某行。如果定义了 onSelect() 回调，则当force为false时会通用onSelect进行校验，如果onSelect返回true，则可以选中，否则不可以选中。当force为true时，不会调用onSelect方法。 | 无 |
| selectAll | selectAll(force=false) <br/>全选。 | 无 |
| deselect | dselect(row, force=false) <br/>取消选择。| 无 |
| deselectAll | deselectAll(force=false) <br/>全部取消选择。 |无 |
| getSelection | getSelection() <br/>获取选中记录的idField数组。注意，此函数会使用idField对应的字段，缺省为 'id' | Array |
| getSelectedRows | getSelectedRows() <br/>获取选中记录的对象数组 | Array |
| setSelection | setSelection (selection, force=true) <br/>设置选中行。selection为行对应的idField的数组。| 无 |
| showLoading | showLoading (loading=true, text='') <br/>显示/隐藏正在装载的信息窗。loading用于切换。text为显示的信息内容。缺省为 states.loadingText 中定义的值 | 无 |
| removeRow | removeRow (row) <br/>删除某一行。 | 无 |
| setComment| setComment (row, column, content, type='info') <br/>设置某行某单元格的注释内容。| 无 |
| removeComment | removeComment (row, column) <br/>删除某行某单元格的注释内容。 | 无 |
| setClass (row, column, name) | setClass (row, column, name) <br/>设置某行某单元格的class属性 | 无 |
| removeClass | removeClass (row, column) <br/>删除某行某单元格的class属性 | 无 |
| updateRow | updateRow(row) | 更新某行数据 | 无 |
| addRow | addRow (row, item, position='after', isChild=false) <br/>增加行。row为数据，为null或{}时为空行。item，position和isChild联用表示添加的起始位置。当isChild为true时，item表示父结点。为false时，item表示兄弟结点。对于兄弟结点，position为 'before' 时，是插在它之前。'after' 时，是插在它之后。对于父结点，'before' 是插在它的最开始的子结点的位置。'after' 是追回到所有子结点之后 | Object (新的row对象) |
| addChildRow | addChildRow(row, parent, position) <br/>它是addRow对于插入子结点的包装。| Object |
| addEditRow | addEditRow (row, parent, position, isChild=false)<br/>它和addRow类似，只不过添加之后会自动进行行编辑状态。 | Object |
| addEditChildRow | addEditChildRow (row, parent, position) <br/>添加可编辑的子结点。 | Object |
| getColumn | getColumn (name)<br/>获得指定名字的表头 | Object |
