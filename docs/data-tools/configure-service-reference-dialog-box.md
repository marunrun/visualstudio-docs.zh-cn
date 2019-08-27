---
title: “配置服务引用”对话框
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- msvse_wcf.dlg.ConfigureServiceReference
helpviewer_keywords:
- WCF services, Configure Service Reference dialog box
- service references [Visual Studio], configuring behavior
- Configure Service Reference dialog box
ms.assetid: 25e4c36b-2db6-4e71-9010-b7068255d09d
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 1cf4a809c1353f2fe30383a312f65b6c623083db
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68925673"
---
# <a name="configure-service-reference-dialog-box"></a>“配置服务引用”对话框

通过 "**配置服务引用**" 对话框, 您可以配置 WINDOWS COMMUNICATION FOUNDATION (WCF) 服务的行为。

要访问“配置服务引用”对话框，请右键单击“解决方案资源管理器”中的服务引用，然后选择“配置服务引用”。 还可以通过单击“添加服务引用对话框”中的“高级”按钮来访问该对话框。

## <a name="task-list"></a>任务列表

- 要更改承载 WCF 服务的地址，请在“地址”字段中输入新的地址。

- 要更改 WCF 客户端中类的访问级别，请在“生成的类的访问级别”列表中选择访问级别关键字。

- 要异步调用 WCF 服务方法，请选中“生成异步操作”复选框。

- 要在 WCF 客户端中生成消息约定类型，请选中“始终生成消息约定”复选框。

- 要为 WCF 客户端指定列表集合类型或字典集合类型，请从“集合类型”和“字典集合类型”列表中选择类型。

- 要禁用类型共享，请清除“重新使用引用的程序集中的类型”复选框。 要对引用的程序集的子集启用类型共享，请选中“重新使用引用的程序集中的类型”复选框，接着选中“重新使用所引用的指定程序集中的类型”，然后在“引用的程序集列表”中选择所需的引用。

## <a name="uielement-list"></a>UIElement 列表

**地址**

更新服务引用在其中查找服务的 web 地址。 例如, 在开发过程中, 该服务可能会托管在一个开发服务器上, 稍后会移到生产服务器上, 使得一个地址更改。

> [!NOTE]
> 从“添加服务引用”对话框中显示“配置服务引用”对话框时，“地址”元素不可用。

**生成的类的访问级别**

确定 WCF 客户端类的代码访问级别。

> [!NOTE]
> 对于网站项目，该选项将始终设置为 `Public`，并且无法更改。 有关详细信息，请参阅[服务引用疑难解答](../data-tools/troubleshooting-service-references.md)。

**生成异步操作**

确定是否同步调用 WCF 服务方法 (默认值) 或异步调用。

**生成基于任务的操作**

编写异步代码时, 此选项可让你充分利用随 .NET 4 引入的任务并行库 (TPL)。 请参阅[任务并行库 (TPL)](/dotnet/standard/parallel-programming/task-parallel-library-tpl)。

**始终生成消息约定**

确定是否为 WCF 客户端生成消息协定类型。 有关消息约定的详细信息，请参阅[使用消息约定](/dotnet/framework/wcf/feature-details/using-message-contracts)。

**集合类型**

为 WCF 客户端指定列表集合类型。 默认类型为 <xref:System.Array>。

**字典集合类型**

为 WCF 客户端指定字典集合类型。 默认类型为 <xref:System.Collections.Generic.Dictionary%602>。

**重新使用引用的程序集中的类型**

确定在添加或更新服务时, WCF 客户端是否尝试重用引用程序集中已存在的内容, 而不是生成新类型。 默认情况下，此选项处于选中状态。

**重新使用所有引用的程序集中的类型**

如果选择此选项, 则会在可能的情况下重用**被引用程序集中**的所有类型。 默认情况下，该选项是选中的。

**重新使用所引用的指定程序集中的类型**

如果选择此选项, 则只会重复使用所**引用的程序集列表**中的选定类型。

**引用的程序集列表**

包含项目或网站的被引用程序集的列表。 选择 "**在指定的引用程序集中重用类型**" 时, 可以选择或清除各个程序集。

**添加 Web 引用**

显示“添加 Web 引用”对话框。

> [!NOTE]
> 此选项应仅用于面向 .NET Framework 版本2.0 的项目。
>
> [!NOTE]
> 只有在 "**添加服务引用" 对话框**中显示 "**配置服务引用**" 对话框时, "**添加 Web 引用**" 按钮才可用。

## <a name="see-also"></a>请参阅

- [如何：添加对 web 服务的引用](how-to-add-update-or-remove-a-wcf-data-service-reference.md)
- [Windows Communication Foundation 服务和 WCF 数据服务](../data-tools/configure-service-reference-dialog-box.md)