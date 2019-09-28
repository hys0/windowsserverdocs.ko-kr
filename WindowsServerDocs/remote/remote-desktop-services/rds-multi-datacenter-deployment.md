---
title: Azure의 지역 중복 RDS 데이터 센터
description: 여러 데이터 센터를 사용하여 지리적 위치에 걸쳐 고가용성을 제공하는 RDS 배포를 만드는 방법을 알아봅니다.
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 55b96c112dd7f7294ff674ee4675501af4287da4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403954"
---
# <a name="create-a-geo-redundant-multi-data-center-rds-deployment-for-disaster-recovery"></a>재해 복구를 위한 지역 중복 다중 데이터 센터 RDS 배포 만들기

>적용 대상: Windows Server(반기 채널), Windows Server 2019, Windows Server 2016

Azure에서 여러 데이터 센터를 활용하여 원격 데스크톱 서비스 배포에 재해 복구를 사용할 수 있습니다. 단일 Azure 지역(예: 서유럽)에서 데이터 센터를 사용하는 표준 고가용성 RDS 배포([원격 데스크톱 서비스 아키텍처](desktop-hosting-logical-architecture.md)에서 설명)와 달리, 다중 데이터 센터 배포는 여러 지리적 위치에 있는 데이터 센터를 사용하여 배포 가용성이 향상됩니다. 즉, 하나의 Azure 데이터 센터를 사용할 수 없지만 여러 지역에서 동시에 중단될 가능성은 낮습니다. 지역 중복 RDS 아키텍처를 배포하면 전체 지역에서 치명적인 오류가 발생하는 경우에 장애 조치를 사용하도록 설정할 수 있습니다.

아래 지침을 사용하여 [Microsoft SPLA(Service Provider License Agreement) 프로그램](https://www.microsoft.com/hosting/licensing/splabenefits.aspx)을 통해 지역 중복 데스크톱 호스팅 서비스와 SAL(Subscriber Access License)을 여러 테넌트에 제공하는 Microsoft Azure 인프라 서비스 및 RDS를 활용할 수 있습니다. 또한 아래 단계를 사용하여 [Software Assurance를 통한 RDS 사용자 CAL 확장 권한](https://download.microsoft.com/download/6/B/A/6BA3215A-C8B5-4AD1-AA8E-6C93606A4CFB/Windows_Server_2012_R2_Remote_Desktop_Services_Licensing_Datasheet.pdf)으로 사용자 고유의 직원을 위한 지역 중복 호스팅 서비스를 만들 수도 있습니다.

## <a name="logical-architecture-for-high-availability---single-and-multiple-regions"></a>고가용성에 대한 논리적 아키텍처 - 단일 및 다중 지역
다음 이미지에서는 단일 Azure 지역의 고가용성 배포에 대한 아키텍처를 보여 줍니다.

![단일 Azure 지역의 고가용성 배포](media/rds-ha-single-region.png)

배포는 다음 세 가지 계층으로 구성됩니다.

- Azure 서비스 - Azure Portal 및 API가 포함된 Azure 관리 인터페이스 및 공용 네트워킹 서비스(예: DNS 및 공용 IP 주소 지정)입니다.
- 데스크톱 호스팅 서비스 - 가상 머신, 네트워크, 스토리지, Azure 서비스 및 Windows Server 역할 서비스입니다.
- Azure 패브릭 - 물리적 서버, 스토리지 장치, 네트워크 스위치 및 라우터를 가상화하는 데 사용되고 Hyper-V 역할을 실행하는 Windows Server 운영 체제입니다. Azure 패브릭을 사용하면 기본 하드웨어와 별개로 VM, 네트워크, 스토리지 및 애플리케이션을 만들 수 있습니다.


이에 비해, 여러 Azure 데이터 센터를 사용하는 배포에 대한 아키텍처는 다음과 같습니다.

![여러 Azure 지역을 사용하는 RDS 배포](media/rds-ha-multi-region.png)

전체 RDS 배포가 두 번째 Azure 지역에 복제되어 지역 중복 배포를 만듭니다. 이 아키텍처에서는 한 번에 하나의 RDS 배포만 실행되는 활동-수동 모델을 사용합니다. 두 환경에서 VNet 간 연결을 통해 서로 통신할 수 있습니다. RDS 배포는 단일 Active Directory 포리스트/도메인을 기반으로 하며, AD 서버가 두 배포 간에 복제되어 사용자는 동일한 자격 증명을 사용하여 두 배포 중 하나에 로그인할 수 있습니다. UPD(사용자 프로필 디스크)에 저장된 사용자 설정과 데이터는 2노드 클러스터 스토리지 공간 다이렉트 SOFS(스케일 아웃 파일 서버)에 저장됩니다. 두 번째 동일한 스토리지 공간 다이렉트 클러스터가 두 번째(수동) 지역에 배포되며, 스토리지 복제본이 사용자 프로필을 활성 배포에서 수동 배포로 복제하는 데 사용됩니다. Azure Traffic Manager는 최종 사용자를 현재 활성 상태인 배포로 자동으로 보내는 데 사용됩니다. 최종 사용자 관점에서 최종 사용자는 단일 URL을 사용하여 배포에 액세스하며 최종적으로 사용하는 지역을 인식하지 못합니다.


각 지역에서 고가용성 RDS 배포를 *만들 수 있지만*, 단일 VM이 한 지역에서 다시 시작되는 경우에도 장애 조치가 발생하여 관련 성능에 영향을 주는 장애 조치가 발생할 가능성이 높아집니다.

## <a name="deployment-steps"></a>배포 단계
Azure에서 다음과 같은 리소스를 만들어 지역 중복 다중 데이터 센터 RDS 배포를 만듭니다.

1. 두 개의 개별 Azure 지역에 있는 두 개의 리소스 그룹입니다. 예를 들어 RG A(활성 배포, RG는 "리소스 그룹"을 나타냄) 및 RG B(수동 배포)와 같습니다.
2. RG A의 고가용성 Active Directory 배포입니다. [2개의 도메인 컨트롤러가 있는 새 AD 도메인 템플릿](https://azure.microsoft.com/resources/templates/active-directory-new-domain-ha-2-dc/)을 사용하여 배포를 만들 수 있습니다.
3. RG A의 고가용성 RDS 배포입니다. [기존 활성 디렉터리를 사용하여 RDS 팜 배포](https://azure.microsoft.com/resources/templates/rds-deployment-existing-ad/) 템플릿을 사용하여 기본 RDS 배포를 만든 다음, [원격 데스크톱 서비스 - 고가용성](rds-plan-high-availability.md)의 정보에 따라 다른 RDS 구성 요소를 고가용성으로 구성합니다.
4. RG B의 VNet - RG A의 배포와 겹치지 않는 주소 공간을 사용해야 합니다.
5. 두 리소스 그룹 간의 [VNet 간 연결](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-vnet-vnet-rm-ps)입니다.
6. RG B의 가용성 집합에 있는 두 개의 AD 가상 머신 - VM 이름이 RG A의 AD VM과 달라야 합니다. 두 개의 Windows Server 2016 VM을 단일 가용성 집합에 배포하고, Active Directory Domain Services 역할을 설치한 다음, 1단계에서 만든 도메인의 도메인 컨트롤러로 승격시킵니다.
7. RG B의 두 번째 고가용성 RDS 배포입니다. 
   1. [기존 활성 디렉터리를 사용하여 RDS 팜 배포](https://azure.microsoft.com/resources/templates/rds-deployment-existing-ad/) 템플릿을 다시 사용하지만, 이번에는 다음과 같이 변경합니다. (템플릿을 사용자 지정하려면 갤러리에서 해당 템플릿을 선택하고, **Azure에 배포**를 클릭한 다음, **템플릿 편집**을 클릭합니다.)
      1. DNS 서버 개인 IP의 주소 공간을 RG B의 VNet과 일치하도록 조정합니다. 
      
         변수에서 "dnsServerPrivateIp"를 검색합니다. 기본 IP(10.0.0.4)를 편집하여 RG B의 VNet에 정의된 주소 공간과 일치시킵니다.
   
      2. RG A의 배포 이름과 충돌하지 않도록 컴퓨터 이름을 편집합니다.
      
         템플릿의 **리소스** 섹션에서 VM을 찾습니다. **osProfile** 아래의 **computerName** 필드를 변경합니다. 예를 들어 "gateway"는 "gateway **-b**", "[concat('rdsh-', copyIndex())]"는 "[concat('rdsh-b-', copyIndex())]", "broker"는 "broker **-b**"가 될 수 있습니다.
      
         (템플릿을 실행한 후에 VM 이름을 수동으로 변경할 수도 있습니다.)
   2. 위의 3단계에서와 마찬가지로, [원격 데스크톱 서비스 - 고가용성](rds-plan-high-availability.md)의 정보를 사용하여 다른 RDS 구성 요소를 고가용성으로 구성합니다.
8. 두 배포에 걸쳐 스토리지 복제본이 있는 스토리지 공간 다이렉트 스케일 아웃 파일 서버입니다. [PowerShell 스크립트](https://github.com/robotechredmond/301-s2d-sr-dr-md/tree/master/scripts)를 사용하여 [템플릿](https://github.com/robotechredmond/301-s2d-sr-dr-md)을 리소스 그룹에 배포합니다.

   > [!NOTE]
   > 스토리지는 PowerShell 스크립트 및 템플릿을 사용하는 대신 다음과 같이 수동으로 프로비저닝할 수 있습니다. 
   >1. [2노드 스토리지 공간 다이렉트 SOFS](rds-storage-spaces-direct-deployment.md)를 RG A에 배포하여 UPD(사용자 프로필 디스크)를 저장합니다.
   >2. 두 번째 동일한 스토리지 공간 다이렉트 SOFS를 RG B에 배포합니다. 각 클러스터에서 동일한 양의 스토리지를 사용해야 합니다.
   >3. 둘 사이의 [비동기 복제를 사용하여 스토리지 복제본을 설정](../../storage/storage-replica/cluster-to-cluster-storage-replication.md)합니다.

### <a name="enable-upds"></a>UPD 사용
스토리지 복제본은 데이터를 원본 볼륨(기본/활성 배포와 연결됨)에서 대상 볼륨(보조/수동 배포와 연결됨)으로 복제합니다. 의도적으로 대상 클러스터는 **온라인(액세스 못함)** 으로 표시됩니다. 스토리지 복제본에서 대상 볼륨과 해당 드라이브 문자 또는 탑재 지점을 분리합니다. 즉, 볼륨이 탑재되지 않으므로 파일 공유 경로를 제공하여 보조 배포에 UPD를 사용하도록 설정하는 작업이 실패합니다. 

복제 관리에 대해 자세히 알고 싶은가요? [클러스터 간 스토리지 복제](../../storage/storage-replica/cluster-to-cluster-storage-replication.md)를 확인하세요.

두 배포 모두에서 UPD를 사용하도록 설정하려면 다음을 수행합니다.

1. [Set-RDSessionCollectionConfiguration cmdlet](https://docs.microsoft.com/powershell/module/remotedesktop/set-rdsessioncollectionconfiguration)을 실행하여 기본(활성) 배포용 사용자 프로필 디스크를 사용하도록 설정합니다. 배포 단계의 7단계에서 만든 원본 볼륨의 파일 공유에 대한 경로를 제공합니다.
2. 대상 볼륨이 원본 볼륨이 되도록 스토리지 복제본 방향을 반대로 지정합니다(이 경우 볼륨이 탑재되고 보조 배포에서 액세스할 수 있습니다). 이렇게 하려면 **Set-SRPartnership** cmdlet을 실행할 수 있습니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.

   ```powershell
   Set-SRPartnership -NewSourceComputerName "cluster-b-s2d-c" -SourceRGName "cluster-b-s2d-c" -DestinationComputerName "cluster-a-s2d-c" -DestinationRGName "cluster-a-s2d-c"
   ```
3. 보조(수동) 배포에서 사용자 프로필 디스크를 사용하도록 설정합니다. 1단계에서 기본 배포에 수행한 것과 동일한 단계를 사용합니다.
4. 스토리지 복제본 방향을 반대로 다시 지정하면 원래 원본 볼륨이 다시 SR 파트너 관계의 원본 볼륨이 되고 기본 배포에서 파일 공유에 액세스할 수 있습니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.

   ```powershell
   Set-SRPartnership -NewSourceComputerName "cluster-a-s2d-c" -SourceRGName "cluster-a-s2d-c" -DestinationComputerName "cluster-b-s2d-c" -DestinationRGName "cluster-b-s2d-c"
   ```


### <a name="azure-traffic-manager"></a>Azure Traffic Manager 

[Azure Traffic Manager](/azure/traffic-manager/traffic-manager-overview) 프로필을 만들고, **우선 순위** 라우팅 방법을 선택해야 합니다. 두 엔드포인트를 각 배포의 공용 IP 주소로 설정합니다. **구성** 아래에서 프로토콜을 HTTP 대신 HTTPS로 변경하고, 포트를 443(80 대신)으로 변경합니다. **DNS TTL(Time To Live)** 을 적어두고, 장애 조치 요구 사항에 맞게 적절히 설정합니다. 

Traffic Manager가 "정상"으로 표시되려면 엔드포인트에서 GET 요청에 응답하여 200 OK를 반환해야 합니다. RDS 템플릿에서 만든 publicIP 개체가 작동하지만 경로 추록을 추가하지 않습니다. 대신 최종 사용자에게 "/RDWeb"이 추가된 Traffic Manager URL(예: ```http://deployment.trafficmanager.net/RDWeb```)을 제공할 수 있습니다.

우선 순위 라우팅 방법을 사용하여 Azure Traffic Manager를 배포하면 활성 배포가 작동하는 동안 최종 사용자가 수동 배포에 액세스하지 못하게 됩니다. 최종 사용자가 수동 배포에 액세스하고 스토리지 복제본 방향이 장애 조치로 전환되지 않은 경우, 배포가 수동 스토리지 공간 다이렉트 클러스터의 파일 공유에 액세스하려고 시도하고 실패할 때 사용자 로그인이 중지됩니다. 결국에는 배포를 포기하고 사용자에게 임시 프로필을 제공합니다.  

### <a name="deallocate-vms-to-save-resources"></a>VM을 할당 취소하여 리소스 절약 
두 가지 배포가 모두 구성되면 필요에 따라 보조 RDS 인프라 및 RDSH VM을 종료하고 할당을 취소하여 이러한 VM에 대한 비용을 절감할 수 있습니다. 사용자 계정 및 프로필 동기화를 사용하도록 설정하려면 스토리지 공간 다이렉트 SOFS 및 AD 서버 VM이 항상 보조/수동 배포에서 실행 상태를 유지해야 합니다.  

장애 조치가 발생하면 할당 취소된 VM을 시작해야 합니다. 이 배포 구성은 비용이 적게 들지만 장애 조치 시간을 희생하는 장점이 있습니다. 활성 배포에서 치명적인 오류가 발생하면 수동 배포를 수동으로 시작해야 하거나, 오류를 감지하여 수동 배포를 자동으로 시작하는 자동화 스크립트가 필요합니다. 두 경우 모두 수동 배포를 실행하고 사용자가 로그인할 수 있게 하는 데 몇 분이 걸릴 수 있으며, 이로 인해 서비스에 대한 약간의 가동 중지 시간이 발생할 수 있습니다. 이 가동 중지 시간은 RDS 인프라 및 RDSH VM을 시작하는 데 걸리는 시간(VM이 순차적으로가 아니라 동시에 시작하는 경우 일반적으로 2-4분)과 수동 클러스터를 온라인 상태로 전환하는 데 걸리는 시간(클러스터 크기에 따라 다르며, 노드당 두 개의 디스크가 있는 2노드 클러스터의 경우 일반적으로 2-4분)에 따라 달라집니다. 

### <a name="active-directory"></a>Active Directory 
각 배포의 Active Directory 서버는 동일한 포리스트/도메인 내의 복제본입니다. Active Directory에는 네 개의 도메인 컨트롤러를 동기화 상태로 유지하는 기본 제공 동기화 프로토콜이 있습니다. 그러나 새 사용자가 한 AD 서버에 추가되는 경우 두 배포의 모든 AD 서버 간에 복제하는 데 약간의 시간이 걸릴 수 있습니다. 따라서 도메인에 추가되는 직후 로그인하지 않도록 사용자에게 경고해야 합니다. 

### <a name="rd-license-server"></a>RD 라이선스 서버 
지역 중복 배포에 액세스할 수 있는 권한이 있는 각 명명된 사용자에게 [사용자 단위 RD CAL](rds-client-access-license.md)을 제공합니다. 활성 배포에서 사용자 단위 CAL을 두 RD 라이선스 서버에 고르게 배포합니다. 그런 다음, 이러한 CAL을 수동 배포의 두 RD 라이선스 서버에 복제합니다. CAL은 활성 배포와 수동 배포 간에 복제되므로 하나의 배포만 지정된 시간에 사용자 연결을 통해 활성화할 수 있습니다. 그렇지 않으면 라이선스 계약을 위반하게 됩니다.  

### <a name="image-management"></a>이미지 관리 
소프트웨어 업데이트 또는 새 애플리케이션을 제공하기 위해 RDSH 이미지를 업데이트할 때 두 배포 모두에서 공통된 사용자 환경을 유지할 수 있도록 각 배포에서 개별적으로 RDSH 컬렉션을 업데이트해야 합니다. [RDSH 컬렉션 업데이트 템플릿](https://azure.microsoft.com/resources/templates/rds-update-rdsh-collection/)을 사용할 수는 있지만, 템플릿을 실행하려면 수동 배포의 RDS 인프라 및 RDSH VM이 실행되어야 합니다. 

## <a name="failover"></a>장애 조치(Failover)

활성-수동 배포의 경우 장애 조치를 수행하려면 보조 배포의 VM을 시작해야 합니다. 이 작업은 수동으로 수행하거나 자동화 스크립트를 사용하여 수행할 수 있습니다. 스토리지 공간 다이렉트 SOFS의 치명적 장애 조치의 경우 대상 볼륨이 원본 볼륨이 되도록 스토리지 복제본 파트너 관계 방향을 변경합니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.

   ```powershell
   Set-SRPartnership -NewSourceComputerName "cluster-b-s2d-c" -SourceRGName "cluster-b-s2d-c" -DestinationComputerName "cluster-a-s2d-c" -DestinationRGName "cluster-a-s2d-c"
   ```

자세한 내용은 [클러스터 간 스토리지 복제](../../storage/storage-replica/cluster-to-cluster-storage-replication.md)에서 확인할 수 있습니다.

Azure Traffic Manager는 기본 배포가 실패했고 보조 배포가 정상(RD 게이트웨이 VM이 RG B에서 시작되었음)임을 자동으로 인식하고 사용자 트래픽을 보조 배포로 보냅니다. 사용자는 동일한 Traffic Manager URL을 사용하여 원격 리소스에 대한 작업을 계속하면서 일관된 환경을 사용할 수 있습니다. 클라이언트 DNS 캐시는 Azure Traffic Manager 구성에 설정된 TTL 기간 동안 레코드를 업데이트하지 않습니다.

### <a name="test-failover"></a>테스트 장애 조치(failover)
스토리지 복제본 파트너 관계에서는 한 번에 하나의 볼륨(원본)만 활성화할 수 있습니다. 즉, SR 파트너 관계 방향을 전환하면 기본 배포(RG A)의 볼륨이 복제 대상이 되어 숨겨집니다. 따라서 RG A에 연결하는 모든 사용자는 더 이상 RG A의 SOFS에 저장된 자신의 UPD에 액세스할 수 없게 됩니다. 

사용자가 계속 로그인할 수 있도록 허용하면서 장애 조치를 테스트하려면 다음을 수행합니다.
1. RG B에서 인프라 VM 및 RDSH VM을 시작합니다.
2. SR 파트너 관계 방향을 전환합니다(cluster-b-s2d-c가 원본 볼륨이 됨).
3. Azure Traffic Manager 프로필에서 RG A의 [엔드포인트를 사용하지 않도록 설정](/azure/traffic-manager/traffic-manager-manage-endpoints#to-disable-an-endpoint)하여 ATM에서 트래픽을 RG B로 보내도록 적용합니다. 또는 PowerShell 스크립트를 사용합니다.

   ```powershell
   Disable-AzureRmTrafficManagerEndpoint -Name publicIpA -Type AzureEndpoints -ProfileName MyTrafficManagerProfile -ResourceGroupName RGA -Force
   ```

이제 RG B가 활성 기본 배포입니다. RG A를 기본 배포로 다시 전환하려면 다음을 수행합니다.

1. SR 파트너 관계 방향을 전환합니다(cluster-a-s2d-c가 원본 볼륨이 됨).

   ```powershell
   Set-SRPartnership -NewSourceComputerName "cluster-a-s2d-c" -SourceRGName "cluster-a-s2d-c" -DestinationComputerName "cluster-b-s2d-c" -DestinationRGName "cluster-b-s2d-c"
   ```
2. Azure Traffic Manager 프로필에서 RG A의 엔드포인트를 다시 사용하도록 설정합니다.

   ```powershell
   Enable-AzureRmTrafficManagerEndpoint -Name publicIpA -Type AzureEndpoints -ProfileName MyTrafficManagerProfile -ResourceGroupName RGA 
   ```

## <a name="considerations-for-on-premises-deployments"></a>온-프레미스 배포에 대한 고려 사항

이 문서에서 참조하는 Azure 빠른 시작 템플릿을 온-프레미스 배포에서 사용할 수는 없지만, 모든 인프라 역할을 수동으로 구현할 수 있습니다. Azure 사용으로 인해 비용이 발생하지 않는 온-프레미스 배포에서는 더 빠른 장애 조치를 위해 활성-활성 모델을 사용하는 것이 좋습니다.

Azure Traffic Manager는 온-프레미스 엔드포인트에서 사용할 수 있지만 Azure 구독이 필요합니다. 또는 최종 사용자에게 제공되는 DNS에 대해 사용자를 기본 배포로 보내는 CNAME 레코드를 제공합니다. 장애 조치의 경우 보조 배포로 리디렉션하도록 DNS CNAME 레코드를 수정합니다. 이렇게 하면 최종 사용자는 Azure Traffic Manager와 마찬가지로 사용자를 적절한 배포로 보내는 단일 URL을 사용합니다. 

온-프레미스 및 Azure 사이트 간 모델을 만드는 데 관심이 있으면 [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview)를 사용하는 것이 좋습니다.
