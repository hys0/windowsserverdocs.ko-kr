---
title: 업그레이드, 백업 및 복원 SDN 인프라
description: 이 항목에서는 업데이트, 백업, SDN 인프라를 복원 하는 방법을 알아봅니다.
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: article
ms.assetid: e9a8f2fd-48fe-4a90-9250-f6b32488b7a4
ms.author: grcusanz
author: shortpatti
ms.date: 08/27/2018
ms.openlocfilehash: 7916377f58261d0ccaa3fa24f135fccca3d5e79b
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446336"
---
# <a name="upgrade-backup-and-restore-sdn-infrastructure"></a>업그레이드, 백업 및 복원 SDN 인프라

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 업데이트, 백업, SDN 인프라를 복원 하는 방법을 알아봅니다. 

## <a name="upgrade-the-sdn-infrastructure"></a>SDN 인프라를 업그레이드 합니다.
Windows Server 2019에 Windows Server 2016에서 SDN 인프라를 업그레이드할 수 있습니다. 업그레이드 순서에 대 한 "SDN 인프라 업데이트" 섹션에서 설명한 것 처럼 동일한 일련의 단계를 따릅니다. 업그레이드 하기 전에 네트워크 컨트롤러 데이터베이스의 백업을 수행 하는 것이 좋습니다.

네트워크 컨트롤러 컴퓨터에 대 한 업그레이드가 완료 된 후 노드의 상태를 확인 하려면 Get NetworkControllerNode cmdlet을 사용 합니다. 노드 상태를 다른 노드를 업그레이드 하기 전에 "위쪽"으로 다시 가져온 개체를 확인 합니다. 모든 네트워크 컨트롤러 노드를 업그레이드 한 후 네트워크 컨트롤러 1 시간 이내에 네트워크 컨트롤러 클러스터 내에서 실행 되는 마이크로 서비스를 업데이트 합니다. 업데이트 networkcontroller cmdlet을 사용 하는 즉시 업데이트를 트리거할 수 있습니다. 

포함 하는 소프트웨어 정의 네트워킹 (SDN) 시스템의 운영 체제 구성 요소를 모두에 동일한 Windows 업데이트를 설치 합니다.

- SDN은 Hyper-v 호스트를 사용 하도록 설정
- 네트워크 컨트롤러 Vm
- 소프트웨어 부하 분산 장치 Mux Vm
- RAS 게이트웨이 Vm 

>[!IMPORTANT]
>System Center Virtual Manager를 사용 하는 경우 최신 업데이트 롤업을 사용 하 여 업데이트 해야 합니다.

각 구성 요소를 업데이트 하는 경우 Windows 업데이트를 설치 하기 위한 표준 방법 중 하나를 사용할 수 있습니다. 그러나 워크 로드 및 네트워크 컨트롤러 데이터베이스의 무결성에 대 한 최소 가동 중지 시간을 보장 하려면 다음이 단계를 수행 합니다.

1. 관리 콘솔을 업데이트 합니다.<p>각 네트워크 컨트롤러 Powershell 모듈을 사용할 컴퓨터에 업데이트를 설치 합니다.  RSAT NetworkController 역할을 단독으로 설치할 수 있다고 어디를 포함 합니다. 네트워크 컨트롤러 Vm 자체; 제외 다음 단계에서는 해당를 업데이트 합니다.

2. 첫 번째 네트워크 컨트롤러 VM에서 모든 업데이트를 설치 하 고 다시 시작 합니다.

3. 다음 네트워크 컨트롤러 VM을 계속 하기 전에 `get-networkcontrollernode` cmdlet을 업데이트 하 고 다시 시작 된 노드의 상태를 확인 합니다.

4. 다시 부팅 주기 동안 네트워크 컨트롤러 노드를 중단 한 다음 돌아와야 다시 될 때까지 기다립니다.<p>VM 다시 부팅 한 후에 다시 이동 하기 전에 몇 분 정도 걸릴 수 있습니다 합니다 **_위로_** 상태입니다. 출력의 예제를 참조 하세요. 

5. Load balancer 인프라의 지속적인 가용성을 보장 하려면 한 번에 한 각 SLB Mux VM에 업데이트를 설치 합니다.

6. Hyper-v 호스트 및 RAS 게이트웨이에 있는 RAS 게이트웨이 포함 하는 호스트부터 업데이트 **대기** 모드입니다.<p>RAS 게이트웨이 Vm은 테 넌 트 연결 손실 없이 실시간 마이그레이션할 수 없습니다. 업데이트 주기 동안 횟수를 최소화 하기 위해 주의 해야 새 RAS 게이트웨이 연결 장애 조치를 테 넌 트입니다. 호스트 및 RAS 게이트웨이 업데이트를 조정 하 여 각 테 넌 트 장애 조치 한 번에 많아야 합니다.

    a. 실시간 마이그레이션 수 있는 Vm의 호스트를 끄려고 합니다.<p>RAS 게이트웨이 Vm 호스트에서 유지 되어야 합니다.

    b. 이 호스트에서 각 게이트웨이 VM에 업데이트를 설치 합니다.

    c. 업데이트에는 게이트웨이 VM을 재부팅 해야 하는 경우에 다음 VM 다시 부팅 합니다.  

    d. 게이트웨이 업데이트 된 VM을 포함 하는 호스트에 업데이트를 설치 합니다.

    e. 업데이트에 필요한 경우 호스트를 다시 부팅 합니다.

    f. 대기 게이트웨이 포함 하는 각 추가 호스트에 대해 반복 합니다.<p>대기 게이트웨이가 없습니다. 계속 하는 경우 다음 나머지 모든 호스트에 대해 동일한 단계를 수행 합니다.


### <a name="example-use-the-get-networkcontrollernode-cmdlet"></a>예: Get-networkcontrollernode cmdlet 사용 

이 예제에서는 출력을 표시 합니다 `get-networkcontrollernode` 네트워크 컨트롤러 Vm 중 하나 내에서 cmdlet을 실행 합니다.  

이 예제의 출력에 표시 되는 노드의 상태가입니다.

- NCNode1.contoso.com = Down
- NCNode2.contoso.com =
- NCNode3.contoso.com =

>[!IMPORTANT]
>노드 변경에 대 한 상태가 될 때까지 몇 분 정도 기다려야 _**위로**_ 한 번에 하나씩 추가 노드를 업데이트 하기 전에 합니다.

모든 네트워크 컨트롤러 노드를 업데이트 한 후 네트워크 컨트롤러 1 시간 이내에 네트워크 컨트롤러 클러스터 내에서 실행 되는 마이크로 서비스를 업데이트 합니다. 

>[!TIP]
>사용 하 여 즉시 업데이트를 트리거할 수 있습니다는 `update-networkcontroller` cmdlet.


```Powershell
PS C:\> get-networkcontrollernode
Name            : NCNode1.contoso.com
Server          : NCNode1.Contoso.com
FaultDomain     : fd:/NCNode1.Contoso.com
RestInterface   : Ethernet
NodeCertificate :
Status          : Down

Name            : NCNode2.Contoso.com
Server          : NCNode2.contoso.com
FaultDomain     : fd:/ NCNode2.Contoso.com
RestInterface   : Ethernet
NodeCertificate :
Status          : Up

Name            : NCNode3.Contoso.com
Server          : NCNode3.Contoso.com
FaultDomain     : fd:/ NCNode3.Contoso.com
RestInterface   : Ethernet
NodeCertificate :
Status          : Up
```

### <a name="example-use-the-update-networkcontroller-cmdlet"></a>예: 업데이트 networkcontroller cmdlet 사용
이 예제에서는 출력을 표시 합니다 `update-networkcontroller` 업데이트 네트워크 컨트롤러 cmdlet. 

>[!IMPORTANT]
>설치에 자세한 업데이트가 없을 때이 cmdlet을 실행 합니다.


```Powershell
PS C:\> update-networkcontroller
NetworkControllerClusterVersion NetworkControllerVersion
------------------------------- ------------------------
10.1.1                          10.1.15
```

## <a name="backup-the-sdn-infrastructure"></a>SDN 인프라 백업

네트워크 컨트롤러 데이터베이스의 정기 백업을 재해 또는 데이터 손실이 발생할 경우 비즈니스 연속성을 보장 합니다.  네트워크 컨트롤러 Vm을 백업 하도록 보장 하지는 않습니다 세션 여러 네트워크 컨트롤러 노드에서 계속 되도록 하기 때문에 충분 하지 않습니다.

**요구 사항:**
* SMB 공유 및 공유 및 파일 시스템에 대 한 읽기/쓰기 권한이 있는 자격 증명입니다.
* 필요에 따라 네트워크 컨트롤러 에서도 GMSA를 사용 하 여 설치 된 경우 그룹 관리 서비스 계정 (GMSA)를 사용할 수 있습니다.

**절차:**

1. 선택한 VM 백업 메서드를 사용 하거나 Hyper-v를 사용 하 여 각 네트워크 컨트롤러 VM의 복사본을 내보냅니다.<p>네트워크 컨트롤러 VM을 백업 데이터베이스를 암호 해독에 필요한 인증서를 있는지 확인 합니다.  

2. System Center Virtual Machine Manager (SCVMM)를 사용 하는 경우 SCVMM 서비스를 중지 하 고 SQL Server를 통해 백업 합니다.<p>여기서 목표는 네트워크 컨트롤러 백업 및 SCVMM 간의 불일치를 만들 수는이 시간 동안 SCVMM에 업데이트가 없는 가져올 수 있도록 합니다.  

   >[!IMPORTANT]
   >네트워크 컨트롤러 백업 완료 될 때까지 SCVMM 서비스를 다시 시작 하지 않습니다.

3. 사용 하 여 네트워크 컨트롤러 데이터베이스를 백업 합니다 `new-networkcontrollerbackup` cmdlet.

4. 완료 및 사용 하 여 백업 성공 여부를 확인 합니다 `get-networkcontrollerbackup` cmdlet.

5. SCVMM을 사용 하는 경우 SCVMM 서비스를 시작 합니다.



### <a name="example-backing-up-the-network-controller-database"></a>예: 네트워크 컨트롤러 데이터베이스 백업

```Powershell
$URI = "https://NC.contoso.com"
$Credential = Get-Credential

# Get or Create Credential object for File share user

$ShareUserResourceId = "BackupUser"

$ShareCredential = Get-NetworkControllerCredential -ConnectionURI $URI -Credential $Credential | Where {$_.ResourceId -eq $ShareUserResourceId }
If ($ShareCredential -eq $null) {
    $CredentialProperties = New-Object Microsoft.Windows.NetworkController.CredentialProperties
    $CredentialProperties.Type = "usernamePassword"
    $CredentialProperties.UserName = "contoso\alyoung"
    $CredentialProperties.Value = "<Password>"

    $ShareCredential = New-NetworkControllerCredential -ConnectionURI $URI -Credential $Credential -Properties $CredentialProperties -ResourceId $ShareUserResourceId -Force
}

# Create backup

$BackupTime = (get-date).ToString("s").Replace(":", "_")

$BackupProperties = New-Object Microsoft.Windows.NetworkController.NetworkControllerBackupProperties
$BackupProperties.BackupPath = "\\fileshare\backups\NetworkController\$BackupTime"
$BackupProperties.Credential = $ShareCredential

$Backup = New-NetworkControllerBackup -ConnectionURI $URI -Credential $Credential -Properties $BackupProperties -ResourceId $BackupTime -Force
```

### <a name="example-checking-the-status-of-a-network-controller-backup-operation"></a>예: 네트워크 컨트롤러 백업 작업의 상태를 확인 하는 중

```Powershell
PS C:\ > Get-NetworkControllerBackup -ConnectionUri $URI -Credential $Credential -ResourceId $Backup.ResourceId
| ConvertTo-JSON -Depth 10
{
    "Tags":  null,
    "ResourceRef":  "/networkControllerBackup/2017-04-25T16_53_13",
    "InstanceId":  "c3ea75ae-2892-4e10-b26c-a2243b755dc8",
    "Etag":  "W/\"0dafea6c-39db-401b-bda5-d2885ded470e\"",
    "ResourceMetadata":  null,
    "ResourceId":  "2017-04-25T16_53_13",
    "Properties":  {
                    "BackupPath":  "\\\\fileshare\backups\NetworkController\\2017-04-25T16_53_13",
                    "ErrorMessage":  "",
                    "FailedResourcesList":  [

                                            ],
                    "SuccessfulResourcesList":  [
                                                    "/networking/v1/credentials/11ebfc10-438c-4a96-a1ee-8a048ce675be",
                                                    "/networking/v1/credentials/41229069-85d4-4352-be85-034d0c5f4658",
                                                    "/networking/v1/credentials/b2a82c93-2583-4a1f-91f8-232b801e11bb",
                                                    "/networking/v1/credentials/BackupUser",
                                                    "/networking/v1/credentials/fd5b1b96-b302-4395-b6cd-ed9703435dd1",
                                                    "/networking/v1/virtualNetworkManager/configuration",
                                                    "/networking/v1/virtualSwitchManager/configuration",
                                                    "/networking/v1/accessControlLists/f8b97a4c-4419-481d-b757-a58483512640",
                                                    "/networking/v1/logicalnetworks/24fa1af9-88d6-4cdc-aba0-66e38c1a7bb8",
                                                    "/networking/v1/logicalnetworks/48610528-f40b-4718-938e-99c2be76f1e0",
                                                    "/networking/v1/logicalnetworks/89035b49-1ee3-438a-8d7a-f93cbae40619",
                                                    "/networking/v1/logicalnetworks/a9c8eaa0-519c-4988-acd6-11723e9efae5",
                                                    "/networking/v1/logicalnetworks/d4ea002c-c926-4c57-a178-461d5768c31f",
                                                    "/networking/v1/macPools/11111111-1111-1111-1111-111111111111",
                                                    "/networking/v1/loadBalancerManager/config",
                                                    "/networking/v1/publicIPAddresses/2c502b2d-b39a-4be1-a85a-55ef6a3a9a1d",
                                                    "/networking/v1/GatewayPools/Default",
                                                    "/networking/v1/servers/4c4c4544-0058-5810-8056-b4c04f395931",
                                                    "/networking/v1/servers/4c4c4544-0058-5810-8057-b4c04f395931",
                                                    "/networking/v1/servers/4c4c4544-0058-5910-8056-b4c04f395931",
                                                    "/networking/v1/networkInterfaces/058430d3-af43-4328-a440-56540f41da50",
                                                    "/networking/v1/networkInterfaces/08756090-6d55-4dec-98d5-80c4c5a47db8",
                                                    "/networking/v1/networkInterfaces/2175d74a-aacd-44e2-80d3-03f39ea3bc5d",
                                                    "/networking/v1/networkInterfaces/2400c2c3-2291-4b0b-929c-9bb8da55851a",
                                                    "/networking/v1/networkInterfaces/4c695570-6faa-4e4d-a552-0b36ed3e0962",
                                                    "/networking/v1/networkInterfaces/7e317638-2914-42a8-a2dd-3a6d966028d6",
                                                    "/networking/v1/networkInterfaces/834e3937-f43b-4d3c-88be-d79b04e63bce",
                                                    "/networking/v1/networkInterfaces/9d668fe6-b1c6-48fc-b8b1-b3f98f47d508",
                                                    "/networking/v1/networkInterfaces/ac4650ac-c3ef-4366-96e7-d9488fb661ba",
                                                    "/networking/v1/networkInterfaces/b9f23e35-d79e-495f-a1c9-fa626b85ae13",
                                                    "/networking/v1/networkInterfaces/fdd929f1-f64f-4463-949a-77b67fe6d048",
                                                    "/networking/v1/virtualServers/15a891ee-7509-4e1d-878d-de0cb4fa35fd",
                                                    "/networking/v1/virtualServers/57416993-b410-44fd-9675-727cd4e98930",
                                                    "/networking/v1/virtualServers/5f8aebdc-ee5b-488f-ac44-dd6b57bd316a",
                                                    "/networking/v1/virtualServers/6c812217-5931-43dc-92a8-1da3238da893",
                                                    "/networking/v1/virtualServers/d78b7fa3-812d-4011-9997-aeb5ded2b431",
                                                    "/networking/v1/virtualServers/d90820a5-635b-4016-9d6f-bf3f1e18971d",
                                                    "/networking/v1/loadBalancerMuxes/5f8aebdc-ee5b-488f-ac44-dd6b57bd316a_suffix",
                                                    "/networking/v1/loadBalancerMuxes/d78b7fa3-812d-4011-9997-aeb5ded2b431_suffix",
                                                    "/networking/v1/loadBalancerMuxes/d90820a5-635b-4016-9d6f-bf3f1e18971d_suffix",
                                                    "/networking/v1/Gateways/15a891ee-7509-4e1d-878d-de0cb4fa35fd_suffix",
                                                    "/networking/v1/Gateways/57416993-b410-44fd-9675-727cd4e98930_suffix",
                                                    "/networking/v1/Gateways/6c812217-5931-43dc-92a8-1da3238da893_suffix",
                                                    "/networking/v1/virtualNetworks/b3dbafb9-2655-433d-b47d-a0e0bbac867a",
                                                    "/networking/v1/virtualNetworks/d705968e-2dc2-48f2-a263-76c7892fb143",
                                                    "/networking/v1/loadBalancers/24fa1af9-88d6-4cdc-aba0-66e38c1a7bb8_10.127.132.2",
                                                    "/networking/v1/loadBalancers/24fa1af9-88d6-4cdc-aba0-66e38c1a7bb8_10.127.132.3",
                                                    "/networking/v1/loadBalancers/24fa1af9-88d6-4cdc-aba0-66e38c1a7bb8_10.127.132.4"
                                                ],
                    "InProgressResourcesList":  [

                                                ],
                    "ProvisioningState":  "Succeeded",
                    "Credential":  {
                                        "Tags":  null,
                                        "ResourceRef":  "/credentials/BackupUser",
                                        "InstanceId":  "00000000-0000-0000-0000-000000000000",
                                        "Etag":  null,
                                        "ResourceMetadata":  null,
                                        "ResourceId":  null,
                                        "Properties":  null
                                    }
                }
}
```

## <a name="restore-the-sdn-infrastructure-from-a-backup"></a>SDN 인프라 백업에서 복원

필요한 모든 구성 요소를 백업에서 복원 하면 SDN 환경을 작동 상태로 돌아갑니다.  

>[!IMPORTANT]
>단계를 복원 하는 구성 요소 수에 따라 달라 집니다.


1. 필요한 경우에 Hyper-v 호스트 및 필요한 저장소 다시 배포 합니다.

2. 필요한 경우 네트워크 컨트롤러 Vm, RAS 게이트웨이 Vm 및 Mux Vm 백업에서 복원 합니다. 

3. 중지 NC 호스트 에이전트 및 모든 Hyper-v 호스트에서 SLB 호스트 에이전트.

    ```
    stop-service slbhostagent

    stop-service nchostagent
    ```

4. RAS 게이트웨이 Vm을 중지 합니다.

5. SLB Mux Vm을 중지 합니다.

6. 사용 하 여 네트워크 컨트롤러를 복원 합니다 `new-networkcontrollerrestore` cmdlet.

7. 복원 확인 **ProvisioningState** 복원이 성공적으로 완료 했습니다 때 알고 있어야 합니다.

8. SCVMM을 사용 하는 경우에 네트워크 컨트롤러 백업으로 동시에 생성 된 백업을 사용 하 여 SCVMM 데이터베이스를 복원 합니다.

9. 워크 로드 Vm 백업에서 복원 하려는 경우 지금 수행 합니다.

10. 디버그 networkcontrollerconfigurationstate cmdlet 사용 하 여 시스템의 상태를 확인 합니다.

```Powershell
$cred = Get-Credential
Debug-NetworkControllerConfigurationState -NetworkController "https://NC.contoso.com" -Credential $cred

Fetching ResourceType:     accessControlLists
Fetching ResourceType:     servers
Fetching ResourceType:     virtualNetworks
Fetching ResourceType:     networkInterfaces
Fetching ResourceType:     virtualGateways
Fetching ResourceType:     loadbalancerMuxes
Fetching ResourceType:     Gateways
```

### <a name="example-restoring-a-network-controller-database"></a>예: 네트워크 컨트롤러 데이터베이스 복원
 
```Powershell
$URI = "https://NC.contoso.com"
$Credential = Get-Credential

$ShareUserResourceId = "BackupUser"
$ShareCredential = Get-NetworkControllerCredential -ConnectionURI $URI -Credential $Credential | Where {$_.ResourceId -eq $ShareUserResourceId }

$RestoreProperties = New-Object Microsoft.Windows.NetworkController.NetworkControllerRestoreProperties
$RestoreProperties.RestorePath = "\\fileshare\backups\NetworkController\2017-04-25T16_53_13"
$RestoreProperties.Credential = $ShareCredential

$RestoreTime = (Get-Date).ToString("s").Replace(":", "_")
New-NetworkControllerRestore -ConnectionURI $URI -Credential $Credential -Properties $RestoreProperties -ResourceId $RestoreTime -Force
```

### <a name="example-checking-the-status-of-a-network-controller-database-restore"></a>예: 네트워크 컨트롤러 데이터베이스 복원 상태를 확인 하는 중

```PowerShell
PS C:\ > get-networkcontrollerrestore -connectionuri $uri -credential $cred -ResourceId $restoreTime | convertto-json -depth 10
{
    "Tags":  null,
    "ResourceRef":  "/networkControllerRestore/2017-04-26T15_04_44",
    "InstanceId":  "22edecc8-a613-48ce-a74f-0418789f04f6",
    "Etag":  "W/\"f14f6b84-80a7-4b73-93b5-59a9c4b5d98e\"",
    "ResourceMetadata":  null,
    "ResourceId":  "2017-04-26T15_04_44",
    "Properties":  {
                    "RestorePath":  "\\\\sa18fs\\sa18n22\\NetworkController\\2017-04-25T16_53_13",
                    "ErrorMessage":  null,
                    "FailedResourcesList":  null,
                    "SuccessfulResourcesList":  null,
                    "ProvisioningState":  "Succeeded",
                    "Credential":  null
                }
}
```


나타날 수 있는 구성 상태 메시지에 대 한 자세한 내용은 [Windows Server 2016 소프트웨어 정의 네트워킹 스택 문제 해결](https://docs.microsoft.com/windows-server/networking/sdn/troubleshoot/troubleshoot-windows-server-software-defined-networking-stack)합니다.