Hive UDAF 

不可使用 List<Object> data = (List<Object>) partial;

必须使用
List<?> list = ListObjectInspector.getList(partial);
List<Object> fields = StructObjectInspector.getStructFieldsDataAsList(entry);

![2637602653544EACBC3DCBF12B5E228B.png](..%2Fassets%2F2637602653544EACBC3DCBF12B5E228B.png)

1. 数据序列化差异
Hive在跨节点传输数据时，可能使用二进制格式（如LazyBinary）而非原生Java对象。直接强制转换会导致反序列化失败。
2. 类型安全性
ObjectInspector明确声明了数据的物理存储格式（如PrimitiveObjectInspector对应基本类型，StructObjectInspector对应复杂结构）。
3. 兼容性保障
不同Hive版本可能修改内部数据结构，通过ObjectInspector接口访问可屏蔽底层变化。


