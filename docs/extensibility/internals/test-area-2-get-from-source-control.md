---
title: 测试区域 2：从源代码管理获取 |Microsoft Docs
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
ms.openlocfilehash: 31f5f9b9657b0577d6b8e36166049fe46ac2a907
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66331035"
---
# <a name="test-area-2-get-from-source-control"></a>测试区域 2：从源代码管理获取
此测试部分覆盖了用于从通过 Get 命令的版本存储区中检索项的测试用例。 可以应用这些测试用例，对本地和 Web 项目。

## <a name="command-menu-access"></a>命令菜单访问
 以下[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]测试用例中使用集成的开发环境菜单路径。

##### <a name="get-latest-version"></a>获取最新版本：

- **文件**，**源控件**，**获取最新版本**。

- **文件**，**获取最新版本**。

- 快捷菜单中，**获取最新版本**。

- 获取：**文件**，**源控件**，**获取**。

## <a name="expected-behavior"></a>预期的行为

##### <a name="get-latest-version"></a>获取最新版本：
 从版本存储区执行无提示 (无 UI) 检索的项的最新版本。

##### <a name="get"></a>获取：
 显示**获取**对话框中，并允许用户对文件集，将检索，以及修改会影响如何检索这些文件的选项进行更改。

## <a name="test-cases"></a>测试用例

|操作|测试步骤|若要验证的预期的结果|
|------------|----------------|--------------------------------|
|获取最新版本不存在本地的文件|1.创建项目。<br />2.将项添加到项目。<br />3.将受源代码管理项目。<br />4.删除项的本地副本。<br />5.获取项的最新版本 (快捷方式菜单中，**获取最新版本**)。|本地检索项文件。|
|获取本地不存在的文件|1.创建项目。<br />2.将项添加到项目。<br />3.将受源代码管理项目。<br />4.删除项的本地副本。<br />5.获取项 (**文件**，**源代码管理**，**获取**\<项 >)。|本地检索项文件。|
|获取被以独占方式签出和修改本地的文件|1.创建项目。<br />2.将项添加到项目。<br />3.将受源代码管理项目。<br />4.以独占方式签出项目项。<br />5.修改本地副本。<br />6.获取项的最新版本 (**文件**，**获取最新版本的**\<项 >)。 如果此步骤成功，则继续下一步。<br />7.单击**替换为**警告对话框中的按钮。|**步骤 6 中 reResult** `:`<br /><br /> 警告对话框指示签出该文件。<br /><br /> **步骤 7 中 reResult:**<br /><br /> 版本存储区中的原始版本将替换为修改后的本地文件。<br /><br /> 文件是读/写。|
|获取并将文件签出、 共享的并且在本地修改|1.创建新项目。<br />2.将项添加到项目。<br />3.将受源代码管理项目。<br />4.查看为共享的项目项。<br />5.修改本地副本。<br />6.获取项的最新版本 (**文件**，**获取最新版本的**\<项 >)。 如果此步骤成功，则继续下一步。<br />7.单击**替换为**警告对话框中。|**步骤 6 中产生：**<br /><br /> 警告对话框指示签出该文件。<br /><br /> **步骤 7 中的结果：**<br /><br /> 版本存储区中的原始版本将替换为修改后的本地文件。<br /><br /> 文件是读/写。|
|获取本地存在的文件与版本存储区中的最新版本相同|1.创建新项目。<br />2.将项添加到项目。<br />3.将受源代码管理项目。<br />4.获取项 (**文件**，**源代码管理**，**获取**\<项 >)。|本地文件保持不变。|
|获取包含一个项目的解决方案|1.创建包含一个项目的解决方案。<br />2.将受源代码管理解决方案。<br />3.删除所有项目文件本地。<br />4.获取解决方案 (**文件**，**源代码管理**，**获取**)。|将本地还原所有已删除的文件。|

## <a name="see-also"></a>请参阅
- [源代码管理插件的测试指南](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)