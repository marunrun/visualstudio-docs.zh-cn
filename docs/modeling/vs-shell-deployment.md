---
title: VS Shell 部署
ms.date: 11/04/2016
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3ca497244a806324d9d2315fa1b1b89404838ff3
ms.sourcegitcommit: 7b60e81414a82c6d34f6de1a1f56115c9cd26943
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "81444994"
---
# <a name="vs-shell-deployment"></a>VS Shell 部署

通过隔离的 shell，您可以确定需要与域特定语言交互的 Visual Studio 功能，以及该解决方案的显示方式。 有关 Visual Studio 隔离外壳的详细信息，请参阅[自定义隔离外壳](https://docs.microsoft.com/visualstudio/extensibility/customizing-the-isolated-shell)。

要将可视化工作室外壳设置为部署目标，

1. 在**Dsl 包**项目中，打开**source.extension.tt**。

2. 在`<SupportedProducts>`插入下：

   ```xml
   <IsolatedShell Version="1.0">MyIsolatedShell</IsolatedShell>
   ```

   用隔离外壳包的名称替换*My 隔离外壳*。
