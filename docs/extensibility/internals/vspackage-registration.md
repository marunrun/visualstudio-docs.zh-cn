---
title: VS包注册 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- registration, VSPackages
- VSPackages, registering
ms.assetid: ecd20da8-b04b-4141-a8f4-a2ef91dd597a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a05dec8fbef40143f31f2c0ac484824717ea2e32
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80703919"
---
# <a name="vspackage-registration"></a>VSPackage 注册
VSPackages 必须[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]通知已安装并应加载它们。 此过程通过在注册表中写入信息来完成。 这是安装程序的典型工作。

> [!NOTE]
> 在 VSPackage 开发期间，使用自注册是公认的做法。 但是，[!INCLUDE[vsipprvsip](../../extensibility/includes/vsipprvsip_md.md)]合作伙伴不能使用自注册作为设置的一部分来运送其产品。

 Windows 安装程序包中的注册表项通常在注册表表中创建。 您还可以在注册表表中注册文件扩展名。 但是，Windows 安装程序通过编程标识符 （ProgId）、类、扩展和动词表提供内置支持。 有关详细信息，请参阅[数据库表](/windows/desktop/Msi/database-tables)。

 请确保您的注册表项与适合所选并行策略的组件相关联。 例如，共享文件的注册表项应与该文件的 Windows 安装程序组件关联。 同样，特定于版本的文件的注册表项应与该文件的组件关联。 否则，为一个版本安装或卸载 VSPackage[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]可能会中断其他版本的 VSPackage。 有关详细信息，请参阅[支持可视化工作室的多个版本](../../extensibility/supporting-multiple-versions-of-visual-studio.md)。

> [!NOTE]
> 管理注册的最简单方法是在同一文件中使用相同的数据进行开发人员注册和安装时间注册。 例如，某些安装程序开发工具可以在生成时使用 .reg 格式的文件。 如果开发人员维护 .reg 文件以进行自己的日常开发和调试，则这些相同的文件可以自动包含在安装程序中。 如果无法自动共享注册数据，则必须确保安装程序的注册数据副本是最新的。

## <a name="registering-unmanaged-vspackages"></a>注册非托管 VS 包
 非托管 VSPackage（包括由 Visual Studio 软件包模板生成的包包）使用 ATL 样式的 .rgs 文件来存储注册信息。 .rgs 文件格式特定于 ATL，通常不能按设备使用安装创作工具。 VSPackage 安装程序的注册信息必须单独维护。 例如，开发人员可以将 .reg 格式的文件与 .rgs 文件更改同步。 .reg 文件可以与 RegEdit 合并以进行开发工作，也可以由安装程序使用。

## <a name="registering-managed-vspackages"></a>注册托管 VS 包
 RegPkg 工具从托管 VSPackage 读取注册属性，可以将信息直接写入注册表，也可以编写安装程序可以使用的 .reg 格式文件。

> [!NOTE]
> RegPkg 工具不可再分发，不能用于在用户的系统上注册 VSPackage。

## <a name="why-vspackages-should-not-self-register-at-install-time"></a>为什么 VS 包不应在安装时自行注册
 您的 VSPackage 安装程序不应依赖自注册。 乍一看，仅在 VSPackage 本身中保留 VSPackage 的注册表值似乎是个好主意。 鉴于开发人员需要可用于其日常工作和测试的注册表值，因此避免在安装程序中维护注册表数据的单独副本是有意义的。 安装程序可以依靠 VSPackage 本身来写入注册表值。

 虽然理论上是好的，但自我注册有几个缺陷，使其不适合 VSPackage 安装：

- 正确支持安装、卸载、安装回滚和卸载回滚需要针对每个通过调用 RegPkg 自行注册的托管 VSPackage 编写四个自定义操作。

- 并行支持的方法可能需要编写四个自定义操作，针对[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]的每个受支持的版本调用 RegSvr32 或 RegPkg。

- 具有自注册模块的安装无法安全地回滚，因为无法说明其他功能或应用程序是否使用自注册密钥。

- 自注册的 DLL 有时链接到不存在或版本错误的辅助 DLL。 相反，Windows 安装程序可以使用注册表表注册 DLL，而注册表表不依赖于系统的当前状态。

- 如果组件既指定为来自源的运行，又列在 SelfReg 表中，则可以拒绝对网络资源（如类型库）的访问。 这可能导致在管理安装期间安装组件失败。

## <a name="see-also"></a>请参阅
- [Windows 安装程序](/windows/desktop/Msi/windows-installer-portal)
- [托管包注册](https://msdn.microsoft.com/library/f69e0ea3-6a92-4639-8ca9-4c9c210e58a1)
