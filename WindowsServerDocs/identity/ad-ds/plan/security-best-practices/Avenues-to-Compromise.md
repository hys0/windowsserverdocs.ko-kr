---
ms.assetid: d7a4d2e1-217d-4ffc-93f0-817149bd9e7f
title: "손상 수단"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 149a3e4bb2ce4558e40425e42ecfdeec2c5dfcb7
ms.sourcegitcommit: 78d8839ccafa9530784cb9e38c3127ed2c215423
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2018
---
# <a name="avenues-to-compromise"></a>손상 수단

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

*법률 일곱: 가장 안전한 네트워크는 잘 관리 합니다.* - [10 Immutable Laws of Security Administration](https://technet.microsoft.com/library/cc722488.aspx)  
  
심각한 손상을 이벤트가 발생 했을 조직에서 평가 조직의 IT 인프라를 설명 하 는"있는 그대로"의 상태에서 상당히 다를 수 있는의 실제 상태에 대 한 가시성은 제한 된 일반적으로 표시 됩니다. 이러한 차이 자주는 공격자 효과적으로 "소유" 환경을 지점으로 진행 손상 될 때까지 검색의 거의 위험을 손상 시킬 환경을 제공 하는 문제를 도입 합니다.  
  
이러한 조직의 광고 DS 구성, 키 Pki 공개 인프라 (), 서버, 워크스테이션, 응용 프로그램의 상세 평가 액세스 제어 목록을 (Acl) 및 기타 기술 구성 오류 및 설정을, 수 있는 예방 초기 손상 될 수 있는 보안 문제를 확인 합니다.  
  
IT 설명서, 프로세스를 및 절차 분석 취약성 도입 된 Active Directory 숲 손상 완벽 하 게 하는 데 사용 된 권한 결국 얻는 공격자가 활용 하는 방법 관리 간격으로 식별 합니다. 완벽 하 게 손상된 숲 공격자 뿐만 아니라 개별 시스템, 응용 프로그램 또는 사용자 계정이 손상 하지만 대 한 액세스 권한이 있는 수정 하거나 삭제 숲의 모든 측면 수 수준의 얻는 에스컬레이션 하나입니다. 때 Active Directory 설치가 손상 된에 정도 공격자 변경할 수 있는 전체 환경 또는 악화 디렉터리 시스템 및 관리 하는 계정을 제거 하는 상태를 유지 하도록 허용 하는 경우  
  
에 따라 설명에서 일반적으로 발생된 하는 문제점 수는 없지만 Active Directory에 대 한 공격, 공격자 권한 에스컬레이션 (권한이 상승 라고도 함) 공격 실행 결국 대상으로 하며 AD DS 손상를 사용할 수 있는 환경에서 한 발판을 마련 설정할 수 있습니다.  
  
이 섹션이 문서의 공격자는 인프라에 액세스 하 고 결국를 시작할 상승 권한 공격 일반적으로 사용 하는 메커니즘을 설명 하는 중점적 합니다. 또한 다음 섹션을 참조 하십시오.  
  
-   [축소 Active Directory 공격](../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/Reducing-the-Active-Directory-Attack-Surface.md) 자세한 Active directory 안전한 구성에 대 한 추천을 제공 합니다.  
  
-   [손상 기호에 대 한 Active Directory 모니터링](../../../ad-ds/plan/security-best-practices/Monitoring-Active-Directory-for-Signs-of-Compromise.md) 손상 발견할 수 있도록 권장  
  
-   [손상에 대 한 계획](../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/Planning-for-Compromise.md) 에서 인프라에 대해 공격에 대 한 준비를 고급 접근법 IT 및 비즈니스 보기  
  
> [!NOTE]  
> 이 문서에서는 AD DS 도메인에 포함 된 Active Directory 및 Windows 시스템, Active Directory 및 창에만 공격자 거의 집중 합니다. 이 운영 체제, 디렉터리, 응용 프로그램 및 데이터 저장소 함께 환경에서 일반적 비 Windows 시스템 손상도 찾을 수 있습니다. 시스템은 "" 사이의 다리 Windows 및 비 Windows 환경, 파일 서버 하 여 Windows와 UNIX 또는 Linux 클라이언트, 여러 운영 체제를 인증 서비스를 제공 하는 디렉터리 메타 데이터를 다른 디렉터리 간에 동기화 하는 등을 제공 하는 경우 특히 마찬가지입니다.  
>   
> AD DS Windows 시스템 뿐 아니라 다른 클라이언트를 제공 하는 중앙 집중식된 액세스 및 구성 관리 기능으로 인해 대상으로 지정 됩니다. 디렉터리 또는 인증과 구성 관리 서비스를 제공 하는 응용 프로그램, 하 결정된 공격자가 대상이 됩니다. 이 문서는 가능성 설치 Active Directory 비 Windows 컴퓨터를 포함 하는 모든 조직이의 공격을 줄일 수 보호에 초점을 있지만 해당 시스템에 대 한 공격에 대 한 데이터, 디렉터리 또는 응용 프로그램 저장소 준비 또한 해야 합니다.  
  
## <a name="initial-breach-targets"></a>초기 위반 대상  
아무도 IT 인프라를 손상 조직 노출를 의도적으로 작성 합니다. 처음 Active Directory 숲 생성할 일반적으로 그대로 및 현재 되어 있습니다. 년 통과 하 고 자녀가 숲에 추가 하는 새 운영 체제와 응용 프로그램을 구입 합니다. 관리 효율성 혜택 Active Directory를 제공 하는 인식 점점 더 많은 콘텐츠는 디렉터리에 추가 되며, 더 많은 사람들이 AD DS와 응용 프로그램 또는 컴퓨터 통합 및 최신 버전의 Windows 운영 체제에서 제공 하는 새로운 기능을 지원 하기 위해 업그레이드 하는 도메인 합니다. 하지만 또한 시간이 지남에 따라 일어나은 새로운 인프라 그대로 인프라의 다른 부분 뿐만 아니라 처음 했 유지 되지 추가 되 고, 시스템 및 응용 프로그램 제대로 작동 하 고 주의 수신 하지는 조직 레거시 인프라 제거 되지가 잊어버린 하기 시작입니다. 손상 된 인프라 평가 보이는에 따라 이전, 크고 더 복잡 한 환경, 가능성이 높아지도록 일반적으로 발생된 하는 문제점 인스턴스 여러 가지입니다.  
  
공격자 목표로 관계 없이 한 번에 대부분 정보 보안 위반 하나 또는 두 개의 체제의 손상 된 시작합니다. 이러한 초기 이벤트 또는 네트워크로 진입점 자주 수리 되었을 수, 있지만 되지 않았습니다 있는 취약성을 활용 합니다. [2012 데이터 위반 조사 보고서 (DBIR)](http://www.verizonbusiness.com/resources/reports/rp_data-breach-investigations-report-2012_en_xg.pdf), 하는 다양 한 국가 보안 기관 및 다른 회사와 협력 하 여 Verizon 위험 팀에서 생성 된 연간 연구, 공격의 96% 된 "하지 매우 어렵습니다" 지정 하 고 "침해 97% 했음을 간단한 또는 중간 컨트롤을 통해 불가피할." 이러한 발견 때문에 따라는 일반적으로 발생된 하는 문제점입니다 될 수 있습니다.  
  
### <a name="gaps-in-antivirus-and-antimalware-deployments"></a>바이러스 백신 및 맬웨어 방지 배포 차이  
*법률 번호 8: 전혀 오래 된 맬웨어 스캐너 것 스캐너 보다 조금 더만입니다.* - [Ten Immutable Laws of Security (Version 2.0)](https://technet.microsoft.com/security/hh278941.aspx)  
  
조직의 바이러스 백신 및 맬웨어 방지 배포 분석 하는 자주 워크스테이션 대부분은 사용 하도록 설정 하는 바이러스 백신 및 맬웨어 방지 소프트웨어를 구성 하 고 현재 환경을 알 수 있습니다. 예외 워크스테이션 어떤 바이러스 백신 및 맬웨어 방지 소프트웨어 구성 하 고 업데이트를 배포 하기 어려울 수 회사 환경이 나 직원 디바이스 자주 연결 하는 일반적으로입니다.  
  
그러나 서버 채우기 적게 많은 손상 된 환경에서 일관 되 게 보호 하는 경우가 많습니다. 보고 있는 [2012 데이터 위반 조사](http://www.verizonbusiness.com/resources/reports/rp_data-breach-investigations-report-2012_en_xg.pdf)94%의 모든 데이터를 침해 참여 서버 이전 년 동안 18% 증가 나타냅니다 하 고 공격 69% 맬웨어를 포함 합니다. 서버 채우기에는 바이러스 백신 및 맬웨어 방지 설치는 일관 구성, 오래, 잘못 구성 또는 사용 하지 않도록 설정 드문 아닙니다. 경우에 따라 관리 담당자 하 여 바이러스 백신 및 맬웨어 방지 소프트웨어를 사용 하지 하지만 소프트웨어를 통해 다른 취약점 서버에 영향을 미치지 후 공격자 경우도 비활성화 합니다. 바이러스 백신 및 맬웨어 방지 소프트웨어를 사용 하지 않는 경우 공격자 다음 서버에서 맬웨어를 공장와 손상 서버에서 전파에 집중 합니다.  
  
것이 중요 뿐만 아니라 보호 하는 시스템은 현재, 종합적인 맬웨어 보호 기능으로 사용 하지 않도록 설정 했거나 바이러스 백신 및 맬웨어 방지 소프트웨어로 제거에 대 한 시스템을 모니터링을 자동으로 다시 시작 보호 수동으로 불가능 합니다. 바이러스 백신 및 맬웨어 방지 프로그램 소프트웨어가 없는 예방 하 고 모든 감염 감지 보장할 수, 하더라도 제대로 구성 및 배포 된 바이러스 백신 및 맬웨어 방지 구현 감염 될 가능성이 줄일 수 있습니다.  
  
### <a name="incomplete-patching"></a>불완전 패치  
*법률 숫자 3: 경우 최신 보안 픽스도 유지 되지 않는, 네트워크 수 없습니다 여러분 오랫동안 합니다.* - [10 Immutable Laws of Security Administration](https://technet.microsoft.com/library/cc722488.aspx)  
  
Microsoft 가끔 보안 업데이트가 사이 출시 (이 업데이트 "대역" 라고도 함) 월별 보안 업데이트 있지만 보안 공지 매달 두 번째 화요일에 출시 취약점 고객의 시스템에 긴급 위험할 확인 합니다. 소규모 기업 시스템 및 응용 프로그램을 패치 관리 하려면 Windows 업데이트를 사용 하 여 Windows 컴퓨터 구성 든 대기업 관리 등 Configuration Manager SCCM (System Center) 소프트웨어를 사용 하 여 자세한, 계층 요금제에 따라 패치 배포 하는 대부분의 고객 비교적 적시에으로 Windows 인프라 패치.  
  
그러나 몇 인프라 Windows 컴퓨터와 Microsoft 응용 프로그램을 포함 되며 손상 된 환경에서 많기 조직의 패치 관리 전략 격차에 포함 되어 있습니다. 이러한 환경에서 시스템 Windows 패치 일관 됩니다. 비 Windows 운영 체제 전혀 하는 경우 가끔, 패치 됩니다. 상용 기존의 (COTS) 응용 프로그램이 있는 패치 있지만 적용 되지 않은 취약성 포함 되어 있습니다. 네트워킹 디바이스 자주 공장 기본 자격 증명으로 구성 된와 없이 펌웨어 업데이트 설치 후 년 합니다. 응용 프로그램 및 공급 업체에서 더 이상 지원 되지 않는 운영 체제는 종종 유지 자녀가 취약성에 대 한 패치 더 이상 수 있다는 사실을 불구 하 고 실행 합니다. 이러한 각 패치되지 시스템 잠재적인 진입점을 공격자를 나타냅니다.  
  
한 주도 IT가 직원에 도입 된 추가 문제를 해결할 소유 하 고 회사 다른 사람이 소유 했던된 데이터에 액세스할 수 디바이스를 사용 하는 있으며 조직 거의 제어할 수 없거나 직원의 개인 장치 구성 하 고 패치 있을 수 있습니다. 일반적으로 엔터프라이즈급 하드웨어 엔터프라이즈용 구성 옵션와의 각 사용자 지정 하 고 장치 선택 덜 선택 비용 관리 기능을 제공 됩니다. 하드웨어 직원 중심 광범위 한 제조업체, 업체, 보안 기능 하드웨어, 소프트웨어 보안 기능, 관리 기능 및 구성 옵션을 제공 하 고 다양 한 엔터프라이즈 기능 완전히 없을 수 있습니다.  
  
#### <a name="patch-and-vulnerability-management-software"></a>패치 및 취약성 관리  
패치되지 취약성 만들기 공격의 일부 효과적인 패치 관리 시스템을 Windows 시스템 및 Microsoft 응용 프로그램에 대 한 경우 해결 되었습니다. 그러나 비 Windows 시스템, Microsoft 응용 프로그램, 네트워크 infrastructure 및 직원 장치 유지 패치 및 기타 수정 사항에 대해 최신, 하지 않으면 인프라 취약 남아 있습니다. 경우에 따라 응용 프로그램의 공급 업체; 자동 업데이트 기능을 제공할 수 있습니다. 다른 앱에서 정기적으로 검색 하 고 패치 및 기타 수정 사항이 적용 접근 고안 해야 할 수 있습니다.
  
### <a name="outdated-applications-and-operating-systems"></a>오래 응용 프로그램 및 운영 체제  
*"6 개월 역사 공격 으로부터 보호 살 6 운영 체제를 받을 수 있습니다."* 정보 보안 Professional 10 년 이상의 경험 고정 enterprise 설치  
  
하지만 "get 현재, 최신" 위험 많은 조직에서 만들기 마케팅 구문을, 오래 된 운영 체제 및 응용 프로그램 처럼 보일 수 IT 인프라 합니다. 2003에 출시 된 운영 체제는 공급 업체에 의해 지원 및 여전히 운영 체제가 운영 체제의 최신 버전의 추가 보안 기능을 포함 되지 않을 수 있지만 해당 주소의 취약성에 대 한 업데이트와 함께 제공 된 될 수 있습니다. 오래 된 시스템 특정 AD DS 보안 구성 된 컴퓨터의 덜 기능을 지원 하기 위해 약화 필요할 수 있습니다.  
  
일반적으로 응용 프로그램 지원 더 이상 하는 공급 업체에서 레거시 인증 프로토콜을 사용 하 여 작성 된 응용 프로그램이 강력한 인증 메커니즘을 지원 하기 위해 retooled 수 없습니다. 그러나 회사의 Active Directory 도메인 LAN Manager 해시 하거나 해독된 가능한 이러한 응용 프로그램을 지원 하기 위해 암호를 저장 하도록 여전히 구성할 수 있습니다. 새로운 운영 체제의 소개 하기 전에 기록 응용 프로그램 잘 또는 전혀 현재 운영 체제, 조직이 이전와 오래 된 시스템 유지 하 고 일부 경우에, 완전히 지원 되지 않는 하드웨어 및 소프트웨어에서 작동 하지 않을 수 있습니다.  
  
에 조직 도메인 컨트롤러 Windows Server 2012, Windows Server 2008 R2 또는 Windows Server 2008 업데이트의 경우에도 멤버의 중요 한 부분 (는 일반 지원에서 더 이상) Windows Server 2003을 실행 중 이어야 서버 인구 찾거나도 일반적인은 Windows 2000 Server 또는 사항 서버 (하지 않은 완전히 지원). 조직 노화 시스템 유지 오래, 더 기능 집합 간의 차이 증가 함에 따라 되 고 프로덕션 시스템 지원 되지 것입니다 사용할수록 됩니다. 또한, 오래 된 Active Directory 숲 유지 됩니다, 그리고 더 기존 시스템 및 응용 프로그램에서 업그레이드 계획 누락 관찰 했습니다. 이의 레거시 프로토콜로 및 인증 메커니즘을 지원 하도록 구성 된 Active Directory 하기 때문에 단일 응용 프로그램을 실행 하는 하나의 컴퓨터에서 도메인 또는 숲 전체 취약 해질 수 있다는 의미 합니다.  
  
기존 시스템 및 응용 프로그램을 제거 하려면 식별 카탈로그를 켜고 다음를 업그레이드 하거나 교체 응용 프로그램이 나 호스트 여부를 결정할에서 먼저 포커스 해야 합니다. "창의적인 소멸" 이라는 개념이 활용할 수 있도록 수도 매우 특수 응용 프로그램은 지원 지도 업그레이드 경로를 교체 찾기 어려울 수 있지만 새로운 응용 프로그램과 관련 필요한 기능을 제공 하는 레거시 응용 프로그램 교체 해야 합니다. [손상에 대 한 계획](../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/Planning-for-Compromise.md) 뒤에 나오는 "손상 계획"에 더 자세히 설명 되어 있습니다.  
  
### <a name="misconfiguration"></a>잘못 구성  
*법률에 따라 4 번호: 많은 것으로 시작 하지 보호 된 컴퓨터에서 보안 업데이트를 설치 하는 일은 합니다.* - [10 Immutable Laws of Security Administration](https://technet.microsoft.com/library/cc722488.aspx)  
  
현재와 패치 시스템 유지 일반적으로 환경에도 저희 일반적으로 식별 격차 또는 운영 체제의 구성 오류 컴퓨터를 켜고 Active Directory를 실행 하는 응용 프로그램 합니다. 일부 구성 오류 손상, 로컬 컴퓨터에만 제공 되지만 공격자 일반적으로 다른 시스템 전반에서 그리고 Active directory 손상 더 전파에 집중 하는 컴퓨터 "소유 하 고," 후 합니다. 다음은 몇 가지 일반적인 영역 구성 위험을 소개 하는 식별 했습니다.  
  
#### <a name="in-active-directory"></a>Active Directory에  
대상 공격자가 가장 자주 하는 계정 Active Directory에은 도메인 관리자 (DA), Enterprise 관리자 (EA) 또는 Active Directory에 기본 제공 (모음) 관리자가 그룹의 회원 등 가장 많이 권한이 있는 그룹의 회원입니다. 제한 된 이러한 그룹의 공격 되도록 이러한 그룹의 회원 최소 개수의 가능한 계정에 줄어드는 합니다. 것도 가능이 권한이 있는 그룹;의 "영구" 구성원 제거 즉, 해당 도메인 및 숲 전체 권한이 필요한 경우에 일시적으로 이러한 그룹을 채울 수 있도록 설정 구현할 수 있습니다. 매우 권한이 있는 계정을 사용 하는 도메인 컨트롤러 또는 안전 하 게 관리 호스트 같은 지정, 보안 시스템에만 사용 해야 합니다. 제공 되는 자세한 정보를이 구성의 모든 구현 하는 데 도움이 [Active Directory 공격 줄이기](../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/Reducing-the-Active-Directory-Attack-Surface.md)합니다.  
  
Active Directory에 있는 가장 높은 권한이 있는 그룹의 회원, 평가 일반적으로 대부분 권한이 그룹의 모든 세에서 과도 하 게 멤버십을 찾을 했습니다. 경우에 따라 조직에는 DA 그룹의 계정 수백 닫힙니다. 조직 해당 그룹을 생각 기본 관리자가 그룹에 직접 계정을 배치 외의 경우에서 "권한" DAs 그룹 보다 작음 합니다. 그것이 아니야. 종종 사실을 알게 EA 그룹의 회원 영구 소수의 숲 루트 도메인 EA 권한 및 일시적으로 필요 거의 하다는 사실 불구 하 고 합니다. 세 그룹 모두에서 일상 관리자 계정 IT 사용자의 찾기 이기도 일반적인, 이것은 중복 효과적으로 구성 된 경우에 합니다. 에 설명 된 대로 [Active Directory 공격 줄이기](../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/Reducing-the-Active-Directory-Attack-Surface.md)계정을 영구적 소속 이러한 그룹 하나 또는 모두를 인지, 손상 시스템 AD DS 환경 및 계정 관리 하는 것도 삭제 하는 계정을 사용할 수 있습니다. 보안 구성과의 Active Directory 권한이 있는 계정 사용을 위한 권장 사항에 제공 된 [Active Directory 공격 줄이기](../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/Reducing-the-Active-Directory-Attack-Surface.md)합니다.  
  
#### <a name="on-domain-controllers"></a>도메인 컨트롤러에서  
도메인 컨트롤러 평가 자주 발견할 때 찾을 구성 하 고 구성원 서버 보다 더 다르게 관리할 수 있습니다. 때때로 도메인 컨트롤러 동일한 응용 프로그램 및 응용 프로그램은 표준 빌드의 일부 이므로 하지만 도메인 컨트롤러에 필요한 때문 구성원 서버에 설치 된 유틸리티를 실행 합니다. 이러한 응용 프로그램 도메인 컨트롤러에서 최소한의 기능을 제공할 수 있지만 구성 설정을 포트를 열어야 권한이 높은 서비스 계정, 만들거나 인증과 그룹 정책 응용 프로그램이 아닌 다른 목적 도메인 컨트롤러에 연결 하지 해야 하는 사용자가 시스템에 대 한 액세스 권한을 부여 하는 요구 하 여 크게 공격에 추가 합니다. 일부 위반 공격자 뿐만 아니라 도메인 컨트롤러에 액세스할 수 있지만를 수정 하거나 광고 DS 데이터베이스 손상 도메인 컨트롤러에 이미 설치 된 도구 사용 합니다.  
  
Internet Explorer 구성 설정을 도메인 컨트롤러의 압축을 풀려면 했습니다 사용자가 높은 수준의 권한 Active Directory에 있는 개인정보와 이용는 계정을 도메인 컨트롤러에서 인트라넷 고 인터넷에 액세스 하는 계정으로 로그온 한 찾을 했습니다. 어떤 경우에는 계정이 콘텐츠를 인터넷의 다운로드를 허용 하는 도메인 컨트롤러에서 Internet Explorer 설정을 구성 및 프리웨어 유틸리티 인터넷 사이트에서 다운로드 한 고 도메인 컨트롤러에 설치 합니다. Internet Explorer의 보안 강화 구성은 기본적으로 사용자와 관리자에 대 한 사용 하면서도 저희 자주 관찰 즉 관리자가 꺼졌습니다. 매우 권한이 있는 계정 인터넷에 연결 된 컴퓨터에 콘텐츠를 다운로드를 해당 컴퓨터 심각한 위험에 배치 됩니다. 컴퓨터가 도메인 컨트롤러 때 전체 광고 DS 설치 위험에 배치 됩니다.  
  
##### <a name="protecting-domain-controllers"></a>도메인 컨트롤러 보호  
도메인 컨트롤러 중요 한 인프라 구성으로 처리 엄격 더 보안 고 파일, 인쇄 및 응용 프로그램 서버 보다 엄격히 구성 수 해야 합니다. 도메인 컨트롤러 도메인 컨트롤러 공격 으로부터 보호 하지 또는 기능을 도메인 컨트롤러에 필요 하지 않은 소프트웨어를 실행 해야 합니다. 도메인 컨트롤러 인터넷에 액세스 하도록 허용 하지 하 고 보안 설정을 구성 하 고 그룹 정책 개체 (Gpo) 하 여 실행 해야 합니다. 보안 설치 구성과 도메인 컨트롤러의 관리에 대 한 자세한 추천에 제공 된 [공격 으로부터 도메인 컨트롤러 보안](../../../ad-ds/plan/security-best-practices/Securing-Domain-Controllers-Against-Attack.md)합니다.  
  
#### <a name="within-the-operating-system"></a>운영 체제  
*법률에 따라 두: 악성 운영 체제를 컴퓨터에 변경할 수 없는 경우 컴퓨터 더 이상 합니다.* - [Ten Immutable Laws of Security (Version 2.0)](https://technet.microsoft.com/security/hh278941.aspx)  
  
일부 조직 만드는 다양 한 종류의 서버에 대 한 초기 구성 하 고 설치 되는 운영 체제 제한 된 사용자 지정할 수 있도록, 있지만 분석 손상된 환경에 많은 서버 특별 방식에서 배포 하 고 수동으로 및 독립적으로 구성 자주 파악 합니다. 같은 기능을 수행 두 서버 구성 양 서버 안전 하 게 구성를 완전히 다른 수 있습니다. 서버 구성 기준 수 일관 되 게 적용 있지만 일관 되 게 잘못 구성; 반대로 즉, 특정 형식의 모든 서버에 동일한 취약성을 생성 하는 방식에서 서버 구성 됩니다. 동일한 로컬 자격 증명 시스템과 무단으로 응용 프로그램 및 자체의 취약 해질 유틸리티 허가 설치에서 사용 하 여 과도 하 게 권리와 계정 (특히 서비스 계정)에 대 한 권한을 부여 하세요, 잘못 보안 기능을 해제 하는 등 관행 포함 됩니다.  
  
##### <a name="disabling-security-features"></a>보안 기능을 사용 하지 않도록 설정  
때때로 조직 고급 보안 (WFAS)와 Windows 방화벽 사용 안 함 WFAS 구성 하기 어려운 또는 클라우드를 많이 사용 구성 필요한 믿음 활용 합니다. 그러나 부터는 Windows Server 2008 경우 역할 또는 기능 서버에 설치 되어, 역할에 제대로 작동 하도록 기능이 필요한 최소 권한으로 기본적으로 구성 되어 있고 역할 또는 기능을 지원 하기 위해 Windows 방화벽 자동으로 구성 됩니다. WFAS 사용 하지 않도록 설정 합니다 (그리고 제자리에 호스트 기반 다른 방화벽을 사용 하지), 여 조직 전체 Windows 환경의 공격을 늘립니다. Perimeter firewalls provide some protection against attacks that directly target an environment from the Internet, but they provide no protection against attacks that exploit other attack vectors such as [drive-by download](https://www.microsoft.com/security/sir/glossary/drive-by-download-sites.aspx) attacks, or attacks that originate from other compromised systems on the intranet.  
  
서버 관리 담당자 찾기 화면의 지시에 방해가 때문에 사용자 계정 컨트롤 UAC () 설정은 때때로 사용할 수 없습니다. Although [Microsoft Support article 2526083](https://support.microsoft.com/kb/2526083) describes scenarios in which UAC may be disabled on Windows Server, unless you are running a server core installation (where UAC is disabled by design), you should not disable UAC on servers without careful consideration and research.  
  
다른 경우, 서버 설정 보안이 약한 값 조직 오래 서버 구성 설정을 운영 체제의 변경 사항을 반영 하기 위해 기준을 변경 하지 않고 Windows Server 2012, Windows Server 2008 R2 또는 Windows Server 2008, 실행 중인 컴퓨터에 Windows Server 2003 초기 적용 하는 새 운영 체제에 적용 되도록 구성 됩니다. 이전 서버 초기를 새 운영 체제로 달성 새 운영 체제를 배포 하는 경우 대신 보안 변경 및 관련 하 고 새 운영 체제에 대 한 적절 한 구현 설정 되어 있는지 확인 하려면 구성 설정을 검토 하 고 있습니다.  
  
##### <a name="granting-excessive-privilege"></a>과도 하 게 권한을 부여  
평가 우리 거의 모든 환경에서 Windows 시스템에서 및 도메인 기반 로컬 계정 과도 하 게 권한을 부여 됩니다. 사용자가 자신의 워크스테이션에서 로컬 관리자 권한이 부여 됩니다, 구성원 서버 실행 해야 하는 기능을 이상 권한으로 구성 된 서비스 및 닫힙니다 또는 수백 지역 및 도메인 계정을 서버에서 로컬 관리자가 그룹 포함 합니다. 컴퓨터에서 하나만 권한이 있는 계정 손상 될 공격자 모든 사용자 및 서비스 하 고 다른 시스템 손상 전파 수집 및 활용 하는 방법 자격 증명을 컴퓨터에 로그온 하는 계정 손상 시킬 수 있게 합니다.  
  
단계-the-해시 (PTH) 및 기타 자격 증명 도용의 공격은 어디에서 나 오늘 쉽게 무료로 사용할 수 있는 도구는 때문에 이며 되지만의 시스템에 침투 하면 권한 있는 다른 계정 자격 증명 추출 하기 쉬운 얻었습니다 관리자 또는 시스템 수준 컴퓨터에 액세스 하는 합니다. 자격 증명 로그온 세션에서의 수집 수 있는 도구를 않고도 컴퓨터에 액세스 권한을된 가진 공격자 키 입력, 스크린샷, 하 고 클립보드를 캡처하는 키 입력 거를 쉽게 설치할 수 있습니다. An attacker with privileged access to a computer can disable antimalware software, install rootkits, modify protected files, or install malware on the computer that automates attacks or turns a server into a [drive-by download](https://www.microsoft.com/security/sir/glossary/drive-by-download-sites.aspx) host.  
  
확장 한 컴퓨터 이상 위반 하는 데는 전략 다르지만 손상 전파 키는 추가 시스템에 대 한 액세스 권한이 높은 인수 합니다. 모든 시스템에 액세스 권한이 있는 계정 수를 줄일, 해당 컴퓨터의 컴퓨터에서 자격 증명 소중한 수집 공격자 가능성도 공격을 줄일 수 있습니다.  
  
##### <a name="standardizing-local-administrator-credentials"></a>로컬 관리자 자격 증명을 표준화합니다.  
Windows 컴퓨터에서 로컬 관리자 계정 이름 바꾸기에 값 있는지 여부에으로 보안 전문가 사이에서 논의 오래 되었습니다. 로컬 관리자 계정에 대 한 중요 한 실제로 여러 컴퓨터와 동일한 사용자 이름과 암호 구성 여부.  
  
서버에 대해 동일한 값 로컬 관리자 계정을 라고 하는 경우도 계정에 할당 암호 같은 값으로 구성 되어 공격자 계정의 자격 증명에는 관리자 또는 시스템 수준의 액세스 가져온 한 컴퓨터에서 압축 풀기 수 있습니다. 관리자 계정; 손상 처음 하지 않아도 공격자 로컬 시스템 또는 관리자 권한으로 실행 하도록 구성 된 서비스 계정 또는 로컬 관리자가 그룹의 회원 인 사용자 계정이 손상만 시 키 필요 합니다. 다음 공격자가 관리자 계정 자격 증명을 추출 하 고 네트워크에 있는 다른 컴퓨터에 로그온 할 네트워크에서에서 해당 자격 증명을 재생할 수 있습니다.  
  
다른 컴퓨터에 같은 사용자 이름 및 암호 (또는 암호 해시) 제공 되는 계정 자격 증명으로 로컬 계정, 로그온 시도가 성공 및 공격자 얻고 대상으로 컴퓨터에 액세스 권한을된 합니다. In current versions of Windows, the built-in Administrator account is [disabled by default](https://technet.microsoft.com/library/cc753450.aspx), but in legacy operating systems, the account is enabled by default.  
  
> [!NOTE]  
> 일부 조직 다른 모든 권한을된 계정 시스템 잠긴 경우에 "안전" 제공이 믿음 사용 하도록 설정 로컬 관리자 계정을 구성 의도적으로 했습니다. However, even if the local Administrator account is disabled and there are no other accounts available that can enable the account or log on to the system with Administrator privileges, the system can be booted into safe mode and the built-in local Administrator account can be re-enabled, as described in [Microsoft Support article 814777](https://support.microsoft.com/kb/814777). 또한 시스템 Gpo 성공적으로 적용을 일시적으로 다시 사용 하도록 설정 하려면 관리자 계정을 GPO 수정할 수 있는 또는 제한 된 그룹 로컬 관리자가 그룹에 따라 도메인 계정을 추가 하려면 구성할 수 있습니다. 수리 수행할 수 있는 및 관리자 계정을 다시 비활성화할 수 있습니다. 기본 제공 로컬 관리자 계정 자격 증명을 사용 하는 긴 손상을 효과적으로 방지 하려면 고유한 사용자 이름 및 암호 로컬 관리자 계정에 대해 구성 되어야 합니다. To deploy unique passwords for local Administrator accounts via a GPO, see [Solution for management of built-in Administrator account's password via GPO](https://technet.microsoft.com/mt227395.aspx) on technet.  
  
##### <a name="permitting-installation-of-unauthorized-applications"></a>허용 무단으로 응용 프로그램을 설치  
*법률 첫째,는 수 유도할 컴퓨터에서 자신의 프로그램을 실행할 수 없는 경우 컴퓨터 곳을 단독 더 이상 합니다.* - [Ten Immutable Laws of Security (Version 2.0)](https://technet.microsoft.com/security/hh278941.aspx)  
  
허용할지 여부를 조직 배포 서버에 대해 일관 되 게 초기 설정 응용 프로그램에 정의 된 역할은 서버에 속하지 않는 설치 되지 않습니다. 서버의 지정 된 기능에 속하지 않는 소프트웨어를 설치할 수 있으므로, 서버 서버의 공격 늘리거나 응용 프로그램의 취약성을 소개 시스템 안정성 문제를 발생 하는 소프트웨어의 설치 실수로 또는 악성에 표시 됩니다.  
  
#### <a name="applications"></a>응용 프로그램  
앞에서 설명한 대로 응용 프로그램 자주 설치 되 고 응용 프로그램 보다 더 많은 권한을 요구 실제로 허가 된 계정을 사용 하도록 구성 합니다. 경우에 따라 응용 프로그램의 설명서 지정 서비스 계정 해야 하는 서버의 로컬 관리자가 그룹의 회원 또는 로컬 시스템의 상황에 맞는에서 실행 하도록 설정 해야 합니다. 가 자주 하지 때문 응용 프로그램은 이러한 권한에 필요 응용 프로그램 서비스 계정이 필요 추가 시간과 노력에 투자가 필요 어떤 권한과 확인 하기 때문입니다. 응용 프로그램 최소 요구 작동 하도록 응용 프로그램 및 구성 된 기능에 대 한 권한으로 설치 되지 않으면, 시스템 공격 자체에서 운영 체제에 대해 공격 없이 권한을 응용 프로그램을 활용 하 게 표시 됩니다.  
  
### <a name="lack-of-secure-application-development-practices"></a>보안 응용 프로그램 개발 방법 부족  
비즈니스 작업을 지원 하기 위해 인프라 존재 합니다. 이러한 작업은 사용자 지정 응용 프로그램을 구현 하는 것이 중요 하며, 보안 유용한 정보를 사용 하 여 응용 프로그램은 개발 있는지 확인 합니다. 엔터프라이즈 문제의 근본 원인을 분석 초기 손상 사용자 지정을 통해 영향는 자주 표시 응용 프로그램 특히 않은 인터넷 연결입니다. 공격 크로스 사이트 (XSS 스크립트) 및 대부분 이러한 손상의 유명 공격 SQL 삽입 (SQLi) 등의 통해 수행 됩니다.  
  
SQL 삽입 사용자 정의 입력 실행 데이터베이스에 전달 된 SQL 문을 수정할 수 있게 하는 응용 프로그램 취약점입니다. 이 입 응용 프로그램, 매개 (예: 쿼리 문자열 또는 쿠키) 또는 다른 방법 필드를 통해 제공할 수 있습니다. 이 삽입 결과 SQL 정책 데이터베이스에 제공 되는 의도 어떤 개발자 기본적으로 다른입니다. 예를 들어, 사용자 이름/암호 조합이 평가에 사용 되는 일반적인 쿼리를 취하십시오.  
  
`SELECT userID FROM users WHERE username = 'sUserName' AND password = 'sPassword'`  
  
이 데이터베이스 서버에서 수신 되 면 사용자 테이블 살펴보고 사용자 이름 및 암호 일치 하는 아마도 (일종의 로그인 형식)를 통해 사용자가 제공 하는 것 사용자 Id 레코드가 반환 하는 서버를 하도록 합니다. 자연스럽 개발자 의도 경우 반환 하는 것만 유효한 기록 올바른 사용자 이름 및 암호 사용자가 제공 될 수 있습니다. 중 하나를 잘못 입력 데이터베이스 서버를 일치 하는 기록 찾아 빈 결과가 반환 됩니다.  
  
문제가 발생 공격자가 예기치 않은 자신의 SQL 대신 유효한 데이터를 제공 하는 등을 수행 합니다. SQL 해석된에서 즉시 데이터베이스 서버 때문에 개발자 자신에 추가 해야 하는 경우 삽입된 코드 처리할 수 있습니다. 예를 들어, 공격자 입력 **관리자** 사용자 id와 **xyz** 또는 **1 = 1** 결과 정책 데이터베이스에 의해 처리 것으로 암호를:  
  
`SELECT userID FROM users WHERE username = 'administrator' AND password = 'xyz' OR 1=1`  
  
데이터베이스 서버,이 쿼리를 처리 하는 경우 모든 표 행 반환 됩니다 쿼리에 1 = 1는 항상 평가를, 따라서 때문에 올바른 사용자 이름 및 암호 알 수 없거나 제공 되는 경우 중요 하지 않습니다. 대부분의 경우 그 결과, 사용자의 데이터베이스의 첫 번째 사용자로 사용자 로그인 할 됩니다 되었습니다. 대부분의 경우, 관리자가 사용자 됩니다.  
  
간단 하 게 로그온, 잘못 SQL 문 추가 하는 데 사용이 같은 외에도 삭제 또는 데이터를 변경할 또는 전체 테이블 삭제 데이터베이스에서 삭제할 수 있습니다. SQLi 과도 하 게 권한은 함께 매우 경우에서 생성 새 사용자 공격 도구를 다운로드 하거나 선택 공격자의 다른 작업을 수행할 수 있도록 운영 체제 명령의 실행할 수 있습니다.  
  
사이트 간 스크립팅에서 취약점 응용 프로그램의 출력 도입 되었습니다. 응용 프로그램에 잘못 된 데이터를 제공 하는 공격자가로 시작 공격 하지만 잘못 된 데이터가 정품이 브라우저에서 실행 되는 (예: JavaScript) 스크립팅 코드의 형태로 경우에 합니다. XSS 취약성을 공격 공격자 사용자의 컨텍스트에서 대상 응용 프로그램의 모든 기능을 실행 하는 브라우저 시작 허용할 수 있습니다. XSS 공격 응용 프로그램에 연결 하 고 공격 코드를 실행 하는 링크를 클릭 하 여 사용자 피싱 메일을 통해 일반적으로 시작 됩니다.  
  
XSS 온라인 뱅킹 및 공격자 구매 하거나 악용된 사용자의 컨텍스트에서 이체 수 상거래 시나리오에서 자주 이용 됩니다. 사용자 지정 웹 기반 id 관리 응용 프로그램에는 대상된 공격의 경우 자신의 id를 만들고 사용 권한 및 권리를 수정 하 고 시스템 손상 시킬 수를 수 있습니다.  
  
사이트 간 스크립팅 고 SQL 삽입에 대 한 자세한 내용은이 문서의 범위를 벗어나는는 [열기 웹 응용 프로그램 보안 프로젝트 (OWASP)](https://www.owasp.org/index.php/Main_Page) 문제와 대책에 대 한 자세한 내용은 된 상위 10 목록을 게시 됩니다.  
  
보안 인프라에에서 투자를에 관계 없이 잘못 설계 된 및 필기 응용 프로그램 내에서 인프라에 배포 되는 경우 환경을 제조 공격에 취약. 더 잘 보안 인프라 자주 효과적인 대책 이러한 응용 프로그램 공격에 제공할 수 없습니다. 문제가 복합형으로 변환 디자인이 응용 프로그램 서비스 계정을 기능을 응용 프로그램에 대 한 과도 하 게 사용 권한을 부여 될 필요할 수 있습니다.  
  
Microsoft 보안 개발 주기의 (SDL) 초기 수집 및 응용 프로그램의 수명 주기를 통해 역할을 해제 될 때까지 확장 하 여 요구에에서 보안 시작 개선 하기 위해 노력 구조 프로세스 컨트롤 집합입니다. 효과적인 보안 컨트롤의이 통합이은 보안 측면에서 중요 한, 응용 프로그램 보안 비용 인지 확인 하는 중요 하 고 일정을 적용 합니다. 보안 문제에 대 한 응용 프로그램 효과적으로 코드 완료 되 면 평가 하기 전에 또는 응용 프로그램 배포 된 후에 보안 응용 프로그램에 대 한 결정을 내릴 수 조직 필요 합니다. 조직 응용 프로그램 결함이 비용과 지연 헤드 생산에서 응용 프로그램 배포 하기 전에 해결을 위해 선택 하거나 응용 프로그램을 손상 조직 노출 알려진된 보안 결함이 있는 프로덕션에 배포할 수 있습니다.  
  
일부 조직 당 문제, 10, 000 $ 위의 프로덕션 코드에서 보안 문제를 수정 하는 전체 비용 놓고 코드 100, 000 줄 별로 10 개 이상의 심각한 문제가 효과적인 SDL 없이 개발 된 응용 프로그램은 평균적 수 있습니다. 많은 응용 프로그램에서 비용 신속 하 게 전달합니다. 반면, 많은 회사는 sdl 최종 코드 검토 단계에 코드의 100, 000 줄 별로 두 개 이상 덜 문제 벤치 마크를 설정 하 고 0 문제 생산에서 위험한 응용 프로그램에 대 한 것을 목표로 합니다.  
  
보안이 향상 됩니다 SDL 구현 수집 요구 사항에 초기 보안 요구 사항을 포함 하 여 응용 프로그램의 디자인 위협 위험한 응용 프로그램에 대 한 모델링 제공 효과적인 교육 및 개발자; 모니터링 필요 함 코드가 일관 표준과 관행 필요한 확인란의 선택을 취소 합니다. 프로그램 SDL의 효과 감소 비용을 개발, 배포을 유지 하 고, 응용 프로그램을 제거 하는 동안 응용 프로그램 보안에 크게 향상 된 기능입니다. Although a detailed discussion of the design and implementation of SDL is beyond the scope of this document, refer to the [Microsoft Security Development Lifecycle](https://www.microsoft.com/security/sdl/default.aspx) for detailed guidance and information.  
  


