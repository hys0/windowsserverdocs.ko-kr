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
ms.openlocfilehash: 063fe828e906cfdb6b787322942272335591d404
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407049"
---
# <a name="connecting-windows-server-to-azure-hybrid-services"></a>Windows Server를 Azure 하이브리드 서비스에 연결

>적용 대상: Windows Server 2019, Windows Server 2016, Windows Server(반기 채널)

Azure 하이브리드 서비스를 사용하여 Windows Server의 온-프레미스 배포를 클라우드로 확장할 수 있습니다. 이러한 클라우드 서비스는 다음을 비롯하여 여러 유용한 기능을 제공합니다.

- Azure Site Recovery를 통해 가상 머신을 보호하고 클라우드 기반 HA/DR(백업 및 재해 복구)을 사용합니다. 
- Azure Monitor의 고급 분석 및 기계 학습을 통해 애플리케이션, 네트워크 및 인프라 전체에서 발생하는 일을 추적합니다. 
- Azure 네트워크 어댑터를 통해 Azure에 네트워크 연결을 간소화합니다.
- Azure 업데이트 관리를 통해 가상 머신을 최신 상태로 유지합니다.

Azure 하이브리드 서비스는 다음 구성에서 Windows Server와 작동합니다.

- 독립 실행형 물리적 서버 및 VM(가상 머신)
- [Azure Stack HCI](https://docs.microsoft.com/azure-stack/operator/azure-stack-hci-overview)의 인증을 받은 하이퍼 컨버지드 클러스터를 비롯한 클러스터 및 [WSSD(Windows Server 소프트웨어 정의)](https://www.microsoft.com/en-us/cloud-platform/software-defined-datacenter) 프로그램

Azure Portal 및 1-2회 다운로드를 통해 대부분의 Azure 하이브리드 서비스를 설치할 수 있는 한편, 대다수의 Azure 하이브리드 서비스는 Windows Admin Center에 바로 통합되어 해당 서비스의 서버 중심 보기와 간소화된 설치 환경을 제공합니다.

## <a name="azure-hybrid-services-tool"></a>Azure 하이브리드 서비스 도구

[Windows Admin Center](../understand/windows-admin-center.md)의 Azure 하이브리드 서비스 도구는 통합된 모든 Azure 서비스를 중앙 집중식 허브로 통합합니다. 이 중앙 집중식 허브에서 온-프레미스 또는 하이브리드 환경에 가치를 제공하는 사용 가능한 모든 Azure 서비스를 쉽게 검색할 수 있습니다. 

![Azure 하이브리드 서비스 도구를 보여 주는 Windows Admin Center 스크린샷](../media/azure-services/ahs-discover.png)

서버를 이미 활성화된 Azure 서비스에 연결하면 Azure 하이브리드 서비스 도구는 해당 서버에서 활성화된 모든 서비스를 확인할 수 있는 단일 창으로 작동합니다. Windows Admin Center 내에서 관련 도구를 손쉽게 사용하거나, 해당 Azure 서비스를 면밀히 관리하기 위해 Azure Portal을 시작하거나, 간편하게 설명서에서 자세한 내용을 확인할 수 있습니다. 

![서버에 이미 설치되어 있는 Azure 서비스를 보여 주는 Windows Admin Center 스크린샷](../media/azure-services/ahs-dayN.png)

Azure 하이브리드 서비스 도구에서 다음을 수행할 수 있습니다.
- [Azure Backup](azure-backup.md)을 사용하여 Windows Admin Center에서 Windows Server 백업
- [Azure Site Recovery](azure-site-recovery.md)를 사용하여 Windows Admin Center에서 Hyper-V 가상 머신 보호
- [Azure 파일 동기화](azure-file-sync.md)를 사용하여 파일 서버를 클라우드에 동기화
- [Azure 업데이트 관리](azure-update-management.md)를 사용하여 온-프레미스나 클라우드의 모든 Windows 서버에 대한 운영 체제 업데이트 관리
- [Azure Monitor](azure-monitor.md)를 사용하여 온-프레미스나 클라우드의 서버 모니터링 및 경고 구성
- [Azure 네트워크 어댑터](https://aka.ms/WACNetworkAdapter)를 사용하여 온-프레미스 서버를 Azure Virtual Network에 연결

## <a name="services-for-stand-alone-servers-and-vms"></a>독립 실행형 서버 및 VM용 서비스

다음은 독립 실행형 서버 및 VM에 기능을 제공하는 Azure 서비스의 전체 목록입니다.

- **(신규) [Azure 파일 동기화](https://aka.ms/afs)를 사용하여 파일 서버와 클라우드 동기화**  
이 서버의 파일을 Azure 파일 공유와 동기화합니다. 모든 파일을 로컬에 보관하거나 클라우드 계층화를 사용하여 가장 자주 사용하는 파일만 서버에 캐시하여 콜드 데이터를 클라우드에 계층화합니다. 클라우드의 데이터를 백업할 수 있으므로 온-프레미스 서버 백업에 대해 걱정할 필요가 없습니다. 또한 다중 사이트 동기화를 통해 여러 서버에서 파일 세트를 동기화할 수 있습니다.

- **[Azure AD(Azure Active Directory)](https://azure.microsoft.com/services/active-directory/) 인증을 추가하여 Windows Admin Center에 보안 계층 추가**  
사용자가 게이트웨이에 액세스하기 위해 Azure AD(Azure Active Directory) ID를 사용하여 인증하도록 하여 Windows Admin Center에 보안 계층을 추가할 수 있습니다. Azure AD 인증을 사용하면 조건부 액세스 및 다단계 인증과 같은 Azure AD의 보안 기능을 활용할 수도 있습니다.  
자세한 내용은 [Windows Admin Center에 대한 Azure AD 인증 구성](../configure/user-access-control.md#azure-active-directory)을 참조하세요.  

- **[Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview)를 사용하여 Hyper-V 가상 머신 보호**  
재해가 발생하는 경우 업무에 중요한 인프라를 보호할 수 있도록 VM에서 실행되는 워크로드를 복제할 수 있습니다. Windows Admin Center는 Hyper-V 서버 또는 클러스터에서 가상 머신 설치 및 복제 프로세스를 간소화하므로, Azure Site Recovery의 재해 복구 서비스를 통해 환경의 복원력을 쉽게 강화할 수 있습니다.  
자세한 내용은 [Azure Site Recovery 및 Windows Admin Center를 사용하여 VM 보호](azure-site-recovery.md)를 참조하세요.

- **[Azure Backup](https://docs.microsoft.com/azure/backup/backup-overview)을 사용하여 Windows 서버 백업**  
Azure에 Windows 서버를 백업하여 우발적이거나 악의적인 삭제, 손상 및 랜섬웨어로부터 보호할 수 있습니다.  
자세한 내용은 [Azure Backup을 사용하여 서버 백업](azure-backup.md)을 참조하세요.

- **[가상 머신용 Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-overview)를 사용하여 환경의 모든 서버 모니터링 및 메일 경고 수신**  
Virtual Machines Insights라고도 하는 Azure Monitor를 사용하여 서버 상태 및 이벤트를 모니터링하고, 메일 경고를 생성하고, 환경의 서버 성능을 통합된 보기에서 확인하고, 지정된 서버에 연결된 앱, 시스템 및 서비스를 시각화할 수 있습니다.  
자세한 내용은 [Azure Monitor에 서버 연결 및 메일 알림 구성](azure-monitor.md)을 참조하세요.

- **[Azure 업데이트 관리](https://docs.microsoft.com/azure/automation/automation-update-management)를 사용하여 모든 Windows 서버에 대한 운영 체제 업데이트를 중앙에서 관리**  
서버 단위가 아니라, 단일 위치에서 여러 서버 및 VM에 대한 업데이트와 패치를 관리할 수 있습니다. Azure 업데이트 관리를 사용하면 사용 가능한 업데이트의 상태를 신속하게 평가하고 필요한 업데이트 설치를 예약하며 배포 결과를 검토하여 업데이트가 성공적으로 적용되는지 확인할 수 있습니다. 서버가 Azure VM이든, 다른 클라우드 공급자에서 호스트하든, 온-프레미스에 있든 상관없이 가능합니다.  
자세한 내용은 [Azure 업데이트 관리를 위한 서버 구성](azure-update-management.md)을 참조하세요.

- **[Azure 네트워크 어댑터](https://aka.ms/WACNetworkAdapter)를 사용하여 온-프레미스 서버를 Azure Virtual Network에 연결**  
Azure 네트워크 어댑터를 온-프레미스 서버에 추가하여 서버를 Azure Virtual Network에 안전하게 연결할 수 있습니다.  
자세한 내용은 [온-프레미스 Windows Server와 Azure Virtual Network 간에 지점 및 사이트 간 VPN 연결 구성](https://aka.ms/WACNetworkAdapter)을 참조하세요.

- **[Windows Admin Center](manage-azure-vms.md)를 사용하여 Azure IaaS 가상 머신 관리**  
Windows Admin Center를 사용하여 온-프레미스 머신뿐만 아니라 Azure VM도 관리할 수 있습니다. Azure VNet에 연결하기 위해 Windows Admin Center 게이트웨이를 구성하면 Windows Admin Center에서 제공하는 일관되고 간소화된 도구를 사용하여 Azure에서 가상 머신을 관리할 수 있습니다. 자세한 내용은 [Windows Admin Center를 구성하여 Azure에서 VM 관리](manage-azure-vms.md)를 참조하세요.

## <a name="services-for-clusters"></a>클러스터용 서비스

다음은 클러스터에 대한 기능을 제공하는 Azure 서비스입니다(일부 서비스는 아직 Windows Admin Center에 통합되지 않음).

- [Azure Monitor를 사용하여 하이퍼 컨버지드 클러스터 모니터링](../../../storage/storage-spaces/configure-azure-monitor.md)
- [Azure Site Recovery를 사용하여 VM 보호](azure-site-recovery.md)
- [클러스터 클라우드 감시 배포](../../../failover-clustering/deploy-cloud-witness.md)

## <a name="see-also"></a>참고 항목

- [Azure에 Windows Admin Center 연결](azure-integration.md)
- [Azure에서 Windows Admin Center 배포](deploy-wac-in-azure.md)