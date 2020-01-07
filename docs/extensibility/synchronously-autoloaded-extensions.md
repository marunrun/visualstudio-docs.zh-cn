---
title: 以同步方式加载了扩展
ms.date: 12/11/2019
ms.topic: conceptual
ms.assetid: 822e3cf8-f723-4ff1-8467-e0fb42358a1f
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: aaa26585ff4cca909a7fb7c955b351b8860436b4
ms.sourcegitcommit: 8e123bcb21279f2770b28696995450270b4ec0e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/25/2019
ms.locfileid: "75406635"
---
# <a name="synchronously-autoloaded-extensions"></a>以同步方式加载了扩展

同步加载扩展对 Visual Studio 的性能产生负面影响，因此应将其转换为改用异步 autoload。 默认情况下，Visual Studio 2019 会阻止从任何扩展同步加载包，并通知用户。

![扩展兼容性警告](media/extension-compatibility-warning-16-1.png.png)

你可以：

- 单击 "**允许同步 autoload**以允许扩展到 autoload"。 若要在 Visual Studio 的 "选项" 中更改此设置，请单击 "环境"，然后单击 "扩展"，然后选中 "允许同步扩展 autoload" 复选框。 

- 单击 "**管理性能**"，打开 "[性能管理器" 对话框](#performance-manager-dialog)，其中显示了扩展和工具窗口的性能问题。

- 单击 "**不要为当前扩展显示此消息**" 可消除通知，并阻止现有已安装扩展中的未来通知。 如果添加 autoloads 同步的新扩展，则将再次显示此通知。 你将继续获得有关其他 Visual Studio 功能的通知。

## <a name="performance-manager-dialog"></a>性能管理器对话框

![性能管理器对话框](media/performance-manager.png)

所有用户会话中同步加载的所有扩展都显示在 "已**弃用的 api** " 选项卡中。

* 单击**有关此问题的详细信息**，以收集有关弃用的 api 的详细信息。
* 请联系其扩展供应商以获取迁移进度。

## <a name="specify-synchronous-autoload-settings-using-group-policy"></a>使用组策略指定同步 autoload 设置

管理员可以允许组策略允许同步 autoload。 为此，请在以下键上设置基于注册表的策略：

**HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\VisualStudio\SynchronousAutoload**

Entry =**允许**

Value = (DWORD)
* **0**为同步 autoload 不允许
* **1**是否允许同步 autoload

## <a name="extension-authors"></a>扩展作者
扩展作者可以在[迁移到 AsyncPackage](https://github.com/Microsoft/VSSDK-Extensibility-Samples/tree/master/AsyncPackageMigration)中找到迁移到异步 autoload 的包的说明。

## <a name="see-also"></a>另请参阅
有关 Visual Studio 2019 中同步 autoload 设置的详细信息，请参阅[同步 Autoload 行为](https://aka.ms/AA52xzw)页。
