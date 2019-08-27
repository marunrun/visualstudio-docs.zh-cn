---
title: 源控件运行时详细信息 |Microsoft Docs
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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68183367"
---
# <a name="source-control-runtime-details"></a>源代码管理运行时详细信息
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

一个项目添加到源代码管理中，当用户在项目中添加文件到源代码管理，或通过自动化控制器，如向导。 项目未指定为自身很源控件下;它支持源代码管理，但必须手动添加到它。  
  
## <a name="registering-with-a-source-control-package"></a>注册到源代码管理包  
 当你的项目中的文件添加到源代码管理时，环境在调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2.SetSccLocation%2A>提供四个为 cookie 由源代码管理系统的不透明字符串。 在项目文件中存储这些字符串。 这些字符串应传递到源控件存根 （管理源代码管理包的 Visual Studio 组件） 在启动时的项目类型通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2.RegisterSccProject%2A>。 这又依次加载适当的源控制包并将转发到其实现中调用`IVsSccManager2::RegisterSccProject`。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2.RegisterSccProject%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2.SetSccLocation%2A>   
 [支持源代码管理](../../extensibility/internals/supporting-source-control.md)
