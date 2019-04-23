---
title: Azure에서 RDS 데이터 센터 지역 중복
description: 여러 데이터 센터를 사용 하 여 모든 지역에서 고가용성을 제공 하는 RDS 배포를 만드는 방법에 알아봅니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 61c36528-cf47-4af0-83c1-a883f79a73a5
author: haley-rowland
ms.author: elizapo
ms.date: 06/14/2017
manager: dongill
ms.openlocfilehash: 7d895b1098c4d8cdf162c77f35209b7308872d60
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849964"
---
# <a name="create-a-geo-redundant-multi-data-center-rds-deployment-for-disaster-recovery"></a>지역 중복, 다중 데이터 센터 재해 복구를 위해 RDS 배포 만들기

>적용 대상: Windows Server (반기 채널), Windows Server 2016

Azure에서 여러 데이터 센터를 활용 하 여 원격 데스크톱 서비스 배포에 대 한 재해 복구를 사용할 수 있습니다. 항상 사용 가능한 표준 RDS 배포와 달리 (에 설명 된 대로 합니다 [원격 데스크톱 서비스 아키텍처](desktop-hosting-logical-architecture.md)), 단일 Azure 지역 (예: 서유럽)에 데이터 센터를 사용 하는, 데이터를 사용 하는 다중 데이터 센터 배포 배포-Azure 데이터 센터의 가용성을 높이기 여러 지리적 위치에 센터를 사용할 수 있지만 여러 지역은 동시에 다운 그럴 가능성은입니다. 지역 중복을 RDS 아키텍처를 배포 하 여 전체 영역의 치명적인 실패 한 경우 장애 조치를 사용할 수 있습니다.

Microsoft Azure 인프라 서비스 및 지역 중복 데스크톱 호스팅 서비스 및 Sal (구독자 액세스 라이선스)을 제공 하는 RDS를 통해 여러 테 넌 트를 활용 하 여 아래 지침을 사용할 수는 [Microsoft 서비스 공급자 라이선스 SPLA (Agreement) 프로그램](https://www.microsoft.com/hosting/licensing/splabenefits.aspx)합니다. 사용 하 여 사용자 고유의 직원에 대 한 지역 중복 호스팅 서비스를 만들려면 다음 단계를 사용할 수도 있습니다 [RDS 사용자 Cal Software Assurance를 통한 권한 확장](https://download.microsoft.com/download/6/B/A/6BA3215A-C8B5-4AD1-AA8E-6C93606A4CFB/Windows_Server_2012_R2_Remote_Desktop_Services_Licensing_Datasheet.pdf)합니다.

## <a name="logical-architecture-for-high-availability---single-and-multiple-regions"></a>고가용성-단일에 대 한 논리적 아키텍처와 여러 지역
다음 이미지는 단일 Azure 지역에서 항상 사용 가능한 배포에 대 한 아키텍처를 보여 줍니다.

![단일 Azure 지역에서 항상 사용 가능한 배포](media/rds-ha-single-region.png)

배포는 세 가지 계층으로 구성 됩니다.

- Azure 서비스-Azure portal 및 Api 및 공용 IP 주소 및 DNS와 같은 공용 네트워킹 서비스를 포함 하 여 Azure 관리 인터페이스입니다.
- 데스크톱 호스팅 서비스-가상 머신, 네트워크, 저장소, Azure 서비스 및 Windows Server 역할 서비스
- Azure Fabric-Hyper-v 역할을 실행 하는 Windows Server 운영 체제 물리적 서버, 저장소 장치, 네트워크 스위치 및 라우터를 가상화 하는 데 사용 합니다. Azure Fabric을 사용 하 여 Vm, 네트워크, 저장소 및 응용 프로그램에서 기본 하드웨어 독립적인 만들 수 있습니다.


반면에 여러 Azure 데이터 센터를 사용 하는 배포에 대 한 아키텍처 다음과 같습니다.

![여러 Azure 지역에는 RDS 배포](media/rds-ha-multi-region.png)

전체 RDS 배포 지역 중복 배포를 만들려면 두 번째 Azure 지역에 복제 됩니다. 이 아키텍처에 한 번에 하나만 RDS 배포를 실행 하는 위치는 활성-수동 모델을 사용 합니다. VNet 대 VNet 연결을 통해 두 환경을 서로 통신할 수 있습니다. RDS 배포는 단일 Active Directory 포리스트/도메인을 기반으로 하 고 두 배포 간에 AD 서버 복제 의미 사용자가 동일한 자격 증명을 사용 하 여 두 배포에 로그인 할 수 있습니다. 사용자 설정 및 사용자 프로필 디스크 (UPD)에 저장 된 데이터는 2 노드 클러스터 저장소 공간 다이렉트 (s2d) 스케일 아웃 파일 서버 (SOFS)에 저장 됩니다. 두 번째 (수동) 지역에서 두 번째 동일한 S2D 클러스터를 배포 및 저장소 복제본은 복제 하는 데 사용자 프로필 활성에서 수동 배포 합니다. Azure Traffic Manager의 지역을 사용 하 여 결국 최종 사용자가 어떤 배포 하는 최종 사용자 관점에서 현재 활성-, 단일 URL을 사용 하 여 배포를 액세스 및 인식 되지를 자동으로 보내기 위해 사용 됩니다.


있습니다 *없습니다* 각 지역에서 항상 사용 가능한 RDS 배포를 만들지만 단일 VM도 다시 시작 되 면 한 지역에서 장애 조치에서 발생 하는 성능에 미치는 영향 연결 장애 조치 발생 가능성이 커집니다.

## <a name="deployment-steps"></a>배포 단계
지리적 중복 다중 데이터 센터 RDS 배포를 만드는 데는 Azure에서 다음 리소스를 만듭니다.

1. 두 리소스 그룹에 두 개의 Azure 지역으로 구분합니다. 예를 들어 RG는 ("리소스 그룹"는 활성 배포가 RG)와 RG B (수동 배포).
2. RG A의 항상 사용 가능한 Active Directory 배포 사용할 수는 [2 개의 도메인 컨트롤러 템플릿 사용 하 여 새 AD 도메인](https://azure.microsoft.com/resources/templates/active-directory-new-domain-ha-2-dc/) 배포를 만듭니다.
3. RG A. 사용에서 항상 사용 가능한 RDS 배포를 [RDS 배포를 기존 active directory를 사용 하 여 팜](https://azure.microsoft.com/resources/templates/rds-deployment-existing-ad/) 기본 RDS 배포를 만들고 다음에 정보에 따라 템플릿을 [원격 데스크톱 서비스-높음 가용성](rds-plan-high-availability.md) 고가용성을 위해 다른 RDS 구성 요소를 구성 합니다.
4. RG B-VNet RG A. 배포 겹치지 않는 주소 공간을 사용 해야
5. A [VNet 대 VNet 연결](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-vnet-vnet-rm-ps) 두 리소스 그룹 간에 합니다.
6. RG B-에서 가용성 집합을 두 개의 AD 가상 컴퓨터가 VM 이름이 RG 1. 배포 설정, Active Directory Domain Services 역할을 설치 및 도메인 cont 수준 올리기 단일 가용성에서 두 개의 Windows Server 2016 Vm의에서 AD Vm에서 서로 다른 지 확인 1 단계에서 만든 도메인에는 롤러 합니다.
7. RG B의 두 번째 항상 사용 가능한 RDS 배포 
   1. 사용 하 여는 [RDS 배포를 기존 active directory를 사용 하 여 팜](https://azure.microsoft.com/resources/templates/rds-deployment-existing-ad/) 템플릿을 다시 이번 다음과 같이 변경 합니다. (서식 파일을 사용자 지정 하려면 갤러리의 선택, 클릭 **Azure에 배포** 차례로 **템플릿 편집**.)
      1. RG B의 VNet에 해당 하는 DNS 서버 개인 IP 주소 공간을 조정 합니다. 
      
         변수에 "dnsServerPrivateIp"를 검색 합니다. RG B의 VNet에 정의 된 주소 공간에 맞게 기본 IP (10.0.0.4) 편집
   
      2. RG A의 배포에서와 충돌 하지 않도록 컴퓨터 이름 편집
      
         Vm을 찾을 합니다 **리소스** 템플릿의 섹션입니다. 변경 된 **computerName** 아래에 있는 필드 **osProfile**합니다. For example, "gateway" can become"gateway **-b**"; "[concat('rdsh-', copyIndex())]" can become "[concat('rdsh-b-', copyIndex())]", and “broker” can become “broker **-b**”.
      
         (변경할 수 있습니다도 Vm의 이름을 수동으로 템플릿을 실행 한 후.)
   2. 위의 3 단계와 같이 정보를 사용 하 여 [원격 데스크톱 서비스-고가용성](rds-plan-high-availability.md) 고가용성을 위해 다른 RDS 구성 요소를 구성 합니다.
8. 저장소 공간 다이렉트 스케일 아웃 파일 서버 저장소 복제본을 사용 하 여 두 배포에서. 사용 하 여는 [PowerShell 스크립트](https://github.com/robotechredmond/301-s2d-sr-dr-md/tree/master/scripts) 배포 하는 [템플릿](https://github.com/robotechredmond/301-s2d-sr-dr-md) 여러 리소스 그룹.

   > [!NOTE]
   > 수동으로 (대신 저장소 PowerShell 스크립트 및 템플릿을 사용 하 여) 프로 비전 할 수 있습니다. 
   >1. 배포를 [2-노드 S2D SOFS](rds-storage-spaces-direct-deployment.md) RG에 사용자 프로필 디스크 (Upd)를 저장 합니다.
   >2. RG B의 두 번째, 동일한 S2D SOFS를 배포 합니다.-각 클러스터에서 동일한 양의 저장소를 사용 해야 합니다.
   >3. 설정할 [비동기 복제를 사용 하 여 저장소 복제본](../../storage/storage-replica/cluster-to-cluster-storage-replication.md) 둘 사이입니다.

### <a name="enable-upds"></a>Upd를 사용 하도록 설정
저장소 복제본 (보조/수동 배포와 관련 됨)을 대상 볼륨 (기본/활성 배포와 관련 됨)을 원본 볼륨에서 데이터를 복제 합니다. 기본적으로 대상 클러스터 나타납니다 **온라인 (액세스 없음)** -저장소 복제본은 대상 볼륨과 해당 드라이브 문자 또는 탑재 지점을 분리 합니다. 즉, 볼륨 탑재 되지 않은 없으므로 실패 파일 공유 경로 제공 하 여 보조 배포에 대 한 Upd를 사용 하도록 설정 합니다. 

복제를 관리 하는 방법에 대 한 자세히 알아보고 싶습니까? 체크 아웃 [클러스터 간 저장소 복제](../../storage/storage-replica/cluster-to-cluster-storage-replication.md)합니다.

두 배포 모두에서 Upd를 사용 하려면 다음을 수행 합니다.

1. 실행 합니다 [집합 RDSessionCollectionConfiguration cmdlet](https://technet.microsoft.com/itpro/powershell/windows/remote-desktop/set-rdsessioncollectionconfiguration) -기본 (활성) 배포에 대 한 사용자 프로필 디스크를 사용할 수 있도록 원본 볼륨 (7 단계에서에서에서 만든 배포 단계)에서 파일 공유에 대 한 경로 제공 합니다.
2. 대상 볼륨을 원본 볼륨 (이 볼륨을 탑재 및 보조 배포를 통해 액세스할 수 있도록) 되도록 저장소 복제 방향을 반대로 지정 합니다. 실행할 수 있습니다 **Set-srpartnership** cmdlet이 작업을 수행 합니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.

   ```powershell
   Set-SRPartnership -NewSourceComputerName "cluster-b-s2d-c" -SourceRGName "cluster-b-s2d-c" -DestinationComputerName "cluster-a-s2d-c" -DestinationRGName "cluster-a-s2d-c"
   ```
3. 보조 (패시브) 배포에서 사용자 프로필 디스크를 사용 하도록 설정 합니다. 1 단계에서 기본 배포에 대해 수행한 것 처럼 동일한 단계를 따르세요.
4. 방향 바꾸기는 저장소 복제본 다시 원래 원본 볼륨이 다시 SR 파트너 관계의 원본 볼륨 및 기본 배포 파일 공유에 액세스할 수 있도록 합니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.

   ```powershell
   Set-SRPartnership -NewSourceComputerName "cluster-a-s2d-c" -SourceRGName "cluster-a-s2d-c" -DestinationComputerName "cluster-b-s2d-c" -DestinationRGName "cluster-b-s2d-c"
   ```


### <a name="azure-traffic-manager"></a>Azure Traffic Manager 

만들기는 [Azure Traffic Manager](/azure/traffic-manager/traffic-manager-overview) 를 프로 파일링 및 선택 되어 있는지 확인 합니다 **우선 순위** 라우팅 메서드. 각 배포의 공용 IP 주소에 두 개의 끝점을 설정 합니다. 아래 **구성**, 프로토콜 (HTTP) 대신 HTTPS 및 포트 (80) 대신 443 변경 합니다. 기록해는 **DNS time-to-live**의 장애 조치 요구에 따라 적절 하 게 설정 합니다. 

Traffic Manager 끝점을 "정상입니다."로 표시 하려면 GET 요청에 대 한 응답으로 200 확인 반환 해야 한다는 note RDS 템플릿에서 생성 된 publicIP 개체 함수는 경로 추록을 추가 하지 않습니다. 최종 사용자가 사용 하 여 Traffic Manager URL을 제공할 수 대신 "/ RDWeb" 예를 들어 추가: ```http://deployment.trafficmanager.net/RDWeb```

우선 순위 라우팅 메서드를 사용 하 여 Azure Traffic Manager를 배포 하 여 최종 사용자가 활성 배포가 작동 하는 동안 수동 배포에 액세스 하지 못하도록 방지할 수 있습니다. 최종 사용자가 액세스할 수동 배포 및 장애 조치에 대 한 저장소 복제 방향을 전환 된 되지 않은 사용자 로그인 중단 시도 되는 배포와 수동 S2D 클러스터에서 파일 공유에 액세스 하지 못한 경우 최종적으로 배포 됩니다 포기 하 고 제공 임시 프로필을 사용자입니다.  

### <a name="deallocate-vms-to-save-resources"></a>리소스를 저장 하는 Vm의 할당을 취소합니다 
두 배포 모두를 구성한 후 필요에 따라 종료 하는 보조 RDS 인프라와 이러한 Vm에서 비용을 절감할 수 RDSH Vm 할당을 취소 합니다. 항상 사용자 계정 및 프로필 동기화를 사용 하도록 설정 하려면 보조/수동 배포에서 실행 중인 S2D SOFS 및 AD 서버 Vm 있어야 합니다.  

장애 조치가 발생 하는 경우에 할당 취소 된 Vm을 시작 해야 합니다. 이 배포 구성에는 장애 조치 시간이 짧아지며 저렴 한 비용의 장점이 있습니다. 치명적인 장애가 발생 하는 활성 배포의 경우 수동 배포를 수동으로 시작 해야 하거나 자동화 스크립트를 오류를 감지 하 여 수동 배포를 자동으로 시작 해야 합니다. 두 경우 모두 걸릴 수 있습니다 실행 되 고 사용자가 로그인에 사용할 수 있는 수동 배포를 가져오는 데 몇 분 서비스에 대 한 가동 중지 시간이 발생 합니다. 이 가동 중지이 시간에 따라 달라 집니다 기간 해당 RDS 인프라 및 RDSH Vm (일반적으로 2 ~ 4 분에는 Vm이 동시에 보다는 순차적으로 시작 되는 경우) 및 (클러스터의 크기에 따라 달라 집니다 수동 클러스터를 온라인 상태로 전환 하는 시간을 시작 하는 데 걸리는 에서 노드당 2 개의 디스크를 사용 하 여 2 노드 클러스터에 대 한 일반적으로 2 ~ 4 분)입니다. 

### <a name="active-directory"></a>Active Directory 
각 배포에서 Active Directory 서버는 동일한 포리스트/도메인 내에서 복제본입니다. Active Directory에 기본 제공 동기화 프로토콜을 4 개의 도메인 컨트롤러의 동기화를 유지 합니다. 그러나 두 배포에서 모든 AD 서버 간에 복제 하는 데 시간이 걸릴 수 있습니다 새 사용자를 AD 서버 하나에 추가 되 면 있도록 몇 가지 지연이 있을 수 있습니다. 따라서 도메인에 추가 된 후 즉시 로그인 하려고 하는 사용자에 게 경고 해야 합니다. 

### <a name="rd-license-server"></a>RD 라이선스 서버 
제공 된 [사용자별 RD CAL](rds-client-access-license.md) 지역 중복 배포에 액세스할 권한이 있는 각 명명 된 사용자에 대 한 합니다. 배포 된 사용자 Cal에 활성 배포가 두 RD 라이선스 서버 간에 균등 하 게 합니다. 그런 다음 수동 배포의 두 RD 라이선스 서버에 이러한 Cal을 중복 되었습니다. Cal을 하나의 배포만 활성화할 수; 연결 된 사용자를 사용 하 여 특정된 시점에 활성 및 수동 배포 간에 중복 된 때문에 사용권 계약을 침해 합니다.  

### <a name="image-management"></a>이미지 관리 
소프트웨어 업데이트 또는 새 응용 프로그램 제공 하기 위해 RDSH 이미지를 업데이트 하는 대로 별도로 두 배포 모두에 대해 일반적인 사용자 환경을 유지 하는 각 배포에 RDSH 컬렉션을 업데이트 해야 합니다. 사용할 수는 [업데이트 RDSH 컬렉션 템플릿](https://azure.microsoft.com/resources/templates/rds-update-rdsh-collection/), 있지만 템플릿을 실행 하려면 수동 배포의 RDS 인프라 및 RDSH Vm를 실행 되어야 합니다. 

## <a name="failover"></a> 장애 조치 

활성-수동 배포의 경우 장애 조치를 사용 하면 보조 배포의 Vm을 시작 해야 합니다. 이 작업은 수동으로 또는 자동화 스크립트를 사용 하 여 수행할 수 있습니다. S2D SOFS의 치명적인 장애 조치의 경우 저장소 복제본 파트너 관계 방향을 변경 하는 원본 볼륨이 대상 볼륨. 예를 들어 다음과 같은 가치를 제공해야 합니다.

   ```powershell
   Set-SRPartnership -NewSourceComputerName "cluster-b-s2d-c" -SourceRGName "cluster-b-s2d-c" -DestinationComputerName "cluster-a-s2d-c" -DestinationRGName "cluster-a-s2d-c"
   ```

자세히 알아볼 수 있습니다 [클러스터 간 저장소 복제](../../storage/storage-replica/cluster-to-cluster-storage-replication.md)합니다.

Azure Traffic Manager는 자동으로 보조 배포 상태가 정상 인지 하 고 기본 배포가 실패 했음을 인식 (RD 게이트웨이 Vm에서 시작 된 RG b에서) 하 고 보조 배포에 사용자 트래픽을 보냅니다. 일관 된 환경을 즐길 해당 원격 리소스에 대해 작업을 계속 하려면 동일한 Traffic Manager URL을 사용할 수 있습니다. Note 클라이언트 DNS 캐시 Azure Traffic Manager 구성에 설정 된 TTL 기간에 대 한 레코드를 업데이트 하지 않습니다.

### <a name="test-failover"></a>테스트 장애 조치(failover)
저장소 복제본 파트너 관계에서 한 번에 하나의 볼륨 (원본) 활성화할 수 있습니다. 이 즉, SR 파트너 관계 방향을 전환 하는 경우, 기본 배포 (RG A) 볼륨 복제의 대상 되며 따라서 숨겨집니다. 따라서 RG에 연결 하는 사용자에 게는 더 이상 RG A의 SOFS에 저장 된 Upd에 대 한 액세스 

사용자가 로그인을 계속 하도록 허용 하는 동안 장애 조치를 테스트 합니다.
1. RG B의 인프라 Vm 및 RDSH Vm 시작
2. SR 파트너 관계 방향을 전환 (클러스터-b-s2d-c가 원본 볼륨 됨).
3. [끝점을 사용 하지 않도록 설정](/azure/traffic-manager/traffic-manager-manage-endpoints#to-disable-an-endpoint) RG에 Azure Traffic Manager 프로필에서 B. 또는 RG에 트래픽을 ATM 하도록 PowerShell 스크립트를 사용 합니다.

   ```powershell
   Disable-AzureRmTrafficManagerEndpoint -Name publicIpA -Type AzureEndpoints -ProfileName MyTrafficManagerProfile -ResourceGroupName RGA -Force
   ```

RG B 활성 기본 배포 되었습니다. 다시 전환 하려면 RG는 기본 배포:

1. SR 파트너 관계 방향을 전환 (클러스터에 s2d c가 원본 볼륨 됨):

   ```powershell
   Set-SRPartnership -NewSourceComputerName "cluster-a-s2d-c" -SourceRGName "cluster-a-s2d-c" -DestinationComputerName "cluster-b-s2d-c" -DestinationRGName "cluster-b-s2d-c"
   ```
2. Azure Traffic Manager 프로필에서 끝점 RG a를 다시 사용 하도록 설정:

   ```powershell
   Enable-AzureRmTrafficManagerEndpoint -Name publicIpA -Type AzureEndpoints -ProfileName MyTrafficManagerProfile -ResourceGroupName RGA 
   ```

## <a name="considerations-for-on-premises-deployments"></a>온-프레미스 배포에 대 한 고려 사항

온-프레미스 배포를 Azure 빠른 시작 템플릿은이 문서의 참조를 사용할 수 없습니다 모든 인프라 역할을 수동으로 구현할 수 있습니다. Azure 사용량 비용 결정 되지 않습니다 온-프레미스 배포에서 빠르게 장애 조치에 대 한 활성-활성 모델을 사용 하는 것이 좋습니다.

Azure Traffic Manager를 사용 하 여 온-프레미스 끝점을 사용 하지만 Azure 구독이 필요 합니다. 또는 최종 사용자에 게 제공 하는 DNS에 대 한 권한을 부여 하기만 하면 기본 배포에 사용자를 지시 하는 CNAME 레코드. 장애 조치의 경우 보조 배포를 리디렉션하는 DNS CNAME 레코드를 수정 합니다. 최종 사용자가 방식으로 사용 하 여 Azure Traffic Manager는 적절 한 배포에는 사용자와 마찬가지로 단일 URL을 사용 합니다. 

온-프레미스-Azure-사이트 간 모델을 만드는 데 관심이 있다면 사용을 고려 [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview)합니다.
