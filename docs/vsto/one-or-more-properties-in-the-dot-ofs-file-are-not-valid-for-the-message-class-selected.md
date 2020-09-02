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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62977856"
---
# <a name="one-or-more-properties-in-the-ofs-file-are-not-valid-for-the-message-class-selected"></a>.ofs 文件中的一个或多个属性对于选定的消息类无效
  当您导入在 Outlook 中设计的窗体区域时，将出现此错误，但是窗体区域中的一个或多个字段与在 " **新建窗体区域** " 向导的最后一页上选择的邮件类不兼容。

例如，你可能在“新建窗体区域” **** 向导最后一页上选择了“任务(IPM.Task)” **** 。 如果窗体区域包含 " **业务地址** " 字段，则会收到此错误，因为任务没有企业地址。 因此，" **业务地址** " 字段与 `IPM.Task` 邮件类不兼容。

 你可以选择 " **Task (IPM"。 ** " **新建窗体区域** " 向导最后一页上的任务) 。 如果窗体区域包含 " **业务地址** " 字段，则会收到此错误，因为任务没有企业地址。 因此，" **业务地址** " 字段与 `IPM.Task` 邮件类不兼容。

## <a name="to-correct-this-error"></a>更正此错误

- 在“新建窗体区域” **** 向导最后一页上，选择与窗体区域上的字段兼容的邮件类。

- 在 Outlook 的窗体设计器中，删除与消息类不兼容的字段。 删除你计划在 " **新建窗体区域** " 向导的最后一页上选择的字段。

## <a name="see-also"></a>另请参阅
- [演练：导入在 Outlook 中设计的窗体区域](../vsto/walkthrough-importing-a-form-region-that-is-designed-in-outlook.md)
