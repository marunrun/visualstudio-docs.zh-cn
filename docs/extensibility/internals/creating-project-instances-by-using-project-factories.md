---
title: 使用项目工厂创建的项目实例 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project factories
- projects [Visual Studio SDK], project factories
ms.assetid: 94c90012-8669-459c-af8e-307ac242c8c4
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6b6f6dee7850610b222cf26964dd4811fcf79b5a
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66329396"
---
# <a name="create-project-instances-by-using-project-factories"></a>使用项目工厂创建的项目实例
中的项目类型[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]使用*项目工厂*若要创建的项目对象的实例。 项目工厂是类似于 cocreatable COM 对象的标准类工厂。 但是，项目对象不是 cocreatable;它们只能通过使用项目工厂创建。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE 调用在你的 VSPackage 中实现，当用户加载现有项目或创建新的项目中的项目工厂[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。 新的项目对象提供具有足够的信息的 IDE 来填充**解决方案资源管理器**。 新的项目对象还提供了所需的接口支持所有相关的 UI 操作启动的 IDE。

 您可以实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory>中你的项目中的类接口。 通常情况下，它驻留在其自己的模块。

 支持由所有者所聚合的项目必须保留其项目文件中的所有者密钥。 当<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A>具有所有者键项目上调用方法、 所拥有的项目将其所有者密钥转换为 GUID 然后调用一个项目工厂`CreateProject`上执行的实际创建此项目工厂方法。

## <a name="create-an-owned-project"></a>创建拥有的项目
 所有者在两个阶段中创建拥有的项目：

1. 通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsOwnedProjectFactory.PreCreateForOwner%2A>方法。 这使拥有的项目创建基于输入控制聚合的项目对象有机会`IUnknown`。 拥有的项目将传递内部`IUnknown`和聚合回所有者项目对象。 这使拥有的项目存储在内部有机会`IUnknown`。

2. 通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsOwnedProjectFactory.InitializeForOwner%2A>方法。 此方法调用而不是调用时，拥有的项目将执行其实例化`IVsProjectFactory::CreateProject`就会是项目不属于这种情况。 输入`VSOWNEDPROJECTOBJECT`枚举通常是聚合所有的项目。 拥有的项目可以使用此变量来确定是否已创建的项目对象 （cookie 不等于 NULL） 或必须创建 （cookie 等于 NULL）。

   项目类型进行标识的唯一项目 GUID，类似于 cocreatable COM 对象的 CLSID。 通常情况下，一个项目工厂句柄创建单个项目类型的实例，但也可以有一个项目工厂处理多个项目类型 GUID。

   项目类型都与特定文件扩展名相关联。 当用户尝试打开一个现有项目文件，或尝试通过克隆模板创建一个新的项目时，IDE 会使用文件扩展名来确定相应的项目 GUID。

   IDE 只要 IDE 确定它是否必须创建一个新项目或打开现有项目的特定类型，使用系统注册表中的信息 **[HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Projects]** 以找出哪些 VSPackage 实现所需的项目工厂。 在 IDE 中加载此 VSPackage。 在中<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A>方法中，VSPackage 必须将注册其项目工厂 IDE 通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterProjectTypes.RegisterProjectType%2A>方法。

   主要方法`IVsProjectFactory`接口是<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A>，它应处理两种方案： 打开现有项目并创建一个新的项目。 大多数项目在项目文件中存储其项目状态。 通常情况下，新项目的创建，使模板文件的副本传递给`CreateProject`方法，并打开副本。 现有的项目通过实例化直接打开项目文件传递给`CreateProject`方法。 `CreateProject`方法可以根据需要向用户显示其他 UI 功能。

   项目可以不使用任何文件和，而是将其项目状态存储在文件系统，例如数据库或 Web 服务器以外的存储机制。 在这种情况下，文件名称参数传递给`CreateProject`方法不是实际的文件系统路径，而一个唯一字符串-URL-若要确定项目数据。 不需要将传递到模板文件复制`CreateProject`触发要执行的适当构造序列。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsOwnedProjectFactory>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterProjectTypes>
- [清单：创建新的项目类型](../../extensibility/internals/checklist-creating-new-project-types.md)