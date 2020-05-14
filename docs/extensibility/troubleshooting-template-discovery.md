---
title: 在可视化工作室中排除模板发现 |微软文档
ms.date: 01/02/2018
ms.topic: conceptual
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 078d06c797c3b228c1ea5b1d836dceb0394b3174
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80698937"
---
# <a name="troubleshooting-template-installation"></a>故障排除模板安装

如果在部署项目或项目模板时遇到问题，可以启用诊断日志记录。

::: moniker range="vs-2017"

1. 在*公用 7_IDE_公用扩展文件夹中*为安装创建 pkgdef 文件。 例如 *，C：_程序文件 （x86）\微软可视化工作室\2017_企业_通用7_IDE_通用扩展\启用PkgDef_pkgdef*。

::: moniker-end

::: moniker range=">=vs-2019"

1. 在*公用 7_IDE_公用扩展文件夹中*为安装创建 pkgdef 文件。 例如 *，C：_程序文件 （x86）\微软可视化工作室\2019_企业_通用7_IDE_通用扩展\启用PkgDef_pkgdef*。

::: moniker-end

2. 将以下内容添加到 pkgdef 文件：

    ```
    [$RootKey$\VsTemplate]
    "EnableTemplateDiscoveryLog"=dword:00000001
    ```

3. 打开安装并运行`devenv /updateConfiguration`的[开发人员命令提示。](/dotnet/framework/tools/developer-command-prompt-for-vs)

::: moniker range="vs-2017"

4. 打开可视化工作室并启动"新项目"和"新项目"对话框，以初始化两个模板树。

   模板日志现在以 **%LOCALAPPDATA%*Microsoft_VisualStudio_15.0_[实例id]\VsTemplate诊断列表.csv（** 实例id对应于可视化工作室实例的安装 ID） 中显示。 每个模板树初始化都会将条目追加到此日志。

::: moniker-end

::: moniker range=">=vs-2019"

4. 打开可视化工作室并启动 **"创建新项目和****新项目"** 对话框，以初始化两个模板树。

   模板日志现在以 **%LOCALAPPDATA%*Microsoft_VisualStudio_16.0_[实例id]\VsTemplate诊断列表.csv（** 实例id对应于可视化工作室实例的安装 ID） 中显示。 每个模板树初始化都会将条目追加到此日志。

::: moniker-end

日志文件包含以下列：

- **FullPathtoTemplate**， 具有以下值：

  - 1 表示基于清单的部署

  - 0 表示基于磁盘的部署

- **模板文件名称**

- 其他模板属性

> [!NOTE]
> 要禁用日志记录，请删除 pkgdef 文件，或将 的值`EnableTemplateDiscoveryLog`更改为`dword:00000000`，然后再次`devenv /updateConfiguration`运行。

## <a name="see-also"></a>请参阅

- [创建自定义项目和项目模板](creating-custom-project-and-item-templates.md)
