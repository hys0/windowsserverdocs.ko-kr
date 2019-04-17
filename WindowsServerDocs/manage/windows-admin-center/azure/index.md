---
title: Windows Server 하이브리드 Azure 서비스에 연결
description: Azure 하이브리드 서비스를 사용 하 여 클라우드로 Windows Server의 온-프레미스 배포를 확장할 수 있습니다.
ms.technology: manage
ms.topic: article
author: jasongerend
ms.author: jgerend
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.date: 04/12/2019
ms.openlocfilehash: 625bd4b79d277dfaa81767cd781c2ba1316d637e
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/12/2019
ms.locfileid: "9297027"
---
# Windows Server 하이브리드 Azure 서비스에 연결

>적용 대상: Windows Server 2019, Windows Server 2016

Azure 하이브리드 서비스를 사용 하 여 클라우드로 Windows Server의 온-프레미스 배포를 확장할 수 있습니다. 이러한 클라우드 서비스는 유용한 기능을 포함 하 여 다음 배열을 제공 합니다.

- 가상 컴퓨터를 보호 하 고 Azure Site Recovery로 클라우드 기반 백업 및 재해 복구 (HA/DR)를 사용 합니다. 
- 응용 프로그램, 네트워크 및 고급 분석 및 기계 학습 Azure 모니터에서 사용 하 여 인프라에서 상황을 추적 합니다. 
- Azure 네트워크 어댑터와 함께 Azure 네트워크 연결을 간소화 합니다.
- 가상 컴퓨터는 Azure 업데이트 관리를 사용 하 여 최신 상태로 유지 합니다.

Azure 하이브리드 서비스는 다음과 같은 구성에서 Windows 서버 함께 작동합니다.

- 독립 실행형 물리적 서버와 가상 컴퓨터 (Vm)
- [Azure 스택 HCI](../../../azure-stack-hci/index.md)및 [windows server 소프트웨어 정의 (WSSD)](https://www.microsoft.com/en-us/cloud-platform/software-defined-datacenter) 프로그램에서 인증 하는 하이퍼 수렴 형 클러스터를 포함 하 여 클러스터

Azure portal 및 다운로드 였습니까 아니면 2를 사용 하 여 가장 Azure 하이브리드 서비스를 설정할 수 있는 동안 서비스 서버 중심 뷰와 간소화 된 설치 환경을 제공 하기 위해 Windows Admin Center에 직접 통합 되어 많은 합니다.

## Azure 하이브리드 서비스 도구

모든 사용 가능한 Azure 서비스를 온-프레미스 또는 하이브리드 값을을 쉽게 찾을 수 있는 중앙 집중식된 허브로 모든 통합된 Azure 서비스를 통합 하는 [Windows 관리 센터](../understand/windows-admin-center.md) 에서 Azure 하이브리드 서비스 도구 환경입니다. 

![스크린샷의 Windows Admin Center는 Azure 하이브리드 서비스 도구를 보여 주는](../media/azure-services/ahs-discover.png)

이미 사용 하는 Azure 서비스를 사용 하 여 서버에 연결 하는 경우 Azure 하이브리드 서비스 도구 유리 해당 서버에서 사용된 하는 모든 서비스를 단일 보기 창을 역할도 합니다. 쉽게 Windows Admin Center 내에서 관련 도구에, 손쉽게 해당 Azure 서비스 또는 읽기를 설명서를 사용 하 여 더 많은 깊은 관리에 대 한 Azure 포털에 시작할 수 있습니다. 

![스크린샷의 Windows Admin Center 서버에 이미 설치 된 Azure 서비스를 표시 합니다.](../media/azure-services/ahs-dayN.png)

Azure 하이브리드 서비스 도구에서 다음을 수행할 수 있습니다.
- [Azure Backup](azure-backup.md) 을 사용 하 여 Windows 관리 센터에서 Windows 서버 백업
- [Azure Site Recovery](azure-site-recovery.md) 로 Windows Admin Center에서 Hyper-v 가상 컴퓨터를 보호 합니다.
- [Azure 파일 동기화](azure-file-sync.md) 를 사용 하 여 클라우드와 파일 서버에 동기화
- 모든 Windows 서버에 대 한 운영 체제 업데이트 관리 모두 온-프레미스 또는 클라우드, [Azure 업데이트](azure-update-management.md) 관리
- 모니터링 서버를 모두 온-프레미스 또는 클라우드, [Azure 모니터](azure-monitor.md) 를 사용 하 여 경고를 구성
- 온-프레미스 서버 [Azure 네트워크 어댑터](https://aka.ms/WACNetworkAdapter) 를 사용 하 여 Azure 가상 네트워크에 연결

## 독립 실행형 서버 및 Vm에 대 한 서비스

이 독립 실행형 서버와 Vm에 기능을 제공 하는 Azure 서비스의 전체 목록은:

- **(신규) [Azure 파일 동기화](https://aka.ms/afs) 를 사용 하 여 클라우드와 파일 서버에 동기화**  
Azure 파일 공유를 사용 하 여이 서버에 파일을 동기화 합니다. 모든 파일은 로컬 유지 하거나 사용 하 여 클라우드 계층으로 구성 및 캐시에만 가장 자주 클라우드 콜드 데이터 계층 서버에서 파일을 사용 합니다. 클라우드에서 데이터 온-프레미스 서버 백업에 걱정할 필요가 없도록를 백업할 수 있습니다. 또한 사이트-동기화 수 동기화 된 상태로 유지할 파일 집합의 여러 서버.

- **[Azure Active Directory (Azure AD)](https://azure.microsoft.com/services/active-directory/) 인증을 추가 하 여 보안 계층을 Windows Admin Center를 추가 합니다.**  
사용자가 Azure Active Directory (Azure AD) id를 사용 하 여 게이트웨이 액세스를 인증 하도록 요구 하 여 추가 보안 계층도 Windows Admin Center를 추가할 수 있습니다. 또한 azure AD 인증 조건부 액세스 다단계 인증 등의 Azure AD의 보안 기능을 활용할 수 있습니다.  
자세한 내용은 참조 [Windows Admin Center에 대 한 구성 Azure AD 인증.](../configure/user-access-control.md#azure-active-directory)  

- **[Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) 로 Hyper-v 가상 컴퓨터를 보호 합니다.**  
재해가 발생 하는 경우 업무에 중요 한 인프라를 보호할 Vm에서 실행 되는 워크 로드를 복제할 수 있습니다. Windows Admin Center 환경 Azure Site Recovery 재해 복구 서비스와의 복원 력을 강화을 더욱 쉽게 설정 및 Hyper-v 서버 또는 클러스터에 가상 컴퓨터를 복제 하는 프로세스 간소화 합니다.  
자세한 내용은 [Azure Site Recovery 및 Windows Admin Center를 사용 하 여 Vm 보호](azure-site-recovery.md)를 참조 하세요.

- **[Azure Backup](https://docs.microsoft.com/azure/backup/backup-overview) 을 사용 하 여 Windows server 백업**  
사용자를 악성 또는 실수로 삭제, 손상, 및 랜 섬 웨어 로부터 보호 Azure에 Windows server를 백업할 수 있습니다.  
자세한 내용은 [Azure 백업 사용 하 여 서버를 백업](azure-backup.md)을 참조 하세요.

- **모니터링 하 고 [가상 컴퓨터에 대 한 Azure 모니터](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-overview) 를 사용 하 여 환경에 있는 모든 서버에 대 한 메일 알림 받기**  
서비스에 연결 및 Azure 모니터 라고도 가상 컴퓨터 관련 정보를 사용 하 여 서버 상태 및 이벤트 모니터링, 이메일 알림을 생성, 사용자 환경에 서버 성능은 통합된 된 보기 넘어갈 및 응용 프로그램, 시스템을 시각화 하는 지정 된 서버입니다.  
자세한 내용은 [Azure 모니터에 서버 연결 및 메일 알림 구성](azure-monitor.md)을 참조 하세요.

- **[Azure 업데이트 관리](https://docs.microsoft.com/azure/automation/automation-update-management) 를 사용 하 여 모든 Windows Server에 대 한 운영 체제 업데이트를 중앙에서 관리**  
서버 단위로 아니라 단일 위치에서 업데이트 및 여러 서버 및 Vm에 대 한 패치를 관리할 수 있습니다. Azure 업데이트 관리를 신속 하 게 사용 가능한 업데이트의 상태를 평가, 필요한 업데이트의 설치를 예약 하 고 사용할 수 성공적으로 적용 되는 업데이트를 확인 하려면 배포 결과 검토 합니다. 이 가능한 서버가 Azure Vm에서 다른 클라우드 공급자가 호스트 인지 또는 온-프레미스.  
자세한 내용은 [Azure 업데이트 관리에 대 한 구성 서버](azure-update-management.md)를 참조 하세요.

- **온-프레미스 서버 [Azure 네트워크 어댑터](https://aka.ms/WACNetworkAdapter) 를 사용 하 여 Azure 가상 네트워크에 연결**  
Azure 가상 네트워크에 안전 하 게 서버에 연결 하는 데 온-프레미스 서버에 Azure 네트워크 어댑터를 추가할 수 있습니다.  
자세한 정보는 [온-프레미스 Windows Server 및 Azure 가상 네트워크 사이 지점-사이트 구성 VPN 연결](https://aka.ms/WACNetworkAdapter)을 참조 하세요.

- **[Windows Admin Center](manage-azure-vms.md) 를 사용 하 여 Azure IaaS 가상 컴퓨터 관리**  
온-프레미스 컴퓨터 뿐만 아니라 Azure Vm에 관리를 Windows Admin Center를 사용할 수 있습니다. Azure VNet에 연결 하 여 Windows Admin Center 게이트웨이 구성 하 여 Windows Admin Center를 제공 하는 일관 되 고 간소화 된 도구를 사용 하는 Azure의 가상 컴퓨터를 관리할 수 있습니다. 자세한 내용은 [azure에서 Vm 관리 구성 Windows Admin Center](manage-azure-vms.md)를 참조 하세요.

## 클러스터에 대 한 서비스

전체 클러스터에 기능을 제공 하는 Azure 서비스 (이러한 되지 모두에 통합 된 Windows Admin Center 아직):

- [Azure 모니터를 사용 하 여 하이퍼 수렴 형 클러스터를 모니터링](../../../storage/storage-spaces/configure-azure-monitor.md)
- [Azure Site Recovery로 Vm 보호](azure-site-recovery.md)
- [클러스터 클라우드 감시 배포](../../../failover-clustering/deploy-cloud-witness.md)

## 기타 참조

- [Azure에 Windows Admin Center에 연결](azure-integration.md)
- [Azure에서 Windows Admin Center를 배포 합니다.](deploy-wac-in-azure.md)