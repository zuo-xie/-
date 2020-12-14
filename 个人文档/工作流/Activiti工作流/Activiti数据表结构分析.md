### Activiti数据表结构分析

![Acticiti数据表]()

`activiti`中表数据以`act_`作为开头，然后在进行相关分类
表分类|说明
--|--
`act_evt`|
`act_ge`|`ge`代表`general`（通用）表中存储通用的数据，适用不同场景的数据
`act_hi`|`hi`代表`history`（历史）表中存储历史的流程实例，变量和任务等。
`act_procdef`|`procdef`代表`processdefine`（过程）记录流程信息
`act_re`|`re`代表`repository`（资料库）表中存储一些静态资源
`act_ru`|`ru`代表`Runtime`（运行时）记录运行时数据

####  `Activit_evt_log`

字段名|说明
--|--
`LOG_NR_`|

#### `ACT_GE_BYTEARRAY`通用的流程定义和流程资源

字段名|说明
--|--
`ID_`|自增主键
`REV_`|版本号
`NAME_`|部署文件名称
`DEPLOYMENT_ID_`|父表`ACT_RE_DEPLOYMENT`的主键
`BYTES_`|存储字节流文件
`GENERATED_`|是否由引擎生成

#### `act_ge_property`系统相关属性
字段名|说明
--|--
`NAME_`|属性名称
`VALUE_`|属性值
`REV_`|版本号


