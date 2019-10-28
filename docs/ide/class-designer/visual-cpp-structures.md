---
title: 类设计器中的 C++ 结构
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Class Designer [Visual Studio], structures
ms.assetid: bad18ab6-d956-47a6-a413-811cc26db5f5
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: 65fb4738b3124daf48b501c6db416d3803da32ec
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72748909"
---
# <a name="c-structures-in-class-designer"></a>类设计器中的 C++ 结构

类设计器支持使用关键字 `struct` 声明的 C++ 结构  。 下面是一个示例：

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

- [使用 C++ 代码](working-with-visual-cpp-code.md)
- [类和结构](/cpp/cpp/classes-and-structs-cpp)
- [struct](/cpp/cpp/struct-cpp)