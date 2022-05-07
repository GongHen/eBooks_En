### 摘自《C和指针》
> **结构--P195** </br>
`聚合数据类型`能够同时存储超过一个的单独数据。C提供了两种类型的聚合数据类型，`数组和结构`。数组是相同类型元素的集合，它的每个元素通过下标引用或指针间接访问来选择。结构变量属于标量类型，一个结构的成员长度不同，通过名字访问。
``` 
枚举，相当于注册一个实体
typedef enum _device_ID {
    pressure_sensor_1 = 1,  // 压力传感器1
    flow_standard,          // 流量计
    led_1,                  // LED1
    led_2                   // LED2
} device_ID;
抽象出出一个通用接口
typedef struct _SENSOR {
    device_ID device_id;
    GPIO_TypeDef *SCL_gpio;
    uint16_t SCL_pin;
    GPIO_TypeDef *SDA_gpio;
    uint16_t SDA_pin;
    float sensor_val_1;
    int sensor_val_2;
    
} SENSOR;
typedef struct _SENSOR_DISPLAY {
    device_ID device_id;
    char integer_1_txt[20];
    char decimal_1_txt[20];
    char integer_2_txt[20];
    char decimal_2_txt[20];
    float* sensor_val_1;
    int* sensor_val_2;
} DISPLAY;
实例化结构
传感器引脚数组
SENSOR g_sensors[] = {
    {
        // 流量传感器
        flow_sensor,
        GPIOB,
        GPIO_Pin_6,
        GPIOB,
        GPIO_Pin_7,
        15.1,
        0
    },
    {
        // 流量计
        flow_standard,
        GPIOA,
        GPIO_Pin_0,
        GPIOA,
        GPIO_Pin_1,
        16.2,
        10
    },
};
DISPLAY g_display[] = {
    {
        // 高压测试
        pressure_sensor_1,
        "n114.val=",
        "n113.val="
    },
    {
        // 温湿度
        temp_humi_sensor,
        "n12.val=",
        "n121.val=",
        "n13.val=",
    }
};
程序调用
if (g_sensors[i].device_id == flow_standard) {
    flow_standard_measure(i);
}
if (strcmp(g_display[dis].integer_1_txt, "") != 0) {
    hmi_send_float(*g_display[dis].sensor_val_1, g_display[dis].integer_1_txt, g_display[dis].decimal_1_txt);
}
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
