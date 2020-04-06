---
title: 创作 Windows 安装程序包 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- .msi files, VSPackages
- msi files, VSPackages
ms.assetid: 0ce7c21d-0d3f-47fe-a0bb-eed506e32609
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 03d30c0e2b3b375e6e0efedddd3a017fbfb8646a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710030"
---
# <a name="author-a-windows-installer-package"></a>编写 Windows 安装程序包
数据驱动 Windows 安装程序模型。 例如，您不是编写过程脚本来复制文件和编写注册表项，而是在包含文件和注册表数据的数据库表中创作行和列。

## <a name="database-entries"></a>数据库条目
要安装 VSPackage，Windows 安装程序包必须包含数据库条目才能执行以下任务：

- 搜索系统以查找 VSPackage[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]支持的版本（使用包括应用搜索、CompLocator、RegLocator、DrLocator 和签名在内的 Windows 安装程序表）。

- 如果未安装支持的版本[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]或不符合 VS 包的另一个系统要求（使用启动条件表），则取消安装。

- 安装 VSPackage 和从属文件（使用目录、组件和文件表）。

- 向注册表添加 VSPackage 的适当信息（使用注册表表）。

- 通过调用[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]**devenv.exe /安装程序**（使用自定义操作表）将 VSPackage 集成到其中。

有关详细信息，请参阅[Windows 安装程序](/windows/desktop/Msi/windows-installer-portal)。

## <a name="setup-tools"></a>设置工具
各种第三方设置工具为 Windows 安装程序包提供了开发环境。 提供以下免费工具：

- 安装护盾限量版

   您可以通过可视化工作室**新项目**对话框获得有限版本的安装程序。 展开**其他项目类型**，然后选择 **"设置和部署**"。 选择安装护盾模板。

- Windows 安装程序 XML 工具集

   Windows 安装程序 XML （WiX） 工具集从 XML 源文件生成 Windows 安装程序包。 WiX 工具集是 Microsoft 开源项目。 你可以从[Wix工具集](https://sourceforge.net/projects/wix/)下载源代码和可执行文件。

   有关[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]通过使用 集成到 中的商业产品，[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]请参阅[可视化工作室市场](https://marketplace.visualstudio.com/)。

## <a name="see-also"></a>请参阅
- [使用 Windows 安装程序安装 VS 包](../../extensibility/internals/installing-vspackages-with-windows-installer.md)
