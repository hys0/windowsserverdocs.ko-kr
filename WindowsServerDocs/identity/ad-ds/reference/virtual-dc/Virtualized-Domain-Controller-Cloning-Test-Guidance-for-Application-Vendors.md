---
ms.assetid: fde99b44-cb9f-49bf-b888-edaeabe6b88d
title: "공급 업체 응용 프로그램에 대 한 테스트 지침 복제 가상화 도메인 컨트롤러"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 72c4e818f82d3252c45776b26fb59e095893f2c7
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="virtualized-domain-controller-cloning-test-guidance-for-application-vendors"></a>공급 업체 응용 프로그램에 대 한 테스트 지침 복제 가상화 도메인 컨트롤러

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에 설명 공급 업체 응용 프로그램의 응용 프로그램을 계속는 가상화 DC (도메인 컨트롤러) 복제 프로세스를 완료 한 후 예상 대로 작동 하도록 보장 하기 위해 고려해 야 합니다. 해당 관심 응용 프로그램 공급 업체와 시나리오를 추가로 테스트 보증 복제 프로세스의 해당 기능을 다룹니다. 했음을 복제 된 가상화 도메인 컨트롤러에서 자녀가 응용 프로그램이 작동 하는지 확인 하는 응용 프로그램 공급 업체는 사용자가 유효성 검사에 대해 자세히 알아보려면 수 회사의 웹 사이트에 대 한 링크와 함께이 항목의 아래쪽에 커뮤니티 콘텐츠의 응용 프로그램의 이름을 표시 합니다.  
  
## <a name="overview-of-virtualized-dc-cloning"></a>DC 가상화 복제 개요  
복제 프로세스 가상화 도메인 컨트롤러에 자세히 설명 되어 [Active Directory 도메인 서비스 AD DS Virtualization (수준을 100) 소개](https://technet.microsoft.com/library/hh831734.aspx) 및 [가상화 도메인 컨트롤러 기술 참조 (300 수준)](https://technet.microsoft.com/library/jj574214.aspx)합니다. 된 대리점 관점에서 복제 응용 프로그램에 미치는 영향을 평가 하는 경우 고려해 야 할 몇 가지 사항을입니다.  
  
-   원래 컴퓨터는 제거 되지 않습니다. 하는 클라이언트와의 상호 작용 하는 네트워크에 계속 유지 됩니다. 원래 컴퓨터 DNS 레코드 제거 되어 이름 바꾸기, 달리 원본 도메인 컨트롤러에 대 한 원래 레코드 남아 있습니다.  
  
-   복제 과정에서 새 처음 컴퓨터 id 이전 컴퓨터에서 시간을 잠시 동안 복제 프로세스 시작 되 고 필요한 변경 될 때까지 합니다. 기록 호스트에 대 한 만드는 응용 프로그램 복제 컴퓨터 복제 프로세스 중 원래 호스트에 대 한 기록을 덮어쓰지 않도록 않는 확인 해야 합니다.  
  
-   복제 다른 서버 역할 복제 하는 일반적인 용도의 확장 되지 유일한 가상화 도메인 컨트롤러에 대 한 특정 배포 기능입니다. 일부 서버 역할은 복제에 대 한 지원 하지는 않습니다.  
  
    -   DHCP(Dynamic Host Configuration Protocol) DHCP)  
  
    -   Active Directory 인증서 서비스 (AD CS)  
  
    -   Active Directory 무게는 가벼우며 디렉터리 서비스 (AD LDS)  
  
-   복제 프로세스의 일부로 원래 DC 나타내는 전체 VM 복사 하므로 응용 프로그램에서 해당 VM 상태도 복사 합니다. 확인 응용 프로그램 적응 복제 DC에서 로컬 호스트 상태에서 이러한 변경 하는 관여 하지 같은 서비스를 다시 시작 해야 하는 경우 또는 합니다.  
  
-   복제의 일환으로, 새 DC 새로운 컴퓨터 id 및 규정 자체로 가져옵니다 복제 DC 토폴로지의. 응용 프로그램의 이름, 계정, SID 등 컴퓨터 id를에 따라 달라 집니다 여부를 확인 합니다. 것에 자동으로 맞춰집니다 복제에 컴퓨터 id 변경 하나요? 캐시 된 데이터를 해당 응용 프로그램을 캐시 될 수 있는 컴퓨터 id 데이터에 의존 하지 않는 확인 합니다.  
  
## <a name="what-is-interesting-for-application-vendors"></a>공급 업체 응용 프로그램에 대 한 흥미로운은 무엇 인가요?  
  
### <a name="customdccloneallowlistxml"></a>CustomDCCloneAllowList.xml  
응용 프로그램 또는 서비스가 실행 되는 도메인 컨트롤러 응용 프로그램 될 때까지 복제할 없습니다 나 서비스 중 하나는 다음과 같습니다.  
  
-   Get ADDCCloningExcludedApplicationList Windows PowerShell cmdlet 사용 하 여 CustomDCCloneAllowList.xml 파일에 추가  
  
또는  
  
-   도메인 컨트롤러에서 제거  
  
처음 실행할 Get ADDCCloningExcludedApplicationList cmdlet 사용자 서비스와 응용 프로그램 도메인 컨트롤러에서 실행 중인 하지만 서비스와 응용 프로그램에 복제 지원 되는 기본 목록에 없는 목록이 반환 됩니다. 기본적으로 서비스 또는 응용 프로그램 나열 되지 않습니다. 서비스 또는 목록 응용 프로그램의 응용 프로그램 및 서비스 안전 하 게 될 수 있는 추가 복제 Get ADDCCloningExcludedApplicationList cmdlet 다시-GenerateXML 옵션을 추가 하 고 CustomDCCloneAllowList.xml 하기 위해 파일 사용자 실행 됩니다. 자세한 내용은 참조 [2 단계: 실행 Get ADDCCloningExcludedApplicationList cmdlet](https://technet.microsoft.com/library/hh831734.aspx#bkmk6_run_get_addccloningexcludedapplicationlist_cmdlet)합니다.  
  
### <a name="distributed-system-interactions"></a>분산된 시스템 상호 작용  
일반적으로 로컬 컴퓨터에 격리 서비스 통과 또는 복제에 참여 하는 경우에 실패 합니다. 배포 서비스 하는 데 호스트 컴퓨터의 두 가지 인스턴스 네트워크에서 동시에 짧은 기간 동안 우려할 수 있습니다. 이 복제 id의 새로운 공급 업체는 라고 파트너 시스템에서 정보를 가져와 하려고 서비스 인스턴스도 나타날 수 있습니다. 또는 서비스의 모두 인스턴스 다른 결과를 동시에 AD DS 데이터베이스에 정보에 배포할 수 있습니다. 예를 들어, 것은 아닙니다 명확한 Windows 테스트 기술을 (WTT) 서비스는 두 가지 컴퓨터가 도메인 컨트롤러를 사용 하 여 네트워크에 있는 경우 컴퓨터에으로 전달 됩니다.  
  
분산된 DNS 서버 서비스에 대 한 복제 프로세스 복제 도메인 컨트롤러 새 IP 주소를 사용 하 여 시작 하면 원본 도메인 컨트롤러의 DNS 레코드 덮어쓰지 신중 하 게 방지 합니다.  
  
하지 복제 끝날 때까지 오래 id를 모두 제거 하는 컴퓨터 사용 해야 합니다. 새 도메인 컨트롤러 새로운 컨텍스트 내 수준 올린, 후 컴퓨터의 자세한 상태가를 정리 하려면 공급자는 실행 Sysprep 선택 합니다. 예를 들어, 것이 시점에서 컴퓨터의 오래 된 인증서를 제거 하 고 컴퓨터에 액세스할 수 있는 암호화 비밀 변경 됩니다.  
  
복제 시기에 따라 다른 위대한 요소 개체 수 PDC에서 복제 하는입니다. 오래 된 미디어 완료 복제 하는 데 걸리는 시간은 증가 합니다.  
  
서비스 또는 응용 프로그램을 알 수 없는 때문에 실행 남아 있습니다. 복제 프로세스 비 Windows 서비스의 상태를 변경 되지 않습니다.  
  
또한 새 컴퓨터에 원래 컴퓨터 보다 다른 IP 주소를 합니다. 이러한 문제를 서비스 또는 응용 프로그램 서비스 또는 응용 프로그램이이 환경에서 작동 하는 방법에 따라 부작용 발생할 수 있습니다.  
  
## <a name="additional-scenarios-suggested-for-testing"></a>테스트 추천 추가 시나리오  
  
### <a name="cloning-failure"></a>오류 복제  
서비스 업체 컴퓨터에 디렉터리 복구 모드 (DSRM 서비스)를 안전 모드 형태의 부팅 실패를 복제할 때 때문에이 시나리오를 테스트 해야 합니다. 이제 컴퓨터는 복제을 완료 되지 않았습니다. 일부 상태 변경 될 수 있습니다 및 일부 상태 원래 도메인 컨트롤러에서 유지 될 수 있습니다. 응용 프로그램에 미칠 수 어떤 영향을 알아보려면이 시나리오를 테스트 합니다.  
  
복제 오류를 유도 도메인 컨트롤러를 복제 하는 데 사용 권한을 부여 하지 않고 복제 하 해 보세요. 이 경우 컴퓨터는만 변경 IP 주소 및 대부분의 원래 도메인 컨트롤러에서 상태로 계속 합니다. 복제할 도메인 컨트롤러 권한을 부여 하면에 대 한 자세한 내용은 참조 [1 단계: 원본 가상화 도메인 컨트롤러 복제 될 수 있는 권한을 부여](https://technet.microsoft.com/library/hh831734.aspx#bkmk4_grant_source)합니다.  
  
### <a name="pdc-emulator-cloning"></a>복제 PDC 에뮬레이터  
서비스 및 응용 프로그램 공급 업체 PDC 에뮬레이터 복제 되 재부팅 있기 때문에이 시나리오를 테스트 해야 합니다. 또한, 대부분의 복제 복제 프로세스 중 PDC 에뮬레이터와 상호 작용 하는 새로운 복제 수 있도록 임시 id 수행 됩니다.  
  
### <a name="writable-versus-read-only-domain-controllers"></a>읽기 전용 도메인 컨트롤러 및 쓸 수 있는  
서비스 및 응용 프로그램 공급 같은 유형의 도메인 컨트롤러를 사용 하 여 복제 테스트 해야 (즉, 쓰기 가능한 또는 읽기 전용 도메인 컨트롤러에서) 서비스에서 실행 되도록 예정입니다.  
  


