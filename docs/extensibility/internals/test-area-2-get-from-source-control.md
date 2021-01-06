---
title: 测试区域2：从源代码管理获取 |Microsoft Docs
description: 此测试区域涵盖了用 Get 从版本存储中检索项的测试用例。 这些测试用例可同时应用于本地项目和 web 项目。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, getting items from source control
- source control [Visual Studio SDK], getting items from
ms.assetid: cbd345c5-ca43-4630-b7a4-85564f4e2090
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 98ed765f78a9e7330e5e1d3864c8a91b63239a3f
ms.sourcegitcommit: 0c9155e9b9408fb7481d79319bf08650b610e719
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/05/2021
ms.locfileid: "97877697"
---
# <a name="test-area-2-get-from-source-control"></a>测试区域 2：从源代码管理获取
此测试区域涵盖通过 Get 命令从版本存储区中检索项的测试用例。 这些测试用例可同时应用于本地项目和 Web 项目。

## <a name="command-menu-access"></a>命令菜单访问
 以下 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 集成开发环境菜单路径用于测试用例。

##### <a name="get-latest-version"></a>获取最新版本：

- **文件**、 **源代码管理**、 **获取最新版本**。

- **文件**， **获取最新版本**。

- 快捷菜单， **获取最新版本**。

- Get： **文件**、 **源代码管理**、 **获取**。

## <a name="expected-behavior"></a>预期行为

##### <a name="get-latest-version"></a>获取最新版本：
 执行无提示 (UI) 从版本存储区中检索项的最新版本。

##### <a name="get"></a>获取：
 显示 " **获取** " 对话框，允许用户对要检索的文件集进行更改，以及修改影响文件检索方式的选项。

## <a name="test-cases"></a>测试用例

|操作|测试步骤|要验证的预期结果|
|------------|----------------|--------------------------------|
|获取本地不存在的文件的最新版本|1. 创建项目。<br />2. 向项目添加项。<br />3. 将项目置于源代码管理下。<br />4. 删除项的本地副本。<br />5. 获取项的最新版本 (快捷菜单上，获取) 的 **最新版本** 。|项目文件在本地检索。|
|获取本地不存在的文件|1. 创建项目。<br />2. 向项目添加项。<br />3. 将项目置于源代码管理下。<br />4. 删除项的本地副本。<br />5. 获取项 (**文件**、 **源代码管理**、 **获取** \<item>) 。|项目文件在本地检索。|
|获取以独占方式签出并在本地修改的文件|1. 创建项目。<br />2. 向项目添加项。<br />3. 将项目置于源代码管理下。<br />4. 仅签出项目项。<br />5. 修改本地副本。<br />6. 获取最新版本的项 (**文件**， **获取) 的最新版本** \<item> 。 如果此步骤成功，则继续下一步。<br />7. 在警告对话框中单击 " **替换** " 按钮。|**步骤6中的 ReResult**`:`<br /><br /> "警告" 对话框指示已签出文件。<br /><br /> **步骤7中的 ReResult：**<br /><br /> 修改后的本地文件被版本存储区中的原始版本替换。<br /><br /> 文件是可读/写的。|
|获取并替换已签出、共享和在本地修改的文件|1. 创建一个新项目。<br />2. 向项目添加项。<br />3. 将项目置于源代码管理下。<br />4. 以共享方式签出项目项。<br />5. 修改本地副本。<br />6. 获取最新版本的项 (**文件**， **获取) 的最新版本** \<item> 。 如果此步骤成功，则继续下一步。<br />7. 在警告对话框中单击 " **替换** "。|**步骤6中的结果：**<br /><br /> "警告" 对话框指示已签出文件。<br /><br /> **步骤7中的结果：**<br /><br /> 修改后的本地文件被版本存储区中的原始版本替换。<br /><br /> 文件是可读/写的。|
|获取在本地存在的文件，与版本存储区中的最新版本相同|1. 创建一个新项目。<br />2. 向项目添加项。<br />3. 将项目置于源代码管理下。<br />4. 获取项 (**文件**、 **源代码管理**、 **获取** \<item>) 。|本地文件保持不变。|
|获取包含一个项目的解决方案|1. 创建一个包含一个项目的解决方案。<br />2. 将解决方案置于源代码管理下。<br />3. 在本地删除所有项目文件。<br />4 **. 获取 (** **文件**、**源代码管理**) 的解决方案。|所有删除的文件都在本地还原。|

## <a name="see-also"></a>另请参阅
- [源代码管理插件的测试指南](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)
