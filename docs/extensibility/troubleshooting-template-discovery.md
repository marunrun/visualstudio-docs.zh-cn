---
title: 排查 Visual Studio 中的模板发现问题 |Microsoft Docs
ms.date: 01/02/2018
ms.topic: troubleshooting
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c5225c741206e6a43ff024a5f184404f1ac2bc63
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85904488"
---
# <a name="troubleshooting-template-installation"></a>模板安装故障排除

如果在部署项目或项模板时遇到问题，可以启用诊断日志记录。

::: moniker range="vs-2017"

1. 在*Common7\IDE\CommonExtensions*文件夹中为你的安装创建 .pkgdef 文件。 例如， *C:\Program Files （x86） \Microsoft Visual Studio\2017\Enterprise\Common7\IDE\CommonExtensions\EnablePkgDefLogging.pkgdef*。

::: moniker-end

::: moniker range=">=vs-2019"

1. 在*Common7\IDE\CommonExtensions*文件夹中为你的安装创建 .pkgdef 文件。 例如， *C:\Program Files （x86） \Microsoft Visual Studio\2019\Enterprise\Common7\IDE\CommonExtensions\EnablePkgDefLogging.pkgdef*。

::: moniker-end

2. 将以下内容添加到 .pkgdef 文件：

    ```
    [$RootKey$\VsTemplate]
    "EnableTemplateDiscoveryLog"=dword:00000001
    ```

3. 打开安装的[开发人员命令提示](/dotnet/framework/tools/developer-command-prompt-for-vs)，然后运行 `devenv /updateConfiguration` 。

::: moniker range="vs-2017"

4. 打开 Visual Studio 并启动 "新建项目" 和 "新建项" 对话框以初始化两个模板树。

   模板日志现在显示在 **%LOCALAPPDATA%\Microsoft\VisualStudio\15.0_ [instanceid] \VsTemplateDiagnosticsList.csv**中（Instanceid 与 Visual Studio 实例的安装 ID 相对应）。 每个模板树初始化都会向此日志追加条目。

::: moniker-end

::: moniker range=">=vs-2019"

4. 打开 Visual Studio 并启动 "新建**项目**" 和 "**新建项**" 对话框以初始化两个模板树。

   模板日志现在显示在 **%LOCALAPPDATA%\Microsoft\VisualStudio\16.0_ [instanceid] \VsTemplateDiagnosticsList.csv**中（Instanceid 与 Visual Studio 实例的安装 ID 相对应）。 每个模板树初始化都会向此日志追加条目。

::: moniker-end

日志文件包含以下列：

- **FullPathToTemplate**，它具有以下值：

  - 1用于基于清单的部署

  - 对于基于磁盘的部署为0

- **TemplateFileName**

- 其他模板属性

> [!NOTE]
> 若要禁用日志记录，请删除 .pkgdef 文件，或将的值更改 `EnableTemplateDiscoveryLog` 为 `dword:00000000` ，然后 `devenv /updateConfiguration` 再次运行。

## <a name="see-also"></a>另请参阅

- [创建自定义项目和项模板](creating-custom-project-and-item-templates.md)
