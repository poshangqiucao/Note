# 开发常用注解

* @RequestParam(value=”参名”,required=”true/false”,defaultValue=””)

  接收/path/?name=xx&sex=man，也就是查询字符串

* @PathVariable接收请求url中的路径值

* @RequiredArgsConstructor 生成带有必需参数的构造函数

* @NotEmpty :不能为null，且Size>0

* @NotNull:不能为null，但可以为empty,没有Size的约束

* @NotBlank:只用于String,不能为null且trim()之后size>0

* @JsonFormat(pattern="yyyy-MM-dd",timezone = "GMT+8")

* @DateTimeFormat(pattern = "yyyy-MM-dd")  要是前后到后台的时间格式的转换

* @TableLogic(value="原值",delval="改值")   在字段上加上这个注解再执行BaseMapper的删除方法时，删除方法会变成修改

* 