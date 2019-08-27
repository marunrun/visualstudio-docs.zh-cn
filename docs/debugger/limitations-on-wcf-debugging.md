---
title: WCF 调试的限制 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging, WCF
- WCF, debugging limitations
ms.assetid: 8e0333c4-1ddc-4abe-8f1c-d19bf6a2a07a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 34b69ac69c580fbd40278b5b7a0c9be26d672fa3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62905953"
---
# <a name="limitations-on-wcf-debugging"></a>WCF 调试的限制
有三种开始 WCF 服务调试的方式：

- 调试调用服务的客户端进程。 调试器单步执行该服务。 该服务不必与客户端应用程序处于同一个解决方案中。

- 调试请求服务的客户端进程。 该服务必须是解决方案的一部分。

- 使用“附加到进程”可附加到当前正在运行的服务。 调试将在该服务内部开始。

  本主题描述了有关这些方案的限制。

## <a name="limitations-on-stepping-into-a-service"></a>单步执行服务的限制
 若要从正在调试的客户端应用程序单步执行服务，必须满足下列条件：

- 客户端必须使用同步客户端对象调用服务。

- 协定操作不能是单向的。

- 如果服务器是异步的，则无法在服务内部执行代码时查看完整的调用堆栈。

- 必须使用 app.config 或 Web.config 文件中的以下代码启用调试：

    ```xml
    <system.web>
      <compilation debug="true" />
    </system.web>
    ```

     此代码只需添加一次。 可以通过编辑 .config 文件或使用“附加到进程”将代码附加到服务中来添加此代码。 在对服务使用“附加到进程”时，调试代码将自动添加到 .config 文件中。 随后，您可以调试并单步执行该服务，而无需编辑 .config 文件。

## <a name="limitations-on-stepping-out-of-a-service"></a>跳出服务的限制
 跳出服务并返回到客户端与单步执行服务具有相同的限制（如上所述）。 另外，调试器必须附加到客户端上。 若要调试客户端并单步执行服务，调试器将继续附加到服务中。 无论使用“启动调试”启动客户端，还是使用“附加到进程”将调试器附加到客户端，都是如此。 如果是通过附加到服务开始调试的，则说明尚未将调试器附加到客户端。 在这种情况下，如果需要跳出服务并返回到客户端，必须先使用“附加到进程”手动附加到客户端。

## <a name="limitations-on-automatic-attach-to-a-service"></a>自动附加到服务的限制
 自动附加到服务具有下列限制：

- 该服务必须是要调试的 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 解决方案的一部分。

- 该服务必须进行托管。 它可以是网站项目（文件系统和 HTTP）、Web 应用程序项目（文件系统和 HTTP）或 WCF 服务库项目的一部分。 WCF 服务库项目可以是服务库或工作流服务库。

- 必须从 WCF 客户端调用该服务。

- 必须使用 app.config 或 Web.config 文件中的以下代码启用调试：

  ```xml
  <system.web>
    <compilation debug="true" />
  <system.web>
  ```

## <a name="self-hosting"></a>自我托管
 “自承载服务”是指不在 IIS、WCF 服务主机或 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 开发服务器内部运行的 WCF 服务。 有关如何调试自承载的服务的信息，请参阅[如何：调试自我托管的 WCF 服务](../debugger/how-to-debug-a-self-hosted-wcf-service.md)。

## <a name="self-hosting"></a>自我托管
 若要启用 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 3.0 或 3.5 应用程序的调试，则必须在安装 [!INCLUDE[vs_dev10_long](../code-quality/includes/vs_dev10_long_md.md)] 之前安装 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 3.0 或 3.5。 如果在安装 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 3.0 或 3.5 之前安装了 [!INCLUDE[vs_dev10_long](../code-quality/includes/vs_dev10_long_md.md)]，则在尝试调试 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 3.0 或 3.5 应用程序时会出错。 错误消息为：无法自动单步执行服务器。 若要解决此问题，请使用 Windows **Control Panel** > **程序和功能**修复你[!INCLUDE[vs_dev10_long](../code-quality/includes/vs_dev10_long_md.md)]安装。

## <a name="see-also"></a>请参阅
- [调试 WCF 服务](../debugger/debugging-wcf-services.md)
- [如何：调试自托管 WCF 服务](../debugger/how-to-debug-a-self-hosted-wcf-service.md)
