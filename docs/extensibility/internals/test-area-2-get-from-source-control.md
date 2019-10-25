---
title: 测试区域2：从源代码管理获取 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, getting items from source control
- source control [Visual Studio SDK], getting items from
ms.assetid: cbd345c5-ca43-4630-b7a4-85564f4e2090
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: dca98c927209062d2a1fc67c309d2f32c18d1b5d
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72722569"
---
# <a name="test-area-2-get-from-source-control"></a>测试区域 2：从源代码管理获取
此测试区域涵盖通过 Get 命令从版本存储区中检索项的测试用例。 这些测试用例可同时应用于本地项目和 Web 项目。

## <a name="command-menu-access"></a>命令菜单访问
 以下 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 集成开发环境菜单路径在测试用例中使用。

##### <a name="get-latest-version"></a>获取最新版本：

- **文件**、**源代码管理**、**获取最新版本**。

- **文件**，**获取最新版本**。

- 快捷菜单，**获取最新版本**。

- Get：**文件**、**源代码管理**、**获取**。

## <a name="expected-behavior"></a>预期行为

##### <a name="get-latest-version"></a>获取最新版本：
 从版本存储区中执行项的最新版本的无提示（无 UI）检索。

##### <a name="get"></a>获取：
 显示 "**获取**" 对话框，允许用户对要检索的文件集进行更改，以及修改影响文件检索方式的选项。

## <a name="test-cases"></a>测试用例

|操作|测试步骤|要验证的预期结果|
|------------|----------------|--------------------------------|
|获取本地不存在的文件的最新版本|1. 创建项目。<br />2. 向项目添加项。<br />3. 将项目置于源代码管理下。<br />4. 删除项的本地副本。<br />5. 获取项的最新版本（快捷菜单，**获取最新版本**）。|项目文件在本地检索。|
|获取本地不存在的文件|1. 创建项目。<br />2. 向项目添加项。<br />3. 将项目置于源代码管理下。<br />4. 删除项的本地副本。<br />5. 获取项（**文件**、**源代码管理**、**获取**\<item >）。|项目文件在本地检索。|
|获取以独占方式签出并在本地修改的文件|1. 创建项目。<br />2. 向项目添加项。<br />3. 将项目置于源代码管理下。<br />4. 仅签出项目项。<br />5. 修改本地副本。<br />6. 获取项的最新版本（**File**，**获取最新版本的**\<item >）。 如果此步骤成功，则继续下一步。<br />7. 在警告对话框中单击 "**替换**" 按钮。|**步骤6中的 ReResult** `:`<br /><br /> "警告" 对话框指示已签出文件。<br /><br /> **步骤7中的 ReResult：**<br /><br /> 修改后的本地文件被版本存储区中的原始版本替换。<br /><br /> 文件是可读/写的。|
|获取并替换已签出、共享和在本地修改的文件|1. 创建一个新项目。<br />2. 向项目添加项。<br />3. 将项目置于源代码管理下。<br />4. 以共享方式签出项目项。<br />5. 修改本地副本。<br />6. 获取项的最新版本（**File**，**获取最新版本的**\<item >）。 如果此步骤成功，则继续下一步。<br />7. 在警告对话框中单击 "**替换**"。|**步骤6中的结果：**<br /><br /> "警告" 对话框指示已签出文件。<br /><br /> **步骤7中的结果：**<br /><br /> 修改后的本地文件被版本存储区中的原始版本替换。<br /><br /> 文件是可读/写的。|
|获取在本地存在的文件，与版本存储区中的最新版本相同|1. 创建一个新项目。<br />2. 向项目添加项。<br />3. 将项目置于源代码管理下。<br />4. 获取项（**文件**、**源代码管理**、**获取**\<item >）。|本地文件保持不变。|
|获取包含一个项目的解决方案|1. 创建一个包含一个项目的解决方案。<br />2. 将解决方案置于源代码管理下。<br />3. 在本地删除所有项目文件。<br />4. 获取解决方案（**文件**、**源代码管理**、**获取**）。|所有删除的文件都在本地还原。|

## <a name="see-also"></a>请参阅
- [源代码管理插件的测试指南](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)