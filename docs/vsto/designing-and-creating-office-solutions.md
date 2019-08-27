---
title: 设计和创建 Office 解决方案
ms.date: 08/14/2019
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office solutions [Office development in Visual Studio], creating
- Office development in Visual Studio, creating solutions
- solutions [Office development in Visual Studio], creating
- Office project types in Visual Studio
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 8ee2d7470a14836d7369fb916c06f2a8172c4e6b
ms.sourcegitcommit: 209ed0fcbb8daa1685e8d6b9a97f3857a4ce1152
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2019
ms.locfileid: "69551635"
---
# <a name="design-and-create-office-solutions"></a>设计和创建 Office 解决方案

Visual Studio 提供可用于创建几种不同类型的 Office 解决方案的项目模板。 文档的此部分将介绍项目模板和提供有关创建 Office 项目的指导。 有关在创建项目后如何实现代码和用户界面自定义的信息, 请参阅[开发 Office 解决方案](../vsto/developing-office-solutions.md)。

[!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="create-office-projects"></a>创建 Office 项目
 在开始之前，应确定你的需求并找到最适合你的解决方案类型。 例如，如果每次使用应用程序时都必须运行 Office 解决方案，则 VSTO 外接程序最适合你的要求。 如果代码与单个文档紧密集成，则可创建文档级自定义项。 这些项目类型都可用作 Visual Studio 项目模板。 有关包含在 Visual Studio 中的 Office 项目模板的详细信息, 请参阅[office 项目模板概述](../vsto/office-project-templates-overview.md)。 有关如何创建 Office 项目的详细信息, 请参阅[如何:在 Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)中创建 Office 项目。

 Office 项目具有的功能和项目项与 Visual Studio 中的其他类型的项目不同。 例如，当创建文档级项目时，项目中的文档和工作簿都可以在 Visual Studio 内部打开和编辑。 有关详细信息, 请参阅[Visual Studio 环境中的 Office 项目](../vsto/office-projects-in-the-visual-studio-environment.md)。

## <a name="choose-a-net-framework-version"></a>选择 .NET Framework 版本
 选择最适合你需求的项目类型之后，可以选择在开发过程中要使用的 .NET Framework 版本。 你可以选择 Office 项目中的以下 .NET Framework 版本作为目标：

- [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]

- [!INCLUDE[net_client_v40_long](../vsto/includes/net-client-v40-long-md.md)]

- [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)]

  要运行解决方案的最终用户计算机上需要为项目选择的 .NET Framework 版本。 例如, 如果你的[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]项目面向, 则在最终用户计算机上是必需的。 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 在此示例中, 如果最终用户计算机上仅安装了 .NET Framework 3.5, 则解决方案将不会运行。

  如果迁移的 VSTO 外接程序项目面向 .NET Framework 3.5，则 Visual Studio 会将你项目的目标框架更改为 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本，具体取决于已安装的 Office 版本。

  但是，在 Visual Studio 更改目标框架之后，你可能需要修改项目中的某些代码才能使用某些功能。 有关如何更改目标框架的详细信息, 请参阅[如何:面向 .NET Framework 的某个版本](../ide/how-to-target-a-version-of-the-dotnet-framework.md)。 有关你可能需要在项目中进行的更改的详细信息, 请参阅将[Office 解决方案迁移到 .NET Framework 4 或更高版本](../vsto/migrating-office-solutions-to-the-dotnet-framework-4-or-later.md)。

  如果 Visual Studio 更改项目的目标 .NET Framework 并且使用 ClickOnce 部署解决方案, 请确保在 "**系统必备**" 对话框中选择相应的 .NET Framework 版本。 此选择不会在你更改项目的目标框架时自动更改。 有关详细信息，请参阅[如何：在最终用户计算机上安装必备组件以运行 Office](https://msdn.microsoft.com/74dd2c52-838f-4abf-b2b4-4d7b0c2a0a98)解决方案。

> [!NOTE]
> 不能面向通过使用 [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)] 创建的 Office 项目中的 .NET Framework 3.5 或更早版本。 通过使用 [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)] 创建的 Office 项目需要在 [!INCLUDE[net_client_v40_long](../vsto/includes/net-client-v40-long-md.md)] 中首次引入的功能

### <a name="understand-when-the-office-pias-are-required-on-end-user-computers"></a>了解最终用户计算机上需要 Office Pia 的时间
 默认情况下, 如果项目中每个 Office PIA 引用的 "**嵌入互操作类型**" 属性设置为 " **True**" (默认值), 则无需在最终用户计算机上安装 Office 主互操作程序集 (pia)。 在本方案中，你的解决方案使用的 PIA 类型的类型信息会在生成项目时嵌入到解决方案程序集中。 在运行时, 使用嵌入的类型信息 (而不是 Pia) 来调入 Office 应用程序的基于 COM 的对象模型。 有关如何在解决方案中嵌入 Pia 的类型的详细信息, 请参阅[类型等效性和嵌入的互操作类型](/dotnet/framework/interop/type-equivalence-and-embedded-interop-types)。

 如果项目中每个 Office PIA 引用的 "**嵌入互操作类型**" 属性设置为 " **False**", 则必须在运行该解决方案的每个最终用户计算机上的全局程序集缓存中安装并注册 Office pia。 在大多数情况下，PIA 会随 Office 一起默认安装，但你还可以将PIA 可再发行组件作为解决方案的必备组件包括进去。 有关详细信息, 请参阅[部署的 Office 解决方案必备组件](https://msdn.microsoft.com/9f672809-43a3-40a1-9057-397ce3b5126e)。

### <a name="understand-the-client-profile"></a>了解客户端配置文件
 .NET Framework Client Profile 是完整版 .NET Framework 的子集。 如果只需使用 .NET Framework 中的客户端功能，并且想要为你的 Office 解决方案提供最快的部署体验，则可以面向 .NET Framework Client Profile。 有关详细信息, 请参阅[.NET Framework 客户端配置文件](/dotnet/framework/deployment/client-profile)。

 当创建面向 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 的 Office 项目时，默认情况下，将面向 [!INCLUDE[net_client_v40_long](../vsto/includes/net-client-v40-long-md.md)]。 如果想要开发完整的 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]，则必须在项目创建之后设置此选项。 有关详细信息，请参阅[如何：面向 .NET Framework 的某个版本](../ide/how-to-target-a-version-of-the-dotnet-framework.md)。

## <a name="create-solutions-for-the-64-bit-edition-of-microsoft-office"></a>为64位版本的 Microsoft Office 创建解决方案
 Microsoft Office 可提供 64 位和 32 位版本。 若要创建可在任一版本中运行的 Office 解决方案, 必须将项目的 "平台目标" 设置设置为 "**任何 CPU**"。 这是 Office 项目的默认值。 有关详细信息, 请参阅[生成 Office 解决方案](../vsto/building-office-solutions.md)。

 存在供 64 位和 32 位版本的 Microsoft Office 使用的单独的 64 位和 32 位版本的 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]。 有关详细信息, 请参阅[Visual Studio Tools for Office 运行时概述](../vsto/visual-studio-tools-for-office-runtime-overview.md)。

## <a name="assemblies-in-office-solutions"></a>Office 解决方案中的程序集
 当使用 Visual Studio 中的 Office 开发工具创建 Office 项目时，你编写的代码最终将被编译成程序集。 该程序集将部署到共享服务器或客户端计算机上的目录中。

 Office 解决方案中的程序集通过 Office 应用程序加载。 加载程序集之后，程序集中的代码可以响应在应用程序中引发的事件（例如，用户单击菜单项时）。 程序集中的代码也可以调入对象模型，以便自动处理和扩展应用程序，并且它可以使用 [!INCLUDE[dnprdnshort](../sharepoint/includes/dnprdnshort-md.md)] 中的任何类。 有关详细信息, 请参阅[文档级自定义项的体系结构](../vsto/architecture-of-document-level-customizations.md)和[VSTO 外接程序的体系结构](../vsto/architecture-of-vsto-add-ins.md)。

 Office 解决方案使用部署清单和应用程序清单来标识程序集。 清单包含有关程序集的名称、版本和位置信息，因此，应用程序可以查找、链接到并运行正确的程序集。 有关详细信息, 请参阅[Office 解决方案中的应用程序和部署清单](../vsto/application-and-deployment-manifests-in-office-solutions.md)。

 文档级项目包括一个文档和一个程序集。 该文档可充当应用程序的前端，是所有用户发生交互的地方。 每个文档只能包含一个与之相关的主项目程序集；但是，多个文档可以指向同一个程序集。

 文档级项目中的程序集不会嵌入到文档；而是存储到其他位置，可通过文档的应用程序清单进行标识。

## <a name="security-considerations-for-assemblies"></a>程序集的安全注意事项
 对于要在一台计算机上运行 Office 解决方案，必须信任该解决方案使用的程序集才能运行。 有关安全性的详细信息, 请参阅[保护 Office 解决方案的安全](../vsto/securing-office-solutions.md)。

 默认情况下，解决方案程序集和项目输出文件夹中任何引用的程序集是受信任的，以便在生成项目时在开发计算机上运行。 有关详细信息, 请参阅[生成 Office 解决方案](../vsto/building-office-solutions.md)。

 出于安全考虑，最好是在本地计算机上创建项目，而不是在共享位置进行开发。 有关详细信息, 请参阅[Office 解决方案的协作开发](../vsto/collaborative-development-of-office-solutions.md)。

## <a name="referenced-assemblies"></a>引用的程序集
 该程序集可以引用项目引用中列出的其他程序集。 但是，一个文档级项目程序集不能引用另一个文档级项目程序集。

## <a name="see-also"></a>请参阅
- [Office 项目模板概述](../vsto/office-project-templates-overview.md)
- [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [Visual Studio 环境中的 Office 项目](../vsto/office-projects-in-the-visual-studio-environment.md)
- [Office 项目中的属性](../vsto/properties-in-office-projects.md)
- [在 Microsoft Office 的不同版本中运行解决方案](../vsto/running-solutions-in-different-versions-of-microsoft-office.md)
- [如何：通过主互操作程序集面向 Office 应用程序](../vsto/how-to-target-office-applications-through-primary-interop-assemblies.md)
- [Office 解决方案中的应用程序和部署清单](../vsto/application-and-deployment-manifests-in-office-solutions.md)
- [如何：为 Office 解决方案设置配置信息](../vsto/how-to-set-up-configuration-information-for-an-office-solution.md)
- [在 Visual Studio 中使用 Office 功能](../vsto/using-office-functionality-inside-of-visual-studio.md)
- [部署 Office 解决方案](../vsto/deploying-an-office-solution.md)
- [Office 编程中的常见任务](../vsto/common-tasks-in-office-programming.md)
- [开发 Office 解决方案](../vsto/developing-office-solutions.md)
- [Visual Studio 中 Office 解决方案的体系结构](../vsto/architecture-of-office-solutions-in-visual-studio.md)
