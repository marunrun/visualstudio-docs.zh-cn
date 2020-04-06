---
title: 源代码管理运行时详细信息 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], runtime details
ms.assetid: 1acd30e0-f98c-4bde-b9cd-4076845887df
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 92ce5e822ec7360b3b1a4010d250a4349443c142
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705042"
---
# <a name="source-control-runtime-details"></a>源代码管理运行时详细信息
当用户将项目中的文件添加到源代码管理或通过自动化控制器（如向导）时，项目将添加到源代码管理。 项目本身未指定它处于源代码控制之下;因此，项目本身并未指定项目处于源代码管理之下。它支持源代码管理，但必须手动添加到源代码管理中。

## <a name="registering-with-a-source-control-package"></a>注册源代码管理包
 将项目中的文件添加到源代码管理时，环境将调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2.SetSccLocation%2A>为您提供四个不透明字符串，这些字符串被源代码管理系统用作 Cookie。 将这些字符串存储在项目文件中。 在启动项目类型时，这些字符串应传递到源控制存根（管理源代码管理包的可视化 Studio 组件），通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2.RegisterSccProject%2A>启动项目类型。 这反过来加载适当的源代码管理包，并将调用转发到其实现`IVsSccManager2::RegisterSccProject`。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2.RegisterSccProject%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2.SetSccLocation%2A>
- [支持源代码管理](../../extensibility/internals/supporting-source-control.md)
