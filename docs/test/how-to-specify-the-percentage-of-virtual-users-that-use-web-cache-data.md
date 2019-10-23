---
title: 负载测试：使用 web 缓存数据设置虚拟用户百分比
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, virtual users
ms.assetid: f66d5d43-4121-4487-b27f-d0a0baaf7601
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: bc8baf2586e0c0ce682436387bfd612af14e18bd
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72653383"
---
# <a name="how-to-specify-the-percentage-of-virtual-users-that-use-web-cache-data"></a>如何：指定使用 Web 高速缓存数据的虚拟用户的百分比

使用“新建负载测试向导”创建负载测试后，可使用“负载测试编辑器”来更改方案属性以满足测试需求和目标   。 有关负载测试方案属性及其说明的完整列表，请参阅[负载测试方案属性](../test/load-test-scenario-properties.md)。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

在“属性”窗口中设置“新用户的百分比”属性   。 在负载测试编辑器中编辑负载测试方案属性  。

“新用户的百分比”  属性会影响负载测试对 Web 浏览器所执行缓存的模拟方式。 默认情况下，“新用户的百分比”属性设置为 0%  。 如果“新用户的百分比”  属性的值设置为 100%，则负载测试中的每次 Web 性能测试运行都被视为用户第一次访问网站，这些用户在之前访问的浏览器缓存中没有来自网站的任何内容。 因此，将下载 Web 测试中的所有请求，包括所有从属请求（如图像）。

> [!NOTE]
> 当 Web 测试中多次请求同一个可缓存资源时，将不下载请求。

如果对具有大量可能拥有本地缓存的图像和其他可缓存内容的返回用户的网站进行负载测试，那么将“新用户的百分比”  属性设置为 100% 所生成的下载请求数将大于实际应用中所生成的请求数。 在此情况下，应当估计第一次访问网站的用户的访问百分比，然后据此设置“新用户的百分比”  属性。

## <a name="to-specify-the-percentage-of-new-users-for-a-scenario"></a>指定某一方案新用户的百分比

1. 打开一个负载测试。

     “负载测试编辑器”随即显示  。 其中显示负载测试树。

2. 在负载测试树的“方案”  文件夹中，选择要为其更改新用户百分比值的方案节点。

3. 在“视图”菜单上选择“属性窗口”   。

     该方案的类别和属性将显示在“属性”  窗口中。

4. 通过输入新用户的百分比的数值，设置“新用户的百分比”属性的值  。

5. 更改完此属性后，请选择“文件”菜单上的“保存”   。 然后，可使用新的“新用户的百分比”  值运行负载测试。

## <a name="see-also"></a>请参阅

- [编辑负载测试方案](../test/edit-load-test-scenarios.md)
- [演练：创建和运行负载测试](../test/walkthrough-create-and-run-a-load-test.md)
- [测试控制器和测试代理](configure-test-agents-and-controllers-for-load-tests.md)
- [负载测试方案属性](../test/load-test-scenario-properties.md)
- [编辑负载模式以便为虚拟用户活动建模](../test/edit-load-patterns-to-model-virtual-user-activities.md)