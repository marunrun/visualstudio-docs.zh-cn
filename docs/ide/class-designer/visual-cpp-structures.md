---
title: 类设计器中的 Visual C++ 结构
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Class Designer [Visual Studio], structures
ms.assetid: bad18ab6-d956-47a6-a413-811cc26db5f5
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: e9b8e81ee25e081a324a8520317fa57a1314ccd0
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62975029"
---
# <a name="visual-c-structures-in-class-designer"></a>类设计器中的 Visual C++ 结构

类设计器支持使用关键字 `struct` 声明的 C++ 结构。 下面是一个示例：

```cpp
struct MyStructure
{
   char a;
   int i;
   long j;
};
```

若要详细了解如何使用 `struct` 类型，请参阅 [struct](/cpp/cpp/struct-cpp)。

类图中的 C++ 结构形状的外观和运行方式都与类形状相似，不同之处在于它的标签名为 **Struct**，且为方角（而不是圆角）。

|代码元素|类设计器视图|
|------------------| - |
|`struct StructureName {};`|**StructureName**<br /><br /> 结构|

## <a name="see-also"></a>请参阅

- [使用 Visual C++ 代码](working-with-visual-cpp-code.md)
- [类和结构](/cpp/cpp/classes-and-structs-cpp)
- [struct](/cpp/cpp/struct-cpp)