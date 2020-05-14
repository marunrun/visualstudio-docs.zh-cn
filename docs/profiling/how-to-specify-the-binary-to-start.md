---
title: 如何：指定要启动的二进制文件 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.property.itemlaunch
helpviewer_keywords:
- profiling tools, launching
- performance tools, launching
- performance sessions, launching
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: fd3379b9769cfd6bfe1335b12545e635a9bde782
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "74778682"
---
# <a name="how-to-specify-the-binary-to-start"></a>如何：指定要启动的二进制文件

若要分析二进制文件（如 DLL），必须在“**目标> 属性页”对话框中输入信息\<** 。 这些信息指示 DLL 项目查找调用应用程序的位置。

1. 在“性能资源管理器”  中，右键单击目标二进制文件，然后单击“属性”  。

2. 在“属性页”对话框中单击“启动”属性   。

3. 选中“重写项目属性”复选框  。

4. 在“要启动的可执行文件”文本框中，指定文件的位置  。

5. 在“参数”文本框中，指定启动应用程序所需的参数  。

6. 在“工作目录”文本框中  ，指定目录的位置。

7. 单击 **“确定”** 。

## <a name="see-also"></a>另请参阅

[配置性能会话](../profiling/configuring-performance-sessions.md)
