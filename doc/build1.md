# 基本构建

<div id="ex-build-01">
  <build ref="build" :data="data" :value="value" :errors="errors" :rules="rules" :choices="choices"></build>
  <div>
    {{value}}
  </div>
</div>
<script>
var ex_build_01 = new Vue({
  el: '#ex-build-01',
  data: function () {
    var self = this
    var data = [
      {
        name: 'basic',
        title: '基本信息',
        labelWidth: 150,
        staticSuffix: '_static',
        static: false,
        fields: [
          {name: 'str1', label: '字符串1', placeholder: '请输入...', help: '帮助信息',
            info: 'info信息', required: true, rule: {type: 'email'}},
          {name: 'str2', label: '静态字符串2', static: true, required: true, format: function(v){
            return '<a href="#">' + v + '</a>'
          }},
          {name: 'select1', label: '选择1', type: 'select', required: true, options: {clearable: true,disabled: true}},
          {name: 'select2', label: '选择2', type: 'select', static: true, options: {clearable: true},
            help: '这是设置了select2_static的结果，未使用缺省机制'
          },
          {name: 'select1_1', label: '远程选择1', type: 'select', type: 'select', options: {
            clearable: true,
            filterable: true, 
            remote: true, 
            rich: true, 
            remoteMethod: function(query, callback){
              setTimeout(function(){
                if (query === 'a')
                  callback([{value:'A', label:'Test A', text: 'A'}, {value:'B', label:'Test B', text: 'B'}, {value:'C', label:'Test C', text: 'C'}])
                else
                  callback([{value:'D', label:'Test D', text: 'D'}, {value:'E', label:'Test E', text: 'E'}, {value:'F', label:'Test F', text: 'F'}])
                }, 1000)
              }
            }
          },
          {name: 'select3', label: '选择3', type: 'select', required: true, multiple: true, options: {choices: [
            {label:'选项一', value: 'A'},
            {label:'选项二', value: 'B'},
            ],
            onChanging: function(value, selected) {
              if (value === 'A' && !selected) {
                self.$Message.info("Can't removed")
                return false
              }
              return true
            }},
          },
          {name: 'select4', label: '选择4', type: 'select', multiple: true, static: true, options: {choices: [
            {label:'选项一', value: 'A'},
            {label:'选项二', value: 'B'},
            ]}
          },
          {name: 'radio1', label: '选择5', type: 'radio', required: true, options: {choices: [
            {label:'选项一', value: 'A'},
            {label:'选项二', value: 'B'},
            ]}
          },
          {name: 'radio2', label: '选择6', type: 'radio', static: true, options: {choices: [
            {label:'选项一', value: 'A'},
            {label:'选项二', value: 'B'},
            ]}
          },
          {name: 'checkboxgroup1', label: '选择7', type: 'checkboxgroup', multiple: true, required: true, options: {choices: [
            {label:'选项一', value: 'A'},
            {label:'选项二', value: 'B'},
            ]}
          },
          {name: 'checkboxgroup2', label: '选择8', type: 'checkboxgroup', static: true, options: {choices: [
            {label:'选项一', value: 'A'},
            {label:'选项二', value: 'B'},
            ]}
          },
          {name: 'checkbox1', label: '选择9', type: 'checkbox', required: true},
          {name: 'checkbox2', label: '选择10', type: 'checkbox', static: true},
          {name: 'text1', label: '文本1', type: 'text', required: true, rule:{max:20}, help: '最多输入20个汉字'},
          {name: 'text2', label: '文本2', type: 'text', static: true, rule:{max:20}, help: '最多输入20个汉字'},
          {name: 'date1', label: '日期1', required: true, type: 'date'},
          {name: 'date2', label: '日期2', type: 'date', static: true},
          {name: 'date3', label: '日期1', required: true, type: 'datetime'},
          {name: 'date4', label: '日期2', type: 'datetime', static: true},
          {name: 'daterange1', label: '日期范围1', required: true, type: 'datepickerrange', options: {type: 'month'}, rule: {type: 'array'}},
          {name: 'daterange2', label: '日期范围2', required: true, type: 'datepickerrange', options: {type: 'year'}, rule: {type: 'array'}},
          {name: 'tree1', label: '树选择', required: true, type: 'treeselect', multiple: true, options: {
            checkStrictly: true,
            onlyLeaf: false,
            choices:
            [ {
                  id: 'fruits',
                  title: 'Fruits',
                  children: [ {
                    id: 'apple',
                    title: 'Apple',
                  }, {
                    id: 'grapes',
                    title: 'Grapes',
                  }, {
                    id: 'pear',
                    title: 'Pear',
                  }, {
                    id: 'strawberry',
                    title: 'Strawberry',
                  }, {
                    id: 'watermelon',
                    title: 'Watermelon',
                  } ],
                }, {
                  id: 'vegetables',
                  title: 'Vegetables',
                  children: [ {
                    id: 'corn',
                    title: 'Corn',
                  }, {
                    id: 'carrot',
                    title: 'Carrot',
                  }, {
                    id: 'eggplant',
                    title: 'Eggplant',
                  }, {
                    id: 'tomato',
                    title: 'Tomato',
                  } ],
                } ]
              }
          },
          {name: 'switch', label: '开关', type: 'i-switch'},
          {name: 'slider', label: '滑块', type: 'Slider', required: true, rule: {type: 'number'}},
          {name: 'input1', label: '输入', type:'Input', options: {search: true, "enter-button": '查询'},
            on: {'on-search': function () {
              self.$Message.info('on-search')
            },
            'on-focus': function () {
              self.$Message.info('on-focus')
            }}
          }
        ],
        layout: [
          ['str1', 'str2'],
          ['select1', 'select2'],
          [{name: 'select1_1', clospan: 12}],
          ['select3', 'select4'],
          ['radio1', 'radio2'],
          ['checkboxgroup1', 'checkboxgroup2'],
          ['checkbox1', 'checkbox2'],
          ['text1'],
          ['text2'],
          ['date1', 'date2'],
          ['date3', 'date4'],
          ['daterange1', 'daterange2'],
          ['tree1'],
          ['switch', 'slider'],
          ['input1']
        ],
        boxComponent: 'Box',
        boxOptions: {widthBorder: false, headerClass: 'primary'},
        buttons: {
          items: [
            [{label: '查看结果', type:'primary', onClick: function(target, data){
                console.log(target, data)
              }
            }],
            [{label: '校验', type:'primary', onClick: function(target, data){
                //target.validate(self.save) 旧的写法，使用回调
                //以下为新的写法，使用promise
                target.validate().then(function(){
                  self.save()
                }).catch(function(error){
                  self.save(error)
                })
              }
            }],
            [{label: '重置', type:'info', onClick: function(target, data){
                target.reset()
              }
            }],
            [{label: '合并出错结果', type:'info', onClick: function(target, data){
                self.errors = {select1: '这是合并后的错误'}
              }
            }],
            [{label: '更新select1-2 choices', type:'info', onClick: function(target, data){
                target.fields.select1.options.choices = [
                  {label:'选项A', value: 'A'},
                  {label:'选项B', value: 'B'},
                  {label:'选项C', value: 'C'}
                ]
                target.fields.select2.options.choices = [
                  {label:'选项A', value: 'A'},
                  {label:'选项B', value: 'B'},
                  {label:'选项C', value: 'C'}
                ]
              }
            }],
            [{label: '提交测试', type:'info', name: 'submit', onClick: function(target, data){
                console.log(this)
                this.disabled = true
                this.btns.submit.loading = true
                var self = this
                setTimeout(function () {
                  self.btns.submit.loading = false
                  self.disabled = false
                }, 5000)
              }
            }]
          ],
          size: ''
        }
      },
      {
        name: 'basic',
        title: '',
        labelWidth: 150,
        staticSuffix: '_static',
        fields: [
          {name: 'str1', label: '字符串1', placeholder: '请输入...', help: '帮助信息',
            info: 'info信息', required: true, rule: {type: 'email'}},
        ],
        layout: [
          ['str1']
        ],
        boxComponent: ''
      }
    ]
    return {
            data:data,
            value: {
              str1: 'email@gmail.com',
              str2: 'aaa',
              select1: 'A',
              select2_static: '静态结果',
              select1_1: {label: '选择X', value: 'X'},
              select3: ['A', 'B'],
              select4: ['A', 'B'],
              radio2: 'A',
              checkboxgroup2: ['A', 'B'],
              checkbox2: 'B',
              text1: 'Line 1\nLine 2',
              text2: 'Line 3\nLine 4\nLine 5\nLine 6\nLine 7\nLine 8',
              date2: '2017-12-12',
              date4: '2017-12-12 12:01:28',
              tree1: ['apple', 'grapes']
            },
            choices: {
                select1: [
                  {label:'选项一', value: 'A'}
                ]
            },
            errors: {},
            rules: {
              str1: function(rule, value, callback, source, options) {
                if (value !== 'abc@gmail.com') {
                  callback (new Error('邮件地址必须为 abc@gmail.com'))
                } else {
                  callback()
                }
              }
            }
          }
  },
  methods: {
    save: function(error) {
      if (error) {
        this.$Message.error(error)
      } else {
        this.$Message.info('saved')
      }
    }
  },
  mounted: function () {
    /* var self = this
    setTimeout(function () {
      var c = [
        {label:'选项一', value: 'A'},
        {label:'选项二', value: 'B'},
        {label:'选项三', value: 'C'}
      ]
      self.$set(self.choices, 'select1', c)
    }, 1000) */
  }
})
</script>


## 参数说明

| 属性 | 说明 | 缺省值 |
|-----|-----|-------|
| data | Build参数，结构为一个Object，详细格式见下面 |  |
| labelWidth | 标签宽度 | 150px |
| staticSuffix | 静态字段后缀，当字段定义为static时，缺省先找形式为 name_suffix 的值 | '_static' |
| value | 传入的数据 | {} |
| errors | 错误信息，方便从外部传入。key为字段名 | {} | 
| rules | 单独定义的校验规则。key为字段名。它是在字段上定义的rule的一个补充 | {} |
| choices | select字段的choices值。方便从外部传入 | {} |

## 方法说明

| 方法名 | 说明 | 返回值 |
|----------|-----|------|
| validate | 对Build的数据进行校验。支持回调模式 `validate(callback)` ,其中 `callback(error)` ，如果error为undefined时表示成功，error有值时，为最早一个出错信息。promise模式，可以在 `then()` 或 `catch((error)=>{})` 中继续处理成功或出错。| Promoise |
| loadData | 装入数据，可用于刷新 | Promise 或 无 |

