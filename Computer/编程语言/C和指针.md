### 摘自《C和指针》
> **结构--P195** </br>
`聚合数据类型`能够同时存储超过一个的单独数据。C提供了两种类型的聚合数据类型，`数组和结构`。数组是相同类型元素的集合，它的每个元素通过下标引用或指针间接访问来选择。结构变量属于标量类型，一个结构的成员长度不同，通过名字访问。
``` 
结构声明
typedef struct _DEVICE_ID {
    MessageID_t message_id;
    GPIO_TypeDef *SCL_gpio;
} DEVICE_ID;
枚举
typedef enum _MESSAGE_ID {
    ERR_DEVICE = 1;
    ERR_OPRATION;
} MessageID_t; 
```
> **结构和指针--组合使用结构和指针创建数据结构 P235** </br>
* 链表：链表(linked list)就一些包含数据的独立数据结构(通常称为节点)的集合。
