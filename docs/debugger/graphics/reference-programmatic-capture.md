---
title: 引用（编程捕获）| Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: ef60eb8d-1ac2-4e3a-9b4b-f6da0bdd9da8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a462d22df9768d2ffc8b344933e9f5c1f556575a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62895516"
---
# <a name="reference-programmatic-capture"></a>引用（编程捕获）
图形诊断支持通过编程捕获 API 对其捕获功能进行编程控制。 此 API 可用于切换消息和将消息添加到图形诊断 HUD（提醒显示）、初始化和创建图形日志文件以及捕获图形信息。

## <a name="programmatic-capture-apis"></a>编程捕获 API

### <a name="classes"></a>类

|“属性”|描述|
|----------|-----------------|
|[VsgDbg 类](vsgdbg-class.md)|表示接口，通过该接口以编程方式控制图形诊断的应用内组件。|

### <a name="preprocessor-symbols"></a>预处理器符号

|“属性”|描述|
|----------|-----------------|
|[DONT_SAVE_VSGLOG_TO_TEMP](dont-save-vsglog-to-temp.md)|通过其存在定义图形日志文件是否保存到用户的临时文件目录。|
|[VSG_DEFAULT_RUN_FILENAME](vsg-default-run-filename.md)|定义图形日志文件的默认文件名。|
|[VSG_NODEFAULT_INSTANCE](vsg-nodefault-instance.md)|通过其存在定义是否提供了 `VsgDbg` 类的默认实例。|

## <a name="related-articles"></a>相关文章

| Title | 描述 |
| - | - |
| [Capturing Graphics Information](capturing-graphics-information.md) | 演示如何从基于 DirectX 的应用捕获图形信息，以便使用 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 图形诊断工具来诊断呈现问题。 |
| [概述](overview-of-visual-studio-graphics-diagnostics.md) | 演示图形诊断可如何帮助你调试 DirectX 游戏和应用中的呈现错误。 |
