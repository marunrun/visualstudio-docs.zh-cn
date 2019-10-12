---
title: 自动应用产品密钥
description: 了解如何在部署 Visual Studio 时以编程方式应用产品密钥。
ms.date: 09/24/2019
ms.custom: seodec18
ms.topic: conceptual
ms.assetid: d79260be-6234-4fd3-89b5-a9756b4a93c1
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 4c3e8313e1357095a9732c9304a695dd3b13b465
ms.sourcegitcommit: 0554b59a2a251661e56824fb9cd6e9b1f326cef1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/03/2019
ms.locfileid: "71831846"
---
# <a name="automatically-apply-product-keys-when-deploying-visual-studio"></a>在部署 Visual Studio 时自动应用产品密钥

可采用编程方式将产品密钥作为用于自动化 Visual Studio 部署的脚本的一部分进行应用。 安装 Visual Studio 期间或安装已完成后，可采用编程方式在设备上设置产品密钥。

## <a name="apply-the-license-after-installation"></a>安装完成后应用许可证

::: moniker range="vs-2017"

可在静默模式下在目标计算机上使用 `StorePID.exe` 实用工具，从而使用产品密钥激活 Visual Studio 的已安装版本。 `StorePID.exe` 是在以下默认位置随 Visual Studio 2017 一起安装的实用工具程序： <br> `C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE`

::: moniker-end

::: moniker range="vs-2019"

可在静默模式下在目标计算机上使用 `StorePID.exe` 实用工具，从而使用产品密钥激活 Visual Studio 的已安装版本。 `StorePID.exe` 是在以下默认位置随 Visual Studio 2019 一起安装的实用工具程序： <br> `C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE`

::: moniker-end

 通过使用 System Center 代理或提升的命令提示符，运行具有提升的权限的 `StorePID.exe`。 后接产品密钥和 Microsoft Product Code (MPC)。

>[!IMPORTANT]
> 请务必在产品密钥中添加短划线。

 ```cmd
 StorePID.exe [product key including the dashes] [MPC]
 ```

::: moniker range="vs-2017"

下面展示了用于应用 Visual Studio 2017 Enterprise 许可证（其中 MPC 为 08860，产品密钥为 `AAAAA-BBBBB-CCCCC-DDDDDD-EEEEEE`）的示例命令行（假设在默认安装位置上）：

```cmd
"C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\StorePID.exe" AAAAA-BBBBB-CCCCC-DDDDDD-EEEEEE 08860
```

::: moniker-end

::: moniker range="vs-2019"

下面展示了用于应用 Visual Studio 2019 Enterprise 许可证（其中 MPC 为 09260，产品密钥为 `AAAAA-BBBBB-CCCCC-DDDDDD-EEEEEE`）的示例命令行（假设在默认安装位置上）：

```cmd
"C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE\StorePID.exe" AAAAA-BBBBB-CCCCC-DDDDDD-EEEEEE 09260
```

::: moniker-end

::: moniker range="vs-2017"

 下表列出了 Visual Studio 的每个版本的 MPC 代码：

| Visual Studio 版本                | MPC   |
|--------------------------------------|-------|
| Visual Studio Enterprise 2017        | 08860 |
| Visual Studio Professional 2017      | 08862 |
| Visual Studio Test Professional 2017 | 08866 |

::: moniker-end

::: moniker range="vs-2019"

| Visual Studio 版本                | MPC   |
|--------------------------------------|-------|
| Visual Studio Enterprise 2019        | 09260 |
| Visual Studio Professional 2019      | 09262 |

::: moniker-end

如果 `StorePID.exe` 成功应用产品密钥，则会返回值为 0 的 `%ERRORLEVEL%`。 如果遇到错误，则会返回下列代码之一（具体视错误条件而定）：

| 错误                     | 代码 |
|---------------------------|------|
| `PID_ACTION_SUCCESS`      | 0    |
| `PID_ACTION_NOTINSTALLED` | 1    |
| `PID_ACTION_INVALID`      | 2    |
| `PID_ACTION_EXPIRED`      | 3    |
| `PID_ACTION_INUSE`        | 4    |
| `PID_ACTION_FAILURE`      | 5    |
| `PID_ACTION_NOUPGRADE`    | 6    |

> [!NOTE]
> 运行 Visual Studio 的虚拟实例时，请确保也虚拟化了本地 AppData 文件夹和注册表。 若要对虚拟实例进行故障排除，请运行 `C:\Program Files (x86)\Microsoft Visual Studio\<version>\Common7\IDE\DDConfigCA.exe`。  

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>请参阅

* [安装 Visual Studio](../install/install-visual-studio.md)
* [创建 Visual Studio 的脱机安装](../install/create-an-offline-installation-of-visual-studio.md)
