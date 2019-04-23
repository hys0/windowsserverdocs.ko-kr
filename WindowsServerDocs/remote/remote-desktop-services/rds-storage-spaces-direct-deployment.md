---
title: 2 노드 저장소 공간 다이렉트 SOFS UPD Azure 저장소에 대 한 배포
description: Rds.를 사용 하 여 저장소 공간 다이렉트를 사용 하는 방법 알아보기
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1099f21d-5f07-475a-92dd-ad08bc155da1
author: haley-rowland
ms.author: harowl
ms.date: 07/17/2018
manager: scottman
ms.openlocfilehash: 8af3a389ec726bbb5ebd62db57d9b3a9861ac63f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890964"
---
# <a name="deploy-a-two-node-storage-spaces-direct-scale-out-file-server-for-upd-storage-in-azure"></a>Azure에서 UPD 저장소에 대 한 2 노드 저장소 공간 다이렉트 스케일 아웃 파일 서버 배포

>적용 대상: Windows Server (반기 채널), Windows Server 2016

원격 데스크톱 서비스 (RDS) 사용자 프로필 디스크 (Upd)에 대 한 도메인에 가입 된 파일 서버가 필요합니다. Azure에서 고가용성 도메인에 가입 된 스케일 아웃 파일 서버 (SOFS)를 배포 하려면 Windows Server 2016 저장소 공간 다이렉트를 사용 합니다. Upd 또는 원격 데스크톱 서비스에 잘 알고 아닐 경우 체크 아웃 [원격 데스크톱 서비스를 시작](welcome-to-rds.md)합니다.

> [!NOTE] 
> 방금 게시 한 Microsoft는 [저장소 공간 다이렉트 스케일 아웃 파일 서버를 배포 하는 Azure 템플릿은](https://azure.microsoft.com/documentation/templates/301-storage-spaces-direct/)! 템플릿을 사용 하 여 배포를 만들 수도 있고이 문서의 단계를 사용할 수 있습니다. 

DS 시리즈 Vm 및 프리미엄 저장소 데이터 디스크를 사용 하 여 프로그램 SOFS를 배포 하는 것이 좋습니다 없는 동일한 수와 각 VM에 데이터 디스크의 크기입니다. 최소 두 개의 저장소 계정이 필요 합니다. 

소규모 배포에 대 한 볼륨 2 복사본과 미러된 여기서 클라우드 미러링 모니터가 있는 2 노드 클러스터를 권장 합니다. 데이터 디스크를 추가 하 여 소규모 배포를 확장 합니다. 대규모 배포 (Vm) 노드를 추가 하 여 증가 합니다. 

이러한 지침은 2 노드 배포에 대 한 것입니다. 다음 표에서 비즈니스에 사용자의 수에 대 한 Upd를 저장 해야 디스크 및 VM 크기를 보여 줍니다. 

| 사용자 | 총 (GB) | VM | # 디스크 | 디스크 유형 | 디스크 크기 (GB) | Configuration   |
|-------|------------|----|---------|-----------|----------------|-----------------|
| 10    | 50         | DS1 | 2       | P10       | 128            | 2 x (d s 1 + 2 P10)  |
| 25    | 125        | DS1 | 2       | P10       | 128            | 2 x (d s 1 + 2 P10)  |
| 50    | 250        | DS1 | 2       | P10       | 128            | 2 x (d s 1 + 2 P10)  |
| 100   | 500        | DS1 | 2       | P20       | 512            | 2x(DS1 + 2 P20)  |
| 250   | 1250       | DS1 | 2       | P30       | 1024           | 2 x (d s 1 + 2 P30)  |
| 500   | 2500       | DS2 | 3       | P30       | 1024           | 2x(DS2 + 3 P30)  |
| 1000  | 5000       | DS3 | 5       | P30       | 1024           | 2 x (d s 3 + 5 P30)  |
| 2500  | 12500      | DS4 | 13      | P30       | 1024           | 2 x (DS4 + 13 P30) |
| 5000  | 25000      | 5까지 | 25      | P30       | 1024           | 2 x (5 까지의 + 25 P30) | 

했습니다 ("내 dc" 우리 아래) 도메인 컨트롤러를 만들고 두 개의 노드 Vm ("내 fsn1" 및 "내-fsn2")는 2 노드 저장소 공간 다이렉트 SOFS 되도록 Vm을 구성 하는 다음 단계를 사용 합니다.

1. 만들기는 [Microsoft Azure 구독](https://azure.microsoft.com)합니다.
2. [Azure 포털](https://ms.portal.azure.com)할 수 있습니다.
3. 만들기는 [Azure 저장소 계정](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/#create-a-storage-account) Azure 리소스 관리자에서. 에 새 리소스 그룹을 만들고 다음 구성을 사용 합니다.
   - 배포 모델: Resource Manager
   - 저장소 계정 유형: 일반적인 용도
   - 성능 계층: Premium
   - 복제 옵션: LRS
4. 빠른 시작 템플릿을 사용 하 여 또는 포리스트를 수동으로 배포 하 여 Active Directory 포리스트를 설정 합니다. 
   - Azure 빠른 시작 템플릿을 사용 하 여 배포 합니다.
      - [새 AD 포리스트를 사용 하 여 Azure VM 만들기](https://azure.microsoft.com/documentation/templates/active-directory-new-domain/)
      - [도메인 컨트롤러 2와 새 AD 도메인을 만듭니다](https://azure.microsoft.com/documentation/templates/active-directory-new-domain-ha-2-dc/) (고가용성)에 대 한
   - 수동으로 [포리스트 배포](https://azure.microsoft.com/documentation/articles/active-directory-new-forest-virtual-machine/) 다음 구성을 사용 합니다.
      - 저장소 계정으로 동일한 리소스 그룹에 가상 네트워크를 만듭니다.
      - 권장된 크기: DS2 (도메인 컨트롤러에 더 많은 도메인 개체 호스팅할 경우 크기를 늘리는)
      - 자동으로 생성 된 VNet을 사용 합니다.
      - AD DS를 설치 하는 단계를 수행 합니다.
5. 파일 서버 클러스터 노드를 설정 합니다. 배포 하 여 이렇게 합니다 [Windows Server 2016 저장소 공간 다이렉트 SOFS 클러스터 Azure 템플릿](https://azure.microsoft.com/resources/templates/301-storage-spaces-direct/) 또는 수동으로 배포 하려면 6 ~ 11 단계를 수행 하 여 합니다.
5. 파일 서버 클러스터 노드를 수동으로 설정 합니다.
   1. 첫 번째 노드를 만듭니다. 
      1. Windows Server 2016 이미지를 사용 하 여 새 가상 컴퓨터를 만듭니다. (클릭 **새로 만들기 > 가상 컴퓨터 > Windows Server 2016 합니다.** 선택 **리소스 관리자**, 를 클릭 하 고 **만들기**.)
      2. 기본 구성을 다음과 같이 설정 합니다.
         - -Fsn1 이름: 내
         - SSD VM 디스크 유형
         - 3 단계에서 만든 기존 리소스 그룹을 사용 합니다. 
      3. 크기: DS1, DS2, DS3, DS4, 또는 사용자에 따라 5 까지의 (이러한 지침의 시작 부분에 있는 표 참조) 해야 합니다. Premium을 지 원하는 디스크 선택 되었는지 확인.
      4. 설정: 
         - 저장소 계정: 3 단계에서 만든 저장소 계정을 선택 합니다.
         - 고가용성-새 가용성 집합을 만듭니다. (클릭 **고가용성 > 새로 만들기**, 를 선택한 다음 이름 (예를 들어 s2d 클러스터)를 입력 합니다. 기본값을 사용 하 여 **업데이트 도메인** 및 **도메인 오류**.)
   2. 두 번째 노드를 만듭니다. 다음 변경 내용으로 위의 단계를 반복 합니다.
      - -Fsn2 이름: 내
      - 고가용성-가용성 집합을 선택이 만듭니다.  
6. [데이터 디스크 연결](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-attach-disk-portal/) 사용자에 따라 클러스터 노드 Vm에 (처럼 위의 표에) 필요 합니다. 후 데이터 디스크를 만들고 VM에 연결 된 설정 **호스트 캐싱** 하 **None**합니다.
7. 모든 Vm에 대 한 IP 주소를 설정 **정적**합니다. 
   1. 리소스 그룹에서 VM을 선택 하 고 클릭 한 다음 **네트워크 인터페이스** (아래 **설정을**). 표시 되는 네트워크 인터페이스를 선택 하 고 클릭 한 다음 **IP 구성을**합니다. 나열 된 IP 구성을 선택, 선택 **정적**, 를 클릭 하 고 **저장**합니다.
   2. 도메인 컨트롤러 내-dc (예를 들어) 개인 IP 주소 (10.x.x.x) note 합니다.
8. 내 dc 서버에 클러스터 노드 Vm의 Nic에 기본 DNS 서버 주소를 설정 합니다. VM을 선택한 다음 클릭 **네트워크 인터페이스 > DNS 서버 > 사용자 지정 DNS**합니다. 위에 설명 된 개인 IP 주소를 입력 한 다음 클릭 **저장할**합니다.
9. 만들기는 [Azure 저장소 계정을 클라우드 감시](https://docs.microsoft.com/windows-server/failover-clustering/deploy-cloud-witness)합니다. (링크 된 지침을 사용 하는 경우 중지 됨 "구성 클라우드 미러링 모니터 서버와 장애 조치 클러스터 관리자 GUI"에 도달할 때 해당 단계 아래 작업을 수행 합니다.)
10. 저장소 공간 다이렉트 파일 서버를 설정 합니다. 노드 VM에 연결한 다음 Windows PowerShell cmdlet을 실행 합니다.
   1. 두 개의 파일 서버 클러스터 노드 Vm에 장애 조치 클러스터링 기능 및 파일 서버 기능을 설치 합니다.

      ```powershell
      $nodes = ("my-fsn1", "my-fsn2")
      icm $nodes {Install-WindowsFeature Failover-Clustering -IncludeAllSubFeature -IncludeManagementTools} 
      icm $nodes {Install-WindowsFeature FS-FileServer} 
      ```
   2. 클러스터 노드 Vm을 확인 하 고 2-노드 SOFS 클러스터를 만듭니다.

      ```powershell
      Test-Cluster -node $nodes
      New-Cluster -Name MY-CL1 -Node $nodes –NoStorage –StaticAddress [new address within your addr space]
      ``` 
   3. 클라우드 미러링 모니터 서버를 구성 합니다. 클라우드 미러링 모니터 서버 저장소 계정 이름과 액세스 키를 사용 합니다.

      ```powershell
      Set-ClusterQuorum –CloudWitness –AccountName <StorageAccountName> -AccessKey <StorageAccountAccessKey> 
      ```
   4. 저장소 공간을 직접 사용 하도록 설정 합니다.

      ```powershell
      Enable-ClusterS2D 
      ```
      
   5. 가상 디스크 볼륨을 만듭니다.

      ```powershell
      New-Volume -StoragePoolFriendlyName S2D* -FriendlyName VDisk01 -FileSystem CSVFS_REFS -Size 120GB 
      ```
      SOFS 클러스터에서 클러스터 공유 볼륨에 대 한 정보를 보려면 다음 cmdlet을 실행 합니다.

      ```powershell
      Get-ClusterSharedVolume
      ```
   
   6. 스케일 아웃 파일 서버 (SOFS)를 만듭니다.

      ```powershell
      Add-ClusterScaleOutFileServerRole -Name my-sofs1 -Cluster MY-CL1
      ```

   7. SOFS 클러스터에서 새로운 SMB 파일 공유를 만듭니다.

      ```powershell
      New-Item -Path C:\ClusterStorage\Volume1\Data -ItemType Directory
      New-SmbShare -Name UpdStorage -Path C:\ClusterStorage\Volume1\Data
      ```

이제 공유 &#92;\my-sofs1\UpdStorage UPD 저장소에 사용할 수 있는 경우 있습니다 [UPD를 사용 하도록 설정](https://social.technet.microsoft.com/wiki/contents/articles/15304.installing-and-configuring-user-profile-disks-upd-in-windows-server-2012.aspx) 사용자에 대 한 합니다. 
