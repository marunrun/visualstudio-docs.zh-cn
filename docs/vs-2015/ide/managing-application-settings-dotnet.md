---
title: 管理应用程序设置 (.NET) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- msvse_settingsdesigner.err.nameblank
helpviewer_keywords:
- application settings [Visual Studio]
ms.assetid: 35254321-ad14-47d9-b8c6-39ab3203c5d9
caps.latest.revision: 27
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 85cc90170b2dc665bcdd5acd97860c47ef5a14c4
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74293869"
---
# <a name="managing-application-settings-net"></a>管理应用程序设置 (.NET)

[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通过应用程序设置，可以动态存储应用程序信息。 通过设置，可将不应包含在应用程序代码中的信息（例如连接字符串）、用户首选项以及运行时需要的其他信息存储在用户端计算机上。

应用程序设置取代了 Visual Studio 早期版本中使用的动态属性。

每个应用程序设置必须具有唯一的名称。 该名称可以是字母、数字或下划线的任意组合，但名称不能以数字开头且不能包含空格。 可通过 `Name` 属性来更改名称。

应用程序设置可以存储为可序列化成 XML 或包含实现 `TypeConverter` / `ToString`/`FromString`的任何数据类型。 最常见的类型有 `String`、 `Integer`和 `Boolean`，但也可以将值存储为 <xref:System.Drawing.Color>、 <xref:System.Object>或连接字符串。

应用程序设置还包含值。 这些值通过 **“值”** 属性来设置，而且必须与设置的数据类型匹配。

此外，在设计时可将应用程序设置绑定到窗体或控件的属性。

有两类基于范围的应用程序设置：

- 应用程序范围的设置可以用于诸如 Web 服务的 URL 或数据库连接字符串这类的信息。 这些值是与应用程序关联的。 因此，用户无法在运行时更改这些值。

- 用户范围的设置可以用于诸如保持窗体的最后位置或字体首选项这类的信息。 用户可以在运行时更改这些值。

  可以使用 **“范围”** 属性更改设置类型。

  项目系统将应用程序设置存储在两个 XML 文件中：一个是 app.config 文件，它是创建第一个应用程序设置时在设计时创建的；另一个是 user.config 文件，它是当运行应用程序的用户更改任何用户设置的值时在运行时创建的。 请注意，用户设置中的更改不会写到磁盘，除非应用程序专门调用某一方法这样做。

## <a name="creating-application-settings-at-design-time"></a>在设计时创建应用程序设置

在设计时，可用两种方法来创建应用程序设置：通过使用 **“项目设计器”** 的 **“设置”** 页，或通过使用窗体或控件的 **“属性”** 窗口，都可以让你将设置直接绑定到属性。

当你创建应用程序范围的设置（例如，数据库连接字符串或对服务器资源的引用）时， [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 将它与 `<applicationSettings>` 标记一起保存在 app.config 文件中。 （连接字符串保存在 `<connectionStrings>` 标记下。）

当你创建用户范围的设置（例如，默认字体、主页或窗口大小）时， [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 将它与 `<userSettings>` 标记一起保存在 app.config 中。

> [!IMPORTANT]
> 当你将连接字符串存储在 app.config 中时，应该采取预防措施以避免泄露连接字符串中的敏感信息（如密码或服务器路径）。
>
> 如果从外部源获取连接字符串信息（如用户提供用户 ID 和密码），则必须小心以确保用于构造连接字符串的值不会包含可以更改连接行为的附加连接字符串参数。
>
> 可考虑使用“受保护的配置”功能以加密配置文件中的敏感信息。 有关详细信息，请参阅 [Protecting Connection Information](https://msdn.microsoft.com/library/1471f580-bcd4-4046-bdaf-d2541ecda2f4)（保护连接信息）。

> [!NOTE]
> 由于没有类库的配置文件模型，应用程序设置不适用于类库项目。 Visual Studio Tools for Office DLL 项目是一个例外，它可以有一个配置文件。

## <a name="using-customized-settings-files"></a>使用自定义的设置文件

可以将自定义的设置文件添加到项目中，以方便进行设置组的管理。 单个文件中包含的设置会作为一个单元进行加载和保存。 因此，如果能够将常用组和不常用组的设置分开存储在单独的文件中，则可以节省加载和保存设置的时间。

例如，可以将诸如 SpecialSettings.settings 的文件添加到项目中。 虽然 `SpecialSettings` 类未在 `My` 命名空间中公开，但可以使用 **“查看代码”** 读取包含 `Partial Class SpecialSettings`的自定义设置文件。

“设置设计器”首先搜索项目系统创建的 Settings.settings 文件；此文件是“项目设计器”在 **“设置”** 选项卡中显示的默认文件。Settings.settings 位于 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 项目的 My Project 文件夹和 [!INCLUDE[csprcs](../includes/csprcs-md.md)] 项目的 Properties 文件夹中。 然后，“项目设计器”在项目的根文件夹中搜索其他设置文件。 因此，你应当将自定义的设置文件放在此根文件夹中。 如果将 .settings 文件添加到项目中的其他地方，则“项目设计器”将无法找到此文件。

## <a name="accessing-or-changing-application-settings-at-run-time-in-visual-basic"></a>在运行时访问或更改 Visual Basic 应用程序的设置

在 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 项目中，你可以使用 `My.Settings` 对象在运行时访问应用程序设置。 在 **“设置”** 页上，单击 **“查看代码”** 按钮以查看 Settings.vb 文件。 Settings.vb 定义 `Settings` 类，此类使你能够处理设置类上的以下事件： <xref:System.Configuration.ApplicationSettingsBase.SettingChanging>、 <xref:System.Configuration.ApplicationSettingsBase.PropertyChanged>、 <xref:System.Configuration.ApplicationSettingsBase.SettingsLoaded>和 <xref:System.Configuration.ApplicationSettingsBase.SettingsSaving>。 请注意，Settings.vb 中的 `Settings` 类是分部类，其中仅显示用户所有的代码，而不显示整个生成的类。 有关使用 `My.Settings` 对象访问应用程序设置的更多信息，请参阅 [Accessing Application Settings](https://msdn.microsoft.com/library/e38d0cc7-247a-46ca-ba04-f2913f0adb2e)的任何数据类型。

在运行时用户更改的任何用户范围的设置的值（例如窗体的位置）都存储在 user.config 文件中。 请注意，默认值仍保存在 app.config 中。

如果在运行期间（例如在测试应用程序过程中）已更改任何用户范围的设置，并要将这些设置重置为其默认值，请单击 **“同步”** 按钮。

强烈建议使用 `My.Settings` 对象和默认 .settings 文件来访问设置。 原因是可以使用“设置设计器”为设置分配属性，此外，还将在应用程序关闭之前自动保存用户设置。 但是， [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 应用程序可以直接访问设置。 在这种情况下，你必须访问 `MySettings` 类并使用项目根目录中的自定义 .settings 文件。 与处理 C# 应用程序时一样，在结束应用程序之前还必须保存用户设置；下一节会对此进行说明。

<!-- markdownlint-disable MD003 MD020 -->
## <a name="accessing-or-changing-application-settings-at-run-time-in-visual-c"></a>在运行时访问或更改 Visual C# 应用程序的设置
<!-- markdownlint-enable MD003 MD020 -->

在 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]以外的语言（如 [!INCLUDE[csprcs](../includes/csprcs-md.md)]）中，必须直接访问 `Settings` 类，如下面的 [!INCLUDE[csprcs](../includes/csprcs-md.md)] 示例中所示。

```csharp
Properties.Settings.Default.FirstUserSetting = "abc";
```

还必须显式调用此包装器类的 `Save` 方法，才能持久地保存用户设置。 此操作通常在主窗体的 `Closing` 事件处理程序中完成。 下面的 [!INCLUDE[csprcs](../includes/csprcs-md.md)] 示例演示对 `Save` 方法的调用。

```csharp
Properties.Settings.Default.Save();
```

有关通过 `Settings` 类访问应用程序设置的常规信息，请参阅 [Application Settings Overview](https://msdn.microsoft.com/library/0dd8bca5-a6bf-4ac4-8eec-5725d08b38dc)（应用程序设置概述）。 有关循环访问设置的信息，请参阅此 [论坛帖子](https://social.msdn.microsoft.com/Forums/en-US/40fbb470-f1e8-4a02-a4a0-9f62b54d0fc4/is-this-possible-propertiessettingsdefault?forum=csharpgeneral)。

## <a name="see-also"></a>另请参阅

- [访问应用程序设置](https://msdn.microsoft.com/library/e38d0cc7-247a-46ca-ba04-f2913f0adb2e)
