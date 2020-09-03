---
title: 使用存储查看器进行调试 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, store viewer
- Domain-Specific Language, store
ms.assetid: 0178db2e-ae99-4ed3-9b87-8620fa9fa8e4
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: a870c66b1c14dc6ddf3e38fb6e5be8c116be3573
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72654889"
---
# <a name="debugging-by-using-the-store-viewer"></a>使用存储查看器进行调试
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用存储区查看器，可以检查使用的 *存储* 的状态 [!INCLUDE[dsl](../includes/dsl-md.md)] 。 存储查看器将显示特定存储中的所有域模型元素，以及元素的属性和元素之间的链接。

## <a name="opening-store-viewer"></a>打开存储查看器
 在实验性生成中时 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ，在存储实例包含模型信息的断点处停止代码。 然后，在 " **即时** " 窗口中键入以下命令，打开存储查看器：

```
Microsoft.VisualStudio.Modeling.Diagnostics.StoreViewer.Show(mystore);
```

> [!NOTE]
> 必须将替换 `mystore` 为存储实例的名称。 此外，如果将命名空间添加到代码中，则可以键入命令来显示存储查看器，而无需完全限定的命名空间：
>
> `using Microsoft.VisualStudio.Modeling.Diagnostics;`
>
> `…`
>
> `StoreViewer.Show(mystore);`

 `Show`方法具有多个重载。 可以指定存储或分区的实例作为参数。

 作为替代方法，你可以将显示存储查看器的代码行放在代码中你传递给该方法的参数位于范围内的任何位置 `Show` 。 此操作在代码行作为存储内容的快照执行时显示商店查看器。

### <a name="using-store-viewer"></a>使用存储查看器
 当存储区查看器打开时，将显示无模式 Windows 窗体窗口，如下图所示。

 ![](../modeling/media/storeviewer2.png "storeviewer2") 存储查看器

 存储查看器有三个窗格：左窗格、右上窗格和右下窗格。 左窗格是存储的成员中的类型的树视图 `DomainDataDirectory` 。 如果展开分区节点并单击某个元素，则该元素的属性将显示在右上窗格中。 如果元素链接到其他元素，则其他元素将显示在右下窗格中。 如果双击右下方窗格中的某个元素，则将在左窗格中突出显示该元素。

## <a name="see-also"></a>另请参阅
 [在程序代码中导航和更新模型](../modeling/navigating-and-updating-a-model-in-program-code.md)
