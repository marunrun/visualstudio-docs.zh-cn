---
title: Windows 安装程序基础知识 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Windows Installer, VSPackages
- VSPackages, Windows Installer basics
ms.assetid: 497e479b-add8-4644-870a-917f15306b97
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: aeea0b17a3c234bb7670642fb9ae0a442c9d60cd
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80703418"
---
# <a name="windows-installer-basics"></a>Windows Installer 基本知识
Windows 安装程序在用户的计算机上安装和卸载应用程序或软件产品，以称为 Windows 安装程序组件（有时称为 WIC 或只是组件）的单位执行这些任务。 GUID 标识每个 WIC，这是使用 Windows 安装程序的安装和引用计数的基本单元。

 有关 Windows 安装程序的全面文档，请参阅平台 SDK 主题["Windows 安装程序](/previous-versions/2kt85ked(v=vs.120))"。

## <a name="authoring-a-vspackage"></a>创作 VS 包
 Windows 安装程序使用安装包，其中包含 Windows 安装程序安装、卸载或修复产品以及运行安装用户界面 （UI） 所需的信息。 每个安装包都包含一个 .msi 文件，该文件包含安装数据库、摘要信息流和安装各个部分的数据流。 要使用安装程序，必须编写安装。 由于安装程序围绕组件的概念组织安装，并将有关安装的信息存储在关系数据库中，因此创作安装包的过程大致需要以下步骤：

1. 规划设置创作以支持版本控制和并行策略。

2. 标识要呈现给用户的功能。

3. 将 VS 包和依赖项组织到组件中。

4. 使用信息填充安装数据库。

5. 验证安装包。

   本文档主要涉及该过程的第一个和第三步。 在这些步骤中，您将 VSPackage 功能组织到 WIC 中，以便可以制定版本控制和服务策略，以考虑[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]的后续版本。 其余三个步骤详在平台 SDK 中的 Windows 安装程序文档中。

## <a name="key-terms"></a>主要术语
 以下是与 Windows 安装程序技术相关的关键术语的定义。

 可能安装到计算机的资源文件、注册表项、快捷方式等。 这些资源以逻辑方式分组到 Windows 安装程序组件中。

 Windows 安装程序组件 （WIC） 表示作为设备安装并卸载的相关资源的逻辑分组的基本安装单元。 Windows 安装程序组件由唯一组件 ID 或 GUID 标识。 此外，Windows 安装程序在 WIC 级别保持其引用计数。 为了获得最大的版本控制灵活性，在给定的 WIC 中只包含一个主资源（如 DLL）。 请注意，在标识和填充 WIC、为其提供 GUID 并部署它后，无法更改其组成。 有关详细信息，请参阅[将应用程序组织到组件](/windows/desktop/Msi/organizing-applications-into-components)中。

 包（Redist 包）一个部署单元，由 .msi 文件和外部源文件组成，此文件可能会指向该文件。 包包含 Windows 安装程序运行 UI 以及安装或卸载应用程序所需的所有信息。

 .msi 文件 A COM 结构化存储文件，其中包含安装应用程序所需的说明和数据。 每个包至少包含一个 .msi 文件。 .msi 文件包含安装程序数据库、摘要信息流，以及可能一个或多个转换和内部源文件。 要安装的文件可以压缩到机柜中并存储在 .msi 文件中的流中，也可以存储在源介质上的 .msi 文件之外，进行压缩或未压缩。 有关详细信息，请参阅[Windows 安装程序文件扩展名](/windows/desktop/Msi/windows-installer-file-extensions)。

## <a name="windows-installer-rules-enforcement"></a>Windows 安装程序规则强制
 两组规则确定通过设置的组件部署资源。 一个规则集由 Windows 安装程序本身维护，而应强制第二个集作为安装作者。

> [!NOTE]
> 仅当运行 .msi 文件的验证时，才会强制实施 Windows 安装程序规则。 不过，请注意，应将这些规则视为最佳实践。 有关详细信息，请参阅[验证安装数据库](/windows/desktop/Msi/validating-an-installation-database)和[包验证](/windows/desktop/Msi/package-validation)。

#### <a name="installer-enforced-rules"></a>安装程序强制规则

- 给定组件中的所有文件都必须安装到同一目录。 相反，安装到独立文件夹的文件必须属于单独的组件。

- 每个组件只能有一个密钥路径。 密钥路径只是表示整个组件的文件或注册表项。

#### <a name="component-provider-responsibilities"></a>组件-供应商职责

- 在后续版本中可能单独提供的任何两个资源都应存在于单独的组件中。 仅当确定这些资源永远不会单独发货时，才应将资源分组到同一组件中。 事实上，建议所有主资源（例如 DLL）始终存在于单独的 WIC 中。 有关详细信息，请参阅[定义安装程序组件](/windows/desktop/Msi/defining-installer-components)。

- 任何版本化资源都不应在多个 WIC 中发货。

## <a name="see-also"></a>请参阅
- [如果组件规则断开，会发生什么情况？](/windows/desktop/Msi/what-happens-if-the-component-rules-are-broken)
