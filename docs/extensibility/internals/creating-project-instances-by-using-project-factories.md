---
title: 使用项目工厂创建项目实例 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project factories
- projects [Visual Studio SDK], project factories
ms.assetid: 94c90012-8669-459c-af8e-307ac242c8c4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 31ba5dd11af18f8a723b2271544eff2bd292e2e8
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709065"
---
# <a name="create-project-instances-by-using-project-factories"></a>使用项目工厂创建项目实例
正在使用[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]*项目工厂*创建项目对象的实例的项目类型。 项目工厂类似于可组合 COM 对象的标准类工厂。 但是，项目对象不可预测;因此，项目对象无法创建。它们只能通过使用项目工厂创建。

 当用户[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]加载现有项目或在 中[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]创建新项目时，IDE 调用在 VSPackage 中实现的项目工厂。 新的项目对象为 IDE 提供了足够的信息来填充**解决方案资源管理器**。 新的项目对象还提供支持 IDE 启动的所有相关 UI 操作所需的接口。

 您可以在项目中的类<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory>中实现接口。 通常，它驻留在自己的模块中。

 支持由所有者聚合的项目必须在其项目文件中保留所有者密钥。 当在<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A>具有所有者密钥的项目上调用该方法时，拥有的项目将其所有者密钥转换为项目工厂 GUID，然后调用此项目工厂上`CreateProject`的方法执行实际创建。

## <a name="create-an-owned-project"></a>创建拥有的项目
 所有者分两个阶段创建自有项目：

1. 通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsOwnedProjectFactory.PreCreateForOwner%2A>方法。 这使拥有的项目有机会根据输入控制`IUnknown`创建聚合项目对象。 拥有的项目将内部`IUnknown`对象和聚合对象传递回所有者项目。 这给了拥有的项目一个存储内部的机会`IUnknown`。

2. 通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsOwnedProjectFactory.InitializeForOwner%2A>方法。 调用此方法时，拥有的项目将执行其所有实例化，而不是`IVsProjectFactory::CreateProject`调用不属于私有的项目的情况。 输入`VSOWNEDPROJECTOBJECT`枚举通常是聚合拥有的项目。 拥有的项目可以使用此变量来确定其项目对象是否已创建（Cookie 不等于 NULL）或必须创建（Cookie 等于 NULL）。

   项目类型由唯一的项目 GUID 标识，类似于可克隆 COM 对象的 CLSID。 通常，一个项目工厂处理创建单个项目类型的实例，尽管可以让一个项目工厂处理多个项目类型 GUID。

   项目类型与特定的文件名扩展名相关联。 当用户尝试打开现有项目文件或尝试通过克隆模板创建新项目时，IDE 将使用该文件上的扩展名来确定相应的项目 GUID。

   一旦 IDE 确定是必须创建新项目还是打开特定类型的现有项目，IDE 就会使用 **[HKEY_LOCAL_MACHINE_软件_Microsoft_VisualStudio_8.0_Project]** 下的系统注册表中的信息来查找哪些 VSPackage 实现了所需的项目工厂。 IDE 加载此 VS 包。 在<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A>该方法中，VSPackage 必须通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterProjectTypes.RegisterProjectType%2A>方法将其项目工厂注册到 IDE。

   `IVsProjectFactory`接口的主要方法是<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A>，应处理两种情况：打开现有项目和创建新项目。 大多数项目将其项目状态存储在项目文件中。 通常，通过使模板文件的副本传递给`CreateProject`方法，然后打开副本来创建新项目。 通过直接打开传递给`CreateProject`方法的项目文件来实例化现有项目。 该方法`CreateProject`可以根据需要向用户显示其他 UI 功能。

   项目也可以不使用任何文件，而是将其项目状态存储在文件系统以外的存储机制中，如数据库或 Web 服务器。 在这种情况下，传递给`CreateProject`方法的文件名参数实际上不是文件系统路径，而是标识项目数据的唯一字符串（URL）。 您无需复制传递给的模板文件`CreateProject`，以触发要执行的相应构造序列。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsOwnedProjectFactory>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterProjectTypes>
- [检查表：创建新的项目类型](../../extensibility/internals/checklist-creating-new-project-types.md)
