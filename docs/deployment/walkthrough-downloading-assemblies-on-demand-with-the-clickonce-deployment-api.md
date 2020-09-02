---
title: 用 ClickOnce 部署 API 按需下载程序集
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- assemblies, downloading [ClickOnce]
- ClickOnce deployment, on-demand download
- on-demand assemblies, ClickOnce
ms.assetid: d20e2789-8621-4806-b5b7-841122da1456
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f52d853399bb568407b5022dca7f6288e3901a7a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "66262907"
---
# <a name="walkthrough-download-assemblies-on-demand-with-the-clickonce-deployment-api"></a>演练：通过 ClickOnce 部署 API 按需下载程序集
默认情况下，应用程序中包含的所有程序集 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 都会在应用程序首次运行时下载。 但是，你的应用程序的某些部分可能由一小部分用户使用。 在这种情况下，你希望仅当创建其类型之一时才下载程序集。 下面的演练演示如何将应用程序中的某些程序集标记为“可选”，以及如何在公共语言运行时 (CLR) 需要它们时使用 <xref:System.Deployment.Application> 命名空间中的类下载它们。

> [!NOTE]
> 应用程序必须在完全信任下运行才能使用此过程。

## <a name="prerequisites"></a>先决条件
 要完成本演练，你将需要以下组件之一：

- Windows SDK。 可以从 Microsoft 下载中心下载 Windows SDK。

- Visual Studio。

## <a name="create-the-projects"></a>创建项目

#### <a name="to-create-a-project-that-uses-an-on-demand-assembly"></a>创建使用按需程序集的项目

1. 创建名为 ClickOnceOnDemand 的目录。

2. 打开 Windows SDK 命令提示符或 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 命令提示符。

3. 更改为 ClickOnceOnDemand 目录。

4. 使用以下命令生成公钥/私钥对：

   ```cmd
   sn -k TestKey.snk
   ```

5. 使用记事本或其他文本编辑器，使用名为的单个属性定义名为的类 `DynamicClass` `Message` 。

    [!code-vb[ClickOnceLibrary#1](../deployment/codesnippet/VisualBasic/walkthrough-downloading-assemblies-on-demand-with-the-clickonce-deployment-api_1.vb)]
    [!code-csharp[ClickOnceLibrary#1](../deployment/codesnippet/CSharp/walkthrough-downloading-assemblies-on-demand-with-the-clickonce-deployment-api_1.cs)]

6. 将该文本保存为一个名为 *ClickOnceLibrary.cs* 或 *找到 clickoncelibrary.dll*的文件（具体取决于你使用的语言）到 *ClickOnceOnDemand* 目录。

7. 将文件编译到程序集。

   ```csharp
   csc /target:library /keyfile:TestKey.snk ClickOnceLibrary.cs
   ```

   ```vb
   vbc /target:library /keyfile:TestKey.snk ClickOnceLibrary.vb
   ```

8. 若要获取程序集的公钥标记，请使用以下命令：

   ```cmd
   sn -T ClickOnceLibrary.dll
   ```

9. 使用文本编辑器创建一个新文件，然后输入以下代码。 此代码创建一个 Windows 窗体应用程序，该应用程序在需要时下载找到 clickoncelibrary.dll 程序集。

     [!code-csharp[ClickOnceOnDemandCmdLine#1](../deployment/codesnippet/CSharp/walkthrough-downloading-assemblies-on-demand-with-the-clickonce-deployment-api_2.cs)]
     [!code-vb[ClickOnceOnDemandCmdLine#1](../deployment/codesnippet/VisualBasic/walkthrough-downloading-assemblies-on-demand-with-the-clickonce-deployment-api_2.vb)]

10. 在代码中，找到对的调用 <xref:System.Reflection.Assembly.LoadFile%2A> 。

11. 设置 `PublicKeyToken` 为之前检索到的值。

12. 将该文件另存*Form1.cs*为 Form1.cs*或 node.js。*

13. 使用以下命令将其编译为可执行文件。

    ```csharp
    csc /target:exe /reference:ClickOnceLibrary.dll Form1.cs
    ```

    ```vb
    vbc /target:exe /reference:ClickOnceLibrary.dll Form1.vb
    ```

## <a name="mark-assemblies-as-optional"></a>将程序集标记为可选

#### <a name="to-mark-assemblies-as-optional-in-your-clickonce-application-by-using-mageuiexe"></a>使用 MageUI.exe 在 ClickOnce 应用程序中将程序集标记为可选

1. 按照[演练：手动部署 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)中所述，使用*MageUI.exe*创建应用程序清单。 对于应用程序清单，请使用以下设置：

    - 命名应用程序清单 `ClickOnceOnDemand` 。

    - 在 " **文件** " 页上的 " *ClickOnceLibrary.dll* " 行中，将 " **文件类型** " 列设置为 " **无**"。

    - 在 " **文件** " 页上的 " *ClickOnceLibrary.dll* " 行中，在 `ClickOnceLibrary.dll` " **组** " 列中键入。

2. 按照[演练：手动部署 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)中所述，使用*MageUI.exe*创建部署清单。 对于部署清单，请使用以下设置：

    - 命名部署清单 `ClickOnceOnDemand` 。

## <a name="testing-the-new-assembly"></a>测试新程序集

#### <a name="to-test-your-on-demand-assembly"></a>测试按需程序集

1. 将部署上传 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 到 Web 服务器。

2. [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]通过在 Web 浏览器中输入部署清单的 URL 来启动使用部署的应用程序。 如果调用 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序 `ClickOnceOnDemand` ，并将其上传到 adatum.com 的根目录，则 URL 将如下所示：

   ```
   http://www.adatum.com/ClickOnceOnDemand/ClickOnceOnDemand.application
   ```

3. 在主窗体显示时按 <xref:System.Windows.Forms.Button>。 应在消息框窗口中看到一个显示为“Hello, World!”的字符串。

## <a name="see-also"></a>另请参阅
- <xref:System.Deployment.Application.ApplicationDeployment>