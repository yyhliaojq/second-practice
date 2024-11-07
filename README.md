# second-practice
markdown study note

- ##### *编写程序时合理使用#indef 	#define	#endif 避免重复定义*

  ##                                           编写跑马灯实验-库函数

  ### <u>1</u>.<u>总引</u>

  1.首先使能GPIO时钟

  ```
  RCC_AHB1PeriphClockCmd();
  ```

  2.初始化IO口模式

  ```
  GPIO_Init();
  ```

  3.操作IO口，输出高低电平

  ```
  GPIO_SetBits();
  GPIO_ResetBits();
  ```

  ### 2.GPIO基础知识

  - 每组IO口含有10个寄存器
  - STM32F407Z有7组IO口，共有112个IO口

  ### 3.跑马灯硬件连接

  - LED0接PF9
  - LED1接PF10

  ==注==：LED灯本质是一个二极管，根据物理知识，应注意电流进出方向。

  ​       使用强上下拉，通过控制IO口高低电平的输出，使LED两端产生与否电压差，达成LED亮灭效果。

  ​        0（亮）

  ​        1（灭）

  ​      因此 GPIO输出方式为推挽输出（上拉）【开漏为外部上下拉决定】

  

  ### 4.库函数介绍

  头文件：stm32f4xx_gpio.h

  源文件：stm32f4xx_gpio.c

  二者包含了GPIO相关的定义和函数申明（因对其函数大致了解）

  - 不用的外设固件库文件可删去，节省编译时间

  #### 重要函数：

  - 1个初始化函数：

  ```
  void GPIO_Init(GPIO_TypeDef*GPIOx,GPIO_InitTypeDef*GPIO_InitStruct);
  ```

  ==注==：外设（包括GPIO）在使用前，几乎都要先使能对应的时钟【时钟使能函数都在rcc.h中】

  

  *用来设置模式，输出类型，输出速度，上下拉寄存器*

  ```
  (GPIOx_MOEDR)
  (GPIOx_OTYPER)
  (GPIOx_OSPEEDR)
  (GPIOx_PUPDR)
  ```

  - 2个读取输入电平函数

  ```
  unit8_t GPIO_ReadInputDataBit();
  unit16_t GPIO_ReadInputData();
  ```

  - 2个读取输出电平函数

  ```
  unit8_t GPIO_ReadOutputDataBit();
  unit16_t GPIO_ReadOutputData();
  ```

  - 2个常用的设置输出电平函数

  ```
  void GPIO_SetBits();//1
  void GPIO_ResetBits();//0
  ```

  ### 写跑马灯实验

