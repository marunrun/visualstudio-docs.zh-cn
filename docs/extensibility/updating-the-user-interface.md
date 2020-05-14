---
title: 更新用户界面 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- user interfaces, updating
- commands, updating UI
ms.assetid: 376e2f56-e7bf-4e62-89f5-3dada84a404b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1c51ae790eb35645fbe9aec5d9c422e1051aaa69
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80698886"
---
# <a name="updating-the-user-interface"></a>更新用户接口
实现命令后，可以添加代码以使用新命令的状态更新用户界面。

 在典型的 Win32 应用程序中，可以连续轮询命令集，并在用户查看命令时调整各个命令的状态。 但是，由于[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]shell 可以承载无限数量的 VSPackages，因此大量轮询可能会降低响应能力，尤其是在托管代码和 COM 之间的内部程序集中轮询。

### <a name="to-update-the-ui"></a>更新 UI

1. 执行以下步骤之一：

    - 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.UpdateCommandUI%2A> 方法。

         可以从<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell>服务获取接口，<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>如下所示。

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

         如果 的参数<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.UpdateCommandUI%2A>是非零 （），`TRUE`则更新将同步并立即执行。 我们建议您通过此参数的 0`FALSE`（ ）， 以帮助保持良好的性能. 如果要避免缓存，`DontCache`请在 .vsct 文件中创建命令时应用标志。 但是，谨慎使用标志，否则性能可能会下降。 有关命令标志的详细信息，请参阅[命令标志元素](../extensibility/command-flag-element.md)文档。

    - 在通过在窗口中使用就地激活模型承载 ActiveX 控件的 VS 包中，使用<xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentUIManager.UpdateUI%2A>该方法可能更方便。 接口<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.UpdateCommandUI%2A>中<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell>的方法和<xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentUIManager.UpdateUI%2A><xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentUIManager>接口中的方法在功能上等效。 两者都会导致环境重新查询所有命令的状态。 通常，不会立即执行更新。 相反，更新会延迟到空闲时间。 shell 缓存命令状态以帮助保持良好的性能。 如果要避免缓存，`DontCache`请在 .vsct 文件中创建命令时应用标志。 但是，谨慎使用标志，因为性能可能会下降。

         请注意<xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentUIManager>，您可以通过在`QueryInterface`<xref:Microsoft.VisualStudio.Shell.Interop.IOleComponentUIManager>对象上调用 方法或从<xref:Microsoft.VisualStudio.Shell.Interop.SOleComponentUIManager>服务获取接口来获取接口。

## <a name="see-also"></a>请参阅
- [VSPackage 如何添加用户界面元素](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [实现](../extensibility/internals/command-implementation.md)
