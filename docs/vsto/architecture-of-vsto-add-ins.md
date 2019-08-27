---
title: VSTO 外接程序的体系结构
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- VSTOLoader.dll
- architecture [Office development in Visual Studio], application-level add-ins
- vstoee.dll
- application-level add-ins [Office development in Visual Studio], architecture
- add-ins [Office development in Visual Studio], architecture
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 401ce9b8421cd636fc72c59dcd6641ff4e05d968
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63440352"
---
# <a name="architecture-of-vsto-add-ins"></a>VSTO 外接程序的体系结构
  使用 Visual Studio 中的 Office 开发人员工具创建的 VSTO 外接程序具有强调稳定性和安全性的体系结构功能，并使其能够与 Microsoft Office 紧密合作。 本主题介绍 VSTO 外接程序的以下方面：

- [了解 VSTO 外接程序](#UnderstandingAddIns)

- [VSTO 外接程序的组件](#AddinComponents)

- [VSTO 外接程序如何与 Microsoft Office 应用程序协同工作](#HowAddinsWork)

  [!INCLUDE[appliesto_allapp](../vsto/includes/appliesto-allapp-md.md)]

  有关创建 VSTO 外接程序的常规信息，请参阅[Office 解决方案开发概述&#40;VSTO&#41; ](../vsto/office-solutions-development-overview-vsto.md)并[VSTO 外接程序编程入门](../vsto/getting-started-programming-vsto-add-ins.md)。

## <a name="UnderstandingAddIns"></a> 了解 VSTO 外接程序
 当您使用在 Visual Studio 中的 Office 开发人员工具生成 VSTO 外接程序中时，您将创建由 Microsoft Office 应用程序加载的托管的代码程序集。 加载该程序集后，VSTO 外接程序可以响应在应用程序中引发的事件（例如，用户单击菜单项时）。 VSTO 外接程序也可以调入对象模型，以便实现应用程序自动化和扩展应用程序，并且它可以使用 [!INCLUDE[dnprdnshort](../sharepoint/includes/dnprdnshort-md.md)]中的任何类。

 程序集通过应用程序的主互操作程序集与应用程序的 COM 组件进行通信。 有关详细信息，请参阅[Office 主互操作程序集](../vsto/office-primary-interop-assemblies.md)并[Office 解决方案开发概述&#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)。

 如果为应用程序安装了多个 VSTO 外接程序，那么，每个 VSTO 外接程序都会加载到不同的应用程序域中。 这意味着某个行为不正确的 VSTO 外接程序不会导致其他 VSTO 外接程序失败。 这还有助于确保在关闭应用程序时，所有 VSTO 外接程序程序集都将从内存中卸载。 有关应用程序域的详细信息，请参阅[应用程序域](/dotnet/framework/app-domains/application-domains)。

> [!NOTE]
> 对于使用 Visual Studio 中的 Office 开发人员工具创建的 VSTO 外接程序，仅当最终用户启动主机 Microsoft Office 应用程序时才会使用。 如果以编程方式（例如，通过使用自动化）启动应用程序，VSTO 外接程序可能不会按预期工作。

## <a name="AddinComponents"></a> VSTO 外接程序的组件
 尽管 VSTO 外接程序程序集是主要组件，但有其他若干组件对 Microsoft Office 应用程序如何发现和加载 VSTO 外接程序起重要作用。

### <a name="registry-entries"></a>注册表项
 Microsoft Office 应用程序通过查找一组注册表项来发现 VSTO 外接程序。 有关使用 VSTO 外接程序的注册表项的完整列表，请参阅[VSTO 外接程序的注册表项](../vsto/registry-entries-for-vsto-add-ins.md)。

 生成解决方案时，Visual Studio 会在开发计算机上创建所有必需的注册表项，以便你调试和运行 VSTO 外接程序。 有关详细信息，请参阅[生成 Office 解决方案](../vsto/building-office-solutions.md)。

 如果使用 ClickOnce 来部署你的解决方案，安装程序自动生成的发布过程的最终用户计算机上创建注册表项。 有关详细信息，请参阅[通过使用 ClickOnce 部署 Office 解决方案](../vsto/deploying-an-office-solution-by-using-clickonce.md)。

### <a name="deployment-manifest-and-application-manifest"></a>部署清单和应用程序清单
 VSTO 外接程序使用部署清单和应用程序清单来标识和加载 VSTO 外接程序程序集的最新版本。 部署清单指向当前应用程序清单。 应用程序清单指向 VSTO 外接程序程序集，并指定要在程序集中执行的入口点类。 有关详细信息，请参阅[应用程序和部署清单在 Office 解决方案中](../vsto/application-and-deployment-manifests-in-office-solutions.md)。

### <a name="visual-studio-tools-for-office-runtime"></a>Visual Studio Tools for Office Runtime
 若要运行 VSTO 加载项通过使用 Visual Studio 中的 Office 开发人员工具创建的最终用户计算机必须具有[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]安装。 运行时包括非托管组件和一组托管程序集。 非托管组件加载 VSTO 外接程序程序集。 托管程序集提供 VSTO 外接程序代码用于实现主机应用程序自动化和扩展主机应用程序的对象模型。

 有关详细信息，请参阅[Visual Studio Tools for Office runtime 概述](../vsto/visual-studio-tools-for-office-runtime-overview.md)。

## <a name="HowAddinsWork"></a> VSTO 外接程序与 Microsoft Office 应用程序的工作原理
 当用户启动 Microsoft Office 应用程序时，该应用程序使用部署清单和应用程序清单来查找并加载 VSTO 外接程序程序集的最新版本。 下图显示了这些 VSTO 外接程序的基本体系结构。

 ![2007 office 外接程序体系结构](../vsto/media/office07addin.png "2007 Office 外接程序体系结构")

> [!NOTE]
> 在面向 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或 [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)]的 Office 解决方案中，解决方案通过使用嵌入到解决方案程序集中的 PIA 类型信息调入主机应用程序的对象模型，而不是直接调入 PIA。 有关详细信息，请参阅[设计和创建 Office 解决方案](../vsto/designing-and-creating-office-solutions.md)。

### <a name="loading-process"></a>加载过程
 用户启动应用程序时，会执行以下步骤：

1. 应用程序检查注册表中是否存在标识使用 Visual Studio 中的 Office 开发人员工具创建的 VSTO 外接程序的项。

2. 如果应用程序找到这些注册表项，则该应用程序加载 VSTOEE.dll，后者会加载 VSTOLoader.dll。 这些非托管 DLL 是 Visual Studio 2010 Tools for Office Runtime 的加载程序组件。 有关详细信息，请参阅[Visual Studio Tools for Office runtime 概述](../vsto/visual-studio-tools-for-office-runtime-overview.md)。

3. *VSTOLoader.dll*加载[!INCLUDE[dnprdnshort](../sharepoint/includes/dnprdnshort-md.md)]，并启动的托管的部分[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]。

4. [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 检查清单更新，并下载最新的应用程序和部署清单。

5. [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 执行一系列安全检查。 有关详细信息，请参阅[保护 Office 解决方案](../vsto/securing-office-solutions.md)。

6. 如果 VSTO 外接程序受信任，可以运行，则 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 使用部署清单和应用程序清单来检查程序集更新。 如果集有新版本的程序集可用，则运行时会将新版本的程序集下载到客户端计算机上的 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] 缓存中。 有关详细信息，请参阅[部署 Office 解决方案](../vsto/deploying-an-office-solution.md)。

7. [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 创建一个要在其中加载 VSTO 外接程序程序集的新应用程序域。

8. [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 将 VSTO 外接程序程序集加载到应用程序域中。

9. 如果你已重写 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 方法，则 <xref:Microsoft.Office.Tools.AddInBase.RequestComAddInAutomationService%2A> 将在 VSTO 外接程序中调用该方法。

     可以选择重写此方法，以向其他 Microsoft Office 解决方案公开 VSTO 外接程序中的对象。 有关详细信息，请参阅[从其他 Office 解决方案调用 VSTO 外接程序中的代码](../vsto/calling-code-in-vsto-add-ins-from-other-office-solutions.md)。

10. 如果你已重写 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 方法，则 <xref:Microsoft.Office.Tools.AddInBase.RequestService%2A> 将在 VSTO 外接程序中调用该方法。

     可以选择替代此方法，以便通过返回实现扩展性接口的对象来扩展 Microsoft Office 功能。 有关详细信息，请参阅[使用扩展性接口自定义 UI 功能](../vsto/customizing-ui-features-by-using-extensibility-interfaces.md)。

    > [!NOTE]
    > [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 为主机应用程序支持的每个扩展性接口分别调用 <xref:Microsoft.Office.Tools.AddInBase.RequestService%2A> 方法。 尽管对 <xref:Microsoft.Office.Tools.AddInBase.RequestService%2A> 方法的第一次调用通常发生在调用 `ThisAddIn_Startup` 方法之前，但 VSTO 外接程序不应作出有关 <xref:Microsoft.Office.Tools.AddInBase.RequestService%2A> 方法的调用时间和次数的任何假设。

11. [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 在 VSTO 外接程序中调用 `ThisAddIn_Startup` 方法。 此方法是 <xref:Microsoft.Office.Tools.AddInBase.Startup> 事件的默认事件处理程序。 有关详细信息，请参阅[Office 项目中的事件](../vsto/events-in-office-projects.md)。

## <a name="see-also"></a>请参阅
- [Visual Studio 中的 Office 解决方案的体系结构](../vsto/architecture-of-office-solutions-in-visual-studio.md)
- [文档级自定义项的体系结构](../vsto/architecture-of-document-level-customizations.md)
- [Visual Studio Tools for Office runtime 概述](../vsto/visual-studio-tools-for-office-runtime-overview.md)
- [VSTO 外接程序](../vsto/programming-vsto-add-ins.md)
- [开发 Office 解决方案](../vsto/developing-office-solutions.md)
- [保护 Office 解决方案](../vsto/securing-office-solutions.md)
- [部署 Office 解决方案](../vsto/deploying-an-office-solution.md)
