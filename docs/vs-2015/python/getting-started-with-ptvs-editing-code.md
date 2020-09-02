---
title: PTVS 入门：编辑代码 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-python
ms.topic: conceptual
ms.assetid: b412c87c-2f09-4e25-9cc8-ab54f4c44412
caps.latest.revision: 5
author: kraigb
ms.author: kraigb
manager: jillfra
ms.openlocfilehash: 2e883970b4b265b1864d53ef6e1f347160e5aeb9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62550907"
---
# <a name="getting-started-with-ptvs-editing-code"></a>PTVS 入门：编辑代码
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

PTVS 为 Python 提供高效的 Visual Studio 编辑器体验。  
  
 你可以在很短的 [youtube 视频](https://www.youtube.com/watch?v=uZGZNEyyeKs&index=3&list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff)中观看这些说明。  
  
 开始使用基本 Python 应用程序项目模板（为空）。  
  
 开始在编辑器中键入 `from … import` 行。  将显示弹出式完成列表，其中附带可用于导入的模板完整列表。  此列表根据安装的 Python 版本和库的不同而有所区别。  使用数学库作为示例。  你将注意到在键入完成列表时，相应项的筛选器中包含了键入的字符。  通过导入 `sin` 标识符完成语句。  
  
```python  
from math import sin  
  
```  
  
 编写代码时，如果使用的是未绑定但可在库中找到的标识符，PTVS 会提供弹出式快速修补程序来添加所需的适当导入语句。  例如，如果键入 `cos`，你会看到提供了“从数学导入”****。  
  
 可使用代码段生成代码。  在“编辑”菜单下，依次选择 IntelliSense 和“插入代码段”。  现在选择 "Python"，然后选择 "def"。 调用函数 `make_dot_string` 并添加一个参数 `x` 。  现在可将断言添加到文件用于测试驱动开发，此时 PTVS 已经可以在完成列表中提供新函数。  
  
```python  
assert make_dot_string(90) == '          o'  
assert make_dot_string(180) == 'o'  
  
```  
  
 现在返回到新函数，并开始编写以下正文：  
  
```python  
return " " * int(10 * cos(radians(x)) + 10) + "o"  
  
```  
  
 此时 PTVS 假定参数是一个整数，因为 PTVS 已分析了此函数的调用站点。   还需要使用快速修补程序导入 `radians`。  
  
 通过在顶级键入 `main`、调用智能标记 UI 并使用选项卡选择“def main ….”，使用另一个代码段创建主块  编写一个基本循环来调用 `make_dot_string`。  如果按句号并查看提供的完成功能，会发现 PTVS 知道函数返回了字符串。  此类型信息将在整个程序中流动，因此无论你的值最后停在何处，我们都可以提供工具提示和完成功能来帮助你更好地了解和编写代码。  
  
 若要打印，请添加调用并应拥有一个与以下类似的主体：  
  
```python  
def main ():  
    for i in range(10000000):  
        s = make_dot_string(i)  
        print(s)  
```  
  
 如果按 F5，代码将在 cmd.exe 窗口中运行，并且将显示来回振荡的圆点。  
  
 你可以在很短的 [youtube 视频](https://www.youtube.com/watch?v=uZGZNEyyeKs&index=3&list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff)中观看这些说明。  
  
## <a name="see-also"></a>另请参阅  
 [Wiki 文档](https://github.com/Microsoft/PTVS/wiki/Editor-Features)   
 [PTVS 入门和深入了解视频](https://www.youtube.com/playlist?list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff)
