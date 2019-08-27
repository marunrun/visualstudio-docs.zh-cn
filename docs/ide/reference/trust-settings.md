---
title: 文件和文件夹的信任设置
description: 了解如何更改文件和文件夹的信任设置以确保 Visual Studio 的安全。
author: abuchholtzau
ms.author: allisb
ms.date: 09/05/2018
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Environment.PathTrustOptions
helpviewer_keywords:
- file security
- folder security
- mark of the web
- trusted files
- trusted folders
ms.openlocfilehash: 011673bca7be569b5b350dc264148d5a7890d39c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62789617"
---
# <a name="configure-trust-settings-for-files-and-folders"></a>配置文件和文件夹的信任设置

Visual Studio 在打开具有 [Web 标记](/previous-versions/windows/internet-explorer/ie-developer/compatibility/ms537628(v=vs.85))的项目之前，将提示用户批准。 为了增强安全性，还可以配置 Visual Studio，使其在打开具有 Web 属性标记或者未指定为“受信任”的任何文件或文件夹之前提示用户批准。 默认情况下，禁用文件和文件夹检查。

> [!WARNING]
> 在审批文件、文件夹或解决方案之前，仍应先确保它们来自受信任的人员或受信任的位置。

## <a name="configure-trust-settings"></a>配置信任设置

若要更改信任设置，请执行以下步骤：

1. 打开“工具” > “选项” > “信任设置”，然后选择右侧窗格中的“配置信任设置”链接。

2. 选择所需的文件和文件夹检查级别。 可以对每个文件和文件夹进行不同的检查。 选项为：

   * **不验证**：Visual Studio 不执行任何检查。

   * **验证 Web 属性的标记**：如果文件或文件夹具有 Web 属性的标记，则 Visual Studio 将阻止它们并请求打开权限。

   * **验证路径是否可信**：如果文件或文件夹路径不属于“受信任路径”列表，则 Visual Studio 将阻止它们并请求打开权限。

   ![信任验证选项](media/trust-settings.png)

## <a name="add-trusted-paths"></a>添加受信任路径

若要添加受信任路径，请执行以下步骤：

1. 打开“工具” > “选项” > “信任设置”，然后选择右侧窗格中的“配置信任设置”链接。

2. 单击“信任设置”对话框中的“添加”，然后选择“文件”或“文件夹”。

3. 导航到并选择要添加到受信任列表的文件或文件夹。

   文件或文件夹路径显示在“受信任路径”列表中。

   ![已添加受信任路径](media/trusted-paths.png)

## <a name="remove-trusted-paths"></a>删除受信任路径

若要删除受信任路径，请执行以下步骤：

1. 打开“工具” > “选项” > “信任设置”，然后选择右侧窗格中的“配置信任设置”链接。

2. 在“受信任路径”列表中，选择要删除的路径，然后单击“删除”。

   > [!TIP]
   > 若要选择多个项，选择路径的同时按住 Shift。

   所选的路径都将从“受信任路径”列表中删除。
