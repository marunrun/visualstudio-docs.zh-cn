---
title: VS Shell 部署
ms.date: 11/04/2016
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d8793312e0ed022fc7210508efdf20a81b293f0f
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85535845"
---
# <a name="vs-shell-deployment"></a>VS Shell 部署

使用独立 shell 可以确定需要与域特定语言交互的 Visual Studio 功能，以及该解决方案应如何显示。 有关 Visual Studio 独立 shell 的详细信息，请参阅[自定义独立 shell](https://docs.microsoft.com/visualstudio/extensibility/customizing-the-isolated-shell)。

若要将 Visual Studio Shell 设置为部署目标：

1. 在**DslPackage**项目中，打开**source.extension.tt**。

2. 在 `<SupportedProducts>` insert：

   ```xml
   <IsolatedShell Version="1.0">MyIsolatedShell</IsolatedShell>
   ```

   将*MyIsolatedShell*替换为你的独立 shell 包的名称。
