---
title: “设置”页面，项目设计器
ms.date: 06/14/2018
ms.topic: reference
f1_keywords:
- ApplicationSettingsOverview
helpviewer_keywords:
- Settings page in Project Designer
- Project Designer, Settings page
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d7422b87d0f812de2d99d59c2932e9aa2b9e6315
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62989964"
---
# <a name="settings-page-project-designer"></a>“设置”页面，项目设计器

可在项目设计器的“设置”页面上指定项目的应用程序设置。 通过应用程序设置，能够为应用程序动态存储和检索属性设置及其他信息。 这些设置还能让你维护客户端计算机上的自定义应用程序和用户首选项。 有关详细信息，请参阅[管理应用程序设置](../managing-application-settings-dotnet.md)。

要访问“设置”页，请在解决方案资源管理器中选择项目节点，然后选择“项目” > “属性”。 项目设计器出现时，选择“设置”选项卡。

## <a name="header-bar"></a>标题栏

“设置”页顶部的标题栏包含多个控件：

**同步**

“同步”可将应用程序运行时或调试期间使用的用户范围的设置还原为在设计时定义的默认值。 要还原数据，请从磁盘中而不是项目数据中删除运行时生成的应用程序特定文件。

**加载 Web 设置**

“加载 Web 设置”将显示“登录”对话框，让你能够加载经身份验证的用户或匿名用户的设置。 只有在已启用“服务”页上的客户端应用程序服务并指定“Web 设置服务位置”时，才启用此按钮。

**查看代码**

对于 C# 项目，可使用“查看代码”按钮查看 Settings.cs 文件中的代码。 此文件定义 `Settings` 类，可用于处理 `Settings` 对象上的特定事件。 在非 Visual Basic 语言中，必须显式调用此包装类的 `Save` 方法，才能持久保存用户设置。 此操作通常在主窗体的 Closing 事件处理程序中完成。 `Save` 方法调用示例如下所示：

```csharp
Properties.Settings.Default.Save();
```

对于 Visual Basic 项目，可使用“查看代码”按钮查看 Settings.vb 文件中的代码。 此文件定义 `MySettings` 类，可用于处理 `My.Settings` 对象上的特定事件。 要详细了解如何使用 `My.Settings` 对象访问应用程序设置，请参阅[访问应用程序设置](/dotnet/visual-basic/developing-apps/programming/app-settings/accessing-application-settings)。

要详细了解如何访问应用程序设置，请参阅 [Windows 窗体的应用程序设置](/dotnet/framework/winforms/advanced/application-settings-for-windows-forms)。

**访问修饰符**

“访问修饰符”按钮指定 `Properties.Settings`（对于 C#）或 `My.Settings`（对于 Visual Basic）帮助程序类的访问级别，这些类分是 Visual Studio 在 Settings.Designer.cs 或 Settings.Designer.vb 中生成的。

对于 Visual C# 项目，访问修饰符可为“内部”或“公共”。

对于 Visual Basic 项目，访问修饰符可为“友元”或“公共”。

默认情况下，设置在 C# 中为“内部”，在 Visual Basic 中为“友元”。 如果 Visual Basic 以“内部”或“友元”形式生成帮助程序类，则可执行文件 (.exe) 应用程序无法访问已添加到类库（.dll 文件）中的资源和设置。 如果需要共享类库中的资源和设置，请将访问修饰符设置为“公共”。

有关设置帮助程序类的详细信息，请参阅[管理应用程序设置](../managing-application-settings-dotnet.md)。

## <a name="settings-grid"></a>设置网格

“设置网格”用于配置应用程序设置。 此网格包括以下列：

**名称**

在此字段中输入应用程序设置的名称。

**Type**

使用下拉列表选择设置类型。 使用频率最高的类型将显示在下拉列表中，例如 String、(Connection string) 和 System.Drawing.Font。 可选择列表末尾的“浏览”，然后在“选择类型”对话框中选择一种类型，进而改选其他类型。 选择一种类型后，它会添加到下拉列表中的常用类型（仅限当前解决方案）。

**范围**

选择“应用程序”或“用户”。

应用程序范围的设置（例如连接字符串）与应用程序相关联。 用户无法在运行时更改应用程序范围的设置。

用户范围的设置（例如系统字体）旨在用于用户首选项。 用户可在运行时更改这些设置。

**值**

与应用程序设置关联的数据或值。 例如，如果设置为字体，则它的值可以是“Verdana, 9.75pt, 样式=粗体”。

## <a name="see-also"></a>请参阅

- [管理应用程序设置](../managing-application-settings-dotnet.md)
- [访问应用程序设置 (Visual Basic)](/dotnet/visual-basic/developing-apps/programming/app-settings/accessing-application-settings)