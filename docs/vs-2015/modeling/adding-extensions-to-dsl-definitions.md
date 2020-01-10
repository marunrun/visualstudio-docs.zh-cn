---
title: 将扩展添加到 DSL 定义 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: 07e133be-92ab-4936-a02b-45d2012bd0a6
caps.latest.revision: 8
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 72c5968fccb55a265639ff05c600bd5f97a9f90a
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2020
ms.locfileid: "75852108"
---
# <a name="adding-extensions-to-dsl-definitions"></a>向 DSL 定义中添加扩展
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

DSL 定义扩展允许你创建一包扩展到域特定语言（DSL）的扩展。 在 Visual Studio 集成扩展（VSIX）中包含的 DSL 扩展可以与 DSL 相同的方式安装在用户的计算机上。 在运行时可以动态启用和禁用其他功能。 Dsl 无需显式设计为扩展，并且可以在以后或第三方设计扩展，而无需更改扩展 DSL。

 其他功能可能包括：

- 模型和表示元素的属性

- 形状和连接线的修饰器

- 类、关系、形状和连接线

- 验证约束

- 工具箱项和选项卡

  扩展 DSL 的用户可以创建并保存包含其他功能的实例的模型，并且这些用户可以读取已安装适当扩展的其他用户。 尚未安装此扩展的用户不能使用其他功能，但可以更新和保存模型，而不会丢失其他功能。

  有关此功能的示例代码和详细信息，请参阅[Visual Studio 可视化和建模 SDK](https://docs.microsoft.com/samples/browse/?redirectedfrom=MSDN-samples)网站。

## <a name="see-also"></a>请参阅
 [Visual Studio 可视化和建模 SDK](https://docs.microsoft.com/samples/browse/?redirectedfrom=MSDN-samples)
