---
title: 如何：禁用托管进程 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- hosting process, disabling
- vshost.exe, disabling the hosting process
ms.assetid: 9157488d-737f-454b-8d8d-36f99de38bb0
caps.latest.revision: 12
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 95dcd7da113bfe996d00e617b7c8e2f9b68864d7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72667978"
---
# <a name="how-to-disable-the-hosting-process"></a>How to: Disable the Hosting Process
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

启用承载进程时可能会影响对某些 API 的调用。 在这些情况下，必须禁用托管进程以返回正确的结果。

### <a name="to-disable-the-hosting-process"></a>禁用托管进程

1. 在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 中打开可执行项目。 不会生成可执行文件的项目（例如，类库或服务项目）没有此选项。

2. 在 **“项目”** 菜单上，单击 **“属性”** 。

3. 单击“调试”选项卡****。

4. 清除“启用 Visual Studio 托管进程”复选框****。

   禁用托管进程时，几种调试功能会不可用或性能下降。 有关详细信息，请参阅 [调试和承载进程](../debugger/debugging-and-the-hosting-process.md)。

   一般情况下，禁用托管进程时：

- 开始调试 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 应用程序需要的时间会增长。

- 设计时表达式计算不可用。

- 部分信任调试不可用。

## <a name="see-also"></a>另请参阅
 [在应用程序开发期间](https://msdn.microsoft.com/c9497d62-3b7b-4449-88e8-cf27acc9efe6) [，调试和托管](../debugger/debugging-and-the-hosting-process.md)进程[宿主进程 ( # A0) ](../ide/hosting-process-vshost-exe.md)生成
