---
title: Windows 安装程序基础知识 |Microsoft Docs
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
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65687683"
---
# <a name="windows-installer-basics"></a>Windows Installer 基本知识
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Windows 安装程序安装和卸载应用程序或用户的计算机上的软件产品在名为 Windows 安装程序组件 （有时称为 WICs 或只是组件） 的单元中执行这些任务。 一个 GUID 标识每个 WIC，它是安装和引用计数对于使用 Windows 安装程序安装的基本单位。  
  
 Windows 安装程序的综合文档，请参阅平台 SDK 主题[Windows 安装程序](/previous-versions/2kt85ked(v=vs.120))。  
  
## <a name="authoring-a-vspackage"></a>创作 VSPackage  
 Windows 安装程序使用安装包，其中包含 Windows 安装程序需要安装、 卸载或修复产品，并且运行安装程序用户界面 (UI) 的信息。 每个安装包包括一个.msi 文件，其中包含安装数据库、 摘要信息流和数据流的各个部件的安装。 若要使用安装程序，你必须编写安装。 因为安装程序组织安装组件的概念，并将安装的相关信息存储在关系数据库，广泛地创作一个安装包的过程需要执行以下步骤：  
  
1. 规划编写，以支持您的版本控制和并行的策略设置。  
  
2. 标识要呈现给用户的功能。  
  
3. 将 VSPackage 和依赖项组织到组件。  
  
4. 安装使用填充数据库的信息。  
  
5. 验证安装的包。  
  
   本文档主要关心此过程的第一个和第三个步骤。 在执行这些步骤期间您将组织 VSPackage 功能到 WICs 以便在版本控制和服务策略才能实现的后续版本可以帧[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。 Platform SDK 中的 Windows Installer 文档中详细介绍剩余三个步骤。  
  
## <a name="key-terms"></a>关键术语  
 以下是与 Windows 安装程序技术相关的重要术语的定义。  
  
 资源  
 文件、 注册表项、 快捷方式，或，依此类推，后者可能会安装到计算机。 这些资源进行逻辑分组到 Windows 安装程序组件中。  
  
 Windows 安装程序组件 (WIC)  
 表示安装和卸载作为一个单元的相关资源的逻辑分组的安装的基本单位。 Windows 安装程序组件通过独特的组件 ID 或 GUID 进行标识。 此外，Windows 安装程序维护其引用计数在 WIC 级别。 为了最大版本控制灵活性，在给定 WIC 包括不超过一个主资源，如的 DLL。 请注意，识别和填充 WIC，使其使用的 GUID，并将其部署后，您不能更改其构成。 有关详细信息，请参阅[组织应用程序组件](https://msdn.microsoft.com/library/aa370561.aspx)。  
  
 包位置 （Redist）  
 此文件可能指向某一.msi 文件和外部源文件组成的部署单元。 包包含 Windows 安装程序需要运行 UI 和安装或卸载应用程序的所有信息。  
  
 .msi 文件  
 包含说明和安装应用程序所需的数据的 COM 结构化存储文件。 每个包包含至少一个.msi 文件。 该.msi 文件包含安装程序数据库、 摘要信息流，并可能是一个或多个转换和内部的源代码文件。 要安装文件可以压缩为 cab 文件和存储在.msi 文件中的流或存储，压缩，或未压缩的.msi 文件的源介质上外部。 有关详细信息，请参阅[Windows 安装程序文件扩展名](https://msdn.microsoft.com/library/aa372842\(VS.85\).aspx)。  
  
## <a name="windows-installer-rules-enforcement"></a>Windows 安装程序规则强制  
 两组规则确定通过安装程序的组件的资源的部署。 虽然应强制安装作者的第二个集由 Windows 安装程序本身，维护一个规则集。  
  
> [!NOTE]
> 仅当你运行.msi 文件的验证，则会发生的 Windows Installer 规则强制执行。 不过，警告将这些规则视为最佳做法。 有关详细信息，请参阅[验证安装数据库](https://msdn.microsoft.com/library/aa372477\(VS.85\).aspx)并[包验证](https://msdn.microsoft.com/library/aa370569\(VS.85\).aspx)。  
  
#### <a name="installer-enforced-rules"></a>安装程序强制实施的规则  
  
- 给定组件中的所有文件必须都安装到同一个目录。 相反，安装在单独的文件夹的文件都必须属于单独的组件。  
  
- 可能有每个组件只有一个注册表项路径。 密钥路径是只是文件或注册表项表示的整个组件。  
  
#### <a name="component-provider-responsibilities"></a>组件提供程序的责任  
  
- 在后续版本中可能会分开提供任何两个资源应位于单独的组件。 仅当确定永远不会将单独提供这些资源，应将资源分组到同一组件。 事实上，建议所有主要资源 (例如 Dll) 中单独 WICs 始终存在。 有关详细信息，请参阅[定义安装程序组件](https://msdn.microsoft.com/library/aa368269\(VS.85\).aspx)。  
  
- 无版本控制的资源不断应在多个 WIC 中提供。  
  
## <a name="see-also"></a>请参阅  
 [如果组件规则中断，会发生什么情况？](https://msdn.microsoft.com/library/aa372795\(VS.85\).aspx)
