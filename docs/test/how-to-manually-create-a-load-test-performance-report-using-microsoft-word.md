---
title: 使用 Microsoft Word 创建负载测试性能报告
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, reporting
- load tests, creating Word reports
ms.assetid: 3b864c75-2699-48c1-a2b4-9651f108c267
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: a82479fabda0cd64e977af01f87492563a02853f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62950067"
---
# <a name="how-to-manually-create-a-load-test-performance-report-using-microsoft-word"></a>如何：使用 Microsoft Word 手动创建负载测试性能报告

可以通过从负载测试结果摘要视图和关系图视图复制和粘贴数据，手动创建 Microsoft Word 负载测试报告。 摘要视图和关系图视图中显示的数据在复制后将以 HTML 格式应用。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

> [!TIP]
> 可以将表视图中的纯文本和详细信息视图中的屏幕快照复制到 Microsoft Word，但复制的内容不会以 HTML 格式应用，需要另外进行格式设置和编辑。

> [!TIP]
> 也可以自动生成有组织的 Microsoft Excel 报表。 有关详细信息，请参阅[如何：使用 Microsoft Excel 创建负载测试性能报告](../test/how-to-create-load-test-performance-reports-using-microsoft-excel.md)。

## <a name="copy-summary-view-data"></a>复制摘要视图数据

1. 在“负载测试结果”中，如果当前未显示摘要视图，请单击工具栏上的“摘要”。

2. 在摘要视图中，右键单击并选择“全选”。

3. 在摘要视图中，右键单击并选择“复制”。 此操作会将摘要视图数据以 HTML 格式呈现到剪贴板。

4. 在 Microsoft Word 中，将摘要视图数据粘贴到所需位置。

5. 此时，您可以对所复制的内容进行修改、格式设置和删除以满足报告需求。

## <a name="copy-graph-view-data"></a>复制关系图视图数据

1. 在“负载测试结果”中，如果当前未显示关系图视图，请选择工具栏上的“关系图”。

2. （可选）对要复制到 Microsoft Word 文档中的特定关系图进行放大，如下图所示。 有关详细信息，请参阅[如何：放大关系图的区域](../test/how-to-zoom-in-on-a-region-of-the-graph-in-load-test-results.md)。

     ![图形视图缩放控件](../test/media/ltest_zoomcontrol.png)

3. 在要复制到 Microsoft Word 文档中的关系图上，右键单击并选择“复制”。

4. 在 Microsoft Word 中的所需位置粘贴关系图以及关联的表数据。

    > [!WARNING]
    > 不能从远程桌面复制关系图并将其粘贴到另一台计算机，因为这样仅复制与关系图关联的表信息而不是复制关系图图像。 关系图图像存储在从中复制它的计算机的临时目录中，另一台计算机不能取消对该目录的引用。

## <a name="see-also"></a>请参阅

- [报告负载测试结果以进行测试比较或趋势分析](../test/compare-load-test-results.md)
- [如何：使用 Microsoft Excel 创建负载测试性能报告](../test/how-to-create-load-test-performance-reports-using-microsoft-excel.md)