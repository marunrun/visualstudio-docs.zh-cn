---
title: 图形帧验证 | Microsoft Docs
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
ms.openlocfilehash: 49248c6209f9e56e51551f6cd3d4af66ecac8b56
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72735499"
---
# <a name="graphics-frame-validation"></a>图形帧验证
<!-- VERSIONLESS -->
Visual Studio 2017 和更高版本支持“帧验证”工具。  “帧验证”窗口显示与事件列表关联的错误和警告。  若要查看此窗口，请选择“视图”>“帧验证”菜单。

![帧验证](media/gfx_diag_frame_validation.png)

单击左上角的“运行验证”按钮以启动分析。  这可能耗费数分钟时间，具体取决于帧的复杂性。  此处显示的数据是来自两个源的组合：启用 [SDK 层](/windows/desktop/direct3d11/overviews-direct3d-11-devices-layers)时 D3D 自身发出的消息，以及从该工具自己的内部状态跟踪收集的数据。 完成后，你将看到几列数据：

| **列** | **说明** |
|------------| - |
| 事件 ID | 映射到[事件列表](graphics-event-list.md)窗口中的条目的 ID。 |
| Severity | 损坏、错误、警告、信息或消息。 |
| 类别 | 由应用程序定义、其他、初始化、清理、编译、状态创建、状态设置、状态获取、执行、资源操作、着色器、冗余和未使用。 |
| 消息 | 与事件关联的消息。 |
| 事件 | 与错误或警告关联的事件。 |

## <a name="see-also"></a>请参阅
[图形诊断（调试 DirectX 图形）](visual-studio-graphics-diagnostics.md)
<!-- /VERSIONLESS -->