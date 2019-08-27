---
title: 更新用户界面 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- user interfaces, updating
- commands, updating UI
ms.assetid: 376e2f56-e7bf-4e62-89f5-3dada84a404b
caps.latest.revision: 42
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: db5be965119d1564f2a4bf8a15892af7142663e0
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68186361"
---
# <a name="updating-the-user-interface"></a>更新用户接口
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

实现命令后，可以添加代码以使用新命令的状态更新用户界面。  
  
 在典型的 Win32 应用程序，可以持续轮询设置的命令和可调整单个命令的状态，用户查看它们。 但是，因为[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]shell 可以托管无限的数量的 Vspackage，广泛轮询可能会降低响应能力，尤其在托管的代码和 COM 之间的互操作程序集之间轮询  
  
### <a name="to-update-the-ui"></a>若要更新 UI  
  
1. 执行以下步骤之一：  
  
    - 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.UpdateCommandUI%2A> 方法。  
  
         <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell>接口可以获取从<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>服务，按如下所示。  
  
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
  
         如果参数的<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.UpdateCommandUI%2A>不为零 (`TRUE`)，则将以同步方式并立即执行更新。 我们建议您传递零 (`FALSE`) 为此参数，以帮助保持良好的性能。 如果你想要避免缓存，应用`DontCache`标志时在.vsct 文件中创建命令。 不过，请谨慎使用标志或可能会降低性能。 有关命令标志的详细信息，请参阅[Command Flag 元素](../extensibility/command-flag-element.md)文档。  
  
    - 在 Vspackage 中的 ActiveX 控件承载在窗口中使用就地激活模型，可能会更方便地使用<xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentUIManager.UpdateUI%2A>方法。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.UpdateCommandUI%2A>中的方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell>接口并<xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentUIManager.UpdateUI%2A>中的方法<xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentUIManager>接口在功能上等效。 同时会导致环境以重新查询所有命令的状态。 通常情况下，不立即执行更新。 相反，更新推迟到空闲时间。 在 shell 缓存命令状态来帮助保持良好的性能。 如果你想要避免缓存，应用`DontCache`标志时在.vsct 文件中创建命令。 不过，使用标志谨慎因为可能会降低性能。  
  
         请注意，你可以获取<xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentUIManager>接口通过调用`QueryInterface`方法<xref:Microsoft.VisualStudio.Shell.Interop.IOleComponentUIManager>对象，或通过获取从接口<xref:Microsoft.VisualStudio.Shell.Interop.SOleComponentUIManager>服务。  
  
## <a name="see-also"></a>请参阅  
 [Vspackage 如何添加用户界面元素](../extensibility/internals/how-vspackages-add-user-interface-elements.md)   
 [实现](../extensibility/internals/command-implementation.md)
