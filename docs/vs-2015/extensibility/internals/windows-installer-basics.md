---
title: Windows Installer 基础知识 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Windows Installer, VSPackages
- VSPackages, Windows Installer basics
ms.assetid: 497e479b-add8-4644-870a-917f15306b97
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4693654e12dc37209cb92e3e2ba95bde8bd13e77
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65687683"
---
# <a name="windows-installer-basics"></a>Windows Installer 基本知识
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Windows Installer 将在用户计算机上安装和卸载应用程序或软件产品，以 Windows Installer 组件的单元执行这些任务， (有时称为 WICs 或只是组件) 。 GUID 标识每个 WIC，这是使用 Windows Installer 安装程序的基本安装和引用计数。  
  
 有关 Windows Installer 的综合文档，请参阅平台 SDK 主题 [Windows Installer](/previous-versions/2kt85ked(v=vs.120))。  
  
## <a name="authoring-a-vspackage"></a>创作 VSPackage  
 Windows Installer 使用安装包，其中包含 Windows Installer 安装、卸载或修复产品以及运行安装程序用户界面)  (UI 的信息。 每个安装包都包含一个 .msi 文件，其中包含安装数据库、摘要信息流和安装的各个部分的数据流。 若要使用安装程序，必须编写安装。 由于安装程序会围绕组件的概念来组织安装，并将有关安装的信息存储在关系数据库中，因此，广泛创作安装包的过程涉及以下步骤：  
  
1. 规划您的设置创作以支持您的版本控制和并行策略。  
  
2. 确定要向用户显示的功能。  
  
3. 将 VSPackage 和依赖项组织到组件中。  
  
4. 用信息填充安装数据库。  
  
5. 验证安装包。  
  
   本文档主要涉及过程的第一个步骤和第三个步骤。 在这些步骤中，你可以将 VSPackage 功能组织到 WICs 中，以便可以将你的版本控制和维护策略加入到的后续版本中 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。 本平台 SDK Windows Installer 文档中详细介绍了其余三个步骤。  
  
## <a name="key-terms"></a>主要术语  
 下面是与 Windows Installer 技术相关的关键术语的定义。  
  
 资源  
 可安装到计算机上的文件、注册表项、快捷方式等。 这些资源以逻辑方式分组到 Windows Installer 组件中。  
  
 Windows Installer 组件 (WIC)   
 基本的安装单位，表示作为一个单元安装和卸载的相关资源的逻辑分组。 Windows Installer 组件由唯一的组件 ID 或 GUID 标识。 此外，Windows Installer 在 WIC 级别维护其引用计数。 为了获得最高版本的灵活性，请在给定的 WIC 中不包含多个主资源（如 DLL）。 请注意，在确定并填充 WIC 后，为其指定 GUID 并进行部署，你无法更改其组合。 有关详细信息，请参阅将 [应用程序组织到组件](https://msdn.microsoft.com/library/aa370561.aspx)。  
  
 打包 (再发行包)   
 一个部署单元，其中包含此文件可能指向的 .msi 文件和外部源文件。 包包含 Windows Installer 运行 UI 和安装或卸载应用程序所需的所有信息。  
  
 .msi 文件  
 COM 结构化存储文件，其中包含安装应用程序所需的指令和数据。 每个包都至少包含一个 .msi 文件。 .Msi 文件包含安装程序数据库、摘要信息流，还可能包含一个或多个转换和内部源文件。 要安装的文件可以压缩到 cabinet 文件中，也可以存储在 .msi 文件中的流中，也可以存储在源介质的 .msi 文件之外、压缩或解压缩。 有关详细信息，请参阅 [Windows Installer 文件扩展名](https://msdn.microsoft.com/library/aa372842\(VS.85\).aspx)。  
  
## <a name="windows-installer-rules-enforcement"></a>强制执行规则 Windows Installer  
 两组规则通过安装的组件确定资源的部署。 一个规则集由 Windows Installer 本身维护，而你应强制第二个设置为安装作者。  
  
> [!NOTE]
> 仅当你运行 .msi 文件的验证时，才会执行 Windows Installer 规则。 不过，您注意事项将这些规则视为最佳做法。 有关详细信息，请参阅 [验证安装数据库](https://msdn.microsoft.com/library/aa372477\(VS.85\).aspx) 和 [包验证](https://msdn.microsoft.com/library/aa370569\(VS.85\).aspx)。  
  
#### <a name="installer-enforced-rules"></a>安装程序强制执行的规则  
  
- 指定组件中的所有文件都必须安装在同一个目录中。 相反，安装到不同文件夹的文件必须属于单独的组件。  
  
- 每个组件只能有一个密钥路径。 密钥路径只是表示整个组件的文件或注册表项。  
  
#### <a name="component-provider-responsibilities"></a>组件提供者责任  
  
- 可能会在后续版本中单独交付的任意两个资源都存在于单独的组件中。 只有确信这些资源不会单独交付时，才应将资源分组到同一个组件中。 事实上，建议所有主资源 (Dll，例如) 在单独的 WICs 中始终存在。 有关详细信息，请参阅 [定义安装程序组件](https://msdn.microsoft.com/library/aa368269\(VS.85\).aspx)。  
  
- 不应在多个 WIC 中交付版本控制资源。  
  
## <a name="see-also"></a>另请参阅  
 [如果组件规则中断，会发生什么情况？](https://msdn.microsoft.com/library/aa372795\(VS.85\).aspx)
