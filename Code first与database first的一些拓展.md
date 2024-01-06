## 在code first里面通过数据库生成实体类的做法是：
1. 运行数据向导的来自数据库的code first，以生成实体类+自定义数据库引用
2. 运行以下powershell,以忽略本次提交的实体对数据库的更新
```powershell
Add-Migration #InitialCreate# –IgnoreChanges
```


* 这个表格映射最好多用一下，属性可以与表的字段的名称不同，同时migration不会因你修改了类的成员名称而删除列因此导致数据丢失了，这在生产环境里面非常值得用。
```vb
<Table("Customer")>
Partial Public Class Customer
    <Column("Id")>
    Public Property Id As Integer

    <Required>
    <Column("Name")>
    Public Property Name As String

    <Required>
    <Phone>
    <Column("Phone")>
    Public Property Phone As String

End Class
```
