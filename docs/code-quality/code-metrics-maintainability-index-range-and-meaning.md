---
title: 代码度量-可维护性索引范围和含义
ms.date: 1/8/2021
description: 了解 Visual Studio 中的代码度量的可维护性索引范围指标。
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 14bee6dcb522b7c1dd0475ca309b829a09c0d4ec
ms.sourcegitcommit: b1f7e7d7a0550d5c6f46adff3bddd44bc1d6ee1c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/11/2021
ms.locfileid: "98069517"
---
# <a name="code-metrics---maintainability-index-range-and-meaning"></a>代码度量-可维护性索引范围和含义

问：可维护性索引已被重置为介于0到100之间。 这是如何实现的？

最初计算度量值的方法如下： `Maintainability Index = 171 - 5.2 * ln(Halstead Volume) - 0.23 * (Cyclomatic Complexity) - 16.2 * ln(Lines of Code)`

使用此公式意味着它的范围从171到无限负数。  在代码倾向到0的情况下，很难维护代码，而代码之间的差异是0，一些负值则没有什么用处。  由于负数和要求尽可能清楚地保持度量值，我们决定将所有0个或更少的索引视为0，然后将171或更小的范围变基为0到100。 出于此原因，我们使用的公式是：

   `Maintainability Index = MAX(0,(171 - 5.2 * ln(Halstead Volume) - 0.23 * (Cyclomatic Complexity) - 16.2 * ln(Lines of Code))*100 / 171)`

除此之外，我们还决定了阈值的保守。  需要的是，如果索引显示为红色，则我们会说，代码有问题。  这为我们提供了以下阈值：

对于阈值，我们决定向下分解此0-100 范围80-20，使噪声级别保持较低，并且仅标记为可疑的代码。 我们使用了以下阈值：

- 0-9 = 红色
- 10-19 = 黄色
- 20-100 = 绿色
