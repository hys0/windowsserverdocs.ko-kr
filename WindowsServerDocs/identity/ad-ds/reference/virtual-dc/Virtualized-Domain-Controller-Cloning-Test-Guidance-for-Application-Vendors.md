---
ms.assetid: fde99b44-cb9f-49bf-b888-edaeabe6b88d
title: 응용 프로그램 공급업체를 위한 가상화된 도메인 컨트롤러 복제 테스트 지침
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 0b2303bc837cdaf9f6e7ebd4b3ccbf6c66aa7ad2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879344"
---
# <a name="virtualized-domain-controller-cloning-test-guidance-for-application-vendors"></a>응용 프로그램 공급업체를 위한 가상화된 도메인 컨트롤러 복제 테스트 지침

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

응용 프로그램 공급 업체 응용 프로그램 계속 가상화 된 도메인 컨트롤러 (DC) 복제 프로세스가 완료 된 후 예상 대로 작동 되도록 하는 데 고려해 야 하는 것이 설명 합니다. 관련 응용 프로그램 공급 업체 및 추가 테스트가 수행 될 수 있습니다 하는 시나리오는 복제 프로세스의 이러한 측면을 설명 합니다. 복제 된 가상화 된 도메인 컨트롤러에서 해당 응용 프로그램이 작동 하는지 유효성을 검사 하는 응용 프로그램 공급 업체는 응용 프로그램에 대 한 링크와 함께이 항목의 맨 아래에 있는 커뮤니티 콘텐츠의 이름을 나열 하는 것이 좋습니다에 조직의 웹 사이트 사용자 수에 대해 자세히 알아보려면 유효성 검사입니다.  
  
## <a name="overview-of-virtualized-dc-cloning"></a>가상화 된 DC 복제 개요  
가상화 된 도메인 컨트롤러 복제 프로세스에서 자세히 설명 되어 [Active Directory Domain Services (AD DS) Virtualization (Level 100) 소개](https://technet.microsoft.com/library/hh831734.aspx) 고 [가상화 된 도메인 컨트롤러 기술 참조 (수준 300)](https://technet.microsoft.com/library/jj574214.aspx)합니다. 응용 프로그램 공급 업체의 관점에서 다음은 응용 프로그램에 대 한 복제의 영향을 평가할 때 고려해 야 할 몇 가지 고려 사항입니다.  
  
-   원래 컴퓨터 소멸 되지 않습니다. 클라이언트와 상호 작용 하는 네트워크에서 유지 됩니다. 원래 컴퓨터의 DNS 레코드는 제거 되는 이름 바꾸기와는 달리 원본 도메인 컨트롤러에 대 한 원래 레코드 유지 됩니다.  
  
-   새 컴퓨터 복제 프로세스 중 처음 복제 프로세스가 시작 되 고 변경 될 때까지 이전 컴퓨터의 id는 짧은 기간에 대 한 실행 됩니다. 호스트에 대 한 레코드를 만드는 응용 프로그램을 복제 된 컴퓨터는 복제 프로세스 중 원본 호스트에 대 한 레코드를 덮어쓰지 않습니다 않습니다 확인 해야 합니다.  
  
-   복제를 다른 서버 역할을 복제 하지 범용 확장만 가상화 된 도메인 컨트롤러에 대 한 특정 배포 기능입니다. 일부 서버 역할 복제에 대 한 지원 특히 되지 않습니다.  
  
    -   DHCP(동적 호스트 구성 프로토콜)  
  
    -   AD CS(Active Directory 인증서 서비스)  
  
    -   AD LDS(Active Directory Lightweight Directory Services)  
  
-   복제 프로세스의 일환으로, 원래 DC를 나타내는 전체 VM은 복사 됩니다 하므로 해당 VM에서 응용 프로그램 상태도 복사 됩니다. 이 변경 된 복제 된 DC에 로컬 호스트의 상태에 맞게 응용 프로그램의 유효성을 검사 개입 서비스를 다시 시작와 같이 필요한 경우.  
  
-   복제의 일부로 새로운 DC 가져옵니다 새 컴퓨터 id 및 프로 비전 자체 복제본 DC로 토폴로지에서. 컴퓨터 id의 이름, 계정, SID 등과 같은 응용 프로그램이 있는지 여부를 확인 합니다. 이 자동으로 조정 복제본에서 컴퓨터 id의 변경에? 해당 응용 프로그램 데이터를 캐시 하는 경우에 캐시 될 수 있는 컴퓨터 id 데이터에 의존 하지 않습니다 확인 합니다.  
  
## <a name="what-is-interesting-for-application-vendors"></a>응용 프로그램 공급 업체에 대 한 흥미로운 란?  
  
### <a name="customdccloneallowlistxml"></a>CustomDCCloneAllowList.xml  
응용 프로그램까지 응용 프로그램 또는 서비스를 실행 하는 도메인 컨트롤러를 복제할 수 없습니다 또는 서비스 중 하나:  
  
-   Get-addccloningexcludedapplicationlist Windows PowerShell cmdlet을 사용 하 여 CustomDCCloneAllowList.xml 파일에 추가 합니다.  
  
-또는-  
  
-   도메인 컨트롤러에서 제거  
  
처음 사용자 Get-addccloningexcludedapplicationlist cmdlet을 실행할 때 서비스와 도메인 컨트롤러에서 실행 되지만 서비스 및 복제에 지원 되는 응용 프로그램의 기본 목록에 없는 응용 프로그램의 목록을 반환 합니다. 기본적으로 서비스 또는 응용 프로그램 나열 되지 않습니다. 서비스 또는 응용 프로그램을 안전 하 게 될 수 있는 서비스 목록에 응용 프로그램에 추가할 복제 Get-addccloningexcludedapplicationlist cmdlet 다시 CustomDCCloneAllowList.xml에 추가 하기 위해 GenerateXML 옵션을 사용 하 여 파일 사용자 실행 합니다. 자세한 내용은 참조 하세요. [2 단계: Get-addccloningexcludedapplicationlist cmdlet 실행](https://technet.microsoft.com/library/hh831734.aspx#bkmk6_run_get_addccloningexcludedapplicationlist_cmdlet)합니다.  
  
### <a name="distributed-system-interactions"></a>분산된 시스템의 상호 작용  
일반적으로 로컬 컴퓨터로 격리 서비스 통과 또는 실패를 복제에 참여 하는 경우. 분산된 서비스는 짧은 기간에 대 한 네트워크의 호스트 컴퓨터의 두 인스턴스가 동시에 있으면 염려 해야 합니다. 이를 가져오려고 파트너 시스템의 정보를 새 공급 업체 id의 복제본에 등록 하는 위치 서비스 인스턴스로 나타날 수 있습니다. 또는 서비스의 두 인스턴스 모두에서 AD DS 데이터베이스에 다른 결과 사용 하 여 동시에 정보를 푸시할 수 있습니다. 예를 들어이 결정적이 지 않습니다 Windows 테스트 기술 (WTT) 서비스는 두 개의 컴퓨터가 도메인 컨트롤러를 사용 하 여 네트워크에 있을 때 사용 하 여 컴퓨터에 전달 됩니다.  
  
분산된 DNS 서버 서비스에 대 한 복제 프로세스에서 복제 도메인 컨트롤러에서 새 IP 주소를 사용 하 여 시작 하는 경우 원본 도메인 컨트롤러의 DNS 레코드를 덮어씁니다를 신중 하 게 방지 합니다.  
  
복제가 끝날 때까지 이전 id를 모두 제거 하려면 컴퓨터에는 안 됩니다. 새 컨텍스트 내에서 새 도메인 컨트롤러 승격 되 면 Sysprep 공급자 실행 되는 컴퓨터의 추가 상태를 정리 하 여 선택 합니다. 예를 들어, 것이 시점에서 컴퓨터의 이전 인증서 제거 되 고 컴퓨터에 액세스할 수 있는 암호화 암호를 변경 합니다.  
  
가장 큰 요소를 복제 하는 시기를 변경 하는 경우 PDC에서 복제 하는 개체 수 오래 된 미디어에는 전체 복제 하는 데 필요한 시간이 늘어납니다.  
  
서비스 또는 응용 프로그램을 알려진 아니므로 계속 실행 됩니다. 복제 프로세스는 비-Windows 서비스의 상태를 변경 되지 않습니다.  
  
또한 새 컴퓨터에 원래 컴퓨터와 다른 IP 주소를 합니다. 이러한 동작은 서비스 또는 서비스나 응용 프로그램에이 환경에서 작동 하는 방법에 따라 응용 프로그램에 파생 작업이 발생할 수 있습니다.  
  
## <a name="additional-scenarios-suggested-for-testing"></a>테스트에 대 한 제안 하는 추가 시나리오  
  
### <a name="cloning-failure"></a>복제 실패  
복제에 실패 하는 경우 컴퓨터에 복구 모드 DSRM (디렉터리 서비스)를 안전 모드의 형태를 부팅 하는 때문에 서비스 공급 업체에서이 시나리오를 테스트 해야 합니다. 이때 컴퓨터는 복제을 완료 되지 않았습니다. 일부 상태 변경 및 일부 상태는 원본 도메인 컨트롤러에서 남아 있을 수 있습니다. 응용 프로그램은 어떤 영향을 이해 하려면이 시나리오를 테스트 합니다.  
  
복제 오류를 유도 하려면 복제 되도록 권한을 부여 하지 않고 도메인 컨트롤러를 복제 하려고 합니다. 이 예에서 컴퓨터만 변경 됩니다 IP 주소를 아직 대부분의 원본 도메인 컨트롤러에서 해당 상태 및 합니다. 복제 도메인 컨트롤러 권한을 부여 하는 방법에 대 한 자세한 내용은 참조 하세요. [1 단계: 원본 가상화 된 도메인 컨트롤러 복제 권한 부여](https://technet.microsoft.com/library/hh831734.aspx#bkmk4_grant_source)합니다.  
  
### <a name="pdc-emulator-cloning"></a>복제는 PDC 에뮬레이터  
서비스 및 응용 프로그램 공급 업체는 PDC 에뮬레이터에 복제 됩니다 때 추가적으로 다시 부팅 때문에이 시나리오를 테스트 해야 합니다. 또한 대부분의 복제는 새 복제는 복제 프로세스 중 PDC 에뮬레이터와 상호 작용할 수 있도록 임시 id 수행 됩니다.  
  
### <a name="writable-versus-read-only-domain-controllers"></a>읽기 전용 도메인 컨트롤러 및 쓰기  
서비스 및 응용 프로그램 공급 업체에서 동일한 유형의 도메인 컨트롤러를 사용 하 여 복제를 테스트 해야 (즉, 쓰기 또는 읽기 전용 도메인 컨트롤러에) 서비스에서 실행할 예정입니다.  
  


