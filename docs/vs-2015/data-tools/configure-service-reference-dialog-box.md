---
title: "\"配置服务引用\" 对话框 |Microsoft Docs"
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: reference
f1_keywords:
- msvse_wcf.dlg.ConfigureServiceReference
helpviewer_keywords:
- WCF services, Configure Service Reference dialog box
- service references [Visual Studio], configuring behavior
- Configure Service Reference dialog box
ms.assetid: 25e4c36b-2db6-4e71-9010-b7068255d09d
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: ac8f4cf619bbdd007bb7aa570f549ae3c0b50e86
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72651114"
---
# <a name="configure-service-reference-dialog-box"></a>“配置服务引用”对话框
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通过 "**配置服务引用**" 对话框，您可以配置 [!INCLUDE[vsindigo](../includes/vsindigo-md.md)] 服务的行为。

> [!NOTE]
> 显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在“工具”菜单上选择“导入和导出设置”。 有关详细信息，请参阅[在 Visual Studio 中自定义开发设置](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。

 要访问“配置服务引用”对话框，请右键单击“解决方案资源管理器”中的服务引用，然后选择“配置服务引用”。 还可以通过单击“添加服务引用对话框”中的“高级”按钮来访问该对话框。

## <a name="task-list"></a>任务列表

- 要更改承载 WCF 服务的地址，请在“地址”字段中输入新的地址。

- 要更改 WCF 客户端中类的访问级别，请在“生成的类的访问级别”列表中选择访问级别关键字。

- 要异步调用 WCF 服务方法，请选中“生成异步操作”复选框。

- 要在 WCF 客户端中生成消息约定类型，请选中“始终生成消息约定”复选框。

- 要为 WCF 客户端指定列表集合类型或字典集合类型，请从“集合类型”和“字典集合类型”列表中选择类型。

- 要禁用类型共享，请清除“重新使用引用的程序集中的类型”复选框。 要对引用的程序集的子集启用类型共享，请选中“重新使用引用的程序集中的类型”复选框，接着选中“重新使用所引用的指定程序集中的类型”，然后在“引用的程序集列表”中选择所需的引用。

## <a name="uielement-list"></a>UIElement 列表
 **地址**用于更新服务引用用于查找服务的 Web 地址。 例如，在开发过程中服务可能承载在开发服务器上，之后又移到了生产服务器上，因而需要进行地址更改。

> [!NOTE]
> 从“添加服务引用”对话框中显示“配置服务引用”对话框时，“地址”元素不可用。

 **生成的类的访问级别**确定 WCF 客户端类的代码访问级别。

> [!NOTE]
> 对于网站项目，该选项将始终设置为 `Public`，并且无法更改。 有关详细信息，请参阅[服务引用故障排除](../data-tools/troubleshooting-service-references.md)。

 **生成异步操作**确定是以同步方式还是异步方式调用 WCF 服务方法（默认值）。

 **生成基于任务的操作**编写异步代码时，此选项可让你充分利用随 .Net 4 引入的任务并行库（TPL）。 请参阅[任务并行库（TPL）](https://msdn.microsoft.com/library/dd460717.aspx)。

 **始终生成消息约定**确定是否将为 WCF 客户端生成消息协定类型。 有关消息约定的详细信息，请参阅[使用消息协定](https://msdn.microsoft.com/library/1e19c64a-ae84-4c2f-9155-91c54a77c249)。

 **集合类型**为 WCF 客户端指定列表集合类型。 默认类型为 <xref:System.Array>。

 **字典集合类型**指定 WCF 客户端的字典集合类型。 默认类型为 <xref:System.Collections.Generic.Dictionary%602>。

 **重新使用引用的程序集中的类型**确定在添加或更新服务时，WCF 客户端是否将尝试重复使用已在引用的程序集中存在的，而不是生成新类型。 默认情况下，此选项处于选中状态。

 **重新使用所有引用的程序集中的类型**如果选择此选项，则会在可能的情况下重用**被引用程序集中**的所有类型。 默认情况下，该选项是选中的。

 **重新使用指定的引用程序集中的类型**如果选择此选项，将只重用**引用的程序集列表**中的选定类型。

 **引用的程序集列表**包含项目或网站引用的程序集的列表。 如果选择了 "**在指定的引用程序集中使用类型**"，则可以选择或清除各个程序集。

 **添加 Web 引用**显示 "[笔尖：添加 Web 引用" 对话框](https://msdn.microsoft.com/bdf05776-c591-40af-bfd7-e1e2aa1e87b5)。

> [!NOTE]
> 此选项只应该用于针对 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 2.0 版的项目。

> [!NOTE]
> 仅当在 "**添加服务引用" 对话框**中显示 "**配置服务引用**" 对话框时，"**添加 Web 引用**" 按钮才可用。

## <a name="see-also"></a>请参阅
 [如何：添加、更新或移除服务引用](https://msdn.microsoft.com/library/cacc14bd-4455-4a44-be78-d2ac16113dd9)[如何：向 Web 服务添加引用](https://msdn.microsoft.com/library/952e49a1-567e-4a74-8cd7-f2e7b62c3168) [Windows Communication Foundation 服务和 WCF 数据服务](../data-tools/configure-service-reference-dialog-box.md)
