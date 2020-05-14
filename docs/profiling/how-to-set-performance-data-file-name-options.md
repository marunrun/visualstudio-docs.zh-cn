---
title: 如何：设置性能数据文件名选项 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: d7a8d6b9-ab23-46fb-98ed-774781157860
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: cc42b63524a867c0893aa255180c740d03d4b5fe
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "74778760"
---
# <a name="how-to-set-performance-data-file-name-options"></a>如何：设置性能数据文件名选项

默认情况下，使用以下语法保存分析数据 (.vsp) 文件  ：

*Path\VSP-File\YYMMDD(N)* **.vsp**

在性能会话属性对话框的“常规”页上，可以更改任意命名参数  。

|||
|-|-|
|*路径*|包含报告的目录。 默认位置为解决方案文件夹或用户项目和解决方案的默认位置。|
|*VSP-File*|分析数据文件的名称。 默认名称是所分析的解决方案或可执行文件的名称。|
|*YYMMDD*|显示收集分析数据的年、月、日的日期戳。|
|*(N)*|如果存在多个分析数据文件，文件名后会用括号加上递增的数字。|

## <a name="to-change-the-naming-syntax-of-the-profiling-data-files-of-a-performance-session"></a>更改性能会话分析数据文件的命名语法

1. 在“性能资源管理器”  中，右键单击性能会话的名称，然后单击“属性”  。

2. 单击“常规”  。

3. 在“报告”下更改下列任意设置： 

    |||
    |-|-|
    |**报告位置**|指定用于存储分析数据文件的目录。|
    |**报表名称**|指定文件的基名称。|
    |**自动向会话添加新报告**|选中该复选框会自动将数据文件添加到性能会话中。|
    |**将一个递增的数字附加到生成的报告**|选中该复选框后，如果存在多个同名文件，文件名后会加上递增的数字。 清除该复选框会覆盖现有文件。|
    |**在数字中使用时间戳**|选中该复选框会为文件名添加日期戳。|
