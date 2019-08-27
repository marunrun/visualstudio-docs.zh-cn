---
title: 以同步方式加载了扩展
ms.date: 02/16/2019
ms.topic: conceptual
ms.assetid: 822e3cf8-f723-4ff1-8467-e0fb42358a1f
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8b18642269326c516c2af0baef57cb306f60ae6a
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66316718"
---
# <a name="synchronously-autoloaded-extensions"></a>以同步方式加载了扩展

以同步方式加载扩展对 Visual Studio 的性能产生负面影响，应将转换为改为使用异步自动加载。 从 Visual Studio 2019 预览版 2 开始，当扩展以同步方式在加载时通知用户。 该扩展将加载并照常工作。

![扩展兼容性警告](media/extension-compatibility-warning.png)

用户可以：

- 单击**了解详细信息**，转到此信息页面。

- 单击**管理性能**以打开[性能管理器对话框](#performance-manager-dialog)显示扩展和工具窗口的性能问题。

- 单击**不再显示此消息**以取消通知。 选择此选项还会阻止从以同步方式加载扩展所有将来的通知。 用户将继续获取有关其他 Visual Studio 功能的通知。

## <a name="performance-manager-dialog"></a>性能管理器对话框

![性能管理器对话框](media/performance-manager.png)

以同步方式在任何用户会话中加载任何包的所有扩展会都出现**已弃用 Api**选项卡。

* 用户可以单击**有关此问题的详细信息**以收集有关不推荐使用的 Api 的详细信息。
* 用户可以联系其扩展供应商获取迁移进度。

扩展创建者可以找到有关迁移说明包部署到在异步 autoload[迁移到 AsyncPackage](https://github.com/Microsoft/VSSDK-Extensibility-Samples/tree/master/AsyncPackageMigration)。

## <a name="specify-synchronous-autoload-settings-using-group-policy"></a>指定同步自动加载设置，请使用组策略

启动 Visual Studio 2019 Update 1 中，默认情况下，Visual Studio 安装块同步自动加载。 启用组策略时，可以配置为允许同步自动加载单个计算机上的 Visual Studio。 为此，请在以下键上设置基于注册表的策略：

**HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\VisualStudio\SynchronousAutoload**

条目 =**允许**

Value = (DWORD)
* **0**同步自动加载不允许
* **1**允许同步自动加载

有关 Visual Studio 2019 Update 1 中的同步自动加载设置的详细信息，请参阅[同步自动加载行为](https://aka.ms/AA52xzw)页。
