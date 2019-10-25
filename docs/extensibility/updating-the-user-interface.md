---
title: 更新用户界面 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- user interfaces, updating
- commands, updating UI
ms.assetid: 376e2f56-e7bf-4e62-89f5-3dada84a404b
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bf41a41e68aa73e07bdcafe8bcdcd335fff6e6eb
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72718784"
---
# <a name="updating-the-user-interface"></a>更新用户接口
实现命令后，可以添加代码以使用新命令的状态更新用户界面。

 在典型的 Win32 应用程序中，可以对命令集进行持续轮询，并在用户查看它们时调整各个命令的状态。 但是，因为 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] shell 可以托管无限数量的 Vspackage，所以，广泛轮询可能会降低响应能力，尤其是在托管代码和 COM 之间跨互操作程序集轮询。

### <a name="to-update-the-ui"></a>更新 UI

1. 执行以下步骤之一：

    - 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.UpdateCommandUI%2A> 方法。

         可以从 <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> 服务获取 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> 接口，如下所示。

        ```csharp
        void UpdateUI(Microsoft.VisualStudio.Shell.ServiceProvider sp)
        {
            IVsUIShell vsShell = (IVsUIShell)sp.GetService(typeof(IVsUIShell));
            if (vsShell != null)
            {
                int hr = vsShell.UpdateCommandUI(0);
                Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure(hr);
            }
        }

        ```

         如果 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.UpdateCommandUI%2A> 的参数为非零（`TRUE`），则更新将以同步方式和立即执行。 建议为此参数传递零（`FALSE`），以帮助保持良好的性能。 如果要避免缓存，请在 .vsct 文件中创建命令时应用 `DontCache` 标志。 尽管如此，请谨慎使用标志，否则性能可能会降低。 有关命令标志的详细信息，请参阅[命令标志元素](../extensibility/command-flag-element.md)文档。

    - 在 Vspackage 中，通过在窗口中使用就地激活模型承载 ActiveX 控件，使用 <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentUIManager.UpdateUI%2A> 方法可能更方便。 @No__t_1 接口中的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.UpdateCommandUI%2A> 方法和 <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentUIManager> 接口中的 <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentUIManager.UpdateUI%2A> 方法在功能上是等效的。 这两种方法都会导致环境重新查询所有命令的状态。 通常不会立即执行更新。 相反，更新将推迟到空闲时间。 Shell 将缓存命令状态以帮助保持良好的性能。 如果要避免缓存，请在 .vsct 文件中创建命令时应用 `DontCache` 标志。 尽管如此，请谨慎使用标志，因为性能可能会降低。

         请注意，您可以通过对 <xref:Microsoft.VisualStudio.Shell.Interop.IOleComponentUIManager> 对象调用 `QueryInterface` 方法或从 <xref:Microsoft.VisualStudio.Shell.Interop.SOleComponentUIManager> 服务获取接口来获取 <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentUIManager> 接口。

## <a name="see-also"></a>请参阅
- [VSPackage 如何添加用户界面元素](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [实现](../extensibility/internals/command-implementation.md)