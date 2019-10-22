---
title: 如何：连接到服务中的数据 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- data [Visual Studio], connecting to Web services
- data sources, creating from Web services
- data [Visual Studio], reading from Web services
- reading data, from Web services
- Web services, reading data
- Web services, as data sources
- Web services, connecting
ms.assetid: a6b54353-05fe-4e5c-8631-90231fc95504
caps.latest.revision: 35
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d9bfa6c776e3a2137f751d4253feb0239811d95a
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72654692"
---
# <a name="how-to-connect-to-data-in-a-service"></a>如何：连接到服务中的数据
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通过运行 "[数据源配置向导](https://msdn.microsoft.com/library/c4df7de5-5da0-4064-940c-761dd6d9e28f)" 并在 "**选择数据源类型**" 页上选择 "**服务**"，将应用程序连接到从服务返回的数据。

 完成向导后，服务引用将添加到项目中，并在 "[数据源" 窗口](https://msdn.microsoft.com/library/0d20f699-cc95-45b3-8ecb-c7edf1f67992)中立即可用。

> [!NOTE]
> “数据源”窗口中显示的项取决于该服务返回的信息。 某些服务可能没有为“数据源配置”向导创建可绑定的对象提供足够的信息。 例如，如果服务返回非类型化数据集，则在完成该向导时，"**数据源" 窗口**中将不会显示任何项。 这是因为非类型化数据集不提供架构，因此向导没有足够的信息来创建数据源。

 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]

### <a name="to-connect-your-application-to-a-service"></a>将应用程序连接到服务

1. 在 **“数据”** 菜单上，单击 **“添加新数据源”** 。

2. 选择 "**选择数据源类型**" 页上的 "**服务**"，然后单击 "**下一步**"。

3. 输入要使用的服务的地址，或单击 "**发现**" 以定位当前解决方案中的服务，然后单击 "**开始**"。

4. （可选）可以键入新的**命名空间**来代替默认值。

    > [!NOTE]
    > 单击 "**高级**" 打开 "[配置服务引用" 对话框](../data-tools/configure-service-reference-dialog-box.md)。

5. 单击 **"确定"** 将服务引用添加到项目。

6. 单击 **“完成”** 。

     数据源随即添加到“数据源”窗口中。

## <a name="next-steps"></a>后续步骤

#### <a name="to-add-functionality-to-your-application"></a>将功能添加到你的应用程序

- 在 "**数据源**" 窗口中选择一个项，然后将其拖到窗体上以创建绑定控件。 有关详细信息，请参阅[在 Visual Studio 中将控件绑定到数据](../data-tools/bind-controls-to-data-in-visual-studio.md)。

## <a name="see-also"></a>请参阅
 在 Visual Studio 中[将 WPF 控件绑定到 WCF 数据服务](../data-tools/bind-wpf-controls-to-a-wcf-data-service.md) [Windows Communication Foundation 服务和 WCF 数据服务](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)
