---
title: 如何：从生成中排除项目 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: 17a837ca-5db9-46cd-b5a7-b14ad1d2c47d
caps.latest.revision: 8
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: ffa2b0fd8cab35fc73031d3ead8a5803558c2c07
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72667947"
---
# <a name="how-to-exclude-projects-from-a-build"></a>如何：从生成中排除项目
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你可以生成解决方案，但不生成其包含的所有项目。 例如，你可以排除会中断生成的项目。 在调查并解决问题之后，你可以再生成该项目。

 可以采用以下方法排除项目：

- 将其从活动解决方案配置中暂时删除。

- 创建不包含该项目的解决方案配置。

  有关详细信息，请参阅[了解生成配置](../ide/understanding-build-configurations.md)。

### <a name="to-temporarily-remove-a-project-from-the-active-solution-configuration"></a>从活动解决方案配置中暂时删除项目

1. 在菜单栏上，依次选择 **“生成”** 、 **“配置管理器”** 。

2. 在“项目上下文”表中，找到要从生成中排除的项目。

3. 在项目的“生成”列中，清除复选框。

4. 选择“关闭”按钮，然后重新生成解决方案。

### <a name="to-create-a-solution-configuration-that-excludes-a-project"></a>创建排除项目的解决方案配置

1. 在菜单栏上，依次选择 **“生成”** 、 **“配置管理器”** 。

2. 在“活动解决方案配置”列表中，选择“\<新建>”。

3. 在“名称”框中，输入解决方案配置的名称。

4. 在“从以下对象复制设置”列表中，选择新配置所要基于的解决方案配置（例如，“调试”），然后选择“确定”按钮。

5. 在“配置管理器”对话框中，清除待排除项目的“生成”列中的复选框，然后选择“关闭”按钮。

6. 在“标准”工具栏上，确保“解决方案配置”框中的新解决方案配置是活动配置。

7. 在菜单栏上，依次选择“生成”、“重新生成解决方案”。

## <a name="see-also"></a>请参阅
 [了解生成配置](../ide/understanding-build-configurations.md)[如何：创建和编辑配置](../ide/how-to-create-and-edit-configurations.md)[如何：同时生成多个配置](../ide/how-to-build-multiple-configurations-simultaneously.md)
