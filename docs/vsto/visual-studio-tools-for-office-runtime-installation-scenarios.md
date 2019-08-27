---
title: Visual Studio Tools for Office runtime 安装方案
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Visual Studio Tools for Office runtime, installation scenarios
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 507bce496405f615343a9c109ff71196d814af08
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63438729"
---
# <a name="visual-studio-tools-for-office-runtime-installation-scenarios"></a>Visual Studio Tools for Office runtime 安装方案
  以下三种方式，可以安装 Visual Studio 2010 Tools for Office 运行时：

- 安装 Visual Studio 时。

- 安装 Microsoft Office 时。

- 当你安装 Visual Studio 2010 Tools for Office runtime 可再发行组件。

  安装的运行时组件取决于计算机的配置和安装方案。

## <a name="runtime-components-that-are-installed-in-each-installation-scenario"></a>在每个安装方案中安装的运行时组件
 Visual Studio 2010 Tools for Office 运行时有三个组件： Office 解决方案加载程序、.NET Framework 3.5 的 Office 扩展和的 Office 扩展[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]或更高版本。 在安装运行时时，始终安装 Office 解决方案加载程序。 .NET Framework 的 Office 扩展的安装取决于计算机的配置和安装方案。 如果在首次安装运行时时 Office 扩展之一不能安装，则当满足某些需求时，运行时将稍后自动安装缺少的 Office 扩展。 在运行时此功能被称为*按需安装*。

 下表显示每个运行时安装方案中默认安装的运行时组件。 有关每个方案的详细信息将在后面显示。

|运行时安装方案|Office 解决方案加载程序|.NET Framework 3.5 的 Office 扩展|[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 的 Office 扩展|[!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] 的 Office 扩展|
|-----------------------------------|----------------------------|--------------------------------------------------| - |---------------------------------------------------------------------------|
|通过 [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)] 及更高版本|是|是的，如果已安装 .NET Framework 3.5。|是|是|
|通过 [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)]|是|是的，如果已安装 .NET Framework 3.5。|否|否|
|通过 Office 2010 Service Pack 1 (SP1) 或更高版本|是|是的，如果已安装 .NET Framework 3.5。|是的，如果已安装 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]。|否|
|通过运行时可再发行组件|是|是的，如果已安装 .NET Framework 3.5|是的，如果已安装 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]。|是的，如果已安装 [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)]。|

### <a name="install-the-runtime-with-visual-studio-or-the-microsoft-office-developer-tools-for-visual-studio"></a>安装运行时使用 Visual Studio 或 Microsoft Office Developer Tools for Visual Studio
 在 Visual Studio 中安装 Office 开发人员工具时，[!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] 和 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 的 Office 扩展始终安装在开发计算机上。 仅当 .NET Framework 3.5 已位于开发计算机上时，才会安装 .NET Framework 3.5 的 Office 扩展。 如果在安装 [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)] 后安装 .NET Framework 3.5，则在首次创建面向 .NET Framework 3.5 的 Office 项目时，运行时将自动安装 .NET Framework 3.5 的 Office 扩展。

> [!WARNING]
> 不能使用 [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)] 或更高版本创建面向 .NET Framework 3.5 的 Office 项目。

 有关如何安装 Office 开发人员工具的详细信息，请参阅[如何：配置计算机以开发 Office 解决方案](../vsto/how-to-configure-a-computer-to-develop-office-solutions.md)。

### <a name="install-the-runtime-with-office"></a>与 Office 一起安装在运行时
 安装 Office 时，如果 .NET Framework 3.5 已位于计算机上，则安装 .NET Framework 3.5 的 Office 扩展。 如果在安装 Office 之后安装 .NET Framework 3.5，则在 Office 应用程序首次尝试加载面向 .NET Framework 3.5 的解决方案时，运行时将自动安装 .NET Framework 3.5 的 Office 扩展。

 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本的 Office 扩展不与 Office 一起安装，即使安装 Office 时 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本已存在。

 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 的 Office 扩展随 Office 一起安装。 最终用户可以通过安装 Windows 更新来获得 [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] 的 Office 扩展。

 若要确保你的用户具有必要的扩展以使用你的应用程序，包括最新版本的 Visual Studio 2010 Tools for Office 运行时可再发行组件为你的解决方案的必备组件。 有关先决条件的详细信息，请参阅[用于部署 Office 解决方案必备组件](https://msdn.microsoft.com/9f672809-43a3-40a1-9057-397ce3b5126e)。

### <a name="install-the-runtime-by-using-the-runtime-redistributable"></a>使用运行时可再发行组件安装在运行时
 通过手动运行 Visual Studio 2010 Tools for Office runtime 可再发行组件或包括可再发行的必备组件，在部署 Office 解决方案时，可以安装在运行时。

 当使用 Visual Studio 2010 Tools for Office runtime 可再发行组件、.NET Framework 3.5 的 Office 扩展和的 Office 扩展安装运行时[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]或更高版本时将安装相应版本的.NET框架已在计算机上存在。 如果在运行时已安装的情况下计算机缺少 .NET Framework 的这些版本之一，则此时将不安装缺少的 .NET framework 版本的 Office 扩展。 如果你于稍后安装 .NET Framework 所缺少的版本，则下一次解决方案需要已安装（如果运行时与使用 ClickOnce 部署的解决方案一起安装）或已加载（如果运行时与使用 Windows Installer 部署的解决方案一起安装）扩展时，运行时将自动安装相应的 Office 扩展。

 有关 ClickOnce 解决方案中将必备组件的详细信息，请参阅[如何：若要运行 Office 解决方案的最终用户计算机上安装的必备组件](https://msdn.microsoft.com/74dd2c52-838f-4abf-b2b4-4d7b0c2a0a98)。 有关如何手动安装可再发行组件包中的运行时的详细信息，请参阅[如何：安装 Visual Studio Tools for Office runtime 可再发行组件](../vsto/how-to-install-the-visual-studio-tools-for-office-runtime-redistributable.md)。

## <a name="see-also"></a>请参阅
- [Visual Studio Tools for Office runtime 概述](../vsto/visual-studio-tools-for-office-runtime-overview.md)
- [Visual Studio Tools for Office runtime 中的程序集](../vsto/assemblies-in-the-visual-studio-tools-for-office-runtime.md)
