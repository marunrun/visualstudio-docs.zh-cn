---
title: 如何：在报表视图中配置降噪 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performance.noisereduction.dialog
helpviewer_keywords:
- profiling tools, trimming
- profiling tools, report noise reduction
- profiling tools, folding
ms.assetid: b07e0375-bb73-47e3-8d1d-b9b492fb16c9
caps.latest.revision: 18
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5871473eaba749833714d6382beb487702ebe02d
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63432772"
---
# <a name="how-to-configure-noise-reduction-in-report-views"></a>如何：在报告视图中配置降噪
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通过限制“调用关系树”视图和“分配”视图中显示的数据量，可针对降噪配置性能报表。 通过使用降噪，性能问题能够更加醒目。 分析性能报告时，这非常有用。  
  
 降噪配置选项包括以下设置：  
  
- **修整** 如后面的修整过程中所述，对报告进行了分析后，视图将忽略值降低的函数和已配置的阈值设置。 默认情况下，会启用修整。  
  
- **折叠** 如后面的折叠过程中所述，启用折叠时，将合并满足已配置设置的路径上的连续函数。 折叠在默认情况下处于启用状态。  
  
### <a name="to-configure-trimming-for-a-performance-report"></a>配置性能报告的修整  
  
1. 当生成的报表中显示“调用关系树”视图或“分配”视图时，在“开发者”菜单上，单击“探查器”，然后单击“降噪选项”。  
  
     将出现“降噪”对话框。  
  
2. 若要启用修整，请按照以下步骤操作：  
  
    1. 选择“启用修整”。 此为默认设置。  
  
        > [!NOTE]
        > 如果启用了降噪，报表中将显示信息栏。 有关详细信息，请参阅[“调用关系树”视图](../profiling/call-tree-view.md)和[“分配”视图](../profiling/dotnet-memory-allocations-view.md)。  
  
    2. 使用“值”下拉列表并选择适用的设置，以配置值设置。  
  
    3. 通过在“阈值”文本框中键入百分比值配置所需的阈值设置。  
  
    4. 若要在生成的报告中启用降噪警告，请选择“启用降噪时显示警告”。 此为默认设置。  
  
3. 若要禁用修整，请清除“启用修整”。  
  
4. 单击 **“确定”**。  
  
### <a name="to-configure-folding-for-a-performance-report"></a>配置性能报告的折叠  
  
1. 在“开发者”菜单上，单击“探查器”，然后单击“降噪选项”。  
  
     将出现“降噪”对话框。  
  
2. 若要启用折叠，请按照以下步骤操作：  
  
    1. 选择“启用折叠”。 此为默认设置。  
  
        > [!NOTE]
        > 如果启用了降噪，报表中将显示信息栏。 有关详细信息，请参阅[“调用关系树”视图](../profiling/call-tree-view.md)和[“分配”视图](../profiling/dotnet-memory-allocations-view.md)。  
  
    2. 使用“值”下拉列表并选择适用的设置，以配置值设置。  
  
    3. 通过在“阈值”文本框中键入百分比值配置所需的阈值设置。  
  
    4. 若要在生成的报告中启用降噪警告，请选择“启用降噪时显示警告”。 此为默认设置。  
  
3. 若要禁用折叠，请清除“启用折叠”。  
  
4. 单击 **“确定”**。  
  
## <a name="see-also"></a>请参阅  
 [自定义性能工具报表视图](../profiling/customizing-performance-tools-report-views.md)   
 [如何：排除或包括短函数从检测](../profiling/how-to-exclude-or-include-short-functions-from-instrumentation.md)   
 [“调用关系树”视图](../profiling/call-tree-view.md)   
 [“分配”视图](../profiling/dotnet-memory-allocations-view.md)
