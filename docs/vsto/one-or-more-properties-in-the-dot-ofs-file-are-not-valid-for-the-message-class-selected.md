---
title: .ofs 文件中的一个或多个属性对于选定的消息类无效
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VSTO.NewFormRegionWizard.OFSPropertyError
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: d58ad6ff89d8cf41ec60135cfbfe3deac1382f1e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62977856"
---
# <a name="one-or-more-properties-in-the-ofs-file-are-not-valid-for-the-message-class-selected"></a>.ofs 文件中的一个或多个属性对于选定的消息类无效
  导入在 Outlook 中设计的窗体区域时，会出现此错误，但窗体区域上的一个或多个字段不兼容的最后一页上选择的邮件类**新建窗体区域**向导。

例如，你可能在“新建窗体区域”  向导最后一页上选择了“任务(IPM.Task)”  。 如果窗体区域**企业地址**字段中，你将收到此错误，因为任务没有办公地址。 因此，**企业地址**字段不是与兼容`IPM.Task`message 类。

 您可以选择**任务 (IPM。任务）** 的最后一页上**新建窗体区域**向导。 如果窗体区域**企业地址**字段中，你将收到此错误，因为任务没有办公地址。 因此，**企业地址**字段不是与兼容`IPM.Task`message 类。

## <a name="to-correct-this-error"></a>更正此错误

- 在“新建窗体区域”  向导最后一页上，选择与窗体区域上的字段兼容的邮件类。

- 在 Outlook 中窗体设计器中删除不兼容的邮件类的字段。 删除计划的最后一页选择的字段**新建窗体区域**向导。

## <a name="see-also"></a>请参阅
- [演练：导入在 Outlook 中设计的窗体区域](../vsto/walkthrough-importing-a-form-region-that-is-designed-in-outlook.md)
