---
title: “工具箱”->“数据”选项卡 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- Toolbox, Data tab
- Data tab, Toolbox
- data [Visual Studio], Toolbox
ms.assetid: 2ae38b2a-29d2-461c-a67d-29dad274bf45
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 9349745eeee24f2f8b1e62eb2b01bd75273c86d8
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72658586"
---
# <a name="toolbox-data-tab"></a>工具箱，“数据”选项卡
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

显示可添加到窗体和组件的数据对象。 创建具有关联设计器的项目时，将会显示“工具箱”的“数据”选项卡   。 默认情况下，“工具箱”将出现在 Visual Studio 集成开发环境中；如果需要显示“工具箱”，请从“视图”菜单中选择“工具箱”     。

> [!TIP]
> 运行“数据源配置向导”将自动创建和配置大部分数据项。 有关详细信息，请参阅[使用 Visual Studio 创建数据应用程序](https://msdn.microsoft.com/28edce21-220a-484c-b461-a75b0232d293)。

## <a name="ui-element-list"></a>UI 元素列表
 若要直接转到某个组件的 .NET Framework 参考页，请针对“工具箱”中的项或设计器栏中的组件项按“F1”   。

|name|说明|
|----------|-----------------|
|<xref:System.Data.DataSet>|向窗体或组件中添加类型化或非类型化数据集的实例。 将此对象拖到设计器上后，它将显示一个对话框，可在其中选择一个现有的类型化数据集类或指定希望创建新的非类型化空数据集。 注意：  不要使用“工具箱”上的 <xref:System.Data.DataSet> 对象创建新的类型化数据集架构和类  。 有关详细信息，请参阅[创建和配置数据集](../../data-tools/create-and-configure-datasets-in-visual-studio.md)。|
|<xref:System.Windows.Forms.DataGridView>|提供一种以表格格式显示数据的功能强大且灵活的方法。|
|<xref:System.Windows.Forms.BindingSource>|简化将控件绑定到基础数据源的过程。|
|<xref:System.Windows.Forms.BindingNavigator>|表示窗体上绑定到数据的控件的导航和操作用户界面 (UI)。|

## <a name="see-also"></a>另请参阅
 [数据演练](https://msdn.microsoft.com/library/15a88fb8-3bee-4962-914d-7a1f8bd40ec4)[将 Windows 窗体控件绑定到 visual studio 中的数据，](../../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)使[应用程序能够](https://msdn.microsoft.com/library/c17bdb7e-c234-4f2f-9582-5e55c27356ad)[在 visual Studio 中接收数据绑定控件](../../data-tools/bind-controls-to-data-in-visual-studio.md)[验证数据](https://msdn.microsoft.com/library/b3a9ee4e-5d4d-4411-9c56-c811f2b4ee7e)