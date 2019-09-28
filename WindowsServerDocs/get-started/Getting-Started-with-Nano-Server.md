---
title: Nano 서버 설치
description: Nano Server 새로 설치, 업그레이드, 마이그레이션 및 평가
ms.prod: windows-server
ms.service: na
manager: dougkim
ms.technology: server-nano
ms.date: 09/06/2017
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 2c2fa45b-6f3b-4663-b421-2da6ecc463bf
author: jaimeo
ms.author: jaimeo
ms.localizationpriority: medium
ms.openlocfilehash: d395c72a1e21cd8eda043eebf3b72bbd5c9a13e8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71391796"
---
# <a name="install-nano-server"></a>Nano 서버 설치

>적용 대상: Windows Server 2016

> [!IMPORTANT]
> Windows Server, 버전 1709부터 [컨테이너 기본 OS 이미지](/virtualization/windowscontainers/quick-start/using-insider-container-images#install-base-container-image)로만 Nano 서버를 사용할 수 있습니다. [Nano 서버 변경 사항](nano-in-semi-annual-channel.md)을 확인하여 그 의미를 알아보세요. 

Windows Server 2016은 새로운 설치 옵션인 Nano 서버를 제공합니다. Nano 서버는 프라이빗 클라우드 및 데이터 센터에 최적화된 원격 관리 서버 운영 체제입니다. Server Core 모드의 Windows Server와 유사하지만 훨씬 작고 로컬 로그온 기능이 없으며 64비트 응용 프로그램, 도구 및 에이전트에만 지원합니다. Windows Server보다 훨씬 적은 디스크 공간을 차지하고, 훨씬 빠르게 설치되며, 필요한 업데이트 및 다시 시작 횟수가 훨씬 적습니다. 다시 시작 속도가 훨씬 빠릅니다. Nano 서버 설치 옵션은 Windows Server 2016 Standard 및 Datacenter 버전에 제공됩니다.  

Nano 서버는 다음과 같은 다양한 시나리오에 이상적입니다.  
  
-   클러스터에 있든 그렇지 않든, Hyper-V 가상 컴퓨터의 "컴퓨팅" 호스트  
  
-   스케일 아웃 파일 서버의 스토리지 호스트.  
  
-   DNS 서버  
  
-   IIS(인터넷 정보 서비스)를 실행하는 웹 서버  
  
-   클라우드 응용 프로그램 패턴을 사용하여 개발되어 컨테이너 또는 가상 컴퓨터 게스트 운영 체제에서 실행되는 응용 프로그램의 호스트  
  
## <a name="important-differences-in-nano-server"></a>Nano Server의 중요한 차이점

Nano Server는 컨테이너 및 마이크로서비스를 기반으로 하는 "클라우드-네이티브" 애플리케이션을 실행하기 위한 간단한 운영 체제로 또는 훨씬 더 작은 공간을 차지하는 민첩하고 비용 효과적인 데이터 센터 호스트로 최적화되어 있으므로 Nano Server와 Server Core 또는 데스크톱 환경 포함 Server 설치 간에는 중요한 차이점이 있습니다.

- Nano Server는 "헤드리스" 방식이며, 로컬 로그온 기능 또는 그래픽 사용자 인터페이스가 없습니다.
- 64비트 애플리케이션, 도구 및 에이전트만 지원됩니다.
- Nano Server는 Active Directory 도메인 컨트롤러로 작동할 수 없습니다.
- 그룹 정책은 지원되지 않습니다. 그렇지만 [원하는 상태 구성](https://msdn.microsoft.com/powershell/dsc/nanoDsc)을 사용하여 대규모로 설정을 적용할 수 있습니다.
- Nano 서버는 프록시 서버를 사용하여 인터넷에 액세스하도록 구성할 수 없습니다.
- NIC 팀(부하 분산과 장애 조치(failover), LBFO)은 지원되지 않습니다. 대신 SET(Switch-embedded teaming)가 지원됩니다.
- System Center Configuration Manager 및 System Center Data Protection Manager는 지원되지 않습니다.
- BPA(모범 사례 분석기) cmdlet 및 서버 관리자와의 BPA 통합은 지원되지 않습니다.
- Nano 서버는 가상 HBA(호스트 버스 어댑터)를 지원하지 않습니다.
- Nano 서버는 제품 키로 정품 인증할 필요가 없습니다. Hyper-V 호스트로 작동하는 경우 Nano 서버는 [자동 가상 머신 정품 인증](https://technet.microsoft.com/library/dn303421%28v=ws.11%29.aspx)(AVMA)을 지원하지 않습니다. Nano 서버 호스트에서 실행되는 가상 머신은 일반 볼륨 라이선스 키를 통한 [키 관리 서비스](https://technet.microsoft.com/library/jj612867(v=ws.11).aspx)(KMS) 또는 [Active Directory 기반 정품 인증](https://technet.microsoft.com/library/dn502534(v=ws.11).aspx)을 사용하여 정품 인증할 수 있습니다.
- Nano 서버와 함께 제공되는 Windows PowerShell 버전에는 중요한 차이점이 있습니다. 자세한 내용은 [Nano Server의 PowerShell](PowerShell-on-Nano-Server.md)을 참조하세요.
- Nano Server는 CBB(비즈니스용 현재 분기) 모델에서만 지원되며, 현재는 Nano Server의 LTSB(장기 서비스 분기) 릴리스가 없습니다. 자세한 내용은 다음 하위 섹션을 참조하세요.

### <a name="current-branch-for-business"></a>비즈니스용 현재 분기
Nano Server는 빠른 개발 주기를 사용하여 "클라우드 주기"에 따라 이동하는 고객을 지원하기 위해 CBB(비즈니스용 현재 분기)라고 하는 좀 더 활성화된 모델로 제공됩니다. 이 모델에서는 Nano Server의 기능 업데이트 릴리스가 1년에 2~3회로 예상됩니다. 또한 프로덕션에 배포되고 작동되는 Nano Server에 대한 [Software Assurance](https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx)가 필요합니다. 지원을 유지하려면 관리자가 CBB 릴리스를 2개까지 유지해야 합니다. 그러나 이러한 릴리스는 기존 배포를 자동으로 업데이트하지 않습니다. 따라서 관리자가 필요 시 새 CBB 릴리스를 수동으로 설치합니다. 추가 정보에 대해서는 [Windows Server 2016의 새 비즈니스용 현재 분기 서비스 옵션](https://blogs.technet.microsoft.com/windowsserver/2016/07/12/windows-server-2016-new-current-branch-for-business-servicing-option/)을 참조하세요.

Server Core 및 데스크톱 환경 포함 서버 설치 옵션은 5년 간의 주요 지원과 5년 간의 연장 지원으로 구성된 [LTSB(장기 서비스 분기) 모델](https://support.microsoft.com/lifecycle#gp%2Fgp_msl_policy)에 따라 계속 제공됩니다.

## <a name="installation-scenarios"></a>설치 시나리오

### <a name="evaluation"></a>평가
[Windows Server 평가판](https://www.microsoft.com/evalcenter/evaluate-windows-server-2016)에서 Windows Server 180일 라이선스 평가판 사본을 얻을 수 있습니다. Nano 서버를 사용해 보려면 **Nano 서버 | 64비트 EXE 옵션**을 선택한 다음, [Nano 서버 빠른 시작](Nano-Server-Quick-Start.md) 또는 [Nano 서버 배포](Deploy-Nano-Server.md)로 돌아가서 시작합니다.

### <a name="clean-installation"></a>새로 설치
VHD를 구성하여 Nano 서버를 설치하기 때문에 새로 설치하는 것이 가장 빠르고 간단한 배포 방법입니다.

- DHCP로 IP 주소를 가져와서 신속하게 Nano 서버 기본 배포를 시작하려면 [Nano 서버 빠른 시작](Nano-Server-Quick-Start.md)을 참조하세요. 
- 이미 Nano 서버의 기본 사항을 잘 알고 있다면 [Nano 서버 배포](Deploy-Nano-Server.md)로 시작하는 보다 구체적인 토픽을 통해 이미지 사용자 지정, 도메인 작업, 온라인 및 오프라인으로 서버 역할과 기타 기능에 대한 패키지를 설치하는 등의 작업에 대한 지침을 확인할 수 있습니다.

> [!IMPORTANT]  
> 설치가 완료되고 필요한 모든 서버 역할과 기능을 설치하는 즉시 Windows Server 2016에 제공되는 업데이트를 확인하고 설치합니다. Nano 서버의 경우 [Nano 서버 관리](Manage-Nano-Server.md)의 "Nano Server에서 업데이트 관리"를 참조하세요.

### <a name="upgrade"></a>업그레이드
Nano 서버는 Windows Server 2016의 새로운 제품이므로 이전 운영 체제 버전에서 Nano 서버로 업그레이드하는 경로가 없습니다.

### <a name="migration"></a>마이그레이션
Nano 서버는 Windows Server 2016의 새로운 제품이므로 이전 운영 체제 버전에서 Nano 서버로 마이그레이션하는 경로가 없습니다.
  
-------------------------------------
다른 설치 옵션이 필요한 경우 [Windows Server 2016 기본 페이지로 돌아갈 수 있습니다](windows-server-2016.md). 

  


 
