---
title: 处理专用的部署 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- deploying applications [Visual Studio SDK]
- specialized deployment
ms.assetid: de068b6a-e806-45f0-9dec-2458fbb486f7
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 81bc5459f9f4b721d0ce0741b22b04a07bfcc771
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66329050"
---
# <a name="handle-specialized-deployment"></a>处理专用的部署
部署是项目的可选操作。 Web 项目中，例如，支持的部署，以便更新 Web 服务器的项目。 同样，**智能设备**项目支持将复制到目标设备生成的应用程序的部署。 项目子类型可以通过实现来提供专门的部署行为<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg>接口。 此接口定义一组完整的部署操作：

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg.AdviseDeployStatusCallback%2A>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg.Commit%2A>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg.QueryStartDeploy%2A>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg.QueryStatusDeploy%2A>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg.Rollback%2A>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg.StartDeploy%2A>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg.StopDeploy%2A>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg.UnadviseDeployStatusCallback%2A>

  应在单独的线程，以便执行实际部署操作[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]甚至更好地响应用户交互。 提供的方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg>来异步调用[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]和允许环境查询在任何时间执行部署操作的状态或停止该操作，如有必要在后台运行。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg>接口部署操作由环境在用户选择部署命令时调用。

  若要通知的环境的部署操作已开始或结束，项目子类型需要调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployStatusCallback.OnStartDeploy%2A>和<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployStatusCallback.OnEndDeploy%2A>方法。

## <a name="to-handle-a-specialized-deployment-by-a-subtype-project"></a>若要处理专用的部署由子类型项目

- 实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg.AdviseDeployStatusCallback%2A>方法来注册要接收通知的部署状态事件的环境。

    ```vb
    Private adviseSink As Microsoft.VisualStudio.Shell.EventSinkCollection = New Microsoft.VisualStudio.Shell.EventSinkCollection()
    Public Function AdviseDeployStatusCallback(ByVal pIVsDeployStatusCallback As IVsDeployStatusCallback, _
                                               ByRef pdwCookie As UInteger) As Integer

        If pIVsDeployStatusCallback Is Nothing Then
            Throw New ArgumentNullException("pIVsDeployStatusCallback")
        End If

        pdwCookie = adviseSink.Add(pIVsDeployStatusCallback)
        Return VSConstants.S_OK

    End Function
    ```

    ```csharp
    private Microsoft.VisualStudio.Shell.EventSinkCollection adviseSink = new Microsoft.VisualStudio.Shell.EventSinkCollection();
    public int AdviseDeployStatusCallback(IVsDeployStatusCallback pIVsDeployStatusCallback,
                                          out uint pdwCookie)
    {
        if (pIVsDeployStatusCallback == null)
            throw new ArgumentNullException("pIVsDeployStatusCallback");

        pdwCookie = adviseSink.Add(pIVsDeployStatusCallback);
        return VSConstants.S_OK;
    }

    ```

- 实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg.UnadviseDeployStatusCallback%2A>方法来取消环境的注册以接收通知的部署状态事件。

    ```vb
    Public Function UnadviseDeployStatusCallback(ByVal dwCookie As UInteger) As Integer
        adviseSink.RemoveAt(dwCookie)
        Return VSConstants.S_OK
    End Function
    ```

    ```csharp
    public int UnadviseDeployStatusCallback(uint dwCookie)
    {
        adviseSink.RemoveAt(dwCookie);
        return VSConstants.S_OK;
    }

    ```

- 实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg.Commit%2A>方法来执行特定于应用程序提交操作。  此方法主要用于数据库部署。

    ```vb
    Public Function Commit(ByVal dwReserved As UInteger) As Integer
        'Implement commit operation here.
        Return VSConstants.S_OK
    End Function
    ```

    ```csharp
    public int Commit(uint dwReserved)
    {
         //Implement commit operation here.
         return VSConstants.S_OK;
    }

    ```

- 实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg.Rollback%2A>方法来执行回滚操作。 调用此方法时，部署项目必须执行任何适于回滚更改并还原项目的状态。 此方法主要用于数据库部署。

    ```vb
    Public Function Commit(ByVal dwReserved As UInteger) As Integer
        'Implement commit operation here.
        Return VSConstants.S_OK
    End Function
    ```

    ```csharp
    public int Rollback(uint dwReserved)
    {
        //Implement Rollback operation here.
        return VSConstants.S_OK;
    }

    ```

- 实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg.QueryStartDeploy%2A>方法，以确定项目是否能够启动部署操作。

    ```vb
    Public Function QueryStartDeploy(ByVal dwOptions As UInteger, ByVal pfSupported As Integer(), ByVal pfReady As Integer()) As Integer
        If Not pfSupported Is Nothing AndAlso pfSupported.Length > 0 Then
            pfSupported(0) = 1
        End If
        If Not pfReady Is Nothing AndAlso pfReady.Length > 0 Then
            pfReady(0) = 0
            If Not deploymentThread Is Nothing AndAlso (Not deploymentThread.IsAlive) Then
                pfReady(0) = 1
            End If
        End If
        Return VSConstants.S_OK
    End Function
    ```

    ```csharp
    public int QueryStartDeploy(uint dwOptions, int[] pfSupported, int[] pfReady)
    {
        if (pfSupported != null && pfSupported.Length >0)
            pfSupported[0] = 1;
        if (pfReady != null && pfReady.Length >0)
        {
            pfReady[0] = 0;
            if (deploymentThread != null && !deploymentThread.IsAlive)
                pfReady[0] = 1;
        }
        return VSConstants.S_OK;
    }

    ```

- 实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg.QueryStatusDeploy%2A>方法，以确定是否已成功完成部署操作。

    ```vb
    Public Function QueryStatusDeploy(ByRef pfDeployDone As Integer) As Integer
        pfDeployDone = 1
        If Not deploymentThread Is Nothing AndAlso deploymentThread.IsAlive Then
            pfDeployDone = 0
        End If
        Return VSConstants.S_OK
    End Function
    ```

    ```csharp
    public int QueryStatusDeploy(out int pfDeployDone)
    {
        pfDeployDone = 1;
        if (deploymentThread != null && deploymentThread.IsAlive)
            pfDeployDone = 0;
        return VSConstants.S_OK;
    }

    ```

- 实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg.StartDeploy%2A>方法以开始部署操作在单独的线程。 将代码放在应用程序部署到特定`Deploy`方法。

    ```vb
    Public Function StartDeploy(ByVal pIVsOutputWindowPane As IVsOutputWindowPane, ByVal dwOptions As UInteger) As Integer
        If pIVsOutputWindowPane Is Nothing Then
            Throw New ArgumentNullException("pIVsOutputWindowPane")
        End If

        If Not deploymentThread Is Nothing AndAlso deploymentThread.IsAlive Then
            Throw New NotSupportedException("Cannot start deployment operation when it is already started; Call QueryStartDeploy first")
        End If

        outputWindow = pIVsOutputWindowPane

        ' Notify that deployment is about to begin and see if any user wants to cancel.
        If (Not NotifyStart()) Then
            Return VSConstants.E_ABORT
        End If

        operationCanceled = False

        ' Create and start our thread
        deploymentThread = New Thread(AddressOf Me.Deploy)
        deploymentThread.Name = "Deployment Thread"
        deploymentThread.Start()

        Return VSConstants.S_OK
    End Function
    ```

    ```csharp
    public int StartDeploy(IVsOutputWindowPane pIVsOutputWindowPane, uint dwOptions)
    {
        if (pIVsOutputWindowPane == null)
            throw new ArgumentNullException("pIVsOutputWindowPane");

        if (deploymentThread != null && deploymentThread.IsAlive)
            throw new NotSupportedException("Cannot start deployment operation when it is already started; Call QueryStartDeploy first");

        outputWindow = pIVsOutputWindowPane;

        // Notify that deployment is about to begin and see if any user wants to cancel.
        if (!NotifyStart())
            return VSConstants.E_ABORT;

        operationCanceled = false;

        // Create and start our thread
        deploymentThread = new Thread(new ThreadStart(this.Deploy));
        deploymentThread.Name = "Deployment Thread";
        deploymentThread.Start();

        return VSConstants.S_OK;
    }

    ```

- 实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg.StopDeploy%2A>方法来停止部署操作。 当用户按下调用此方法**取消**在部署过程中的按钮。

    ```vb
    Public Function StopDeploy(ByVal fSync As Integer) As Integer
        If Not deploymentThread Is Nothing AndAlso deploymentThread.IsAlive Then
            Return VSConstants.S_OK
        End If

        outputWindow.OutputStringThreadSafe("Canceling deployment")
        operationCanceled = True
        If fSync <> 0 Then
            ' Synchronous request, wait for the thread to terminate.
            If (Not deploymentThread.Join(10000)) Then
                Debug.Fail("Deployment thread did not terminate before the timeout, Aborting thread")
                deploymentThread.Abort()
            End If
        End If

        Return VSConstants.S_OK
    End Function
    ```

    ```csharp
    public int StopDeploy(int fSync)
    {
        if (deploymentThread != null && deploymentThread.IsAlive)
            return VSConstants.S_OK;

        outputWindow.OutputStringThreadSafe("Canceling deployment");
        operationCanceled = true;
        if (fSync != 0)
        {
            // Synchronous request, wait for the thread to terminate.
            if (!deploymentThread.Join(10000))
            {
                Debug.Fail("Deployment thread did not terminate before the timeout, Aborting thread");
                deploymentThread.Abort();
            }
        }

        return VSConstants.S_OK;
    }

    ```

> [!NOTE]
> 本主题中提供的所有代码示例都是在一个更大示例的组成部分[VSSDK 示例](https://aka.ms/vs2015sdksamples)。

## <a name="see-also"></a>请参阅
- [项目子类型](../../extensibility/internals/project-subtypes.md)