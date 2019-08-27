---
title: PTVS 入门：调试 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-python
ms.topic: conceptual
ms.assetid: 82803559-1d60-4c57-98fb-2dc1e0182b42
caps.latest.revision: 5
author: kraigb
ms.author: kraigb
manager: jillfra
ms.openlocfilehash: b636dd4f3a5c5265231898573bfdf52de2dff84e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68197716"
---
# <a name="getting-started-with-ptvs-debugging"></a>PTVS 入门：调试
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 交互式调试器可轻松诊断并解决 Python 代码中的问题。  
  
 你可以在很短的 [youtube 视频](https://www.youtube.com/watch?v=bO7wpzgy74A&list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff&index=4)中观看这些说明。  
  
 在上一个入门主题中，你创建一个空的 Python 应用程序项目，并在 PythonApplication1.py 中输入了以下代码：  
  
```python  
from math import sin, cos, radians  
import sys  
  
def make_dot_string(x):  
    return ' ' * int(10 * cos(radians(x)) + 10) + 'o'  
  
assert make_dot_string(90) == "          o"  
assert make_dot_string(180) == "o"  
  
def main():  
    for i in range(10000000):  
        s = make_dot_string(i)  
        print(s)  
  
if __name__ == "__main__":  
    sys.exit(int(main() or 0))  
```  
  
 通常，在处理 Visual Studio 中的代码时，按 F5 来开始运行代码。  此命令生成需要生成的项目的任何部分，并开始在调试器下运行代码。  若不使用调试器，可以按 Ctrl+F5 生成和启动代码。  若使用调试器，代码运行速度会稍微变慢，但调试功能发挥很好。  
  
 启动代码的另一种方法是使用“单步执行”命令（通常绑定到 F11）。  它与 F5 的功能很类似，但会在每个语句处暂停执行。  如果想要在某一点中断该程序，可以按代码编辑器中左边距的左侧指针按钮来设置断点。  按 F5 时，程序的执行将中断，或者停在断点行处。  “调试”菜单具有多个可用于单步执行的选项，例如逐过程执行函数调用 (F10)、单步执行函数调用 (F11) 或跳过函数末尾 (shift-F11)。  
  
 当在调试器中中断时，还可以进行多个操作。  “局部变量”窗口显示局部变量的当前值。  单步执行代码时，局部变量将自动显示更新。  “自动”窗口显示执行停止的当前行附近的变量。  可在“监视”窗口键入每次执行停止时调试器自动更新的任何 Python 表达式。  还可以将指针悬停在“编辑器”窗口中的变量，以查看弹出窗口中显示的变量值，并且此数据提示显示允许检查对象。  一些数据类型（例如带 HTML、XML 或 JSON 等特殊格式的字符串）拥有可从数据提示显示访问的特殊可视化工具。  
  
 “调用堆栈”窗口显示引向调试器停止时所在的的当前语句的挂起函数调用。  可以选择不同的堆栈帧（调用堆栈中的行）跳转到代码将每个函数中继续执行、查找变量值等的位置。  
  
 你可以在很短的 [youtube 视频](https://www.youtube.com/watch?v=bO7wpzgy74A&list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff&index=4)中观看这些说明。  
  
## <a name="see-also"></a>另请参阅  
 [Wiki 文档](https://github.com/Microsoft/PTVS/wiki/Debugging)   
 [PTVS 入门和深入了解视频](https://www.youtube.com/playlist?list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff)
