---
title: Windows Server 2016/2019의 도메인 클러스터 마이그레이션 교차
ms.prod: windows-server-threshold
ms.manager: eldenc
ms.technology: failover-clustering
ms.topic: article
author: johnmarlin-msft
ms.date: 01/18/2019
description: 이 문서에서 설명 하는 한 도메인에서 Windows Server 2019 클러스터를 다른 컴퓨터로 이동
ms.localizationpriority: medium
ms.openlocfilehash: bcfd458c94d33820f434cde3313dc069fc42ffd9
ms.sourcegitcommit: 21677706eb85cb1396c1f40bf443146c09ef1b0d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2019
ms.locfileid: "9042037"
---
# 장애 조치 클러스터 도메인 마이그레이션

> 적용 대상: Windows Server 2019, Windows Server 2016

이 항목에서는 다른 도메인 간 클러스터인 경우 이동 Windows Server 장애 조치에 대 한 개요를 제공 합니다.

## 도메인 간에 마이그레이션하는 이유

하나의 doamin에서 다른 클러스터를 마이그레이션하는 필요한 몇 가지 시나리오가 있습니다.

- CompanyA는 CompanyB와 병합 하 고 모든 클러스터 CompanyA 도메인으로 이동 해야 합니다.
- 클러스터는 주 데이터 센터에 기본 제공 되며 원격 위치에 배송
- 클러스터 작업 그룹 클러스터로 빌드된 및 도메인의 일부가 될 해야
- 클러스터는 도메인 클러스터로 빌드된 및 작업 그룹의 일부가 될 해야
- 클러스터를 다른 회사의 한 영역으로 이동 되 고 다른 하위 도메인입니다.

Microsoft 내부 응용 프로그램 작업이 지원 되는 경우 도메인에서 리소스를 다른 컴퓨터로 이동 하려고 하는 관리자에 게 지원을 제공 하지 않습니다. 예를 들어 Microsoft 한 도메인에서 Microsoft Exchange 서버를 다른 컴퓨터로 이동 하려고 하는 관리자에 게 지원을 제공 하지 않습니다.

   > [!WARNING]
   > 클러스터를 이동 하기 전에 클러스터의 모든 공유 저장소의 전체 백업의 수행 하는 것이 좋습니다.

## Windows Server 2016 이전 버전

Windows Server 2016 및 이전 버전에서는 클러스터 서비스 도메인에서 다른 컴퓨터로 이동 하는 기능이 없었습니다.  이것은 Active Directory 도메인 서비스 및 만든 가상 이름에 향상 된 장점을 때문입니다.   

## 옵션

이러한 이동 작업을 수행 하기 위해 두 가지 옵션이 있습니다.

첫 번째 옵션이 클러스터를 삭제 하 고 새 도메인에 다시 작성 해야 합니다.

![삭제 및 다시 빌드](media\Cross-Domain-Cluster-Migration\Cross-Cluster-Domain-Migration-1.gif)

이 옵션은 단계를 따라 파괴적인 애니메이션에서 볼 수 있듯이 되 고 있습니다.

1. 클러스터를 삭제 합니다.
2. 새 도메인에 노드의 도메인 구성원을 변경 합니다.
3. 업데이트 된 도메인에 새 페이지로 클러스터를 다시 만듭니다.  이 모든 리소스를 다시 만들 해야 합니다.

두 번째 옵션 걸리지 이지만 새 도메인에 기본 제공 되어야 하는 새 클러스터는 필요에 따라 추가 하드웨어가 필요 합니다.  클러스터에서 새 도메인을 되 면 리소스를 마이그레이션할 클러스터 마이그레이션 마법사를 실행 합니다. Note 데이터 마이그레이션 하지이- [저장소 마이그레이션 서비스](../storage/storage-migration-service/overview.md)(후 클러스터 지원이 추가 되었습니다)와 같은 데이터를 마이그레이션할 다른 도구를 사용 해야 합니다.

![빌드 및 마이그레이션](media\Cross-Domain-Cluster-Migration\Cross-Cluster-Domain-Migration-2.gif)

애니메이션에서 볼 수 있듯이이 옵션 파괴적인 되지 않지만 다른 하드웨어 또는 기존 클러스터에서 노드 보다 제거 되었습니다.

1. 사용할 수 있는 기존 클러스터 여전히 하면서 새로운 clusterin 새 도메인을 만듭니다.
2. [클러스터 마이그레이션 마법사](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754481(v=ws.10)) 를 사용 하 여 새 클러스터에 모든 리소스를 마이그레이션합니다. 미리 알림,이 복사 하지 않습니다 데이터를 별도로 수행 해야 합니다.
3. 해제 하거나 기존 클러스터를 삭제 합니다.

두 옵션 모두에서 새 클러스터의 모든 [클러스터 인식 응용 프로그램](https://technet.microsoft.com/aa369082(v=vs.90)) 설치 된 드라이버를 모두 최신 정보를 포함 해야 하며 제대로 실행 됩니다 모두 확인 하는 테스트 가능 합니다.  데이터도 이동 해야 할 경우 많은 시간이 소요입니다.

## WindowsServer 2019

Windows Server 2019의 크로스 클러스터 도메인 마이그레이션 기능을 도입 했습니다.  이제 위에 나열 된 시나리오를 쉽게 할 수 하 고 다시 필요 더 이상 필요 합니다.  

도메인 간 클러스터 이동 있듯 프로세스입니다. 이렇게 하려면 두 가지 새로운 PowerShell commandlet이 있습니다.

**새로 만들기-ClusterNameAccount** - **제거 ClusterNameAccount** Active Directory 클러스터 이름 계정을 만듭니다 – Active Directory에서 클러스터 이름 계정 제거

이 작업을 수행 하는 프로세스 새 도메인을 다시 작업 그룹에 도메인 간 클러스터를 변경 하는 것입니다.  필요성을 파괴 클러스터, 클러스터 다시 빌드, 응용 프로그램 설치 등 필요는 없습니다. 예를 들어,이 다음과 같습니다.

![마이그레이션](media\Cross-Domain-Cluster-Migration\Cross-Cluster-Domain-Migration-3.gif)

## 새 도메인에 클러스터 마이그레이션

다음 단계에서는 새 Fabrikam.com 도메인에 클러스터 Contoso.com 도메인에서 이동 됩니다.  클러스터 이름은 *CLUSCLUS* *FS CLUSCLUS*라는 파일 서버 역할을 합니다.

1. 동일한 이름과 클러스터의 모든 서버에서 암호를 사용 하 여 로컬 관리자 계정을 만듭니다.  서버가 도메인 간에 이동 하는 동안 로그인이 필요할 수 있습니다.
2. Active Directory에 클러스터 이름 개체 (CNO), 가상 컴퓨터 개체 (VCO) 권한을 가진 도메인 사용자 또는 관리자 계정 사용 하 여 첫 번째 서버에 로그인 하 고 클러스터를 열고 PowerShell 액세스할 수 있습니다.
3. 모든 클러스터 네트워크 이름 리소스는 오프 라인 상태 및 실행 하는 아래 명령 합니다.  이 명령은 클러스터 할 수 없는 Active Directory 개체 제거 됩니다.

   ```PowerShell
   Remove-ClusterNameAccount -Cluster CLUSCLUS -DeleteComputerObjects
   ```
4. Active Directory 사용자 및 컴퓨터를 사용 하 여 CNO 및 VCO 컴퓨터 관련 된 모든 클러스터 이름 개체 제거 되었습니다.

   > [!NOTE]
   > 모든 서버 클러스터에서 클러스터 서비스를 중지 하 고 도메인을 변경 하는 동안 서버를 다시 시작 될 때 클러스터 서비스가 시작 되지 않도록 서비스 시작 유형을 수동으로 설정 하는 것이 좋습니다.

   ```PowerShell
   Stop-Service -Name ClusSvc

   Set-Service -Name ClusSvc -StartupType Manual
   ```

5. 작업 그룹 서버의 도메인 구성원을 변경, 서버를 다시 시작, 서버 새 도메인에 가입 및 다시 시작 합니다.
6. 새 도메인에 있는 서버에 Active Directory 개체를 만들 수 있는 권한이, 클러스터에 액세스할 수 있는 도메인 사용자 또는 관리자 계정 사용 하 여 서버에 로그인 한 PowerShell을 엽니다. 클러스터 서비스를 시작 하 고 자동으로 다시 설정 합니다.

   ```PowerShell
   Start-Service -Name ClusSvc

   Set-Service -Name ClusSvc -StartupType Automatic
   ```
7. 클러스터 이름 및 다른 모든 클러스터 네트워크 이름 리소스에 생명을 온라인 상태로.

   ```PowerShell
   Start-ClusterResource -Name "Cluster Name"

   Start-ClusterResource -Name FS-CLUSCLUS
   ```

8. 연결 된 active directory 개체를 사용 하 여 새 도메인의 일부가 되도록 클러스터를 변경 합니다. 이 작업을 수행 하려면 다음 명령을 아래 사용 및 네트워크 이름 리소스는 온라인 상태 여야 합니다.  이 명령을 수행 하는 Active Directory에 이름 개체를 다시 만들입니다.

   ```PowerShell
   New-ClusterNameAccount -Name CLUSTERNAME -Domain NEWDOMAINNAME.com -UpgradeVCOs
   ```

    참고: 네트워크 이름 (즉, 가상 컴퓨터만을 사용 하 여 Hyper-v 클러스터)를 사용 하 여 추가 그룹이 있으면-UpgradeVCOs 매개 변수 스위치 필요 하지 않습니다.

9. Active Directory 사용자 및 컴퓨터를 사용 하 여 새 도메인을 확인 하 고 연결 된 컴퓨터 개체 생성 된 있는지 확인 합니다. 있는 피드백 이라면 온라인 그룹에 나머지 리소스를 다음 상태로 만듭니다.

   ```PowerShell
   Start-ClusterGroup -Name "Cluster Group"

   Start-ClusterGroup -Name FS-CLUSCLUS
   ```

## 알려진 문제

새로운 USB 감시 기능을 사용 하는 새 도메인에 클러스터를 추가할 수 없습니다.  그 이유는 파일 공유 감시 형식을 인증에 Kerberos를 이용해 야 합니다.  클러스터를 도메인에 추가 하기 전에 none 감시를 변경 합니다.  완료 되 면 USB 감시를 다시 만듭니다.  나타납니다 오류가입니다.

```
New-ClusternameAccount : Cluster name account cannot be created.  This cluster contains a file share witness with invalid permissions for a cluster of type AdministrativeAccesssPoint ActiveDirectoryAndDns. To proceed, delete the file share witness.  After this you can create the cluster name account and recreate the file share witness.  The new file share witness will be automatically created with valid permissions.
```

