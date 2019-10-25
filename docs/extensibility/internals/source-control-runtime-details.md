---
title: 源代码管理运行时详细信息 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], runtime details
ms.assetid: 1acd30e0-f98c-4bde-b9cd-4076845887df
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1d2469bc25fabd9659e09d6ca841ebc44a743cca
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72723411"
---
# <a name="source-control-runtime-details"></a>源代码管理运行时详细信息
当用户将项目中的文件添加到源代码管理中，或通过自动化控制器（如向导）添加项目时，会将项目添加到源代码管理。 项目不会自行指定它处于源代码管理下;它支持源代码管理，但必须手动添加。

## <a name="registering-with-a-source-control-package"></a>向源代码管理包注册
 将项目中的文件添加到源代码管理中时，环境将调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2.SetSccLocation%2A> 以提供四个不透明字符串，由源代码管理系统用作 cookie。 将这些字符串存储在项目文件中。 在启动项目类型时，应通过调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2.RegisterSccProject%2A> 将这些字符串传递到源控件存根（用于管理源代码管理包的 Visual Studio 组件）。 这反过来会加载相应的源代码管理包，并将调用转发到 `IVsSccManager2::RegisterSccProject` 的实现。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2.RegisterSccProject%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2.SetSccLocation%2A>
- [支持源代码管理](../../extensibility/internals/supporting-source-control.md)