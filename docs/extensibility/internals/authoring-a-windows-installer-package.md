---
title: 创作 Windows Installer 包 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- .msi files, VSPackages
- msi files, VSPackages
ms.assetid: 0ce7c21d-0d3f-47fe-a0bb-eed506e32609
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: aa967b5f23ff9f4e5afa67b9b1cb4e83707616c6
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72982231"
---
# <a name="author-a-windows-installer-package"></a>创作 Windows Installer 包
数据驱动 Windows Installer 模型。 例如，您可以在数据库表中创作包含文件和注册表数据的行和列，而不是编写过程脚本来复制文件和写入注册表项。

## <a name="database-entries"></a>数据库条目
若要安装 VSPackage，Windows Installer 包必须包含用于执行以下任务的数据库条目：

- 搜索系统，查找 VSPackage 支持的 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 版本（使用包括 AppSearch、CompLocator、RegLocator、DrLocator 和签名的 Windows Installer 表）。

- 如果未安装支持的 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 版本，或者未满足 VSPackage 的其他系统要求（使用 LaunchCondition 表），则取消安装。

- 安装 VSPackage 和相关文件（使用目录、组件和文件表）。

- 将 VSPackage 的相应信息添加到注册表（使用注册表表）。

- 通过调用 VSPackage **/setup** （使用 CustomAction 表）将中的集成 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 在一起。

有关详细信息，请参阅[Windows Installer](/windows/desktop/Msi/windows-installer-portal)。

## <a name="setup-tools"></a>安装工具
许多第三方安装工具为 Windows Installer 包提供了一个开发环境。 提供以下免费工具：

- InstallShield 受限版本

   可以通过 Visual Studio 的 "**新建项目**" 对话框获取有限版本的 InstallShield。 展开 "**其他项目类型**"，然后选择 "**安装和部署**"。 选择 InstallShield 模板。

- Windows Installer XML 工具集

   Windows Installer XML （WiX）工具集从 XML 源文件生成 Windows Installer 包。 WiX 工具集是一个 Microsoft 开源项目。 可以从[Wix 工具集](https://sourceforge.net/projects/wix/)下载源代码和可执行文件。

   有关使用 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]集成到 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 的商业产品，请参阅[Visual Studio Marketplace](https://marketplace.visualstudio.com/)。

## <a name="see-also"></a>请参阅
- [安装 Vspackage 与 Windows Installer](../../extensibility/internals/installing-vspackages-with-windows-installer.md)