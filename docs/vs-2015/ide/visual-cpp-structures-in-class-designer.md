---
title: 类设计器中的 Visual C++ 结构 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- Class Designer [Visual Studio], structures
ms.assetid: bad18ab6-d956-47a6-a413-811cc26db5f5
caps.latest.revision: 15
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: ed47509467bd8691b6f81dbd52fac47cf21c3715
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65698196"
---
# <a name="visual-c-structures-in-class-designer"></a>类设计器中的 Visual C++ 结构
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

类设计器支持使用关键字 `struct` 声明的 C++ 结构。 下面是一个示例：  
  
```  
struct MyStructure  
{  
   char a;  
   int i;  
   long j;  
};  
```  
  
 若要详细了解如何使用 `struct` 类型，请参阅 [struct](https://msdn.microsoft.com/library/3c6ba273-e248-4ff1-8c69-d2abcf1263c6)。  
  
 类图中的 C++ 结构形状的外观和运行方式都与类形状相似，不同之处在于它的标签名为 **Struct**，且为方角（而不是圆角）。  
  
|代码元素|类设计器视图|  
|------------------|-------------------------|  
|`struct StructureName {};`|**StructureName**<br /><br /> 结构|  
  
## <a name="see-also"></a>请参阅  
 [使用 Visual C++ 代码（类设计器）](../ide/working-with-visual-cpp-code-class-designer.md)   
 [类和结构](https://msdn.microsoft.com/library/516dd496-13fb-4f17-845a-e9ca45437873)   
 [struct](https://msdn.microsoft.com/library/3c6ba273-e248-4ff1-8c69-d2abcf1263c6)
