---
title: 如何：解决服务问题 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: troubleshooting
helpviewer_keywords:
- services, troubleshooting
ms.assetid: 001551da-4847-4f59-a0b2-fcd327d7f5ca
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8bfbe4b11c22d6cfd147783f9fb662843cf57fe9
ms.sourcegitcommit: 9a7fb8556a5f3dbb4459122fefc7e7a8dfda753a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/27/2020
ms.locfileid: "87234947"
---
# <a name="how-to-troubleshoot-services"></a>如何：排除服务故障
尝试获取服务时可能会出现几个常见问题：

- 未向注册服务 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。

- 服务由接口类型而不是服务类型请求。

- 请求服务的 VSPackage 尚未被放置。

- 使用了错误的服务提供商。

  如果无法获取请求的服务，则对的调用将 <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> 返回 null。 请求服务后，应始终测试 null：

```csharp
IVsActivityLog log =
    GetService(typeof(SVsActivityLog)) as IVsActivityLog;
if (log == null) return;
```

## <a name="to-troubleshoot-a-service"></a>解决服务问题

1. 检查系统注册表，以查看是否已正确注册该服务。 有关详细信息，请参阅[如何：提供服务](../extensibility/how-to-provide-a-service.md)。

    以下 *.reg*文件片段显示了如何注册 SVsTextManager 服务：

   ```
   [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\<version number>\Services\{F5E7E71D-1401-11d1-883B-0000F87579D2}]
   @="{F5E7E720-1401-11d1-883B-0000F87579D2}"
   "Name"="SVsTextManager"
   ```

    在上面的示例中，版本号是的版本 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ，例如12.0 或14.0，密钥 {F5E7E71D-1401-11d1-883B-0000F87579D2} 是服务的服务标识符（SID） SVsTextManager，默认值 {F5E7E720-1401-11d1-883B-0000F87579D2} 是文本管理器 VSPackage 的包 GUID，它提供服务。

2. 调用 GetService 时，请使用服务类型，而不是接口类型。 从请求服务时 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ，从 <xref:Microsoft.VisualStudio.Shell.Package> 类型中提取 GUID。 如果满足以下条件，则将找不到服务：

   1. 接口类型将传递给 GetService，而不是服务类型。

   2. 未将任何 GUID 显式分配给接口。 因此，系统会根据需要创建对象的默认 GUID。

3. 确保请求该服务的 VSPackage 已被放置。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]在构造 VSPackage 并在调用之前，站点 <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> 。

    如果 VSPackage 构造函数中有需要服务的代码，请将其移动到 `Initialize` 方法。

4. 请确保使用正确的服务提供商。

    并非所有服务提供商都都一样。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]传递到工具窗口的服务提供程序与它传递给 VSPackage 的服务提供程序不同。 工具窗口服务提供商知道 <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> ，但并不知道 <xref:Microsoft.VisualStudio.Shell.Interop.SVsRunningDocumentTable> 。 您可以调用 <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> 来从工具窗口内获取 VSPackage 服务提供程序。

    如果工具窗口承载用户控件或任何其他控件容器，则该容器将由 Windows 组件模型放置，并且将无法访问任何 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 服务。 您可以调用 <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> 来从控件容器中获取 VSPackage 服务提供程序。

## <a name="see-also"></a>请参阅
- [可用服务列表](../extensibility/internals/list-of-available-services.md)
- [使用并提供服务](../extensibility/using-and-providing-services.md)
- [服务基础](../extensibility/internals/service-essentials.md)
- [Visual Studio 疑难解答](/troubleshoot/visualstudio/welcome-visual-studio/)