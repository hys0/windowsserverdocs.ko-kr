---
title: "업데이트, 백업 및 복원 소프트웨어 정의 네트워킹 Infrastructure"
description: "이 항목에서 Windows Server 2016 업데이트, 백업 및 복원 SDN 인프라 방법에 대해 소프트웨어 네트워킹 정의 가이드의 일부입니다."
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: article
ms.assetid: e9a8f2fd-48fe-4a90-9250-f6b32488b7a4
ms.author: grcusanz
author: grcusanz
ms.openlocfilehash: bb7194ec865db980962853b87d68a84a5446269e
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2017
---
# <a name="update-backup-and-restore-software-defined-networking-infrastructure"></a>업데이트, 백업 및 복원 소프트웨어 정의 네트워킹 Infrastructure

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 항목 다음 섹션에 포함 되어 있습니다.

- [SDN 인프라 업데이트](#bkmk_Updating)
- [백업 SDN 인프라](#bkmk_backup)
- [SDN 인프라 백업에서 복원](#bkmk_restore)

## <a name="bkmk_Updating"></a>SDN 인프라 업데이트

업데이트는 모든 소프트웨어가 정의 네트워킹 (SDN)는 시스템 구성 요소 운영 체제에 Windows 업데이트를 설치 하는 프로세스입니다.  여기에 SDN 포함 네트워크 컨트롤러 Vm, 소프트웨어 부하 분산 Mux Vm 및 RAS 게이트웨이 Vm Hyper-v 호스트 사용 하도록 설정 합니다.  것이 설치 된 업데이트 동일한 정확 하 게 설정 하는 모든 이러한 구성 요소 중요 합니다.  System Center 가상 컴퓨터 Manager 사용 하는 경우는 또한 업데이트할 수 있는 최신 업데이트 롤업도으로 좋습니다.

하지만 아래 단계에 설명 된 따라야 보장 작업에 대 한 시간 아래로 최소화 하 고 네트워크 컨트롤러 데이터베이스의 무결성을 표준 방법 중 하나를 사용 하 여 windows 업데이트를 설치 하기 위한 수행할의 각 구성 요소를 업데이트 합니다.

### <a name="step-1-update-the-management-consoles"></a>1 단계: 업데이트 관리 콘솔
네트워크 컨트롤러 Powershell 모듈을 사용 하면 컴퓨터에 필요한 업데이트를 설치 합니다.  어디서 나 RSAT NetworkController 역할이 자동으로 설치 했는지이 포함 됩니다.  이 위치 2 단계에서에서 업데이트는 자체 네트워크 컨트롤러 Vm 포함 되지 않습니다.

### <a name="step-2-update-the-network-controllers"></a>2 단계: 업데이트 네트워크 컨트롤러
네트워크 컨트롤러 VM 각 업데이트 해야 하 고 다음 진행 하기 전에 네트워크 컨트롤러 클러스터에서 완벽 하 게 다시 온라인 업데이트 주기에서 가장 중요 한 단계입니다.

한 네트워크 컨트롤러 VM로 시작 하 고 필요한 업데이트를 모두 설치 합니다.  필요한 경우 VM 다시 시작 합니다.

다음 단계로 진행 하기 전에 네트워크 컨트롤러 VM를 사용 하 여 다운로드 networkcontrollernode 노드 업데이트 된 상태를 확인 하 고 다시 부팅 합니다.  네트워크 컨트롤러 노드 다시 부팅 주기 동안 이동 하 고 다음 다시이 내놓는 아이디어 다시를 때까지 기다립니다.  VM이 다시 부팅 한 후 여전히 위 상태로 전환을 돌아갈 때 몇 분 정도 걸릴 수 있습니다.

#### <a name="example-using-get-networkcontrollernode-to-check-the-status-of-network-controller-nodes"></a>예: 다운로드 networkcontrollernode를 사용 하 여 네트워크 컨트롤러 노드의 상태를 확인 하려면

이 이때는 다운로드-networkcontrollernode에서 내 네트워크 컨트롤러 Vm 중 하나를 실행 한 결과 보여 줍니다.  다른 두 노드 건강 라인일 NCNode1.contoso.com 아래로 임을 표시 됩니다.  때까지 기다려야 상태가 될 때까지 몇 분 정도 노드 변경에 대 한 추가 노드의 업데이트를 계속 하기 전에 위쪽 합니다.

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

위쪽 상태에 있는 모든 네트워크 컨트롤러 노드 후에 수 있는 사용자이 단계를 반복 각 추가 네트워크 컨트롤러 노드에 대 한 합니다.  한 번에 한 각 노드 업데이트를 계속 합니다.

모든 네트워크 컨트롤러 노드 업데이트 되 면 네트워크 컨트롤러 1 시간 내에 내 네트워크 컨트롤러 클러스터에서 실행 microservices를 업데이트 됩니다.  업데이트 networkcontroller cmdlet 사용 하 여 즉시 업데이트를 트리거하 수 있습니다.

#### <a name="example-using-update-networkcontroller-to-force-network-controller-to-update"></a>예: 업데이트 networkcontroller 업데이트 네트워크 컨트롤러를 사용 하 여

이 명령을 업데이트 남아 있는를 설치할 수 없는 경우 업데이트 networkcontroller 결과 보여 줍니다.

```Powershell
PS C:\> update-networkcontroller
NetworkControllerClusterVersion NetworkControllerVersion
------------------------------- ------------------------
10.1.1                          10.1.15
```

### <a name="step-3-update-slb-muxes"></a>3 단계: 업데이트 SLB Muxes

부하 분산 인프라를 계속 사용할 수 있도록 한 번에 한 각 SLB Mux VM에서 업데이트를 설치 합니다.

### <a name="step-4-update-hyper-v-hosts-and-ras-gateways"></a>4 단계: 업데이트 Hyper-v 호스트와 RAS 게이트웨이

테 연결이 끊어지는 없이 마이그레이션 RAS 게이트웨이 Vm 라이브 수 없으므로, 주의 해야 최소화 수 있는 횟수 연결은 수 장애 조치 새로운 RAS 게이트웨이 업데이트 주기 동안 해당 테 하기 위해 합니다.  호스트와 RAS 게이트웨이의 업데이트를 조정 하 여 각 테는만 장애 조치 최대 한 번 합니다.  

시작에 대기 모드에 있는 RAS 게이트웨이 포함 된 호스트 각 호스트 다음이 단계를 따르세요.

1.  실시간 마이그레이션 수 있는 Vm 호스트를 방어 합니다.  RAS 게이트웨이 Vm 호스트에 두어야 합니다.
2.  이 호스트에서 각 게이트웨이 VM에서 업데이트를 설치 합니다.
3.  다시 부팅 하는 VM 게이트웨이 업데이트에 필요한 경우에 다음 VM 다시 부팅 합니다.  
4.  업데이트 된 VM 게이트웨이 포함 된 호스트에 업데이트를 설치 합니다.
5.  업데이트에 필요한 경우 호스트 다시 부팅 합니다.
6.  각 추가 호스트 대기 게이트웨이 포함 된를 반복 합니다.  대기 게이트웨이가 유지 하는 경우 다음에 대 한 모든 나머지 호스트 동일한 단계를 수행 합니다.

## <a name="bkmk_backup"></a>백업 SDN 인프라

네트워크 컨트롤러 데이터베이스를 정기적으로 백업은 장애 되거나 데이터가 손실 발생 하는 경우 비즈니스 연속성 확인 하는 데 중요 합니다.  네트워크 컨트롤러 Vm 백업 해당 쿼럼 여러 네트워크 컨트롤러 노드에서 유지 확인 하지 않는 때문에 충분 하지 않습니다.
요구 사항:
 * SMB 공유 및 읽기/쓰기 권한을 공유 및 파일 시스템을 사용 하 여 자격 증명 합니다.
 * 필요에 따라 네트워크 컨트롤러 GMSA를 제대로 사용 하 여 설치 된 경우에 그룹 관리 서비스 계정 (GMSA)을 사용할 수 있습니다.

백업을 수행 하려면 다음이 단계를 따르세요.

1. Hyper-v를 사용 하 여 각 네트워크 컨트롤러 VM의 복사본을 내보낼 하거나 사용자가 선택한 VM 백업 방법을 사용 하 여 네트워크 컨트롤러 Vm 백업 합니다.  이렇게 하면 전체 빌드 복원 Vm 인프라를 포함 하 여를 다시 수행 되는 경우 암호를 해독 데이터베이스에 필요한 인증서가 표시 됩니다.
2. 시스템 센터 가상 컴퓨터 (SCVMM) 관리자를 사용 하는 경우 SCVMM 서비스를 중지 하 고 백업 네트워크 컨트롤러 및 SCVMM 일치 하지 않게 만들 수 있는이 시간 동안 업데이트가 SCVMM에 수 있도록 SQL Server 통해 백업 합니다.  네트워크 컨트롤러 백업을 완료 될 때까지 SCVMM 서비스를 다시 시작 하지 않습니다.
3. 네트워크 컨트롤러 데이터베이스 networkcontrollerbackup 새로운를 사용 하 여 백업 합니다.

 #### <a name="example-backing-up-the-network-controller-database"></a>예: 데이터베이스를 백업 하는 네트워크 컨트롤러
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

4. Get networkcontrollerbackup를 사용 하 여를 완료 하 고 백업의 성공 여부를 확인 합니다.

 #### <a name="example-checking-the-status-of-a-network-controller-backup-operation"></a>예: 네트워크 컨트롤러 백업 작업의 상태를 확인합니다.

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

5.  SCVMM을 사용 하는 경우 이제 SCVMM 서비스를 시작할 수 있습니다.

## <a name="bkmk_restore"></a>SDN 인프라 백업에서 복원

복원은 필요한 모든 구성 SDN 환경 운영 상태로 돌아갑니다 백업에서 복원 하는 프로세스입니다.  단계 양을 복원할 구성 요소에 따라 약간 다릅니다.

1. 필요한 경우 다시 Hyper-v 호스트 하 고 필요한 저장 공간을 배포 합니다.

2. 필요에 따라 네트워크 컨트롤러 Vm, RAS 게이트웨이 Vm 및 Mux Vm 백업에서 복원 합니다. 

3. 모든 Hyper-v 호스트 NC 호스트 에이전트와 SLB 호스트 에이전트 중지

    ```
    stop-service slbhostagent

    stop-service nchostagent
    ```

4. RAS 게이트웨이 Vm 중지

5. SLB Mux Vm 중지

6. 새 networkcontrollerrestore cmdlet 사용 하 여 네트워크 컨트롤러 복원 합니다.

 #### <a name="example-restoring-a-network-controller-database"></a>네트워크 컨트롤러 데이터베이스를 복원 하는 예:
 
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

7. 복원이 성공적으로 완료 했 알아야 ProvisioningState 복원을 확인 합니다.

 #### <a name="example-checking-the-status-of-a-network-controller-database-restore"></a>예: 네트워크 컨트롤러 데이터베이스 복원의 상태를 확인합니다.

    ```
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

8. SCVMM를 사용 하는 경우 백업을 만든 네트워크 컨트롤러 백업으로 동시에 사용 하 여 SCVMM 데이터베이스를 복원 합니다.

9. 작업 Vm 백업에서 복원 하는 경우에 이제 수행할 수 있습니다.

10. 디버그 networkcontrollerconfigurationstate cmdlet 사용 하 여 컴퓨터의 상태를 확인할 수 있습니다.

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

표시 될 수 있는 구성 상태 메시지에 정보를 참조 하세요. [Windows Server 2016 소프트웨어 정의 네트워킹 스택 해결](https://docs.microsoft.com/windows-server/networking/sdn/troubleshoot/troubleshoot-windows-server-software-defined-networking-stack)합니다.