---
title: 禁用 Debugger for Windows Workflow Foundation （旧版） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
helpviewer_keywords:
- workflows, disabling debugger
- debugging workflows, disabling debugger
- workflow debugger, disabling
ms.assetid: 9da96d0e-f941-4fa9-a1a5-6bab50adfec9
caps.latest.revision: 6
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: e5065de4ec0217123f76eb23d32bcb0facd25dcc
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62823328"
---
# <a name="disabling-the-visual-studio-debugger-for-windows-workflow-foundation-legacy"></a>禁用 Visual Studio Debugger for Windows Workflow Foundation（旧版）
本主题介绍如何在旧 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 中生成 [!INCLUDE[wf](../includes/wf-md.md)] 应用程序时，使用配置文件禁用 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 调试器。 在需要面向 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 或 [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] 时，请使用旧 [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)]。

 默认情况下，为宿主进程启用了 [!INCLUDE[vs_current_long](../includes/vs-current-long-md.md)] Debugger for [!INCLUDE[wf](../includes/wf-md.md)]。 若要禁用工作流调试，您必须显式将其关闭通过添加"DisableWorkflowDebugging"项 **\<交换机 >** 中的元素 **\<system.diagnostics >** 部分中的主机配置文件。

 以下示例显示如何修改主机配置文件以禁用工作流调试。

```
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
   <system.diagnostics>
      <switches>
         <add name="DisableWorkflowDebugging" value="true"/>
      </switches>
   </system.diagnostics>
</configuration>
```

## <a name="see-also"></a>请参阅
 [调用 Visual Studio Debugger for Windows Workflow Foundation （旧版）](../workflow-designer/invoking-the-visual-studio-debugger-for-windows-workflow-foundation-legacy.md) [调试旧版工作流](../workflow-designer/debugging-legacy-workflows.md)