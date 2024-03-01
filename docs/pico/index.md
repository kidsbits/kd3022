# 智能垃圾站 for kidspico

# 1. 开发环境配置



---

# 2. 下载代码

[代码下载链接](./Code.zip)

下载代码并解压存放于方便使用的地方。本课程使用的全部代码在文件夹 **3.Code_kidspico** 中。

---

# 3. 模块介绍

<span style="background:#ff0;color:#000">先设置文件路径。xxxxx</span>

## 3.1 白色LED模块

![1top](media/1top.png)

LED，即发光二极管的简称，由含镓（Ga）、砷（As）、磷（P）、氮（N）等的化合物制成。砷化镓二极管发红光，磷化镓二极管发绿光，碳化硅二极管发黄光，氮化镓二极管发蓝光。在电路及仪器中作为指示灯，或者组成文字或数字显示。

![3101](media/3101.png)

![1bottom](media/1bottom.png)

### 参数

![2top](media/2top.png)

工作电压 ：DC 3.3 ~ 5V

工作电流 ：1.5 mA（峰值2.3mA）

最大功率 ：0.07 W

控制信号 ：数字信号

尺寸 ：24 x 48 x 18 mm（不带壳）

定位孔大小 ：直径为 4.8 mm

接口 ：电话插座

![2bottom](media/2bottom.png)

### 原理

![3top](media/3top-17091966727391.png)

![3102](media/3102.png)

这是一个常用的LED模块，它采用F5-白发白LED（外观白色，显示白光）元件，元件 + 极接VCC，- 极接GND即可导通。但在 - 极和GND之间接了一个三极管，只要三极管导通，LED元件的 - 极就能接到GND，LED就能亮。

那么，如何让三极管导通呢？NPN三极管的导通条件是：Ub > Ue（锗0.2V/硅0.7V）。**S8050是一款小功率NPN型硅管**，所以他的导通条件是基极（B）电压比发射极（E）电压高 0.7V 以上。发射极已经被下拉到GND，只需要给基极一个高电平，Q1就可以导通了。

当电话插座的5脚输入一个高电平时，S8050导通，LED导通，发白光。

![3bottom](media/3bottom.png)

### 接线图

接到1![3103](media/3103.png)

### 实验代码

双击打开 Thonny 软件，在文件管理区选择代码文件所在的路径。

![3104](media/3104.png)

双击打开 3.1Light_on.py ，接着单击![1407](media/1407.png)运行代码。

![3105](media/3105.png)

```python
'''
 * Filename    : Light_on
 * Thonny      : Thonny 4.1.4
 * Auther      : http//www.keyestudio.com
'''
from machine import Pin
import time

led = Pin(11, Pin.OUT)# 构建led对象,外接LED灯连接与引脚0相连，并设置引脚0为输出模式
while True:
    led.on()     # led点亮
    time.sleep(1)# 等待1秒
    led.off()    # led熄灭
    time.sleep(1)# 等待1秒
```

### 代码说明

![5top](media/5top.png)

1. `from machine import Pin`

   MicroPython 的 machine 模块是一个用于与特定板上的硬件相关的功能的接口。该模块中的大多数函数允许实现对系统硬件块（如 CPU、定时器、总线等）的直接和不受限制的访问和控制。模块里的一些配置已经设置好了，只需导入它，然后调用。

   这句的含义是从machine模块中导入Pin函数，Pin —— 控制IO引脚。

   ![peg](media/peg.png)

   **machine.pin 类函数详解**
   
   ```python
   machine.Pin(id,mode,pull,value)
   ```


   - id ：GPIO编号，数值为0-29，如使用GPIO11则此处填写11。

   - mode ：指定引脚模式。可以是以下之一：

     ​	Pin.IN(0)，引脚配置为输入；

     ​	Pin.OUT(1)，引脚配置为（正常）输出；

     ​	Pin.OPEN_DEAIN(2)，引脚配置为开漏输出；

   - pull ：指定引脚是否连接了（弱）拉电阻，仅在输入模式下有效，可以是以下之一：

     ​	None - 无上拉或下拉电阻；

     ​	Pin.PULL_UP(1) - 上拉电阻使能；

     ​	Pin.PULL_DOWN(2) - 下拉电阻使能；

   - value ：仅对 Pin.OUT 和 Pin.OPEN_DRAIN 模式有效，并指定初始输出引脚值，否则引脚外设的状态保持不变。0为低(off)、1为高(on)。

   - Pin.on() - 设置引脚为高电平

   - Pin.off() - 设置引脚为低电平

2. `import time`

   这句的含义是导入time 模块。

3. `while True:`

   while循环函数，一般形式：

    ```python
    while 判断条件(condition)：
        执行语句(statements)……
    ```
   
   执行流程图如下：
   
   ![3106](media/3106.png)
   
   执行Gif演示：
   
   ![3107](media/3107.gif)
   
   这句的含义是在此函数下面的语句循环执行，除非True变False。  

4. `=`

   在 Python 中，变量就是变量，它没有类型。等号（=）用来给变量赋值。
   
   等号（=）运算符左边是一个变量名，等号（=）运算符右边是存储在变量中的值。

5. `led = Pin(11, Pin.OUT)`

   所以，这句的含义是构建一个连接引脚为io11，输出模式的GPIO函数，并将其值赋值给变量led。


6. `led.on()`和`led.off()`

   这两句的含义是在该引脚上分别输出1和0，实现亮和灭的效果。

7. `time.sleep(1)`

   time模块用于设置延迟时间。这句的含义是让程序在此延时1秒。

![5bottom](media/5bottom.png)

### 实验结果

![4top](media/4top.png)

​		代码上传成功后，可以看到LED灯亮1秒，灭1秒，按此规律循环亮灭。

​		单击![1413](media/1413.png)或按下键盘上的 Ctrl+C 退出程序。

![4bottom](media/4bottom.png)

---

## 3.2 单路 3V 继电器模块

![1top](media/1top.png)

在日常生活中，一般使用交流电来驱动电气设备，有时我们会用开关来控制电器。如果将开关直接连接到交流电路上，一旦发生漏电，人就有危险。从安全的角度考虑，我们特别设计了这款具有NO（常开）端和NC（常闭）端的继电器模块。

![3201](media/3201.gif)

![1bottom](media/1bottom.png)

### 参数

![2top](media/2top.png)

驱动电压 ：DC 3.3 ~ 5V 

驱动电流 ：驱动电压3.3 V时为125 mA；驱动电压5 V时为75 mA

接点容量 ：250 VAC/3A，30 VDC/3A

额定消耗功率 ：0.15 W

输入信号 ：数字信号

触电电流 ：小于 3 A

工作温度 ：-10°C ~ +50°C

控制信号 ：数字信号

尺寸 ：24 x 48 x 18 mm（不带壳）

定位孔大小 ：直径为 4.8 mm

接口 ：电话插座

![2bottom](media/2bottom.png)

### 原理

![3top](media/3top.png)

![3202](media/3202.png)

一个继电器拥有一个动触点以及两个静触点A和B。

当开关K断开时，继电器线路无电流通过，此时动触点与静触点B相接触，上半部分的电路导通。静触点B被称为常闭触点（NC）。常闭——NC（normal close）通常情况下是关合状态，即线圈未得电的情况下闭合的。

当开关K闭合时，继电器电路通过电流产生磁力，此时动触点与静触点A相接触，下半部分电路导通。静触点A被称为常开触点（NO）。常开——NO（normal open）通常情况下是断开状态，即线圈未得电的情况下断开的。

而动触点也被称为公共触点（COM）。

![3203](media/3203.png) nc no com 端子图

继电器简单来说就是一个开关，VCC表示电源正极、GND表示电源负极、IN表示信号输入脚，COM表示公共端，NC（normal close）表示常闭端，NO（normal open）表示常开端。

![3204](media/3204.png)

Q1是NPN型三极管，当S处给一个高电平时，Q1导通，继电器4脚下拉到地，继电器导通。当S处为低电平是，Q1不导通，继电器不导通。

![3bottom](media/3bottom.png)

### 接线图

接到2![3205](media/3205.png)

### 实验代码

双击打开 3.2Relay.py ，接着单击![1407](media/1407.png)运行代码。

```python
'''
 * Filename    : Relay
 * Thonny      : Thonny 4.1.4
 * Auther      : http//www.keyestudio.com
'''
from machine import Pin
import time

# 继电器接到io8，设置io8输出
relay = Pin(8, Pin.OUT)
 
# 继电器闭合，继电器上的COM和NO断开，COM和NC连接
def relay_on():
    relay(1)
 
# 继电器断开，继电器上COM和NO连接，COM和NC断开 
def relay_off():
    relay(0)
 
# 循环，继电器开一秒关一秒
while True:
    relay_on()
    time.sleep(1)
    relay_off()
    time.sleep(1)
```

### 代码说明

![5top](media/5top.png)

1. `def relay_on():`

我们在编程的过程中往往会发现，实现某一功能的代码块会被频繁地使用。如果每次使用这段代码都得复制粘贴，这会使得代码冗长而又臃肿，增大了代码的阅读难度。为了方便我们实现对代码块的复用，人们提出了函数功能。

函数的定义以关键字def开头，后面接函数名称和圆括号。括号中放入函数需要的参数。通过冒号和缩进控制函数内容。
函数的结构如下所示：

```python
def 函数名(参数):
    函数内容
```

`def relay_on():` 这句的含义是构建一个名为 *relay_on* 的函数，函数内容为 *relay(1)* ，即引脚io8输出高电平给继电器。

同理，`relay_off()` 的含义是使引脚io8输出低电平。

![5bottom](media/5bottom.png)

###  实验结果

![4top](media/4top.png)

​		代码上传成功后，继电器导通1秒，关断1秒，按此规律循环进行。

​		单击![1413](media/1413.png)或按下键盘上的 Ctrl+C 退出程序。

![4bottom](media/4bottom.png)

---

## 3.3 单路按键模块

![1top](media/1top.png)

单路按键模块，它主要由1个轻触开关组成，自带1个黄色按键帽。第二课我们学习了怎么让单片机的引脚输出一个高电平或者低电平，这节课程我们就来学习怎么读取引脚的电平。

按键模块的按键按下，单片机读取到低电平，松开按键读取到高电平。通过读取传感器上S端的高低电平，判断按键是否按下，并且在串口监视器上显示测试结果。

![1bottom](media/1bottom.png)

### 参数

![2top](media/2top.png)

工作电压 ：DC 3.3 ~ 5V 

工作电流 ：1.1 mA

最大功率  ：0.0055 W

工作温度 ：-10°C ~ +50°C

控制信号 ：数字信号

尺寸 ：24 x 48 x 18 mm（不带壳）

定位孔大小 ：直径为 4.8 mm

接口 ：电话插座

![2bottom](media/2bottom.png)

### 原理

![3top](media/3top.png)

![3301](media/3301.png)

按键有四个引脚，其中1与3相连，2与4相连。按键未被按下时，1、3与2、4是断开的。信号端S读取的电平是被4.7K的<span style="color: rgb(10, 10, 200);">上拉电阻R1</span>拉高的高电平。而当按键被按下时，1、3和2、4连通，原本上拉的1、3脚被2、4脚接的GND下拉至低电平，此时信号端S读取到低电平。即按下按键，传感器信号端S为低电平；松开按键，信号端S为高电平。

![3bottom](media/3bottom.png)

### 接线图

接到3![3302](media/3302.png)

### 实验代码

双击打开 3.3Button.py ，接着单击![1407](media/1407.png)运行代码。

```python
'''
 * Filename    : Button
 * Thonny      : Thonny 4.1.4
 * Auther      : http//www.keyestudio.com
'''
from machine import Pin
import time

button = Pin(3, Pin.IN, Pin.PULL_UP)

while True:
    if button.value() == 0:
        print('The button is pressed!')   #按下打印相应信息
    else:
        print('The button is not pressed!')
    time.sleep(0.1) #延时0.1秒
```

### 代码说明

![5top](media/5top.png)

1. `button = Pin(3, Pin.IN, Pin.PULL_UP)`

   这句的含义是构建一个连接引脚为io3，输入上拉模式的GPIO函数。

   如果使用button = Pin(3, Pin.IN)设置为输入模式而不使用输入上拉，此时引脚处于高阻抗状态，会导致不可预测的电平结果。为了确保开关断开时的读数正确，推荐使用上拉或下拉电阻。我们的模块已经使用上拉电阻R1，可以不设置输入上拉，该电阻的目的是在开关断开时将引脚拉至已知状态。通常选择一个4.7K/10 K欧姆的电阻，因为它的阻值足够低，可以可靠地防止输入悬空，同时，该阻值也要足够高，以使开关闭合时不会消耗太多电流。如果使用下拉电阻，则当开关断开时，输入引脚将为低电平；当开关闭合时，输入引脚将为高电平。如果使用上拉电阻，则当开关断开时，输入引脚将为高电平；当开关闭合时，输入引脚将为低电平。

2. `print('The button is pressed!')`

   print 输出，**默认**输出是**换行**的，如果要实现不换行需要在变量末尾加上  *,end=""*：。

   这句的含义是在Shell窗口打印出 *The button is pressed!* 。

3. ```python
   if button.value() == 0:
       print('The button is pressed!')   #按下打印相应信息
   else:
       print('The button is not pressed!')
   time.sleep(0.1) #延时0.1秒
   ```

   Python 条件语句是通过一条或多条语句的执行结果（True 或者 False）来决定执行的代码块。

   执行过程：

   ![3303](media/3303.png)

   代码执行过程：

   ![3304](media/3304.png)

   **if语句**的一般形式如下：

   ```python
   if condition_1:
       statement_block_1
   elif condition_2:
       statement_block_2
   else:
       statement_block_3
   ```

   如果 "condition_1" 为 True 将执行 "statement_block_1" 块语句。

   如果 "condition_1" 为False，将判断 "condition_2"。

   如果"condition_2" 为 True 将执行 "statement_block_2" 块语句。

   如果 "condition_2" 为False，将执行"statement_block_3"块语句。

   <span style="color: rgb(10, 10, 200);">Python 中用 **elif** 代替了 **else if**，所以if语句的关键字为：**if – elif – else**。</span>

   **<span style="color: rgb(10, 10, 200);">注意：</span>**

   1、每个条件后面要使用冒号 :，表示接下来是满足条件后要执行的语句块。

   2、使用缩进来划分语句块，相同缩进数的语句在一起组成一个语句块。

   Gif演示：

   ![3305](media/3305.gif)

   所以，这断循环的含义是：如果读取到按键的数字电平为低（LOW），在Shell窗口打印出 *The button is pressed!* ；如果读取到按键的数字电平为高（HIGH），在Shell窗口打印出 *The button is not pressed!* ，每0.1秒刷新一次。

![5bottom](media/5bottom.png)

### 实验结果

![4top](media/4top.png)

​		代码上传成功后，按下按键时，Shell窗口打印出 **The button is pressed!** ；松开按键时，Shell窗口打印出 **You loosen the button!** 。

![3306](media/3306.png)

​		单击![1413](media/1413.png)或按下键盘上的 Ctrl+C 退出程序。

![4bottom](media/4bottom.png)

---

# 4. 组合实验

## 4.1 手动照明

​		这一课，学习单路按键模块与LED模块的组合使用，实现手动照明的功能。

### 流程图

![4101](media/4101.png)

### 组装积木

![line1](media/line1.png)

**准备积木**

![41_00](media/41_00.png)

![line1](media/line1.png)

**组装步骤1**

![41_01](media/41_01.png)

![line1](media/line1.png)

**组装步骤2**

![41_02](media/41_02.png)



![41_03](media/41_03.png)

![line1](media/line1.png)

**组装步骤3**

![41_04](media/41_04.png)

![line1](media/line1.png)

**组装步骤4**

![41_05](media/41_05.png)

![line1](media/line1.png)

**组装步骤5**

![41_06](media/41_06.png)

![line1](media/line1.png)

**组装步骤6**

![41_07](media/41_07.png)

![line1](media/line1.png)

**组装步骤7**

![41_08](media/41_08.png)

![line1](media/line1.png)

**组装完成**

![41_09](media/41_09.png)

![line1](media/line1.png)

### 接线图

![4102](media/4102.png)

### 实验代码

双击打开 4.1Manual_lighting.py ，接着单击![1407](media/1407.png)运行代码。

```python
'''
 * Filename    : Manual_lighting
 * Thonny      : Thonny 4.1.4
 * Auther      : http//www.keyestudio.com
'''
from machine import Pin
import time

led = Pin(11, Pin.OUT)
button = Pin(3, Pin.IN, Pin.PULL_UP)

while True:
    if button.value() == 0:  #按下按键
        led.on()     # led点亮
    else:
        led.off()    # led熄灭
```

### 代码说明

![5top](media/5top.png)

​		循环执行：按下按键，LED灯点亮；松开按键，LED灯熄灭。

![5bottom](media/5bottom.png)

### 实验结果

![4top](media/4top.png)

​		代码上传成功后，循环执行：按下按键，LED灯点亮；松开按键，LED灯熄灭。

![4103](media/4103.gif)

![4bottom](media/4bottom.png)

---

## 4.2 自动照明

​		这一课，学习光敏电阻传感器与LED模块的组合使用，实现自动照明的功能。

### 流程图

![4201](media/4201.png)

### 组装积木

![line1](media/line1.png)

**准备积木**

![42_00](media/42_00.png)

![line1](media/line1.png)

**组装步骤1**

![42_01](media/42_01.png)

![line1](media/line1.png)

**组装步骤2**

![42_02](media/42_02.png)

![line1](media/line1.png)

**组装步骤3**

![42_03](media/42_03.png)

![line1](media/line1.png)

**组装步骤4**

![42_04](media/42_04.png)

![line1](media/line1.png)

**组装步骤5**

![42_05](media/42_05.png)

![line1](media/line1.png)

**组装步骤6**

![42_06](media/42_06.png)

![line1](media/line1.png)

**组装步骤7**

![42_07](media/42_07.png)

![line1](media/line1.png)

**组装步骤8**

![42_08](media/42_08.png)

![line1](media/line1.png)

**组装完成**

![42_09](media/42_09.png)

![line1](media/line1.png)

### 接线图

![4202](media/4202.png)

### 实验代码

双击打开 4.2Automatic_lighting.py ，接着单击![1407](media/1407.png)运行代码。

```python
'''
 * Filename    : Automatic_lighting
 * Thonny      : Thonny 4.1.4
 * Auther      : http//www.keyestudio.com
'''
from machine import Pin,ADC
import time

led = Pin(11,Pin.OUT)
Photores = ADC(27)  

while True:
    Photores_Value = Photores.read_u16()
    print('ADC Value:',Photores_Value)
    if (Photores_Value < 5000):
        led.on()
    else:
        led.off()
    time.sleep(0.1)
```

### 代码说明

![5top](media/5top.png)

**代码思路：**

​		① 首先读取光敏传感器的值。

​		② 然后循环执行：将读取到的值打印在Shell窗口并与阈值5000（阈值可以根据需求更改）对比。如果读取到的值小于5000，LED灯亮；如果读取到的值大于5000，LED灯不亮。

![5bottom](media/5bottom.png)

### 实验结果

![4top](media/4top.png)

​		代码上传成功后，光敏传感器检测环境的光强度。当光敏传感器读取值小于5000时，LED灯亮；当光敏传感器读取值大于5000时，LED灯不亮。

![4bottom](media/4bottom.png)

---

## 4.3 灯光调节

​		这一课，学习旋转电位器传感器与LED模块的组合使用，实现灯光调节的功能。

### 流程图

 ![4301](media/4301.png)

### 组装积木

![line1](media/line1.png)

**准备积木**

![43_00](media/43_00.png)

![line1](media/line1.png)

**组装步骤1**

![43_01](media/43_01.png)

![line1](media/line1.png)

**组装步骤2**

![43_02](media/43_02.png)

![line1](media/line1.png)

**组装步骤3**

![43_03](media/43_03.png)

![line1](media/line1.png)

**组装步骤4**

![43_04](media/43_04.png)

![line1](media/line1.png)

**组装步骤5**

![43_05](media/43_05.png)

![line1](media/line1.png)

**组装步骤6**

![43_06](media/43_06.png)

![line1](media/line1.png)

**组装完成。**

![43_07](media/43_07.png)

![line1](media/line1.png)

### 接线图

![4302](media/4302.png)

### 实验代码

双击打开 4.3Brightness_adjustment.py ，接着单击![1407](media/1407.png)运行代码。

```python
'''
 * Filename    : Brightness_adjustment
 * Thonny      : Thonny 4.1.4
 * Auther      : http//www.keyestudio.com
'''
from machine import Pin,ADC,PWM
import time

RP = ADC(26)
led = PWM(Pin(11))
led.freq(1000)

while True:
    RP_Value = RP.read_u16()
    print('ADC Value:',RP_Value)
    led.duty_u16(RP_Value)
    time.sleep(0.1)
```

### 代码说明

![5top](media/5top.png)

1. `from machine import Pin,ADC,PWM`

   导入PIN、ADC、PWM模块。


2. `led = PWM(Pin(11))`

   构造一个PWM函数，输出PWM的引脚是io11。

3.  `led.freq(1000)`

   设置PWM输出频率为1000Hz。

4. `led.duty_u16(RP_Value)`

   用于设置占空比。将旋转电位器传感器读取到的ADC值设置为LED模块的占空比。

**代码思路：**

​		① 首先进行初始化设置。

​		② 然后循环执行：读取旋转电位器对应通道的ADC数值，并将其打印在Shell窗口。再将该值设置为LED模块的占空比，以此达到旋转电位器控制LED灯亮的效果。

![5bottom](media/5bottom.png)

### 实验结果

![4top](media/4top.png)

​		代码上传成功后，旋转电位器的旋钮，可以看到LED的亮度随着旋钮的变化而变化。ADC值越大，LED灯越亮。

![4bottom](media/4bottom.png)

---

## 4.4 智能垃圾桶 手动模式

​		这一课，学习摇杆模块与舵机的组合使用，实现智能垃圾桶的手动模式的功能。

### 流程图

![4401](media/4401.png)

### 组装积木

![line1](media/line1.png)

**准备积木**

![44_00](media/44_00.png)

![line1](media/line1.png)

**组装步骤1**

![44_01](media/44_01.png)

![line1](media/line1.png)

**组装步骤2**

![44_02](media/44_02.png)

![line1](media/line1.png)

**组装步骤3**

![44_03](media/44_03.png)

![line1](media/line1.png)

**组装步骤4**

![44_04](media/44_04.png)

![line1](media/line1.png)

**组装步骤5**

![44_05](media/44_05.png)

![line1](media/line1.png)

**组装步骤6**

![44_06](media/44_06.png)

![line1](media/line1.png)

**组装步骤7**

![44_07](media/44_07.png)

![line1](media/line1.png)

**组装步骤8**

![44_08](media/44_08.png)

![line1](media/line1.png)

**组装步骤9**

![44_09](media/44_09.png)

![line1](media/line1.png)

**组装步骤10**

![44_10](media/44_10.png)

​		舵机安装好后，需要进行校准。首先将舵机接到主板的io19，然后通过USB线将主板接到电脑。

​		双击打开 Servo_Calibration.py ，接着单击![1407](media/1407.png)运行代码。
```python
'''
 * Filename    : Servo_Calibration
 * Thonny      : Thonny 4.1.4
 * Auther      : http//www.keyestudio.com
'''
from machine import Pin, PWM
import time

pwm = PWM(Pin(19))
pwm.freq(50)
pwm.duty_u16(4800)
```

​		校准完成后，将主板与电脑断开连接，接着可以继续安装了。

​		注意：组装时请保持垃圾桶盖面水平。

![44_11](media/44_11.png)

![line1](media/line1.png)

**组装步骤11**

![44_12](media/44_12.png)

![line1](media/line1.png)

**组装完成**

![44_13](media/44_13.png)

![line1](media/line1.png)

### 接线图

![4402](media/4402.png)

### 实验代码

​		双击打开 4.4Smart bin_Manual mode.py ，接着单击![1407](media/1407.png)运行代码。

```python
'''
 * Filename    : Smart bin_Manual mode
 * Thonny      : Thonny 4.1.4
 * Auther      : http//www.keyestudio.com
'''
from machine import Pin,PWM
import time
from ROCKER import rocker

scl = Pin(5) 
sda = Pin(4)
bus = 0
servo = PWM(Pin(19))
servo.freq(50)
snsr = rocker (bus, scl, sda)

while True:
    x,y,z = snsr.readXYZ()
    print('y:',y)
    time.sleep(0.1)
    if 0 <= y < 490:
        servo.duty_u16(1400)
    else:
        servo.duty_u16(4800)
```

### 代码说明

![5top](media/5top.png)

1. `<=`

   比较运算符，小于等于，判断左操作数是否小于等于右，返回True或False。

**代码思路：**

​		首先进行初始化设置。设置IIC的引脚，设置舵机的引脚，设置舵机的输出频率。

​		然后循环执行：

​		① 读取摇杆的键值，并每0.1秒刷新打印一次y轴的键值。

​		② 接着判断y轴的键值大于等于0且小于490是否成立（因为在组装时已将舵机校准，所以此时垃圾桶盖呈闭合状态）。

​			成立，则设置舵机的占空比为1400，舵机转动，垃圾桶盖打开。

​			不成立，设置舵机的占空比为4800，舵机转动，垃圾桶盖闭合。

![5bottom](media/5bottom.png)

### 实验结果

![4top](media/4top.png)

​		代码上传成功后，往上推摇杆，可以看到垃圾桶盖打开；松手摇杆回到初始位置，垃圾桶盖闭合，实现手动控制垃圾桶的操作。

![4403](media/4403.gif)

![4bottom](media/4bottom.png)

---

## 4.5 智能垃圾桶 自动模式

​		这一课，学习避障传感器、有源蜂鸣器模块和舵机的组合使用，实现智能垃圾桶的自动模式的功能。

### 流程图

![4501](media/4501.png)

### 组装积木

![line1](media/line1.png)

**准备积木**

![45_00](media/45_00.png)

![line1](media/line1.png)

**组装步骤1**

![45_01](media/45_01.png)

![line1](media/line1.png)

**组装步骤2**

![45_02](media/45_02.png)

![line1](media/line1.png)

**组装步骤3**

![45_03](media/45_03.png)

![line1](media/line1.png)

**组装步骤4**

![45_04](media/45_04.png)

![line1](media/line1.png)

**组装步骤5**

![45_05](media/45_05.png)

![line1](media/line1.png)

**组装步骤6**

![45_06](media/45_06.png)

![line1](media/line1.png)

**组装步骤7**

![45_07](media/45_07.png)

![line1](media/line1.png)

**组装步骤8**

![45_08](media/45_08.png)

![line1](media/line1.png)

**组装步骤9**

![45_09](media/45_09.png)

![line1](media/line1.png)

**组装步骤10**

![45_10](media/45_10.png)

​		舵机安装好后，需要进行校准。首先将舵机接到主板的io19，然后通过USB线将主板接到电脑。

​		双击打开 Servo_Calibration.py ，接着单击![1407](media/1407.png)运行代码。

```python
'''
 * Filename    : Servo_Calibration
 * Thonny      : Thonny 4.1.4
 * Auther      : http//www.keyestudio.com
'''
from machine import Pin, PWM
import time

pwm = PWM(Pin(19))
pwm.freq(50)
pwm.duty_u16(4800)
```

​		校准完成后，将主板与电脑断开连接，接着可以继续安装了。

​		注意：组装时请保持垃圾桶盖的面水平。



![45_11](media/45_11.png)

![line1](media/line1.png)

**组装步骤11**

![45_12](media/45_12.png)

![line1](media/line1.png)

**组装步骤12**

![45_13](media/45_13.png)

![line1](media/line1.png)

**组装步骤13**

![45_14](media/45_14.png)

![line1](media/line1.png)

**组装完成**

![45_15](media/45_15.png)

![line1](media/line1.png)

### 接线图

![4502](media/4502.png)

### 实验代码

​		双击打开 4.5Smart bin_Automatic mode.py ，接着单击![1407](media/1407.png)运行代码。

```python
'''
 * Filename    : Smart bin_Automatic mode
 * Thonny      : Thonny 4.1.4
 * Auther      : http//www.keyestudio.com
'''
from machine import Pin,PWM
import time

Obsensor = Pin(22,Pin.IN)
Buzzer = Pin(2,Pin.OUT)
servo = PWM(Pin(19))
servo.freq(50)

while True:
    Obsensor.value()
    if Obsensor.value() == 0: #检测到有障碍物
        Buzzer.on()           #蜂鸣器响
        servo.duty_u16(1400)  #垃圾桶盖打开
    else:                     #没有检测到障碍物
        Buzzer.off()          #蜂鸣器不响
        servo.duty_u16(4800)  #垃圾桶盖闭合
    time.sleep(0.5)
```

### 代码说明

![5top](media/5top.png)

**代码思路：**

​		首先进行初始化设置。设置避障传感器引脚，设置蜂鸣器的引脚，设置舵机的引脚，设置舵机的输出频率。

​		然后循环执行：

​		① 首先读取避障传感器的数字电平值。

​		② 判断读取到的值是否为0。

​			如果读取到的值为0，即避障传感器检测到障碍物，蜂鸣器工作，发出声响；设置舵机的占空比为1400，舵机转动，垃圾桶盖打开。

​			如果读取到的值不为0，即避障传感器没有检测到障碍物，蜂鸣器不发出声响，设置舵机的占空比为4800，舵机转动，垃圾桶盖闭合。

![5bottom](media/5bottom.png)

### 实验结果

![4top](media/4top.png)

​		代码上传成功后，要先调节避障传感器，调节详情可以返回章节3.5查看。

​		调节完毕后，将手掌放置在避障传感器前方的感应范围内，避障传感器检测到手掌，蜂鸣器发出声响，舵机转动，垃圾桶盖打开；手掌离开感应范围，避障传感器检测不到手掌，蜂鸣器停止发出声响，舵机转动，垃圾桶盖闭合。

![4503](media/4503.gif)

![4bottom](media/4bottom.png)

---

## 4.6 智能垃圾桶 跌落报警

​		这一课，学习SC7A20TR三轴加速传感器和有源蜂鸣器模块的组合使用，实现智能垃圾桶的跌落报警功能。

### 流程图

![4601](media/4601.png)

### 组装积木

![line1](media/line1.png)

**准备积木**

![46_00](media/46_00.png)

![line1](media/line1.png)

**组装步骤1**

![46_01](media/46_01.png)

![line1](media/line1.png)

**组装步骤2**

![46_02](media/46_02.png)

![line1](media/line1.png)

**组装步骤3**

![46_03](media/46_03.png)

![line1](media/line1.png)

**组装步骤4**

![46_04](media/46_04.png)

![line1](media/line1.png)

**组装步骤5**

![46_05](media/46_05.png)

![line1](media/line1.png)

**组装步骤6**

![46_06](media/46_06.png)

![line1](media/line1.png)

**组装完成**

![46_07](media/46_07.png)

![line1](media/line1.png)

### 接线图



### 实验代码



### 代码说明



### 实验结果
