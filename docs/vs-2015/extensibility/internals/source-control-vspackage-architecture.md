---
title: 源代码管理 VSPackage 体系结构 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control packages, architecture
ms.assetid: 453125fc-23dc-49b1-8476-94581f05e6c7
caps.latest.revision: 26
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 3cca9e39714f87024b01ab2c925189aacbe22785
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68183409"
---
# <a name="source-control-vspackage-architecture"></a>源代码管理 VSPackage 体系结构
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

源代码管理包是使用 VSPackage 服务[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]IDE 提供了。 反过来，源代码管理包提供了其功能与源代码管理服务。 此外，源代码管理包是一个更灵活的替代方法比源控件集成到源代码管理插件[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。  
  
 源代码管理插件，它实现源控件插件 API 遵守严格的约定。 例如，插件不能替换默认[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]用户界面 (UI)。 此外，源控制插件 API 不会启用插件来实现其自己的源控件模型。 源代码管理包，但是，克服了这两个这些限制。 源代码管理包具有完全控制的源控制体验[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]用户。 此外，源代码管理包可以使用其自己的源控件模型和逻辑，并且它可以定义所有源控件相关的用户接口。  
  
## <a name="source-control-package-components"></a>源代码管理包组件  
 体系结构关系图中所示[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]名为源存根 （stub） 的组件是集成的源代码管理包的 VSPackage [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。  
  
 源存根 （stub） 处理以下任务。  
  
- 提供常见 UI 所需的源代码管理包注册。  
  
- 加载源代码管理包。  
  
- 将源代码管理包设置为活动/非活动。  
  
  源存根 （stub） 查找活动服务的源代码管理包，并将路由从 IDE 到该包的所有传入服务调用。  
  
  源控件适配器包是一个特殊的源控件打包[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]提供。 此包是用于支持源代码管理插件基于源控制插件 API 的主要组件。 如果源代码管理插件，插件的活动源存根 （stub） 将其事件发送到源控件适配器包。 反过来，源控件适配器包与源代码管理插件通过使用源控制插件 API 进行通信，还提供默认值是很常见的所有源代码管理插件的 UI。  
  
  活动的包的源代码管理包时，手动，源存根 （stub） 直接进行通信与包使用[!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)]源代码管理包的接口。 源代码管理包是负责承载其自己的源控件 UI。  
  
  ![源代码管理体系结构图](../../extensibility/internals/media/vsipsccarch.gif "VSIPSCCArch")  
  
  对于源代码管理包，[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]不提供源代码控制或集成的 API。 中所述的方法与之相比[创建源代码管理插件](../../extensibility/internals/creating-a-source-control-plug-in.md)其中源代码管理插件必须实现一组严格的函数和回调。  
  
  如任何 VSPackage，源代码管理包是可以通过创建一个 COM 对象`CoCreateInstance`。 VSPackage 使本身可供[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]IDE，方法是实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>。 VSPackage 创建实例后，接收站点指针和一个<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>提供对可用的服务和在 IDE 中的接口的 VSPackage 访问接口。  
  
  编写基于 VSPackage 的源代码管理包需要比编写基于源控制插件 API 的更高级的编程专业知识插件。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>   
 [入门](../../extensibility/internals/getting-started-with-source-control-vspackages.md)
