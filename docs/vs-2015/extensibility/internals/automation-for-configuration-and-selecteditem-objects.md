---
title: Configuration 和 SelectedItem 对象的自动化 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- automation [Visual Studio SDK], SelectedItem object
- automation [Visual Studio SDK], builds
ms.assetid: 120377f1-51aa-4445-b2f7-06ab7fc2b47f
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 42faf8127c1ab70d3470aa497a0cdab6058060f8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68157257"
---
# <a name="automation-for-configuration-and-selecteditem-objects"></a>Configuration 和 SelectedItem 对象的自动化
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

可以在中自动执行生成和选定的项过程 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。  
  
## <a name="automation-for-builds"></a>生成自动化  
 生成或配置具有实现时提供的自动化模型 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider> 。 有关详细信息，请参阅[了解生成配置](../../ide/understanding-build-configurations.md)。  
  
 如果创建 VSPackage 并想要控制配置选项，则必须使用自动化模型。  
  
## <a name="automation-for-selecteditem"></a>SelectedItem 自动化  
 不需要为对象提供实现， `SelectedItem` 因为 Visual Studio 包含标准实现。 不过，您可以 `SelectedItem` 根据需要实现对象。 必须实现包含接口的对象 `SelectedItem` ，并返回对 VSITEMID 设置为的方法的调用的响应 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A> <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID> 。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A>   
 [参与自动化模型](../../extensibility/internals/contributing-to-the-automation-model.md)   
 [了解生成配置](../../ide/understanding-build-configurations.md)
