---
title: 图形帧验证 |Microsoft Docs
ms.date: 03/02/2017
ms.topic: conceptual
f1_keywords:
- vs.graphics.FrameValidation
ms.assetid: 1e639182-1301-4e28-9c1e-b5df732f3f1b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ce283e5cbab30b612a02ec447113ad11e206a7f3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62895865"
---
# <a name="graphics-frame-validation"></a>图形帧验证
<!-- VERSIONLESS -->
Visual Studio 2017 和更好的支持**帧验证**工具。  帧验证窗口中显示错误和警告事件列表与相关联。  若要查看此窗口，请选择**视图 > 帧验证**菜单。

![帧验证](media/gfx_diag_frame_validation.png)

单击**运行验证**按钮，位于左上角启动分析。  可能需要几分钟才能完成，具体取决于帧的复杂性。  将显示下面是组合来自两个源的数据： 消息的 D3D 本身发出时[SDK 层](/windows/desktop/direct3d11/overviews-direct3d-11-devices-layers)已启用，并从工具的内部状态跟踪收集的数据。 完成后，你将看到多个列的数据：

| **列** | **说明** |
|------------| - |
| 事件 ID | ID 映射到中的条目[事件列表](graphics-event-list.md)窗口。 |
| 严重性 | 损坏、 错误、 警告、 信息或消息。 |
| 类别 | 已定义的其他应用程序、 初始化、 清理、 编译、 状态创建、 状态设置、 状态获取、 执行、 资源操作、 着色器，冗余的并且未使用。 |
| 消息 | 与事件关联的消息。 |
| Event | 与错误或警告关联的事件。 |

## <a name="see-also"></a>请参阅
[图形诊断（调试 DirectX 图形）](visual-studio-graphics-diagnostics.md)
<!-- /VERSIONLESS -->