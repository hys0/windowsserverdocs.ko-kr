---
title: Windows Server를 Azure 하이브리드 서비스에 연결
description: Azure 하이브리드 서비스를 사용하여 Windows Server의 온-프레미스 배포를 클라우드로 확장할 수 있습니다.
ms.technology: manage
ms.topic: article
author: jasongerend
ms.author: jgerend
ms.localizationpriority: medium
ms.prod: windows-server
ms.date: 05/31/2019
ms.openlocfilehash: b82d2eaa9283d99993102f1656262e2eda86cfff
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/14/2020
ms.locfileid: "75950122"
---
# <a name="connecting-windows-server-to-azure-hybrid-services"></a>Windows Server를 Azure 하이브리드 서비스에 연결

Azure 하이브리드 서비스를 사용하여 Windows Server의 온-프레미스 배포를 클라우드로 확장할 수 있습니다. 이러한 클라우드 서비스는 온-프레미스를 Azure로 확장하고 Azure에서 중앙 집중식으로 관리하는 데 유용한 함수 배열을 제공합니다.

![온-프레미스에서 클라우드로 진행하여 온-프레미스를 Azure로 확장하는 화살표 및 클라우드에서 온-프레미스로 진행하여 Azure에서 중앙 집중식으로 관리하는 화살표를 보여 주는 다이어그램](../media/azure-services/hybrid-framing.png)

Windows Admin Center 내에서 Azure 하이브리드 서비스를 사용하면 다음을 수행할 수 있습니다.

- [가상 머신을 보호하고, 클라우드 기반 HA/DR(백업 및 재해 복구)을 사용합니다](#back-up-and-protect-your-on-premises-servers-and-vms).  
- [Azure에서 스토리지 및 컴퓨팅을 사용하여 온-프레미스 용량을 확장하고, Azure에 대한 네트워크 연결을 간소화합니다](#extend-on-premises-capacity-with-azure).
- [클라우드 인텔리전트 Azure 관리 서비스를 통해 애플리케이션, 네트워크 및 인프라 전체에서 모니터링, 거버넌스, 구성 및 보안을 중앙 집중화합니다](#centrally-manage-your-hybrid-environment-from-azure).  

앱을 다운로드하고 몇 가지 항목을 수동으로 구성하여 대부분의 Azure 하이브리드 서비스를 설정할 수 있지만, 많은 서비스가 Windows Admin Center에 직접 통합되어 간단한 설정 환경과 서버 중심의 서비스 보기를 제공합니다. 또한 Windows Admin Center는 연결된 Azure 리소스와 중앙 집중식 하이브리드 환경 보기를 볼 수 있도록 Azure Portal에 대한 편리한 인텔리전트 하이퍼링크를 제공합니다.

## <a name="discover-integrated-services-in-the-azure-hybrid-services-tool"></a>Azure 하이브리드 서비스 도구에서 통합 서비스 검색

[Windows Admin Center](../overview.md)의 Azure 하이브리드 서비스 도구는 통합된 모든 Azure 서비스를 중앙 집중식 허브로 통합합니다. 이 중앙 집중식 허브에서 온-프레미스 또는 하이브리드 환경에 가치를 제공하는 사용 가능한 모든 Azure 서비스를 쉽게 검색할 수 있습니다.  

![Azure 하이브리드 서비스 도구를 보여 주는 Windows Admin Center 스크린샷](../media/azure-services/ahs-discover.png)

서버를 이미 활성화된 Azure 서비스에 연결하면 Azure 하이브리드 서비스 도구는 해당 서버에서 활성화된 모든 서비스를 확인할 수 있는 단일 창으로 작동합니다. Windows Admin Center 내에서 관련 도구를 손쉽게 사용하거나, 해당 Azure 서비스를 면밀히 관리하기 위해 Azure Portal을 시작하거나, 간편하게 설명서에서 자세한 내용을 확인할 수 있습니다.  

![서버에 이미 설치되어 있는 Azure 서비스를 보여 주는 Windows Admin Center 스크린샷](../media/azure-services/ahs-dayN.png)

Azure 하이브리드 서비스 도구에서 다음을 수행할 수 있습니다.

- [Azure Backup](azure-backup.md)을 사용하여 Windows Admin Center에서 Windows Server 백업
- [Azure Site Recovery](azure-site-recovery.md)를 사용하여 Windows Admin Center에서 Hyper-V 가상 머신 보호
- [Azure 파일 동기화](azure-file-sync.md)를 사용하여 파일 서버를 클라우드에 동기화
- [Azure 업데이트 관리](azure-update-management.md)를 사용하여 온-프레미스나 클라우드의 모든 Windows 서버에 대한 운영 체제 업데이트 관리
- [Azure Monitor](azure-monitor.md)를 사용하여 온-프레미스나 클라우드의 서버 모니터링 및 경고 구성
- [서버용 Azure Arc](https://docs.microsoft.com/azure/azure-arc/servers/overview)를 사용하여 Azure Policy를 통해 온-프레미스 서버에 거버넌스 정책 적용
- [Azure Security Center](https://docs.microsoft.com/azure/security-center/windows-admin-center-integration)를 사용하여 서버 보호 및 고급 위협 방지
- [Azure 네트워크 어댑터](https://aka.ms/WACNetworkAdapter)를 사용하여 온-프레미스 서버를 Azure Virtual Network에 연결
- [Azure 확장 네트워크](https://go.microsoft.com/fwlink/?linkid=2109517&clcid=0x409)를 사용하여 Azure VM을 온-프레미스 네트워크처럼 보이도록 설정

## <a name="back-up-and-protect-your-on-premises-servers-and-vms"></a>온-프레미스 서버 및 VM 백업 및 보호

- **[Azure Backup](https://docs.microsoft.com/azure/backup/backup-overview)을 사용하여 Windows 서버 백업**  
Azure에 Windows 서버를 백업하여 우발적이거나 악의적인 삭제, 손상 및 랜섬웨어로부터 보호할 수 있습니다.  
자세한 내용은 [Azure Backup을 사용하여 서버 백업](azure-backup.md)을 참조하세요.

- **[Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview)를 사용하여 Hyper-V 가상 머신 보호**  
재해가 발생하는 경우 업무에 중요한 인프라를 보호할 수 있도록 VM에서 실행되는 워크로드를 복제할 수 있습니다. Windows Admin Center는 Hyper-V 서버 또는 클러스터에서 가상 머신 설치 및 복제 프로세스를 간소화하므로, Azure Site Recovery의 재해 복구 서비스를 통해 환경의 복원력을 쉽게 강화할 수 있습니다.  
자세한 내용은 [Azure Site Recovery 및 Windows Admin Center를 사용하여 VM 보호](azure-site-recovery.md)를 참조하세요.

- **[스토리지 복제본](https://docs.microsoft.com/windows-server/storage/storage-replica/storage-replica-overview)을 사용하여 Azure에서 VM에 동기 또는 비동기 블록 기반 복제 사용**  
스토리지 복제본을 보조 서버 또는 VM에 사용하여 서버 간 수준에서 블록 기반 또는 볼륨 기반 복제를 구성할 수 있습니다. Windows Admin Center를 사용하면 복제 대상에 맞게 Azure VM을 만들 수 있으므로 새 Azure VM에서 스토리지를 적절한 크기로 조정하고 올바르게 구성할 수 있습니다.  
자세한 내용은 [스토리지 복제본을 사용하여 서버 간 복제](https://docs.microsoft.com/windows-server/storage/storage-replica/storage-replica-ui)를 참조하세요.  

## <a name="extend-on-premises-capacity-with-azure"></a>Azure를 사용하여 온-프레미스 용량 확장

### <a name="extend-storage-capacity"></a>스토리지 용량 확장

- **[Azure 파일 동기화](https://aka.ms/afs)를 사용하여 파일 서버를 클라우드와 동기화**  
이 서버의 파일을 Azure 파일 공유와 동기화합니다. 모든 파일을 로컬로 유지하거나 클라우드 계층화를 사용하여 공간을 확보하고, 서버에서 가장 자주 사용되는 파일만 캐시하여 콜드 데이터를 클라우드에 계층화합니다. 클라우드의 데이터를 백업할 수 있으므로 온-프레미스 서버 백업에 대해 걱정할 필요가 없습니다. 또한 다중 사이트 동기화를 통해 여러 서버에서 파일 세트를 동기화할 수 있습니다.
자세한 내용은 [Azure 파일 동기화를 사용하여 파일 서버를 클라우드와 동기화](azure-file-sync.md)를 참조하세요.

- **[스토리지 마이그레이션 서비스](https://docs.microsoft.com/windows-server/storage/storage-migration-service/overview)를 사용하여 Azure에서 스토리지를 VM으로 마이그레이션**  
단계별 도구를 사용하여 Windows 및 Linux 서버에서 데이터를 인벤토리에 추가한 다음, 데이터를 새 Azure VM으로 전송합니다. Windows Admin Center는 원본 서버에서 데이터를 받도록 적절한 크기로 조정되고 올바르게 구성된 작업에 대한 새 Azure VM을 만들 수 있습니다.  
자세한 내용은 [스토리지 마이그레이션 서비스를 사용하여 서버 마이그레이션](https://docs.microsoft.com/windows-server/storage/storage-migration-service/migrate-data)을 참조하세요.

### <a name="extend-compute-capacity"></a>컴퓨팅 용량 확장

- **Windows Admin Center상에서 새 Azure 가상 머신 만들기**  
Windows Admin Center 내의 *모든 연결* 페이지에서 **추가**로 이동하여 **Azure VM** 아래에서 **새로 만들기**를 선택합니다. 이 단계별 만들기 도구 내에서도 Azure VM을 도메인에 조인하고 스토리지를 구성할 수 있습니다.

- **Azure를 활용하여 [클라우드 감시](https://docs.microsoft.com/windows-server/failover-clustering/deploy-cloud-witness)를 통해 장애 조치 클러스터에서 쿼럼 획득**  
2노드 클러스터에서 쿼럼을 획득하기 위해 추가 하드웨어에 투자하는 대신, Azure 스토리지 계정을 사용하여 Azure Stack HCI 클러스터 또는 다른 장애 조치 클러스터의 클러스터 감시 역할을 수행할 수 있습니다.  
자세한 내용은 [장애 조치(failover) 클러스터용 클라우드 감시 배포](https://docs.microsoft.com/windows-server/failover-clustering/deploy-cloud-witness)를 참조하세요.  

### <a name="simplify-network-connectivity-between-your-on-premises-and-azure-networks"></a>온-프레미스 네트워크와 Azure 네트워크 간의 네트워크 연결 간소화

- **[Azure 네트워크 어댑터](https://aka.ms/WACNetworkAdapter)를 사용하여 온-프레미스 서버를 Azure Virtual Network에 연결**  
Windows Admin Center를 사용하면 지점 및 사이트 간 VPN을 온-프레미스 서버에서 Azure 가상 네트워크로 설정하는 작업을 간소화할 수 있습니다.  

- **[Azure 확장 네트워크](https://go.microsoft.com/fwlink/?linkid=2109517&clcid=0x409)를 사용하여 Azure VM을 온-프레미스 네트워크처럼 보이도록 설정**  
Windows Admin Center는 사이트 간 VPN을 설정하고, 온-프레미스 IP 주소를 Azure vNet으로 확장하여 IP 주소에 대한 종속성을 손상시키지 않고도 워크로드를 Azure로 더 쉽게 마이그레이션할 수 있습니다.

## <a name="centrally-manage-your-hybrid-environment-from-azure"></a>Azure에서 중앙 집중식으로 하이브리드 환경 관리

- **[가상 머신용 Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-overview)를 사용하여 환경의 모든 서버 모니터링 및 메일 경고 수신**  
Virtual Machines Insights라고도 하는 Azure Monitor를 사용하여 서버 상태 및 이벤트를 모니터링하고, 메일 경고를 생성하고, 환경의 서버 성능을 통합된 보기에서 확인하고, 지정된 서버에 연결된 앱, 시스템 및 서비스를 시각화할 수 있습니다. 또한 Windows Admin Center는 서버 상태 성능 및 클러스터 상태 이벤트에 대한 기본 이메일 경고를 설정할 수 있습니다.  
자세한 내용은 [Azure Monitor에 서버 연결 및 메일 알림 구성](azure-monitor.md)을 참조하세요.

- **[Azure 업데이트 관리](https://docs.microsoft.com/azure/automation/automation-update-management)를 사용하여 모든 Windows 서버에 대한 운영 체제 업데이트를 중앙에서 관리**  
서버 단위가 아니라, 단일 위치에서 여러 서버 및 VM에 대한 업데이트와 패치를 관리할 수 있습니다. Azure 업데이트 관리를 사용하면 사용 가능한 업데이트의 상태를 신속하게 평가하고 필요한 업데이트 설치를 예약하며 배포 결과를 검토하여 업데이트가 성공적으로 적용되는지 확인할 수 있습니다. 서버가 Azure VM이든, 다른 클라우드 공급자에서 호스트하든, 온-프레미스에 있든 상관없이 가능합니다.  
자세한 내용은 [Azure 업데이트 관리를 위한 서버 구성](azure-update-management.md)을 참조하세요.

- **[Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro)를 사용하여 보안 상태 향상 및 고급 위협 방지 제공**  
Azure Security Center는 데이터 센터의 보안 상태를 강화하고, 클라우드의 하이브리드 워크로드(Azure에 있는지 여부에 관계없이)와 온-프레미스에 대해 고급 위협 방지를 제공하는 통합 인프라 보안 관리 시스템입니다. Windows Admin Center를 사용하면 서버를 쉽게 설정하고 Azure Security Center에 연결할 수 있습니다.  
자세한 내용은 [Windows Admin Center와 Azure Security Center 통합(미리 보기)](https://docs.microsoft.com/azure/security-center/windows-admin-center-integration)을 참조하세요.  

- **[서버용 Azure Arc](https://docs.microsoft.com/azure/azure-arc/servers/overview) 및 [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview)를 사용하여 하이브리드 환경에서 정책 적용 및 규정 준수 보장**  
Azure에서 온-프레미스 서버를 인벤토리에 추가하고, 구성하고, 관리합니다. Azure Policy를 사용하여 서버를 관리하고, RBAC를 사용하여 액세스를 제어하며, Azure에서 추가 관리 서비스를 사용하도록 설정할 수 있습니다.  

## <a name="clusters-versus-stand-alone-servers-and-vms"></a>클러스터 및 독립 실행형 서버/VM

Azure 하이브리드 서비스는 다음 구성에서 Windows Server와 작동합니다.

- 독립 실행형 물리적 서버 및 VM(가상 머신)
- [Azure Stack HCI](../../../azure-stack-hci/index.md)의 인증을 받은 하이퍼 컨버지드 클러스터를 비롯한 클러스터 및 [WSSD(Windows Server 소프트웨어 정의)](https://www.microsoft.com/cloud-platform/software-defined-datacenter) 프로그램

### <a name="services-for-stand-alone-servers-and-vms"></a>독립 실행형 서버 및 VM용 서비스

다음은 독립 실행형 서버 및 VM에 기능을 제공하는 Azure 서비스의 전체 목록입니다.

- [Azure Backup](azure-backup.md)을 사용하여 Windows Admin Center에서 Windows Server 백업
- [Azure Site Recovery](azure-site-recovery.md)를 사용하여 Windows Admin Center에서 Hyper-V 가상 머신 보호
- [Azure 파일 동기화](azure-file-sync.md)를 사용하여 파일 서버를 클라우드에 동기화
- [Azure 업데이트 관리](azure-update-management.md)를 사용하여 온-프레미스나 클라우드의 모든 Windows 서버에 대한 운영 체제 업데이트 관리
- [Azure Monitor](azure-monitor.md)를 사용하여 온-프레미스나 클라우드의 서버 모니터링 및 경고 구성
- [서버용 Azure Arc](https://docs.microsoft.com/azure/azure-arc/servers/overview)를 사용하여 Azure Policy를 통해 온-프레미스 서버에 거버넌스 정책 적용
- [Azure Security Center](https://docs.microsoft.com/azure/security-center/windows-admin-center-integration)를 사용하여 서버 보호 및 고급 위협 방지
- [Azure 네트워크 어댑터](https://aka.ms/WACNetworkAdapter)를 사용하여 온-프레미스 서버를 Azure Virtual Network에 연결
- [Azure 확장 네트워크](https://go.microsoft.com/fwlink/?linkid=2109517&clcid=0x409)를 사용하여 Azure VM을 온-프레미스 네트워크처럼 보이도록 설정

### <a name="services-for-clusters"></a>클러스터용 서비스

이러한 서비스는 클러스터 전체에 기능을 제공하는 Azure 서비스입니다.

- [Azure Monitor를 사용하여 하이퍼 컨버지드 클러스터 모니터링](../../../storage/storage-spaces/configure-azure-monitor.md)
- [Azure Site Recovery를 사용하여 VM 보호](azure-site-recovery.md)
- [클러스터 클라우드 감시 배포](../../../failover-clustering/deploy-cloud-witness.md)  

## <a name="other-azure-integrated-abilities-of-windows-admin-center"></a>Windows Admin Center의 기타 Azure 통합 기능

- **Windows Admin Center에서 [Azure VM 연결 추가](manage-azure-vms.md)**  
Windows Admin Center를 사용하여 온-프레미스 머신뿐만 아니라 Azure VM도 관리할 수 있습니다. Azure VNet에 연결하기 위해 Windows Admin Center 게이트웨이를 구성하면 Windows Admin Center에서 제공하는 일관되고 간소화된 도구를 사용하여 Azure에서 가상 머신을 관리할 수 있습니다.  
자세한 내용은 [Windows Admin Center를 구성하여 Azure에서 VM 관리](manage-azure-vms.md)를 참조하세요.

- **[Azure AD(Azure Active Directory)](https://azure.microsoft.com/services/active-directory/) 인증을 추가하여 Windows Admin Center에 보안 계층 추가**  
사용자가 게이트웨이에 액세스하기 위해 Azure AD(Azure Active Directory) ID를 사용하여 인증하도록 하여 Windows Admin Center에 보안 계층을 추가할 수 있습니다. Azure AD 인증을 사용하면 조건부 액세스 및 다단계 인증과 같은 Azure AD의 보안 기능을 활용할 수도 있습니다.  
자세한 내용은 [Windows Admin Center에 대한 Azure AD 인증 구성](../configure/user-access-control.md#azure-active-directory)을 참조하세요.  

- **Windows Admin Center에 포함된 [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview)을 통해 Azure 리소스 직접 관리**  
Azure Cloud Shell을 활용하여 Azure 관리 작업에 쉽게 액세스할 수 있는 Bash 또는 PowerShell 환경을 Windows Admin Center 내에 가져옵니다.  
자세한 내용은 [Azure Cloud Shell 개요](https://docs.microsoft.com/azure/cloud-shell/overview)를 참조하세요.


## <a name="see-also"></a>참고 항목

- [Azure에 Windows Admin Center 연결](azure-integration.md)
- [Azure에서 Windows Admin Center 배포](deploy-wac-in-azure.md)
