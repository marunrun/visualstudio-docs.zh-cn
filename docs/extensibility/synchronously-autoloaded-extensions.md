---
title: 以同步方式加载了扩展
ms.date: 12/11/2019
ms.topic: conceptual
ms.assetid: 822e3cf8-f723-4ff1-8467-e0fb42358a1f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ab62d235fd6ed4e47e765fc23868acd5c56efcb2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80699374"
---
# <a name="synchronously-autoloaded-extensions"></a>以同步方式加载了扩展

同步自动加载扩展对 Visual Studio 的性能产生负面影响，应转换为使用异步自动加载。 默认情况下，Visual Studio 2019 阻止任何扩展同步自动加载包并通知用户。

![扩展兼容性警告](media/extension-compatibility-warning-16-1.png.png)

可以：

- 单击"**允许同步自动加载**以允许自动加载扩展"。 要在 Visual Studio 选项中更改此设置，请单击"环境"，然后单击"扩展"，然后选择复选框"允许扩展的同步自动加载"。 

- 单击"**管理性能**"以打开显示扩展和工具窗口的性能问题[的性能管理器对话框](#performance-manager-dialog)。

- 单击"**不要显示当前扩展此消息**"以关闭通知并防止将来通知来自现有已安装的扩展。 如果添加同步自动加载的新扩展，将再次显示此通知。 您将继续收到有关其他视觉工作室功能的通知。

## <a name="performance-manager-dialog"></a>性能管理器对话框

![性能管理器对话框](media/performance-manager.png)

在任何用户会话中同步加载任何包的所有扩展都将显示在 **"已弃用 API"** 选项卡中。

* 单击"**有关此问题的详细信息**"以收集有关已弃用 API 的详细信息。
* 有关迁移进度，请与其扩展供应商联系。

## <a name="specify-synchronous-autoload-settings-using-group-policy"></a>使用组策略指定同步自动加载设置

管理员可以启用组策略以允许同步自动加载。 为此，请在以下键上设置基于注册表的策略：

**HKEY_LOCAL_MACHINE_软件_策略\微软_VisualStudio_同步自动加载**

条目 =**允许**

值 = (DWORD)
* **0**是不允许同步自动加载
* **1**是允许同步自动加载

## <a name="extension-authors"></a>扩展作者
扩展作者可以在[迁移到异步包](https://github.com/Microsoft/VSSDK-Extensibility-Samples/tree/master/AsyncPackageMigration)时找到有关将包迁移到异步自动加载的说明。

## <a name="see-also"></a>请参阅
有关 Visual Studio 2019 中的同步自动加载设置的详细信息，请参阅[同步自动加载行为](https://devblogs.microsoft.com/visualstudio/updates-to-synchronous-autoload-of-extensions-in-visual-studio-2019/)页面。
