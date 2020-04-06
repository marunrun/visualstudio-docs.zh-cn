---
title: 如何：故障排除服务 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- services, troubleshooting
ms.assetid: 001551da-4847-4f59-a0b2-fcd327d7f5ca
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 49560acdf57f5dad2c57f2a8e4649f194d6d8298
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710752"
---
# <a name="how-to-troubleshoot-services"></a>如何：故障排除服务
当您尝试获取服务时，可能会出现几个常见问题：

- 该服务未在 中[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]注册。

- 该服务按接口类型请求，而不是按服务类型请求。

- 请求该服务的 VS 包尚未进行站点。

- 使用错误的服务提供商。

  如果无法获取请求的服务，则对调用<xref:Microsoft.VisualStudio.Shell.Package.GetService%2A>返回 null。 请求服务后，应始终测试 null：

```csharp
IVsActivityLog log =
    GetService(typeof(SVsActivityLog)) as IVsActivityLog;
if (log == null) return;
```

## <a name="to-troubleshoot-a-service"></a>对服务进行故障排除

1. 检查系统注册表以查看服务是否已正确注册。 有关详细信息，请参阅[如何：提供服务](../extensibility/how-to-provide-a-service.md)。

    以下 *.reg*文件片段显示了如何注册 SVTextManager 服务：

   ```
   [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\<version number>\Services\{F5E7E71D-1401-11d1-883B-0000F87579D2}]
   @="{F5E7E720-1401-11d1-883B-0000F87579D2}"
   "Name"="SVsTextManager"
   ```

    在上面的示例中，版本号是[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]版本，如 12.0 或 14.0，密钥 #F5E7E71D-1401-11d1-883B-00000F87579D2] 是服务的服务标识符 （SID）， SVTextManager 和默认值 {F5E7E720-1401-11d1-883B-0000F87579D2} 是提供该服务的文本管理器 VSPackage 的包 GUID。

2. 在调用 GetService 时，请使用服务类型而不是接口类型。 从[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]请求服务时，<xref:Microsoft.VisualStudio.Shell.Package>将从 类型中提取 GUID。 如果存在以下条件，将找不到服务：

   1. 接口类型传递给 GetService 而不是服务类型。

   2. 没有显式分配给接口的 GUID。 因此，系统根据需要为对象创建默认 GUID。

3. 确保请求该服务的 VSPackage 已已已站点。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]在构造 VSPackage 后和调用<xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A>之前对 VSPackage 进行站点。

    如果 VSPackage 构造函数中的代码需要服务，请将其移动到 方法`Initialize`。

4. 确保您使用的是正确的服务提供商。

    并非所有服务提供商都是一样的。 传递到工具窗口的[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]服务提供商不同于它传递给 VSPackage 的提供程序。 工具窗口服务提供商知道 ，<xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection>但不知道 。 <xref:Microsoft.VisualStudio.Shell.Interop.SVsRunningDocumentTable> 您可以调用<xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A>从工具窗口中获取 VSPackage 服务提供商。

    如果工具窗口承载用户控件或任何其他控件容器，则容器将由 Windows 组件模型设置，并且无法访问任何[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]服务。 您可以调用<xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A>从控件容器中获取 VSPackage 服务提供商。

## <a name="see-also"></a>请参阅
- [可用服务列表](../extensibility/internals/list-of-available-services.md)
- [使用和提供服务](../extensibility/using-and-providing-services.md)
- [服务要点](../extensibility/internals/service-essentials.md)
