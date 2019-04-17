---
ms.assetid: c81b8291-fba5-4b30-a43d-7feb2f4b66be
title: "Windows Server 2012 r 2의 지침에 따라 AD FS 디자인"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f618add4c4803142b3bd7278908834a412f30999
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="identify-your-ad-fs-deployment-goals"></a>광고 FS 배포 목표에 사용자의 신원을 확인합니다

>적용 대상: Windows Server 2016, Windows Server 2012 r 2

올바르게 Active Directory Federation Services \(AD FS\) 배포 목표를 식별 하는 것이 ADFS 디자인 프로젝트의 성공 여부에 대 한 중요 합니다. 우선 순위를 지정 하 고, 예를 들어, 디자인 하 고 반복 방법을 통해 ADFS 배포할 수 있도록 배포 목표를 결합 합니다. 끝났으며 민 ADFS 디자인와 관련 된 상황에 맞는 작동 솔루션을 개발 ADFS 배포 목표 미리 기존 이용할 수 있습니다.  
  
Adfs의 이전 버전은 다음 달성 하기 위해 배포 가장 일반적으로 다음과 같습니다.  
  
-   기업의 내 claims\ 기반 응용 프로그램에 액세스할 때 SSO 환경을 web\ 기반으로 직원 나 고객을 제공 합니다.  
  
-   모든 federation 파트너 조직의 리소스에 액세스 하려면 web\ 기반 SSO 환경 직원 나 고객을 제공합니다.  
  
-   웹 사이트 또는 서비스 호스트 원격 액세스 내부적으로 때 SSO 빈 Web\ 기반으로 직원 나 고객을 제공 합니다.  
  
-   리소스 또는 클라우드에서 서비스에 액세스할 때 직원 나 고객 web\ 기반 SSO 환경이 제공 합니다.  
  
뿐만 아니라 ADFS® Windows Server 2012 r 2에 다음 얻는 데 도움이 되는 기능을 추가 합니다.  
  
-   장치 회사 가입 SSO 및 원활 하 게 초 요소 인증 합니다. 이 통해 조직에서 사용자의 개인 장치에서 액세스할 수 있도록 하 고이 액세스를 제공 하는 경우는 위험을 관리할 수 있습니다.  
  
-   관련 된 위험 multi\ 팩터 액세스 제어도 관리 합니다. ADFS 제어 하는 응용 프로그램에 액세스할 수 있는 다양 한 수준의 승인 제공 합니다. 사용자 특성에 따라이 \ (UPN, 메일, 보안 그룹 구성원, 인증 강도 등 \), 디바이스 특성 \ (여부는 디바이스는 회사 joined\) 특성 요청할 또는 \ (위치나 IP 주소, 사용자 agent\ 네트워크).  
  
-   중요 한 응용 프로그램에 대 한 추가 multi\ 요소 인증 된 위험을 관리 합니다. Adfs는 정책이 전체적으로 또는 응용 프로그램에 따라 잠재적으로 multi\ 단계 인증을 요구 하도록 제어할 수 있습니다. 또한 ADFS 모든 multi\ 팩터 공급 업체 최종 사용자에 게 깊은 안전 하 게 완벽 multi\ 팩터 경험에 대 한 통합에 대해서 제공 합니다.  
  
-   웹 응용 프로그램 프록시도 보호 되 고 익스트라넷에서 웹 리소스에 액세스 인증과 기능을 제공 합니다.  
  
즉, Windows Server 2012 r 2에서 ADFS 조직에서 다음과 같은 목표를 달성 하기 배포할 수 있습니다.  
  
### <a name="enable-your-users-to-access-resources-on-their-personal-devices-from-anywhere"></a>어디에서 든 리소스의 개인 장치에 액세스 하 여 사용자가 사용  
  
-   사용자가 자신의 개인 장치 회사 Active Directory에 가입 하 따라서 이러한 디바이스에서 기업 리소스에 액세스할 때 액세스 및 원활한 환경을 얻을 수 있도록 회사 가입  
  
-   회사 네트워크 프록시 웹 응용 프로그램에 의해 보호 되 고에서 인터넷 액세스를 내 리소스 Pre\ 인증 합니다.  
  
-   암호 리소스에 액세스 계속 수 있도록 만료 될 때 디바이스를 참가 하는 모든 회사에서 암호를 변경 하려면 사용자가 암호를 변경 합니다.  
  
### <a name="enhance-your-access-control-risk-management-tools"></a>사용자 액세스 제어 위험 관리 도구 개선  
위험 관리 통제 및 IT에 준수의 중요 한 부분입니다. 수많은 액세스 제어 다음을 포함 한® Windows Server 2012 r 2의 adfs에서 위험 관리 향상은 다음과 같습니다.  
  
-   사용자는 광고 FS\ 보안 응용 프로그램에 액세스 인증 하는 방법을 제어 하는 네트워크 위치에 따라 유연한 컨트롤.  
  
-   사용자는 사용자의 데이터, 디바이스 데이터를 및 네트워크 위치에 따라 multi\ 단계 인증을 수행 해야 하는지 확인 하려면 유연한 정책입니다.  
  
-   SSO 무시 하 고 사용자에 게 중요 한 응용 프로그램에 액세스할 때마다 자격 증명을 제공 하도록 하려면 Per\ 응용 프로그램을 관리 합니다.  
  
-   사용자 데이터, 디바이스 데이터를 또는 네트워크 위치에 따라 유연한 per\ 응용 액세스 정책입니다.  
  
-   광고 FS 엑스트라넷 잠금, Active Directory 계정 무작위 인터넷 공격 으로부터 보호할 수 있는 합니다.  
  
-   모든 회사에 대 한 액세스 해지 가입 디바이스를 사용 하지 않거나 Active Directory에 삭제 합니다.  
  
### <a name="use-ad-fs-to-enhance-the-sign-in-experience"></a>ADFS sign\에서 환경 향상을 사용 하 여  
다음은® Windows Server 2012 r 2의 관리자가 사용자 지정 하 고 sign\에서 환경을 향상 시킬 수 있게 하는 새로운 ADFS 기능입니다.  
  
-   변경 내용을 한 번만 수행 하 고 특정된 농장의 ADFS federation 서버의 나머지 부분에 자동으로 전파 ADFS 서비스의 통합된 사용자 지정 합니다.  
  
-   업데이트 된 sign\에서 페이지를 현대적인 모양과 자동으로 다른 폼 팩터와 제공 합니다.  
  
-   자동 대체 회사 도메인에 가입 하지 않은 하지만 계속 사용 하는 디바이스에 대 한 forms\ 기반 인증에 대 한 지원이 회사 네트워크 \(intranet\) 내에서 액세스 요청을 생성 합니다.  
  
-   간단한 컨트롤 회사 로고, 그림 이미지, 표준 링크 IT 지원, 홈페이지, 개인 정보를 사용자 지정할 수 있습니다.  
  
-   설명 페이지 sign\의 메시지를 사용자 지정 합니다.  
  
-   웹 테마를 사용자 지정 합니다.  
  
-   홈 영역 검색 \(HRD\) 파트너 회사의 개인 정보 보호에 대 한 사용자의 조직 접미사 기반으로 합니다.  
  
-   HRD per\ 응용 별로 필터링을 자동으로 응용 프로그램에 따라 영역을 선택 합니다.  
  
-   클릭 One\ 오류에 대 한 보다 쉽게 보고 IT 문제를 해결 합니다.  
  
-   사용자 지정 가능한 오류 메시지입니다.  
  
-   사용자 인증 선택 개 이상의 인증 공급자가 사용 가능 합니다.  
  
## <a name="see-also"></a>참조 하십시오  
[Windows Server 2012 r 2의 지침에 따라 AD FS 디자인](../../ad-fs/design/AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)  
  

