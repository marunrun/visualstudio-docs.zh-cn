---
title: 为 Windows Workflow Foundation 禁用调试器（旧版） |Microsoft Docs
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
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: eddd72d648e7349f51096a21131f38c2e370a277
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72656789"
---
# <a name="disabling-the-visual-studio-debugger-for-windows-workflow-foundation-legacy"></a>禁用 Visual Studio Debugger for Windows Workflow Foundation（旧版）
本主题介绍如何在旧 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 中生成 [!INCLUDE[wf](../includes/wf-md.md)] 应用程序时，使用配置文件禁用 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 调试器。 在需要面向 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 或 [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] 时，请使用旧 [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)]。

 默认情况下，为宿主进程启用了 [!INCLUDE[vs_current_long](../includes/vs-current-long-md.md)] Debugger for [!INCLUDE[wf](../includes/wf-md.md)]。 若要禁用工作流调试，必须通过在主机配置文件的 **\<system "诊断 >** " 部分中添加 "DisableWorkflowDebugging" 条目 **\<switches >** 元素来显式关闭工作流调试。

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
 [为 Windows Workflow Foundation （旧）](../workflow-designer/invoking-the-visual-studio-debugger-for-windows-workflow-foundation-legacy.md) [调试旧版工作流](../workflow-designer/debugging-legacy-workflows.md)调用 Visual Studio 调试器