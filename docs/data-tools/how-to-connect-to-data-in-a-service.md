---
title: 如何：连接到服务中的数据
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- data [Visual Studio], connecting to web services
- data sources, creating from web services
- data [Visual Studio], reading from web services
- reading data, from web services
- web services, reading data
- web services, as data sources
- web services, connecting
ms.assetid: a6b54353-05fe-4e5c-8631-90231fc95504
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 0b49840a2190abfd223edf5643b8d70da1a59d6b
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85282223"
---
# <a name="how-to-connect-to-data-in-a-service"></a>如何：连接到服务中的数据

通过运行 "[数据源配置向导](../data-tools/media/data-source-configuration-wizard.png)" 并在 "**选择数据源类型**" 页上选择 "**服务**"，将应用程序连接到从服务返回的数据。

完成向导后，服务引用将添加到项目中，并在 "[数据源" 窗口](add-new-data-sources.md#data-sources-window)中立即可用。

> [!NOTE]
> “数据源”窗口中显示的项取决于该服务返回的信息****。 某些服务可能没有为“数据源配置”向导创建可绑定的对象提供足够的信息****。 例如，如果服务返回非类型化数据集，则在完成该向导时，"**数据源**" 窗口中不会显示任何项。 这是因为非类型化数据集不提供架构，因此向导没有足够的信息来创建数据源。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="to-connect-your-application-to-a-service"></a>将应用程序连接到服务

1. 在 **“数据”** 菜单上，单击 **“添加新数据源”**。

2. 选择 "**选择数据源类型**" 页上的 "**服务**"，然后单击 "**下一步**"。

3. 输入要使用的服务的地址，或单击 "**发现**" 以定位当前解决方案中的服务，然后单击 "**开始**"。

4. 或者，您可以键入一个新的**命名空间**来代替默认值。

    > [!NOTE]
    > 单击 "**高级**" 打开 "[配置服务引用" 对话框](../data-tools/configure-service-reference-dialog-box.md)。

5. 单击 **"确定"** 将服务引用添加到项目。

6. 单击“完成”。

     数据源随即添加到“数据源”窗口中****。

## <a name="next-steps"></a>后续步骤

若要向应用程序添加功能，请在 "**数据源**" 窗口中选择一个项，然后将其拖到窗体上以创建绑定控件。 有关详细信息，请参阅[在 Visual Studio 中将控件绑定到数据](../data-tools/bind-controls-to-data-in-visual-studio.md)。

## <a name="see-also"></a>另请参阅

- [将 WPF 控件绑定到 WCF 数据服务](../data-tools/bind-wpf-controls-to-a-wcf-data-service.md)
- [Visual Studio 中的 Windows Communication Foundation 服务和 WCF 数据服务](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)
