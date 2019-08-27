---
title: Visual Studio Tools for Office runtime 概述
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office runtime [Office development in Visual Studio], about Office runtime
- VSTOLoader.dll
- runtime loader [Office development in Visual Studio]
- Office runtime [Office development in Visual Studio], assemblies
- Office runtime [Office development in Visual Studio]
- runtime [Office development in Visual Studio], assemblies
- vstoee.dll
- Visual Studio Tools for Office runtime
- Office solutions [Office development in Visual Studio], runtime
- solutions [Office development in Visual Studio], runtime
- versions [Office development in Visual Studio], runtime
- assemblies [Office development in Visual Studio], runtime
- runtime [Office development in Visual Studio], about VSTO runtime
- solution loader [Office development in Visual Studio]
- runtime [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: e78d20fa0c7d4d0db6db50c2cbb5cde0b79023fb
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62982340"
---
# <a name="visual-studio-tools-for-office-runtime-overview"></a>Visual Studio Tools for Office runtime 概述
  若要运行使用 Visual Studio 中的 Microsoft Office 开发人员工具创建的解决方案，必须在最终用户计算机上安装 Visual Studio 2010 Tools for Office 运行时。 有关详细信息，请参阅[如何：安装 Visual Studio Tools for Office runtime 可再发行组件](../vsto/how-to-install-the-visual-studio-tools-for-office-runtime-redistributable.md)。 Visual Studio 2010 Tools for Office 运行时包含两个主要组件：

- Office 的 .NET Framework 扩展。 这些组件是提供解决方案和 Microsoft Office 应用程序之间的通信层的托管程序集。 有关详细信息，请参阅[了解有关.NET Framework 的 Office 扩展](#officeextensions)。

- Office 解决方案加载程序。 此组件是 Office 应用程序用于加载运行时和解决方案的一组非托管 DLL。 有关详细信息，请参阅[了解 Office 解决方案加载程序](#UnmanagedLoader)。

  可以通过多种不同的方法安装运行时。 根据计算机上的配置，安装运行时期间将安装不同的运行时组件。 有关详细信息，请参阅[Visual Studio Tools for Office runtime 安装方案](../vsto/visual-studio-tools-for-office-runtime-installation-scenarios.md)。

## <a name="officeextensions"></a> 了解.NET Framework 的 Office 扩展
 Visual Studio 2010 Tools for Office 运行时包括.NET Framework 3.5 的 Office 扩展[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]及更高版本。 以 .NET Framework 各版本为目标的解决方法使用该版本适用的扩展。

 这两种扩展包括解决方案用于自动处理和扩展 Office 应用程序的程序集。 在创建新的 Office 项目时，Visual Studio 会自动添加对项目类型和项目的目标 .NET Framework 使用的程序集的引用。 有关 Office 扩展中程序集的详细信息，请参阅[Visual Studio Tools for Office runtime 中的程序集](../vsto/assemblies-in-the-visual-studio-tools-for-office-runtime.md)。

### <a name="design-differences-in-the-office-extensions"></a>中的 Office 扩展的设计差异
 在 Office 的 .NET Framework 3.5 扩展中使用的多数类型是类。 这些是 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]的早期版本中包含的相同的类。 相反，你在 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本的 Office 扩展中使用的大多数类型都是接口。 例如，如果面向的是 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本，则 <xref:Microsoft.Office.Tools.Excel.Worksheet> 和 <xref:Microsoft.Office.Tools.Word.Document> 类型是接口而不是类。

 大多数情况下，无论你的解决方案面向 .NET Framework 3.5 还是 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]，在 Office 解决方案中编写的代码都是相同的。 但是，如果面向 .NET Framework 的不同版本，则某些功能需要不同的代码。 有关详细信息，请参阅[迁移 Office 解决方案为.NET Framework 4 或更高版本](../vsto/migrating-office-solutions-to-the-dotnet-framework-4-or-later.md)。

### <a name="interfaces-in-the-office-extensions-for-the-net-framework-4-or-later"></a>针对.NET Framework 4 或更高版本的 Office 扩展中的接口
 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本的的 Office 扩展中的大多数接口不应由用户代码实现。 用户只能实现名称以字母 **I**开头的接口，如 <xref:Microsoft.Office.Tools.Excel.ISmartTagExtension>。

 不以字母开头的所有接口**我**由 Visual Studio 2010 Tools for Office 运行时在内部实现，这些接口可能会更改在将来的版本。 若要创建实现这些接口的对象，请在项目使用由 `Globals.Factory` 对象提供的方法。 例如，若要获取实现 <xref:Microsoft.Office.Tools.Excel.SmartTag> 接口的对象，请使用 `Globals.Factory.CreateSmartTag` 方法。 有关详细信息`Globals.Factory`，请参阅[对 Office 项目中的对象的全局访问](../vsto/global-access-to-objects-in-office-projects.md)。

### <a name="enable-type-equivalence-and-embedded-types-in-projects-that-target-the-net-framework-4-or-later"></a>启用类型等效性和面向.NET Framework 4 或更高版本的项目中嵌入的类型
 由于 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本的 Office 扩展的对象模型基于接口，因此你可使用 Visual Studio 中的 Visual C# 和 Visual Basic 的类型等效性功能，将类型信息从 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 嵌入你的解决方案。 此功能使 Office 解决方案和 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 的版本相互独立。 例如，如果解决方案将 <xref:Microsoft.Office.Tools.Word.Document> 接口用作嵌入类型，而运行时的下一个版本向 <xref:Microsoft.Office.Tools.Word.Document> 接口添加成员，则该解决方案仍适用于运行时的下一个版本。 如果解决方案不将 <xref:Microsoft.Office.Tools.Word.Document> 接口用作嵌入类型，则该解决方案将不再适用于运行时的下一个版本。

 默认情况下，在创建面向 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本的 Office 项目时不会启用类型等效性功能。 如果要启用此功能，请将项目中以下任何程序集引用的 **“嵌入互操作类型”** 属性设置为 **“True”**：

- Microsoft.Office.Tools.dll

- Microsoft.Office.Tools.Common.dll

- Microsoft.Office.Tools.Excel.dll

- Microsoft.Office.Tools.Outlook.dll

- Microsoft.Office.Tools.Word.dll

  进行此更改后，项目所使用的所有运行时类型的类型信息都会在生成该项目时嵌入到解决方案程序集中。 在运行时的解决方案使用此嵌入的类型信息，而不是中引用的程序集中的类型信息。

## <a name="UnmanagedLoader"></a> 了解 Office 解决方案加载程序
 Visual Studio Tools for Office Runtime 包含一些非托管 DLL，Office 应用程序使用这些 DLL 加载运行时和 Office 解决方案。 虽然从来不必直接使用这些 DLL，但是知道这些 DLL 的用途可以帮助你更好地了解 Office 解决方案的体系结构。

 有关如何在加载过程中使用这些组件的信息，请参阅[的文档级自定义体系结构](../vsto/architecture-of-document-level-customizations.md)并[Architecture of VSTO 外接程序](../vsto/architecture-of-vsto-add-ins.md)。

### <a name="vstoeedll"></a>vstoee.dll
 当用户打开文档级自定义项或 VSTO 外接程序中启动时，Office 应用程序调用到*VSTOEE.dll*执行加载所需的任务[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]。

 *VSTOEE.dll*可确保正确版本的[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]加载为解决方案和安装的 Office 版本。 尽管多个版本的[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]可以安装在同一台计算机，只有一个实例上*VSTOEE.dll*安装一次。 这是*VSTOEE.dll*的已安装在计算机上的运行时的最新版本包括在内。 有关不同版本的详细信息[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]，可用于其他解决方案，请参阅[Microsoft Office 的不同版本中运行解决方案](../vsto/running-solutions-in-different-versions-of-microsoft-office.md)。

### <a name="vstoloaderdll"></a>VSTOLoader.dll
 之后*VSTOEE.dll*加载相应版本[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]， *VSTOLoader.dll*执行加载解决方案程序集所需的工作的大部分。 *VSTOLoader.dll*执行多项操作：

- 它为每个解决方案程序集创建一个应用程序域。

- 它执行一组安全性检查以验证解决方案程序集是否有运行的权限。

- 它加载解决方案所需的 Office 的 .NET Framework 扩展的版本。

  *VSTOLoader.dll*还将执行特定于 VSTO 外接程序的多个操作：

- 它实现 <xref:Extensibility.IDTExtensibility2> 接口。 <xref:Extensibility.IDTExtensibility2> 是一个 Microsoft Office 应用程序的所有 VSTO 外接程序都必须实现的 COM 接口。 此接口定义应用程序为与 VSTO 外接程序通信而调用的方法。

- 它实现 IManagedAddin 接口。 Office 应用程序使用此接口来帮助加载 VSTO 外接程序。有关详细信息，请参阅[IManagedAddin 接口](../vsto/imanagedaddin-interface.md)。

## <a name="understand-the-32-bit-and-64-bit-versions-of-the-runtime"></a>了解运行时的 32 位和 64 位版本
 有单独的 64 位和 32 位版本的 Visual Studio 2010 Tools for Office 运行时。 这两种运行时版本用于在 64 位和 32 位版本的 Office 中运行解决方案。 下表显示 Windows 与 Office 的各种组合所需的运行时版本。

|Windows 版本|Microsoft Office 版本|所需的 Visual Studio Tools for Office Runtime 版本|
|------------------------|---------------------------------|--------------------------------------------------------------------|
|32 位|32 位|32 位|
|64 位|32 位|64 位|
|64 位|64 位|64 位|

 安装 Office 时，所需版本的 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 将与 Office 一起安装。 例如，在 64 位版本的 Windows 上安装 64 位版本的 Office 时，也会安装 64 位版本的 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 。 有关安装的详细信息[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]与 Office，请参阅[Visual Studio Tools for Office runtime 安装方案](../vsto/visual-studio-tools-for-office-runtime-installation-scenarios.md)。

 64 位版本的 Office 也可以运行在 Visual Studio 2008 中使用 2007 Microsoft Office 系统的项目模板创建的 Office 解决方案。 不过，该版本不能运行在 Visual Studio 2008 中使用 Microsoft Office 2003 项目模板创建的 Office 解决方案，或使用 Visual Studio 2005 创建的 Office 解决方案。 有关详细信息，请参阅[不同版本的 Microsoft Office 中运行解决方案](../vsto/running-solutions-in-different-versions-of-microsoft-office.md)。

## <a name="repair-the-visual-studio-2010-tools-for-office-runtime"></a>修复 Visual Studio 2010 Tools for Office 运行时
 如果需要修复此运行时，请在“控制面板”中打开 **“程序和功能”** 或 **“添加或删除程序”** ，在程序列表中选择 **“Microsoft Visual Studio 2010 Tools for Office Runtime”** ，然后单击 **“卸载”**。 通过运行的安装程序即可修复此运行时。 如果单击 **“更改”**，则不会向你提供用于修复此运行时的选项。

## <a name="see-also"></a>请参阅
- [Visual Studio Tools for Office runtime 安装方案](../vsto/visual-studio-tools-for-office-runtime-installation-scenarios.md)
- [Visual Studio Tools for Office runtime 中的程序集](../vsto/assemblies-in-the-visual-studio-tools-for-office-runtime.md)
- [Visual Studio 中的 Office 解决方案的体系结构](../vsto/architecture-of-office-solutions-in-visual-studio.md)
- [文档级自定义项的体系结构](../vsto/architecture-of-document-level-customizations.md)
- [VSTO 外接程序的体系结构](../vsto/architecture-of-vsto-add-ins.md)
- [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [升级和迁移 Office 解决方案](../vsto/upgrading-and-migrating-office-solutions.md)
