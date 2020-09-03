---
title: 源代码管理运行时详细信息 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], runtime details
ms.assetid: 1acd30e0-f98c-4bde-b9cd-4076845887df
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0bb52770557fa37a14040b686dcdfbf345a713a2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68183367"
---
# <a name="source-control-runtime-details"></a>源代码管理运行时详细信息
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

当用户将项目中的文件添加到源代码管理中，或通过自动化控制器（如向导）添加项目时，会将项目添加到源代码管理。 项目不会自行指定它处于源代码管理下;它支持源代码管理，但必须手动添加。  
  
## <a name="registering-with-a-source-control-package"></a>向源代码管理包注册  
 将项目中的文件添加到源代码管理中时，环境将调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2.SetSccLocation%2A> 以提供四个不透明字符串，由源代码管理系统用作 cookie。 将这些字符串存储在项目文件中。 这些字符串应传递到源控件存根 (Visual Studio 组件，该组件通过调用来管理源代码管理包) 在项目类型启动时 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2.RegisterSccProject%2A> 。 这反过来会加载相应的源代码管理包，并将调用转发到其实现 `IVsSccManager2::RegisterSccProject` 。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2.RegisterSccProject%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2.SetSccLocation%2A>   
 [支持源代码管理](../../extensibility/internals/supporting-source-control.md)
