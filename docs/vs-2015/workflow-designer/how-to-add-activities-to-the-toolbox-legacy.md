---
title: 如何：向工具箱添加活动 (旧) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
helpviewer_keywords:
- Toolbox, adding activities
- activities, adding to Toolbox
ms.assetid: b66ea29c-120b-40ba-8a61-c1c8240850fa
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: f3f982372f0189871c4f3d294c07a9e3cfc44391
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72656610"
---
# <a name="how-to-add-activities-to-the-toolbox-legacy"></a>如何：向工具箱添加活动（旧版）
当使用面向或的旧版本生成工作流解决方案时 [!INCLUDE[wfd1](../includes/wfd1-md.md)] [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)] ，可以将自定义活动添加到工作流项目中，并将其设计器放置在 **工具箱** 中以便于访问。 您还可以从动态链接库直接向 **工具箱** 添加活动 (DLL) 。

### <a name="to-add-an-activity-to-the-toolbox-from-a-dll"></a>从 DLL 中将活动添加到工具箱

1. 右键单击 " **Windows 工作流**" 下的 "工具箱" 窗口图面，然后单击 " **选择项**"。

2. 在 " **选择工具箱项** " 对话框中，单击 " **system.web 组件** " 选项卡，然后单击窗口右下角的 " **浏览** "。

3. 从包含要添加到 " **工具箱**" 的自定义活动的实现的文件目录中选择 DLL，然后单击 " **打开**"。

4. 单击 **"确定"** 完成将活动添加到 "工具箱"。

## <a name="see-also"></a>另请参阅
 [使用旧版活动设计器](../workflow-designer/using-the-legacy-activity-designer.md)[旧版工作流活动](../workflow-designer/legacy-workflow-activities.md)