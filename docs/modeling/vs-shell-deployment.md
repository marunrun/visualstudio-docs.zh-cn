---
title: VS Shell 部署
ms.date: 11/04/2016
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 70f39dd23851a2ebc0a48afd05da54b0d8deb24a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62934305"
---
# <a name="vs-shell-deployment"></a>VS Shell 部署

独立的 shell，可以确定哪些 Visual Studio 需要与域特定语言以及如何显示该解决方案应进行交互的功能。 有关 Visual Studio 独立 shell 的详细信息，请参阅[自定义独立 Shell](https://vspartner.com/pages/vsshells)。

若要作为部署目标设置 Visual Studio Shell:

1. 在中**DslPackage**项目中，打开**source.extension.tt**。

2. 下`<SupportedProducts>`插入：

   ```xml
   <IsolatedShell Version="1.0">MyIsolatedShell</IsolatedShell>
   ```

   替换*MyIsolatedShell*与独立的 shell 包的名称。