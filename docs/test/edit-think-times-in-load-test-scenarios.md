---
title: 负载测试的思考时间
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, think times
- load tests, adding delays
- load tests, changing think times
ms.assetid: 8e03bee5-ab7b-4b40-9497-9dbe91ccb90e
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 887d2af9e60be914bd74141041ecc375cfea4f00
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75590028"
---
# <a name="edit-think-times-to-simulate-website-human-interaction-delays-in-load-tests-scenarios"></a>编辑思考时间以模拟负载测试方案中的网站人工交互延迟

思考时间用于模拟人类与网站执行的各种交互之间存在等待时间这种行为。 Web 性能测试中的各个请求之间以及负载测试方案的各个测试迭代之间均会产生思考时间。 在负载测试中使用思考时间对于创建更为精确的负载模拟很有用。 您可以更改是在负载测试中使用思考时间还是忽略它。 可以在“负载测试编辑器”  中更改是否在负载测试中使用思考时间。

“思考时间配置文件”是应用于负载测试中的某个方案的一种设置  。 此设置决定是否在负载测试过程中使用在各个 Web 性能测试中保存的思考时间。 如果想在某些 Web 性能测试中使用思考时间，而在其他 Web 性能测试中不使用此时间，必须将这些测试放在不同的方案中。 有关方案的详细信息，请参阅[编辑负载测试方案](../test/edit-load-test-scenarios.md)。

最初，在使用“新建负载测试向导”  创建负载测试时，可设置是否在负载测试中使用思考时间。 有关详细信息，请参阅[编辑负载测试方案](../test/edit-load-test-scenarios.md)。

下面的列表介绍了“思考时间配置文件”  选项：

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

**Off**

忽略思考时间。 如果希望生成最大负载以便对 Web 服务器进行高强度的压力测试，可使用此设置。 如果尝试更加真实地模拟用户与 Web 服务器的交互情况，请不要使用此设置。

**On**

思考时间的用法与在 Web 性能测试中记录此类时间的方法完全相同。 完全根据记录模拟多个运行 Web 性能测试的用户。 由于负载测试模拟多个用户，使用相同的思考时间会建立一种不自然的负载模式，似乎各个用户正在同步执行操作。

**正态分布**

使用了思考时间，但这些时间沿正态分布曲线变化。 通过对不同请求间的思考时间略加修改，可更真实地模拟虚拟用户的操作。

> [!NOTE]
> 有关负载测试方案属性及其说明的完整列表，请参阅[负载测试方案属性](../test/load-test-scenario-properties.md)。

## <a name="change-the-think-profile"></a>更改思考时间配置文件

### <a name="to-change-a-think-profile-in-a-load-test-scenario"></a>在一个负载测试方案中更改思考时间配置文件

1. 从 Web 性能和负载测试项目中，打开负载测试。

2. 在“负载测试编辑器”中，选择要在其中更改“思考时间配置文件”的方案节点   。 “属性”  窗口中将显示“思考时间配置文件”  。 按 F4  以显示“属性”  窗口。

3. 在“属性”  窗口中更改“思考时间配置文件”  属性。

4. 更改完属性后，请选择“文件”菜单上的“保存”   。 然后，就可以用新的思考时间配置文件运行负载测试了。

## <a name="see-also"></a>请参阅

- [编辑负载测试方案](../test/edit-load-test-scenarios.md)
