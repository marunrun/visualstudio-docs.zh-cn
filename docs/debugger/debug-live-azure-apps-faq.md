---
title: 快照调试的常见问题解答 | Microsoft Docs
ms.date: 11/07/2017
ms.topic: reference
helpviewer_keywords:
- debugger
ms.assetid: 944f1eb0-a74b-4d28-ae2b-a370cd869add
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ceda2dd4e85c8db5b66ef753a748977204b8caab
ms.sourcegitcommit: ea182703e922c74725045afc251bcebac305068a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71211212"
---
# <a name="frequently-asked-questions-for-snapshot-debugging-in-visual-studio"></a>在 Visual Studio 中进行快照调试的常见问答解答

下面列出了在使用 Snapshot Debugger 调试实时 Azure 应用程序时可能出现的问题。

#### <a name="what-is-the-performance-cost-of-taking-a-snapshot"></a>获取快照的性能成本是什么？

当 Snapshot Debugger 捕获应用快照时，它会创建应用进程的分支并挂起分支的副本。 调试快照时，将针对进程的分支副本进行调试。 此过程只需 10-20 毫秒，但不会复制应用的完整堆。 而是仅复制页表并将页设置为写入时复制。 如果堆上的某些应用对象发生更改，则会复制其相应页。 这就是每个快照具有较小的内存中成本的原因（对于大多数应用，大约具有数百千字节）。

#### <a name="what-happens-if-i-have-a-scaled-out-azure-app-service-multiple-instances-of-my-app"></a>如果我有一个横向扩展的 Azure 应用服务（多个应用实例），会发生什么情况？

具有多个应用实例时，快照点会应用于每个实例。 只有符合指定条件的第一个快照点才会创建快照。 如果你有多个快照点，则后续快照将来自创建了第一个快照的同一个实例。 发送到输出窗口的记录点将仅显示来自一个实例的消息，而发送到应用程序日志的记录点将发送来自所有实例的消息。

#### <a name="how-does-the-snapshot-debugger-load-symbols"></a>Snapshot Debugger 如何加载符号？

若要使用 Snapshot Debugger，本地应用程序或部署到 Azure 应用服务的应用程序必须具有匹配的符号。 （目前不支持嵌入的 PDB。）Snapshot Debugger 将自动从 Azure 应用服务下载符号。 自 Visual Studio 2017 版本 15.2 起，部署到 Azure 应用服务时，也会同时部署应用的符号。

#### <a name="does-the-snapshot-debugger-work-against-release-builds-of-my-application"></a>Snapshot Debugger 是否适用于我的应用程序的发布版本？

是 - Snapshot Debugger 适用于发布版本。 当快照点置于某个函数中时，该函数被重新编译回调试版本，使其可调试。 停止 Snapshot Debugger 会将函数返回到发布版本的版本。

#### <a name="can-logpoints-cause-side-effects-in-my-production-application"></a>记录点是否可能在我的生产应用程序中产生副作用？

否 - 添加到应用的任何日志消息都会进行虚拟评估。 它们不会对你的应用程序产生任何副作用。 但是，可能无法使用记录点访问某些本机属性。

#### <a name="does-the-snapshot-debugger-work-if-my-server-is-under-load"></a>如果我的服务器处于负载中，Snapshot Debugger 是否会运行？

是，快照调试可用于处于负载中的服务器。 当服务器上的可用内存量较少时，Snapshot Debugger 会进行限制，并且不会捕获快照。

#### <a name="how-do-i-uninstall-the-snapshot-debugger"></a>如何卸载快照调试器？

可以通过执行以下步骤来卸载应用服务上的 Snapshot Debugger 站点扩展：

1. 通过 Visual Studio 中的 Cloud Explorer 或 Azure 门户关闭应用服务。
1. 导航到应用服务的 Kudu 站点（即，yourappservice.scm.azurewebsites.net）并导航到“站点扩展”。
1. 单击 Snapshot Debugger 站点扩展上的 X 以将其删除。

#### <a name="why-are-ports-opened-during-a-snapshot-debugger-session"></a>为什么在 Snapshot Debugger 会话期间打开端口？

Snapshot Debugger 必须打开一组端口才能调试在 Azure 中获取的快照，这些端口与远程调试所需的端口相同。 [可以在此处找到端口列表](../debugger/remote-debugger-port-assignments.md)。

#### <a name="how-do-i-disable-the-remote-debugger-extension"></a>如何实现禁用远程调试器扩展吗？

对于应用服务：
1. 通过应用服务的 Azure 门户禁用远程调试器扩展。
2. Azure 门户 > 应用程序服务资源边栏选项卡 >*应用程序设置*
3. 导航到 "*调试*" 部分，然后单击 "*关闭*" 按钮进行*远程调试*。

对于 AKS：
1. 更新 Dockerfile，删除[Docker 映像上与 Visual Studio Snapshot Debugger](https://github.com/Microsoft/vssnapshotdebugger-docker)相对应的部分。
2. 重新生成并重新部署已修改的 Docker 映像。

对于虚拟机/虚拟机规模集，请删除远程调试器扩展、证书、KeyVaults 和入站 NAT 池，如下所示：

1. 删除远程调试器扩展

   可以通过多种方式来禁用虚拟机和虚拟机规模集的远程调试器：

      - 通过 Cloud Explorer 禁用远程调试器

         - Cloud Explorer > 虚拟机资源 > 禁用调试（禁用 Cloud Explorer 上虚拟机规模集的调试）。

      - 通过 PowerShell 脚本/Cmdlet 禁用远程调试器

         对于虚拟机：

         ```powershell
         Remove-AzVMExtension -ResourceGroupName $rgName -VMName $vmName -Name Microsoft.VisualStudio.Azure.RemoteDebug.VSRemoteDebugger
         ```

         对于虚拟机规模集：

         ```powershell
         $vmss = Get-AzVmss -ResourceGroupName $rgName -VMScaleSetName $vmssName
         $extension = $vmss.VirtualMachineProfile.ExtensionProfile.Extensions | Where {$_.Name.StartsWith('VsDebuggerService')} | Select -ExpandProperty Name
         Remove-AzVmssExtension -VirtualMachineScaleSet $vmss -Name $extension
         ```

      - 通过 Azure 门户禁用远程调试器
         - Azure 门户 > 虚拟机/虚拟机规模集资源边栏选项卡 > 扩展
         - 卸载 VisualStudio。 VSRemoteDebugger 扩展

         > [!NOTE]
         > 虚拟机规模集-门户不允许删除 DebuggerListener 端口。 你将需要使用 Azure PowerShell。 有关详细信息，请参见以下内容。

2. 删除证书和 Azure KeyVault

   为虚拟机或虚拟机规模集安装远程调试器扩展时，将创建客户端证书和服务器证书，以通过 Azure 虚拟机/虚拟机规模集资源对 VS 客户端进行身份验证。

   - 客户端证书

      此证书是位于 Cert：/CurrentUser/My/中的自签名证书

      ```
      Thumbprint                                Subject
      ----------                                -------

      1234123412341234123412341234123412341234  CN=ResourceName
      ```

      从计算机中删除此证书的一种方法是通过 PowerShell

      ```powershell
      $ResourceName = 'ResourceName' # from above
      Get-ChildItem -Path Cert:\CurrentUser\My | Where-Object {$_.Subject -match $ResourceName} | Remove-Item
      ```

   - 服务器证书
      - 相应的服务器证书指纹作为机密部署到 Azure KeyVault。 VS 将尝试在对应于虚拟机或虚拟机规模集资源的区域中查找或创建前缀为 MSVSAZ * 的 KeyVault。 所有虚拟机或虚拟机规模集部署到该区域的资源将共享同一 KeyVault。
      - 若要删除服务器证书指纹密码，请跳到 Azure 门户，并在承载资源的同一区域中查找 MSVSAZ * KeyVault。 删除应该标记的机密`remotedebugcert<<ResourceName>>`
      - 还需要通过 PowerShell 从资源中删除服务器机密。

      对于虚拟机：

      ```powershell
      $vm.OSProfile.Secrets[0].VaultCertificates.Clear()
      Update-AzVM -ResourceGroupName $rgName -VM $vm
      ```

      对于虚拟机规模集：

      ```powershell
      $vmss.VirtualMachineProfile.OsProfile.Secrets[0].VaultCertificates.Clear()
      Update-AzVmss -ResourceGroupName $rgName -VMScaleSetName $vmssName -VirtualMachineScaleSet $vmss
      ```

3. 删除所有 DebuggerListener 入站 NAT 池（仅虚拟机规模集）

   远程调试器引入了 DebuggerListener 的绑定 NAT 池，这些池应用于规模集的负载均衡器。

   ```powershell
   $inboundNatPools = $vmss.VirtualMachineProfile.NetworkProfile.NetworkInterfaceConfigurations.IpConfigurations.LoadBalancerInboundNatPools
   $inboundNatPools.RemoveAll({ param($pool) $pool.Id.Contains('inboundNatPools/DebuggerListenerNatPool-') }) | Out-Null

   if ($LoadBalancerName)
   {
      $lb = Get-AzLoadBalancer -ResourceGroupName $ResourceGroup -name $LoadBalancerName
      $lb.FrontendIpConfigurations[0].InboundNatPools.RemoveAll({ param($pool) $pool.Id.Contains('inboundNatPools/DebuggerListenerNatPool-') }) | Out-Null
      Set-AzLoadBalancer -LoadBalancer $lb
   }
   ```

#### <a name="how-do-i-disable-snapshot-debugger"></a>如何实现禁用 Snapshot Debugger？

对于应用服务：
1. 通过应用服务的 Azure 门户禁用 Snapshot Debugger。
2. Azure 门户 > 应用程序服务资源边栏选项卡 >*应用程序设置*
3. 删除 Azure 门户中的以下应用设置，并保存所做的更改。
   - INSTRUMENTATIONENGINE_EXTENSION_VERSION
   - SNAPSHOTDEBUGGER_EXTENSION_VERSION

   > [!WARNING]
   > 对应用程序设置的任何更改都将启动应用程序重启。 有关应用程序设置的详细信息，请参阅[在 Azure 门户中配置应用服务应用](/azure/app-service/web-sites-configure)。

对于 AKS：
1. 更新 Dockerfile，删除[Docker 映像上与 Visual Studio Snapshot Debugger](https://github.com/Microsoft/vssnapshotdebugger-docker)相对应的部分。
2. 重新生成并重新部署已修改的 Docker 映像。

对于虚拟机/虚拟机规模集：

可以通过多种方式来禁用 Snapshot Debugger：
- Cloud Explorer > 虚拟机/虚拟机规模集资源 > 禁用诊断

- Azure 门户 > 虚拟机/虚拟机规模集资源边栏选项卡 > 扩展 > 卸载 VMDiagnosticsSettings 扩展

- [Az powershell](https://docs.microsoft.com/powershell/azure/overview)中的 powershell cmdlet

   虚拟机：

   ```powershell
      Remove-AzVMExtension -ResourceGroupName $rgName -VMName $vmName -Name Microsoft.Insights.VMDiagnosticsSettings
   ```

   虚拟机规模集：

   ```powershell
      $vmss = Get-AzVmss -ResourceGroupName $rgName -VMScaleSetName $vmssName
      Remove-AzVmssExtension -VirtualMachineScaleSet $vmss -Name Microsoft.Insights.VMDiagnosticsSettings
   ```

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中进行调试](../debugger/index.yml)
- [使用快照调试器调试实时 ASP.NET 应用](../debugger/debug-live-azure-applications.md)
- [使用 Snapshot Debugger 调试实时 ASP.NET Azure Virtual Machines\Virtual 计算机规模集](../debugger/debug-live-azure-virtual-machines.md)
- [使用 Snapshot Debugger 调试实时 ASP.NET Azure Kubernetes](../debugger/debug-live-azure-kubernetes.md)
- [快照调试的疑难解答和已知问题](../debugger/debug-live-azure-apps-troubleshooting.md)
