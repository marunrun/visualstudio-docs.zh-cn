---
title: 创建诊断数据适配器进行测试
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- Diagnostic Data Adapter [Visual Studio ALM]
- Diagnostic Data Adapter
ms.assetid: b0b53fae-7007-4ad9-a604-21685937622f
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 800e866e2bfa915590060b09a98539533460bed3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62965647"
---
# <a name="create-a-diagnostic-data-adapter-to-collect-custom-data-or-affect-a-test-machine"></a>创建诊断数据适配器以收集自定义数据或影响测试计算机

您可能希望创建自己的诊断数据适配器以便在运行测试时收集数据，或者希望测试的一部分是对测试计算机产生影响。 例如，您可能希望收集由受测应用程序创建的日志文件并将这些文件附加到测试结果中，或者希望在计算机可用磁盘空间有限的情况下运行测试。 使用 Visual Studio Enterprise 中提供的 API 可以编写在测试运行的特定点执行任务的代码。 例如，您可以在开始测试运行之前、每个单独的测试运行之前和之后以及测试运行完成之后执行任务。

可以使用配置设置文件为自定义诊断数据适配器提供默认输入。 例如，可以提供要收集并附加到测试结果中的文件的位置相关信息，也可提供希望系统留出的磁盘空间数。 可为您创建的每个测试设置配置此数据。 可使用 Microsoft 测试管理器中提供的默认编辑器显示和编辑此数据，也可以创建自己的用户控件用作编辑器。 在编辑器中对适配器配置所做的任何更改都将随测试设置一起存储。

如果您是从 Visual Studio 运行测试，则必须将这些测试设置设置为处于活动状态。 有关测试设置的详细信息，请参阅[使用测试设置收集诊断信息](../test/collect-diagnostic-information-using-test-settings.md)。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="tasks"></a>任务

下面的主题用于帮助您创建诊断数据适配器：

|任务|相关主题|
|-|-----------------------|
|**创建诊断数据适配器：** 可通过创建类库来创建诊断数据适配器，然后使用诊断数据适配器 API 来收集所需的信息或对正在用于运行测试的测试系统产生影响。|-   [如何：创建诊断数据适配器](../test/how-to-create-a-diagnostic-data-adapter.md)|
|**选择运行测试时使用的自定义诊断数据适配器：** 可以选择用于测试设置的诊断数据适配器，以便运行测试时使用该适配器。|-   [在测试时收集诊断数据 (Azure Test Plans)](/azure/devops/test/collect-diagnostic-data?view=vsts)<br />-   [在手动测试中收集诊断数据 (Azure Test Plans)](/azure/devops/test/mtm/collect-more-diagnostic-data-in-manual-tests?view=vsts)|

## <a name="see-also"></a>请参阅

- [使用测试设置收集诊断信息](../test/collect-diagnostic-information-using-test-settings.md)