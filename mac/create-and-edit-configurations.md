---
title: 创建和编辑生成配置
description: 本文介绍如何在 Visual Studio for Mac 中创建生成配置
author: heiligerdankgesang
ms.author: dominicn
ms.date: 09/18/2019
ms.assetid: CC1B72D6-12FF-4CCC-A9D4-00F2DC14589F
ms.custom: video
ms.openlocfilehash: 26f6e25bfe1284fc31bcd484b905bf5d75c2ba15
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2020
ms.locfileid: "71128424"
---
# <a name="creating-and-editing-build-configurations"></a>创建和编辑生成配置

通过使用生成配置可以精确地控制生成，从而创建配置以满足不同的测试和分发情况。 可以为单个项目创建生成配置，也可创建适用于整个解决方案的生成配置。

可以使用“项目选项”对话框创建新的配置并编辑项目和解决方案的现有配置。

>[!NOTE]
>本主题适用于 Visual Studio for Mac。 对于 Windows 上的 Visual Studio，请参阅[如何：创建和编辑配置](/visualstudio/ide/how-to-create-and-edit-configurations)。

## <a name="creating-a-project-build-configuration"></a>创建项目生成配置

请按照以下步骤创建项目生成配置：

1. 右键单击项目节点，然后选择“选项”  。 还可以双击项目节点，打开“项目选项”对话框。

2. 在“项目选项”对话框中，选择“生成”>“配置”： 

    ![项目选项中的配置管理器](media/create-and-edit-configurations-image2.png)

3. 要创建新配置，请选择“添加”  。 也可以复制任一现有配置。

创建配置后，可以使用“项目选项”中的“生成”部分调整属性，使其适合配置  ：

![配置生成选项](media/create-and-edit-configurations-image3.png)

## <a name="creating-a-solution-build-configuration"></a>创建解决方案生成配置

请按照以下步骤创建解决方案生成配置：

1. 右键单击解决方案节点，然后选择“选项”  。 还可以双击解决方案节点，打开“解决方案选项”对话框。

2. 在“解决方案选项”对话框中，选择“生成”>“配置”： 

    ![解决方案选项中的配置管理器](media/create-and-edit-configurations-image1.png)

3. 要创建新配置，请选择“添加”  。 也可以复制任一现有配置。

创建配置后，可以使用各个项目的“项目选项”对话框中的“生成”部分调整属性，使其适合配置  ：

![配置生成选项](media/create-and-edit-configurations-image3.png)

## <a name="renaming-a-build-configuration"></a>重命名生成配置

要重命名配置，请导航到项目选项或解决方案选项中的“生成”>“配置”，从配置列表中选择它  ：

![配置列表](media/create-and-edit-configurations-image4.png)

选择“重命名”按钮  。

![“重命名”对话框](media/create-and-edit-configurations-image5.png)

然后单击“确定”以确认  。

## <a name="related-video"></a>相关视频

> [!Video https://channel9.msdn.com/Shows/Visual-Studio-Toolbox/Visual-Studio-for-Mac-Launch-Multiple-Projects/player]

## <a name="see-also"></a>请参阅

- [创建和编辑生成配置（Windows 上的 Visual Studio）](/visualstudio/ide/how-to-create-and-edit-configurations)