---
title: 类设计器中的 Visual C++ 枚举 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- Class Designer [Visual Studio], enumerations
ms.assetid: 11e90ba1-18cd-44f8-9e26-e3746a7a19d1
caps.latest.revision: 14
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 7f967420e37d6337ce6d86cc56524f2751218f56
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72651666"
---
# <a name="visual-c-enumerations-in-class-designer"></a>类设计器中的 Visual C++ 枚举
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

类设计器支持 C++ `enum` 和范围 `enum class` 类型。 下面是一个示例：

```
enum CardSuit {
   Diamonds = 1,
   Hearts = 2,
   Clubs = 3,
   Spades = 4
};

// or...
enum class CardSuit {
   Diamonds = 1,
   Hearts = 2,
   Clubs = 3,
   Spades = 4
};

```

 类图中的 C++ 枚举形状的外观和工作原理与结构形状类似，只不过其标签显示为 **Enum** 或 **Enum class**，标签的颜色为粉色而不是蓝色，并且具有带颜色的边框左边和上边。 两种枚举形状和结构形状都具有方角。

 有关使用 `enum` 类型的更多信息，请参阅[枚举](https://msdn.microsoft.com/library/081829db-5dca-411e-a53c-bffef315bcb3)。

## <a name="see-also"></a>另请参阅
 使用[Visual C++ 代码 (类设计器) ](../ide/working-with-visual-cpp-code-class-designer.md) [枚举](https://msdn.microsoft.com/library/081829db-5dca-411e-a53c-bffef315bcb3)
