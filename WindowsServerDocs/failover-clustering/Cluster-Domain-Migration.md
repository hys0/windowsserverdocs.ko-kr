---
title: 간 Windows Server 2016/2019에 도메인 클러스터 마이그레이션
ms.prod: windows-server-threshold
ms.manager: eldenc
ms.technology: failover-clustering
ms.topic: article
author: johnmarlin-msft
ms.date: 01/18/2019
description: 이 문서에서는 다른 Windows Server 2019 클러스터 도메인 간 이동에 대해 설명 합니다.
ms.localizationpriority: medium
ms.openlocfilehash: 5d5aaa333d2e20fa25e4738e343f326d63f75c6b
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280218"
---
# <a name="failover-cluster-domain-migration"></a>장애 조치 클러스터 도메인 마이그레이션

> 적용 대상: Windows Server 2019, Windows Server 2016

이 항목에서는 다른 도메인 간에 이동 하는 Windows Server 장애 조치에 대 한 개요를 클러스터를 제공 합니다.

## <a name="why-migrate-between-domains"></a>도메인 간에 마이그레이션하는 이유

다른 하나의 doamin에서 클러스터를 마이그레이션하는 데 필요한 몇 가지 시나리오가 있습니다.

- CompanyA는 CompanyB와 병합 하 고 모든 클러스터 CompanyA 도메인으로 이동 해야 합니다.
- 클러스터 주 데이터 센터에 구축 되며 원격 위치로 배송
- 클러스터 작업 그룹 클러스터로 빌드 했 고 이제 도메인의 일부일 필요
- 클러스터는 도메인 클러스터로 빌드된 및 작업 그룹의 일부가 되도록 이제 필요
- 클러스터를 다른 회사의 한 영역으로 이동 되 고 다른 하위 도메인입니다.

Microsoft는 기본 응용 프로그램 작업에 지원 되는 경우 다른 리소스 도메인 간에 이동 하려고 하는 관리자에 게 지원을 제공 하지 않습니다. 예를 들어, Microsoft는 Microsoft Exchange 서버 도메인 간에 이동 하려고 하는 관리자에 게 지원을 제공 하지 않습니다.

   > [!WARNING]
   > 클러스터를 이동 하기 전에 클러스터의 모든 공유 저장소의 전체 백업을 수행 하는 것이 좋습니다.

## <a name="windows-server-2016-and-earlier"></a>Windows Server 2016 및 이전 버전

Windows Server 2016 및 이전 버전에서는 클러스터 서비스가 다른 도메인 간에 이동 하는 기능이 없었습니다.  Active Directory Domain Services의 가상 이름을 생성에 대 한 증가 종속성으로 인해 발생 합니다.   

## <a name="options"></a>변수

이러한 이동을 위해 두 가지 옵션이 있습니다.

첫 번째 옵션은 클러스터를 제거 하 고 새 도메인에 다시 작성 해야 합니다.

![삭제 및 다시 작성](media/Cross-Domain-Cluster-Migration/Cross-Cluster-Domain-Migration-1.gif)

애니메이션에서 알 수 있듯이,이 옵션은 단계에 따라 삭제 중:

1. 클러스터를 삭제 합니다.
2. 새 도메인에 노드의 도메인 멤버 자격을 변경 합니다.
3. 업데이트 도메인에 새 클러스터를 다시 만듭니다.  이 모든 리소스를 다시 만들지 않아도 해야 합니다.

두 번째 옵션 걸리지 이지만 새 클러스터를 새 도메인에 구축 해야 하는 추가 하드웨어가 필요 합니다.  클러스터를 새 도메인의 리소스를 마이그레이션하려는 클러스터 마이그레이션 마법사를 실행 합니다. 이 데이터를 마이그레이션할 하지-데이터를 마이그레이션하려면와 같은 다른 도구를 사용 해야 하는 참고 [저장소 마이그레이션 서비스](../storage/storage-migration-service/overview.md)(후 클러스터 지원이 추가 되었습니다).

![빌드 및 마이그레이션](media/Cross-Domain-Cluster-Migration/Cross-Cluster-Domain-Migration-2.gif)

애니메이션에서 알 수 있듯이,이 옵션 삭제 되지 않지만 다른 하드웨어 또는 기존 클러스터에서 노드 제거 된 것 보다.

1. 사용 가능한 이전 클러스터를 계속 하면서 새 clusterin 새 도메인을 만듭니다.
2. 사용 된 [클러스터 마이그레이션 마법사](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754481(v=ws.10)) 모든 리소스를 새 클러스터로 마이그레이션하려 합니다. 말하지만이 복사 하지 않습니다 데이터를 셰이핑하거나 별도로 수행 해야 합니다.
3. 서비스 해제 하거나 이전 클러스터를 삭제 합니다.

두 옵션 모두에 새 클러스터를 모두 포함 해야 [클러스터 인식 응용 프로그램](https://technet.microsoft.com/aa369082(v=vs.90)) 모든 최신 드라이버를 설치 하 고 모두를 확인 하는 테스트 가능한 제대로 실행 됩니다.  데이터 이동 해야 하는 경우 시간이 많이 걸리는 프로세스입니다.

## <a name="windows-server-2019"></a>Windows Server 2019

Windows Server 2019 간 클러스터 도메인 마이그레이션 기능이 도입 되었습니다.  이제 위에 나열 된 시나리오를 쉽게 수행할 수 있으며 다시 작성 하는 필요성은 더 이상 필요 합니다.  

도메인 간 클러스터를 이동 하는 것은 간단 프로세스입니다. 이렇게 하려면 새 PowerShell commandlet이 두 가지가 있습니다.

**새 ClusterNameAccount** – Active Directory에 클러스터 이름 계정을 만듭니다 **제거 ClusterNameAccount** – Active Directory에서 클러스터 이름 계정을 제거

이 작업을 수행 하는 프로세스를 작업 그룹 및 새 도메인으로 도메인 간 클러스터를 변경 하기 위해서입니다.  클러스터를 삭제, 클러스터를 다시 구축, 응용 프로그램 등을 설치 해야 요구 사항은 아닙니다. 예를 들어, 다음과 같이 표시 됩니다.

![마이그레이션](media/Cross-Domain-Cluster-Migration/Cross-Cluster-Domain-Migration-3.gif)

## <a name="migrating-a-cluster-to-a-new-domain"></a>새 도메인으로 클러스터 마이그레이션

다음 단계에서는 새 Fabrikam.com 도메인에 클러스터를 Contoso.com 도메인에서 이동 되 고 됩니다.  클러스터 이름은 *CLUSCLUS* 와 라는 파일 서버 역할을 *FS CLUSCLUS*합니다.

1. 동일한 이름 및 클러스터의 모든 서버에서 암호를 사용 하 여 로컬 관리자 계정을 만듭니다.  이 로그인에 서버 도메인 간에 이동 하는 동안 필요할 수 있습니다.
2. Active Directory에 클러스터 이름 개체 (CNO)를 가상 컴퓨터 개체 (VCO) 권한을 가진 도메인 사용자 또는 관리자 계정 사용 하 여 첫 번째 서버에 로그인 하 고 클러스터, PowerShell 열기 액세스할 수 있습니다.
3. 모든 클러스터 네트워크 이름 리소스를 오프 라인 상태 및 실행 확인을 아래 명령을 합니다.  이 명령은 클러스터 수 있는 Active Directory 개체를 제거 합니다.

   ```PowerShell
   Remove-ClusterNameAccount -Cluster CLUSCLUS -DeleteComputerObjects
   ```
4. Active Directory 사용자 및 컴퓨터를 사용 하 여 제거 된 모든 클러스터 된 이름과 연결 된 개체는 VCO는 CNO 컴퓨터를 확인 합니다.

   > [!NOTE]
   > 클러스터의 모든 서버에서 클러스터 서비스를 중지 하 고 도메인을 변경 하는 동안 서버를 다시 시작 하는 경우 클러스터 서비스가 시작 되지 않습니다 있도록 서비스 시작 유형이 수동으로 설정 하는 것이 좋습니다.

   ```PowerShell
   Stop-Service -Name ClusSvc

   Set-Service -Name ClusSvc -StartupType Manual
   ```

5. 작업 그룹에는 서버의 도메인 구성원 자격을 변경, 서버를 다시 시작, 서버에 새 도메인에 가입 및 다시 시작 합니다.
6. 새 도메인에 있는 서버 개체를 만들 권한을 Active Directory에 클러스터에 대 한 액세스 권한이 있는 도메인 사용자 또는 관리자 계정 사용 하 여 서버에 로그인 후 PowerShell을 엽니다. 클러스터 서비스를 시작 하 고 자동으로 다시 설정 합니다.

   ```PowerShell
   Start-Service -Name ClusSvc

   Set-Service -Name ClusSvc -StartupType Automatic
   ```
7. 클러스터 이름 및 다른 모든 클러스터 네트워크 이름 리소스를 온라인 상태로 전환 합니다.

   ```PowerShell
   Start-ClusterResource -Name "Cluster Name"

   Start-ClusterResource -Name FS-CLUSCLUS
   ```

8. 클러스터 연결 된 active directory 개체를 사용 하 여 새 도메인의 일부를 변경 합니다. 이렇게 하려면 아래 명령을 이며 네트워크 이름 리소스는 온라인 상태 여야 합니다.  이 명령을 수행 하는 Active Directory에서 개체 이름을 다시 만드는 것입니다.

   ```PowerShell
   New-ClusterNameAccount -Name CLUSTERNAME -Domain NEWDOMAINNAME.com -UpgradeVCOs
   ```

    참고: 네트워크 이름 (예: 가상 머신만을 사용 하 여 Hyper-v 클러스터)를 사용 하 여 추가 그룹이 없는 경우-UpgradeVCOs 매개 변수 스위치를 필요 하지 않습니다.

9. Active Directory 사용자 및 컴퓨터를 사용 하 여 새 도메인을 검사 하 고 연결 된 컴퓨터 개체 생성 된 확인 합니다. 적이 있으면 그룹을 온라인에서 나머지 리소스를 시킵니다.

   ```PowerShell
   Start-ClusterGroup -Name "Cluster Group"

   Start-ClusterGroup -Name FS-CLUSCLUS
   ```

## <a name="known-issues"></a>알려진 문제

새 USB 감시 기능을 사용 하는 새 도메인에 클러스터를 추가할 수 없습니다.  그 이유는 파일 공유 감시 유형이 인증에 Kerberos를 활용 해야 합니다.  도메인에 클러스터를 추가 하기 전에 none으로 미러링 모니터 서버를 변경 합니다.  완료 되 면 USB 미러링 모니터 서버를 다시 만듭니다.  오류 보면 다음과 같습니다.

```
New-ClusternameAccount : Cluster name account cannot be created.  This cluster contains a file share witness with invalid permissions for a cluster of type AdministrativeAccesssPoint ActiveDirectoryAndDns. To proceed, delete the file share witness.  After this you can create the cluster name account and recreate the file share witness.  The new file share witness will be automatically created with valid permissions.
```

