---
title: 如何：创建和编辑配置 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- solution build configurations, editing
- build configurations, creating
- solution build configurations, creating
- build configurations, editing
- builds [Visual Studio], setting up
- property pages
- Configuration Manager
- project build configurations, creating
- project build configurations, editing
ms.assetid: 19be121c-148e-4ece-bbfc-d20b08cfc3f7
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d5f5d8bb92b80942a95528a0b2e4c7e64bbfafc8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72668141"
---
# <a name="how-to-create-and-edit-configurations"></a>如何：创建和编辑配置
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以为一个解决方案创建多个生成配置。 例如，可以配置调试生成供测试人员用于查找和修复问题，也可以配置不同种类的生成，供你分发给不同的客户。

 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]

## <a name="creating-build-configurations"></a>创建生成配置
 可以使用“配置管理器”对话框选择或修改现有生成配置，也可以创建新的生成配置****。

#### <a name="to-open-the-configuration-manager-dialog-box"></a>打开“配置管理器”对话框

- 在“解决方案资源管理器”中，打开解决方案的快捷菜单，然后选择“配置管理器”********。

  > [!NOTE]
  > 如果快捷菜单上没有“配置管理器”命令，请查看菜单栏上的“生成”菜单********。 如果菜单栏上也没有，请依次选择“工具”、“选项”，然后在“选项”对话框的左侧窗格中依次展开“项目和解决方案”、“常规”，之后在右侧窗格中选择“显示高级生成配置”复选框************************。

   在“配置管理器”对话框中，可以使用“活动解决方案配置”下拉列表选择解决方案级生成配置，修改现有配置或创建新的配置********。 可以使用“活动解决方案平台”下拉列表选择配置面向的平台、修改现有平台或添加新的平台****。 “项目上下文”窗格会列出解决方案中的项目****。 对于每个项目，可以选择项目特定的配置和平台、修改现有配置和平台、创建新配置或添加新平台。 使用解决方案级配置生成或部署解决方案时，还可以选择指示是否包含每个项目的复选框。

  设置所需配置后，可以设置适用于这些配置的项目属性。

#### <a name="to-set-properties-based-on-configurations"></a>根据配置来设置属性

- 在“解决方案资源管理器” 中，打开某项目的快捷菜单，然后选择“属性”********。

     “属性页”窗口随即打开****。

     可以针对配置设置属性。 例如，针对“发布”配置，可以指定生成解决方案时优化代码，对于“调试”配置，可以指定包含 `DEBUG` 条件编译符号。 有关属性页设置的详细信息，请参阅[项目设计器简介](https://msdn.microsoft.com/898dd854-c98d-430c-ba1b-a913ce3c73d7)。

## <a name="creating-and-modifying-project-configurations"></a>创建和修改项目配置

#### <a name="to-create-a-project-configuration"></a>创建项目配置

1. 打开“配置管理器”**** 对话框。

2. 在“项目”列中选择一个项目****。

3. 在该项目的“配置”下拉列表中，选择“新建”********。

     “新建项目配置”对话框随即打开****。

4. 在“名称”框中，输入新配置的名称****。

5. 若要使用现有项目配置的属性设置，在“从此处复制设置”下拉列表中，选择一种配置****。

6. 若要同时创建解决方案级配置，勾选“创建新的解决方案配置”复选框****。

#### <a name="to-rename-a-project-configuration"></a>重命名项目配置

1. 打开“配置管理器”**** 对话框。

2. 在“项目”列中，选择项目配置要重命名的项目****。

3. 在该项目的“配置”下拉列表中，选择“编辑”********。

     “编辑项目配置”对话框随即打开****。

4. 选择要更改的项目配置名称。

5. 选择“重命名”，然后输入新名称****。

## <a name="creating-and-modifying-solution-wide-build-configurations"></a>创建和修改解决方案级的生成配置

#### <a name="to-create-a-solution-wide-build-configuration"></a>创建解决方案级的生成配置

1. 打开“配置管理器”**** 对话框。

2. 在“活动解决方案配置”下拉列表中，选择“新建”********。

     “新建解决方案配置”对话框随即打开****。

3. 在“名称”文本框中，输入新配置的名称****。

4. 若要使用现有解决方案配置的设置，在“从此处复制设置”下拉列表中，选择一种配置****。

5. 若要同时创建项目配置，请勾选“创建新的项目配置”复选框****。

#### <a name="to-rename-a-solution-wide-build-configuration"></a>重命名解决方案级的生成配置

1. 打开“配置管理器”**** 对话框。

2. 在“活动解决方案配置”下拉列表中，选择“编辑”********。

     “编辑解决方案配置”对话框随即打开****。

3. 选择要更改的解决方案配置名称。

4. 选择“重命名”，然后输入新名称****。

#### <a name="to-modify-a-solution-wide-build-configuration"></a>修改解决方案级的生成配置

1. 打开“配置管理器”**** 对话框。

2. 在“活动解决方案配置”下拉列表中，选择所需配置****。

3. 在“项目上下文”窗格中，对每个项目，选择所需“配置”和“平台”，并选择是否“生成”该项目以及是否进行“部署”********************。

## <a name="see-also"></a>另请参阅
 [了解生成配置](../ide/understanding-build-configurations.md)[在 Visual Studio 中生成和清理项目和解决方案](../ide/building-and-cleaning-projects-and-solutions-in-visual-studio.md)[笔尖如何：修改项目属性和配置设置](https://msdn.microsoft.com/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)
