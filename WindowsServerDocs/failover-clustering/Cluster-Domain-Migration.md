---
title: Windows Server 2016/2019에서 도메인 간 클러스터 마이그레이션
ms.prod: windows-server
ms.manager: eldenc
ms.technology: failover-clustering
ms.topic: article
author: johnmarlin-msft
ms.date: 01/18/2019
description: 이 문서에서는 Windows Server 2019 클러스터를 한 도메인에서 다른 도메인으로 이동 하는 방법을 설명 합니다.
ms.localizationpriority: medium
ms.openlocfilehash: 68f49795124dedf0655726853a4d865686f6d697
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71361416"
---
# <a name="failover-cluster-domain-migration"></a>장애 조치 (Failover) 클러스터 도메인 마이그레이션

> 적용 대상: Windows Server 2019, Windows Server 2016

이 항목에서는 Windows Server 장애 조치 (failover) 클러스터를 한 도메인에서 다른 도메인으로 이동 하는 방법을 간략하게 설명 합니다.

## <a name="why-migrate-between-domains"></a>도메인 간에 마이그레이션하는 이유

하나의 doamin에서 다른 클러스터로 클러스터를 마이그레이션하는 데 필요한 몇 가지 시나리오가 있습니다.

- CompanyA을 CompanyB와 병합 하 여 모든 클러스터를 CompanyA 도메인으로 이동 해야 합니다.
- 클러스터는 기본 데이터 센터에 빌드되고 원격 위치로 전달 됩니다.
- 클러스터가 작업 그룹 클러스터로 빌드 되었으므로 이제 도메인에 속해야 합니다.
- 클러스터가 도메인 클러스터로 작성 되었으므로 작업 그룹의 일부 여야 합니다.
- 클러스터가 회사의 한 영역으로 이동 하는 중 이며 다른 하위 도메인입니다.

Microsoft는 기본 응용 프로그램 작업이 지원 되지 않는 경우 한 도메인에서 다른 도메인으로 리소스를 이동 하려고 하는 관리자에 게 지원을 제공 하지 않습니다. 예를 들어 microsoft는 한 도메인에서 다른 도메인으로 Microsoft Exchange 서버를 이동 하려고 시도 하는 관리자에 게 지원을 제공 하지 않습니다.

   > [!WARNING]
   > 클러스터를 이동 하기 전에 클러스터의 모든 공유 저장소에 대 한 전체 백업을 수행 하는 것이 좋습니다.

## <a name="windows-server-2016-and-earlier"></a>Windows Server 2016 및 이전 버전

Windows Server 2016 이전 버전에서는 클러스터 서비스 한 도메인에서 다른 도메인으로 이동 하는 기능이 없습니다.  이는 Active Directory Domain Services에 대 한 종속성이 증가 하 여 생성 된 가상 이름 때문 이었습니다.   

## <a name="options"></a>변수

이러한 이동을 수행 하기 위해 두 가지 옵션이 있습니다.

첫 번째 옵션에는 클러스터를 제거 하 고 새 도메인에서 다시 작성 하는 작업이 포함 됩니다.

![삭제 및 다시 빌드](media/Cross-Domain-Cluster-Migration/Cross-Cluster-Domain-Migration-1.gif)

애니메이션에서 볼 수 있듯이이 옵션은 다음과 같은 단계를 통해 수행 됩니다.

1. 클러스터를 제거 합니다.
2. 노드의 도메인 멤버 자격을 새 도메인으로 변경 합니다.
3. 업데이트 된 도메인에서 클러스터를 새로 만듭니다.  이 경우 모든 리소스를 다시 만들어야 합니다.

두 번째 옵션은 더 파괴적인 것은 아니지만 새 도메인에 새 클러스터를 구축 해야 하므로 추가 하드웨어가 필요 합니다.  클러스터가 새 도메인에 있으면 클러스터 마이그레이션 마법사를 실행 하 여 리소스를 마이그레이션합니다. 데이터를 마이그레이션하지 않습니다. [저장소 마이그레이션 서비스](../storage/storage-migration-service/overview.md)(클러스터 지원이 추가 되 면)와 같은 다른 도구를 사용 하 여 데이터를 마이그레이션해야 합니다.

![빌드 및 마이그레이션](media/Cross-Domain-Cluster-Migration/Cross-Cluster-Domain-Migration-2.gif)

애니메이션에서 볼 수 있듯이이 옵션은 파괴적인 것은 아니지만 다른 하드웨어를 요구 하거나 기존 클러스터의 노드를 제거 하는 것과 동일 합니다.

1. 이전 클러스터를 계속 사용 하면서 새 도메인에 새 clusterin 만듭니다.
2. [클러스터 마이그레이션 마법사](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754481(v=ws.10)) 를 사용 하 여 모든 리소스를 새 클러스터로 마이그레이션합니다. 미리 알림은 데이터를 복사 하지 않으므로 별도로 수행 해야 합니다.
3. 이전 클러스터의 서비스를 해제 하거나 제거 합니다.

두 옵션 모두 새 클러스터에는 모든 [클러스터 인식 응용 프로그램](https://technet.microsoft.com/aa369082(v=vs.90)) 을 설치 하 고, 모든 최신 드라이버를 설치 하 고, 모든 것이 제대로 실행 될 수 있도록 테스트 가능 해야 합니다.  데이터도 이동 해야 하는 경우 시간이 오래 걸리는 프로세스입니다.

## <a name="windows-server-2019"></a>Windows Server 2019

Windows Server 2019에서는 클러스터 간 도메인 마이그레이션 기능이 도입 되었습니다.  이제 위에 나열 된 시나리오를 쉽게 수행할 수 있으며, 다시 작성 해야 하는 것은 더 이상 필요 하지 않습니다.  

한 도메인에서 클러스터를 이동 하는 작업은 간단 하 게 진행 됩니다. 이를 위해 두 개의 새로운 PowerShell commandlets이 있습니다.

**새-ClusterNameAccount** – Active Directory **Remove-clusternameaccount** 에서 클러스터 이름 계정을 만듭니다.-에서 클러스터 이름 계정을 제거 Active Directory

이 작업을 수행 하는 프로세스는 클러스터를 한 도메인에서 작업 그룹으로 변경 하 고 다시 새 도메인으로 변경 하는 것입니다.  클러스터를 제거 하 고 클러스터를 다시 빌드하고 응용 프로그램을 설치 해야 하는 것은 요구 사항이 아닙니다. 예를 들어 다음과 같습니다.

![마이그레이션](media/Cross-Domain-Cluster-Migration/Cross-Cluster-Domain-Migration-3.gif)

## <a name="migrating-a-cluster-to-a-new-domain"></a>클러스터를 새 도메인으로 마이그레이션

다음 단계에서는 클러스터가 Contoso.com 도메인에서 새 Fabrikam.com 도메인으로 이동 됩니다.  클러스터 이름은 *CLUSCLUS* 이 고 *CLUSCLUS*라는 파일 서버 역할이 있습니다.

1. 클러스터의 모든 서버에서 동일한 이름과 암호를 사용 하 여 로컬 관리자 계정을 만듭니다.  서버가 도메인 간에 이동 하는 동안 로그인 해야 할 수 있습니다.
2. CNO (클러스터 이름 개체), VCO (가상 컴퓨터 개체)에 대 한 Active Directory 권한이 있는 도메인 사용자 또는 관리자 계정을 사용 하 여 첫 번째 서버에 로그인 하 고, 클러스터에 액세스 하 고, PowerShell을 엽니다.
3. 모든 클러스터 네트워크 이름 리소스가 오프 라인 상태 인지 확인 하 고 아래 명령을 실행 합니다.  이 명령은 클러스터에 포함 될 수 있는 Active Directory 개체를 제거 합니다.

   ```PowerShell
   Remove-ClusterNameAccount -Cluster CLUSCLUS -DeleteComputerObjects
   ```
4. Active Directory 사용자 및 컴퓨터를 사용 하 여 모든 클러스터 된 이름과 연결 된 CNO 및 VCO 컴퓨터 개체가 제거 되었는지 확인 합니다.

   > [!NOTE]
   > 도메인을 변경 하는 동안 서버를 다시 시작 하는 경우 클러스터 서비스 시작 되지 않도록 클러스터의 모든 서버에서 클러스터 서비스를 중지 하 고 서비스 시작 유형을 수동으로 설정 하는 것이 좋습니다.

   ```PowerShell
   Stop-Service -Name ClusSvc

   Set-Service -Name ClusSvc -StartupType Manual
   ```

5. 서버 도메인 구성원 자격을 작업 그룹으로 변경 하 고, 서버를 다시 시작 하 고, 서버를 새 도메인에 조인 하 고, 다시 시작 합니다.
6. 서버가 새 도메인에 있는 경우 도메인 사용자 또는 개체를 만들 수 있는 권한이 Active Directory 있는 관리자 계정으로 서버에 로그인 하 고, 클러스터에 대 한 액세스 권한이 있으며, PowerShell을 엽니다. 클러스터 서비스를 시작 하 고 다시 자동으로 설정 합니다.

   ```PowerShell
   Start-Service -Name ClusSvc

   Set-Service -Name ClusSvc -StartupType Automatic
   ```
7. 클러스터 이름과 다른 모든 클러스터 네트워크 이름 리소스를 온라인 상태로 전환 합니다.

   ```PowerShell
   Start-ClusterResource -Name "Cluster Name"

   Start-ClusterResource -Name FS-CLUSCLUS
   ```

8. 클러스터를 연결 된 active directory 개체를 사용 하 여 새 도메인의 일부가 되도록 변경 합니다. 이렇게 하려면 명령이 아래에 있고 네트워크 이름 리소스가 온라인 상태 여야 합니다.  이 명령은 Active Directory의 이름 개체를 다시 만듭니다.

   ```PowerShell
   New-ClusterNameAccount -Name CLUSTERNAME -Domain NEWDOMAINNAME.com -UpgradeVCOs
   ```

    참고: 네트워크 이름 (예: 가상 머신만 있는 Hyper-v 클러스터)이 포함 된 추가 그룹이 없는 경우-UpgradeVCOs 매개 변수 스위치가 필요 하지 않습니다.

9. Active Directory 사용자 및 컴퓨터를 사용 하 여 새 도메인을 확인 하 고 연결 된 컴퓨터 개체를 만들었는지 확인 합니다. 해당 하는 경우 그룹의 나머지 리소스를 온라인으로 전환 합니다.

   ```PowerShell
   Start-ClusterGroup -Name "Cluster Group"

   Start-ClusterGroup -Name FS-CLUSCLUS
   ```

## <a name="known-issues"></a>알려진 문제

새 USB 감시 기능을 사용 하는 경우에는 새 도메인에 클러스터를 추가할 수 없습니다.  이는 파일 공유 감시 유형이 인증을 위해 Kerberos를 활용 해야 한다는 것입니다.  클러스터를 도메인에 추가 하기 전에 미러링 모니터 서버를 없음으로 변경 합니다.  완료 되 면 USB 감시를 다시 만듭니다.  표시 되는 오류는 다음과 같습니다.

```
New-ClusternameAccount : Cluster name account cannot be created.  This cluster contains a file share witness with invalid permissions for a cluster of type AdministrativeAccesssPoint ActiveDirectoryAndDns. To proceed, delete the file share witness.  After this you can create the cluster name account and recreate the file share witness.  The new file share witness will be automatically created with valid permissions.
```

