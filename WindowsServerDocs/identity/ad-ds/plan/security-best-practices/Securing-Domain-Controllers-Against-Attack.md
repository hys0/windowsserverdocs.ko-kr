---
ms.assetid: ba28bd05-16e6-465f-982b-df49633cfde4
title: "도메인 컨트롤러 공격 으로부터 보호합니다."
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: fc40d0ac536b128b799006214e360fa4d991ee44
ms.sourcegitcommit: 06a84f5caeab49b8480d6eed037aebbb59c77a9f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/14/2018
---
# <a name="securing-domain-controllers-against-attack"></a>도메인 컨트롤러 공격 으로부터 보호합니다.

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

*법률 숫자 3: 악성 무제한 물리적으로 액세스할 컴퓨터를 없는 경우 컴퓨터 더 이상 합니다.* - [Ten Immutable Laws of Security (Version 2.0)](https://technet.microsoft.com/security/hh278941.aspx)  
  
도메인 컨트롤러 실제 저장소 서비스와 효과적으로 서버, 워크스테이션, 사용자 및 응용 프로그램을 관리 하는 엔터프라이즈 수 있도록 하는 데이터 외에도 광고 DS 데이터베이스를 제공 됩니다. 해당 사용자 수 수정, 손상 또는 광고 DS 데이터베이스 소멸 악의적인 사용자가 도메인 컨트롤러에 대 한 액세스 권한을된 받은 경우 및 확장 프로그램의 모든 시스템 및 관리 Active Directory 하는 계정에서 합니다.  
  
도메인 컨트롤러에서 읽고 AD DS 데이터베이스에 있는 사람에 게 쓸 수, 하기 때문에 Active Directory 숲 절대 신뢰할 수 다시 알려진된 적절 한 백업을 사용 하 여 복구 하 고 손상 과정에서 허용 하 고 차이 닫을 수 있는 하지 않는 한 손상 도메인 컨트롤러의 의미 합니다.  
  
에 따라 공격자의 준비, 도구 및 기술을 수정 또는 광고 DS에도 중대 한 손상을 데이터베이스에 시간, 하지 며칠 또는 몇 주를 완료할 수 있습니다. Matters 되지 공격자가 Active Directory에 대 한 액세스 권한이 부여 된 하지만 가져온 공격자 권한에 액세스할 때 순간에 대 한 계획가 얼마나 얼마나 오래 합니다. 도메인 컨트롤러에 영향을 미치지 가장 도움이 경로를 액세스, 다양 한 배율 전파 또는 가장 직접적인 경로 소멸 구성원 서버, 워크스테이션 및 Active Directory를 제공할 수 있습니다. 이 인해 별도로 일반 Windows 인프라 보다 엄격 도메인 컨트롤러 확보 해야 합니다.  

  
## <a name="physical-security-for-domain-controllers"></a>도메인 컨트롤러에 대 한 보안 물리적  
이 섹션 실제로 도메인 컨트롤러 도메인 컨트롤러 물리적 인지 또는 datacenter 위치, 지사에서 및 기본 infrastructure 컨트롤만 사용 하 여 원격도 위치에서 가상 컴퓨터 보안에 대 한 정보를 제공 합니다.  
  
### <a name="datacenter-domain-controllers"></a>Datacenter 도메인 컨트롤러  
  
#### <a name="physical-domain-controllers"></a>실제 도메인 컨트롤러  
데이터 센터에 물리적 도메인 컨트롤러 보안 전용된 랙 또는 일반 서버에서 분리 되어 케이지 설치 해야 합니다. 가능 하면 신뢰할 수 있는 플랫폼 모듈 TPM () 칩이 있는 도메인 컨트롤러를 구성 해야 및 도메인 컨트롤러 서버에 모든 볼륨 BitLocker 드라이브 암호화를 통해 보호 해야 합니다. 일반적으로 BitLocker 성능 자리 비율로 헤드가 하지만 서버에서 디스크를 제거 하는 경우에 디렉터리 손상 으로부터 보호 합니다. BitLocker 부팅 파일을 수정 하 여 원래 바이너리 로드할 수 있도록 복구 모드로 부팅 하는 서버 하면 때문에 시스템 루트킷 등의 공격 으로부터 보호 수 있습니다. 도메인 컨트롤러 RAID, 직렬 attached SCSI 산/NAS 저장소, 소프트웨어를 사용 하도록 구성 된 또는 BitLocker 동적 볼륨 구현할 수 있습니다. (와 또는 하드웨어 RAID 제외) 로컬로 연결 된 저장소 가능 도메인 컨트롤러에 사용할 해야 합니다.  
  
#### <a name="virtual-domain-controllers"></a>가상 도메인 컨트롤러  
가상 도메인 컨트롤러를 구현 하는 경우 별도 실제 호스트 보다 다른 환경에서 가상 컴퓨터에서 도메인 컨트롤러 실행 하는 확인 해야 합니다. 사용 하는 경우에 제 3 자 virtualization 가상 도메인 컨트롤러 최소한의 공격을 제공 하는 Windows Server 2008 R2 또는 Windows Server 2012에서 Hyper-v 서버에 배포 하는 것이 좋습니다 플랫폼과 virtualization 호스트의 나머지 부분으로 관리 하는 대신 섬에는 도메인 컨트롤러를 사용 하 여 관리할 수 있습니다. Virtualization 인프라 관리에 대 한 시스템 센터 가상 컴퓨터 관리자 (SCVMM)를 구현할 경우 상주 하는 도메인 컨트롤러 가상 컴퓨터와 공인된 관리자에 게 자신 도메인 컨트롤러에서 물리적 호스트 위임 수 있습니다. 또한 스토리지 스토리지 관리자 가상 컴퓨터 파일에 액세스 하지 못하도록 가상 도메인 컨트롤러의 구분 하는 것이 좋습니다.  
  
### <a name="branch-locations"></a>분기 위치  
  
#### <a name="physical-domain-controllers"></a>실제 도메인 컨트롤러  
여러 서버 거주 있지만 datacenter 서버는 각도 물리적으로 보호 되지 않는 위치에 있는 모든 서버 볼륨 물리적 도메인 컨트롤러 TPM 칩 및 BitLocker 드라이브 암호화 구성 합니다. 도메인 컨트롤러 분기 위치에 있는 장소에 저장 될 수를 하는 경우 해당 위치의 Rodc 배포 하는 것이 좋습니다.  
  
#### <a name="virtual-domain-controllers"></a>가상 도메인 컨트롤러  
가능 하면 다른 가상 컴퓨터 사이트에 보다 별도 실제 호스트에서 지사에서 가상 도메인 컨트롤러를 실행 해야 합니다. 가상 도메인 컨트롤러 서버 가상 인구의 나머지에서 별도 실제 호스트에서 실행할 수 없는 지점에서는 TPM 칩 및 BitLocker 드라이브 암호화 호스트 가상 도메인 컨트롤러에 최소한을 실행 하 고 가능한 경우 모든 호스트에 구현 해야 합니다. 에 따라 지점의 크기와 물리적 호스트 보안 지사에서 Rodc 배포 고려해 야 합니다.  
  
### <a name="remote-locations-with-limited-space-and-security"></a>원격 위치 공간이 제한 및 보안  
인프라 실제 서버만 설치할 수 있는 위치를 포함 하는 경우 원격 위치에 virtualization 작업을 실행할 수 있는 서버의 설치 해야 하며 BitLocker 드라이브 암호화 서버에 있는 모든 볼륨 보호를 구성 합니다. 서버에서 가상 컴퓨터 한 호스트 별도 가상 컴퓨터도 실행 다른 서버와 RODC, 실행 해야 합니다. 제공 되는 쉽습니다 배포에 대 한 계획에 대 한 정보는 [전용 도메인 컨트롤러 계획 및 배포 가이드](https://go.microsoft.com/fwlink/?LinkID=135993)합니다. 배포 하 고 보안 하기 주기 가상화 도메인 컨트롤러에 대 한 자세한 내용은 참조 [Hyper-v의 도메인 컨트롤러 실행](https://technet.microsoft.com/library/dd363553(v=ws.10).aspx) TechNet 웹 사이트에서 합니다. 가상 컴퓨터를 보호 하 고 위임 가상 컴퓨터 관리를 참조 자세한 Hyper-v 강화 하기 위한 지침을는 [Hyper-v 보안 가이드](https://www.microsoft.com/download/details.aspx?id=16650) Microsoft 웹 사이트에서 바로 가기를 해결 방법입니다.  
  
## <a name="domain-controller-operating-systems"></a>도메인 컨트롤러 운영 체제  
최신 버전의 Windows Server 조직 내에 지원 되 고 제거 하는 도메인 컨트롤러 채우기에서 이전 운영 체제의 우선 순위를 지정 하는 모든 도메인 컨트롤러 실행 해야 합니다. 도메인 컨트롤러 현재 및 제거 레거시 도메인 컨트롤러 유지를의 새로운 기능을 사용 하지 못할 도메인 또는 숲 이전 운영 체제를 실행 하는 도메인 컨트롤러 관련 보안 기능 자주 사용할 수 있습니다. 도메인 컨트롤러 새로 설치 하 고 수준을 올린 되지 않고 됩니다 이전 운영 체제 또는 서버 역할;에서 업그레이드 즉, 하지 도메인 컨트롤러의 현재 위치에서 업그레이드를 수행 않거나 운영 체제가 설치 되어 없는 하지 갓 서버에서 광고 DS 설치 마법사를 실행 합니다. 새로 설치 된 도메인 컨트롤러를 구현 하 여 기존 파일 및 설정을 남아 있지 않습니다 실수로 도메인 컨트롤러에서 및 안전 하 고 일관 된 도메인 컨트롤러 구성 집행 간단 하 게 확인 합니다.  
  
## <a name="secure-configuration-of-domain-controllers"></a>보안 도메인 컨트롤러의 구성  
Gpo 이후 적용 될 수 있는 도메인 컨트롤러에 대 한 초기 보안 구성 기준은 만드는 여러 가지 무료로 사용할 수 있는 도구를 Windows에서 기본적으로 설치 중 일부를 사용할 수 있습니다. 이러한 도구는 다음과 같습니다.  
  
### <a name="security-configuration-wizard"></a>보안 구성 마법사  

모든 도메인 컨트롤러 초기 빌드 시 잠겨 해야 합니다. "기준 빌드와" 도메인 컨트롤러에서 서비스, 레지스트리, 시스템, 및 WFAS 설정을 구성할 수 Windows Server에서 기본적으로 제공 되는 보안 구성 마법사를 사용 하 여 수행할 수 있습니다. 설정은 저장 하 고를 도메인 컨트롤러 각 도메인 숲에서 도메인 컨트롤러의 일관성 있는 구성 적용 하기 위해 연결할 수 있는 GPO 내보낼 수 있습니다. 도메인 여러 버전의 Windows 운영 체제를 있으면 Windows WMI (Management Instrumentation) 필터 Gpo 해당 운영 체제의 버전을 실행 하는 도메인 컨트롤러에만 적용를 구성할 수 있습니다.  
  
### <a name="microsoft-security-compliance-manager"></a>Microsoft 보안 준수 관리자  
[Microsoft 보안 준수 관리자](https://technet.microsoft.com/library/cc677002.aspx) 도메인 컨트롤러 설정은를 배포 되 고 Gpo Active Directory에 도메인 컨트롤러 OU에 배포 적용 하는 도메인 컨트롤러에 대 한 전체 구성 기준 생성할 보안 구성 마법사 설정 함께 사용할 수 있습니다.  
  
### <a name="applocker"></a>AppLocker  
서비스 및 도메인 컨트롤러에서 실행 하도록 허가 된 응용 프로그램 구성 AppLocker 또는 제 3 자 응용 프로그램 whitelisting 도구를 사용 해야 하 고 이러한 허용된 응용 프로그램과 서비스 호스트 AD DS 및 DNS 하나 및 바이러스 백신 소프트웨어와 같은 시스템 보안 소프트웨어를 컴퓨터에 대 한 필요한 것의으로 구성 해야 합니다. 도메인 컨트롤러에서 응용 프로그램을 허용 whitelisting,으로 보안에 추가 보호 계층이 응용 프로그램을 실행할 수 없는 무단으로 응용 프로그램은 도메인 컨트롤러에 설치 하는 경우에 추가 됩니다.  
  
### <a name="rdp-restrictions"></a>RDP 제한  
모든 도메인 컨트롤러에 숲 속의 Ou에 연결 하는 그룹 정책 개체 권한이 있는 사용자와 시스템이 (예: 점프 서버) 에서만 RDP 연결을 허용 구성 합니다. 사용자 권한 설정 및 WFAS 구성 조합을 사용 하 여 수행할 수 있습니다 하 고 일관 되 게 정책이 적용 되도록 Gpo에서 구현 합니다. 사용 하지 않을 경우 다음 그룹 정책 새로 시스템 제대로 구성으로 되돌립니다.  
  
### <a name="patch-and-configuration-management-for-domain-controllers"></a>패치 및 도메인 컨트롤러에 대 한 구성 관리  
다른, 보일 수 있지만 도메인 컨트롤러 및 기타 중요 한 인프라 구성 요소 일반 Windows 인프라와는 별도로 패치 고려해 야 합니다. 인프라에 모든 컴퓨터에 대 한 엔터프라이즈 구성 관리 소프트웨어를 활용 하는 경우를 손상 시키거나 해당 소프트웨어에 의해 관리 하는 모든 인프라 구성 요소를 제거 손상 시스템 관리 소프트웨어를 사용할 수 있습니다. 일반적인 패치 및 시스템 관리 도메인 컨트롤러에 대 한 분리를 함으로써 뿐 아니라 긴밀 하 게 관리할 도메인 컨트롤러에 설치 된 소프트웨어의 양을 줄일 수 있습니다.  
  
### <a name="blocking-internet-access-for-domain-controllers"></a>도메인 컨트롤러에 대 한 인터넷 액세스 차단  

사용과 도메인 컨트롤러에서 Internet Explorer의 구성 검사 Active Directory 보안 Assessment의 일환으로 수행 하는 중 하나입니다. Internet Explorer (또는 다른 웹 브라우저)가 하지 사용할 도메인 컨트롤러에서 있지만 분석 도메인 컨트롤러의 수천에 따르면 많은 경우 권한이 있는 사용자에 게 Internet Explorer 조직의 인트라넷 또는 인터넷 검색 사용 합니다.  
  
"잘못" 섹션에 설명 된 대로 [손상 수단](../../../ad-ds/plan/security-best-practices/Avenues-to-Compromise.md), 조직의 보안에 위험이 있는 특별 한 제시 인터넷 (또는 감염된 인트라넷) (되는 기본적으로 로컬로 도메인 컨트롤러에 로그온 할 수만 계정) 권한이 높은 계정을 사용 하 여 Windows 인프라에 가장 강력한 컴퓨터 중 하나에서 검색 합니다. 맬웨어에 감염 "유틸리티" 다운로드 하거나 다운로드 하 여 드라이브를 통해 여부를 공격자 완전히 손상 되거나 삭제 Active Directory 환경 데 필요한 모든 항목에 대 한 액세스를 얻을 수 있습니다.  
  
Windows Server 2012, Windows Server 2008 R2, Windows Server 2008 및 최신 버전의 Internet Explorer 다양 한 악성 다운로드 로부터 보호를 제공, 있지만 대부분의 경우에 도메인 컨트롤러 및 권한이 있는 계정 사용 된 인터넷을 검색 하는 도메인 컨트롤러 Windows Server 2003을 실행 했다면 또는 보호 기능이 최신 운영 체제 및 브라우저 제공한 의도적 해제 되어 있습니다.  
  
웹 브라우저 도메인 컨트롤러에서 시작 작업이 금지 된 정책, 뿐 아니라 기술 컨트롤을 통해 및 도메인 컨트롤러 인터넷에 액세스 하도록 허용 해야 합니다. 도메인 컨트롤러 사이트 전체의 복제 하기 위해 필요한 사이트 간의 안전 하 게 연결 구현 해야 합니다. 이 문서의 범위를 벗어나는 자세한 구성 지침 이지만는 여러 가지 컨트롤이 오용 또는 잘못 구성 고 이후에 손상 도메인 컨트롤러의 기능이 제한 하려면 구현할 수 있습니다.  
  
### <a name="perimeter-firewall-restrictions"></a>주변 방화벽 제한  
방화벽 아웃 바운드 도메인 컨트롤러에서 인터넷에 연결 차단를 구성 합니다. 방화벽 간 통신에 제공 된 지침에 따라 허용할 구성할 수 있지만 도메인 컨트롤러 사이트 경계 교환 해야 할 수, [구성 방화벽 도메인 및 신뢰 하는 방법을](https://support.microsoft.com/kb/179442) Microsoft 지원 웹 사이트에서 합니다.  
  
### <a name="dc-firewall-configurations"></a>DC 방화벽 구성  

앞에서 설명한 대로 보안 구성 마법사 도메인 컨트롤러에 보안 고급와 Windows 방화벽에 대 한 설정을 구성 캡처를 사용 해야 합니다. 방화벽 구성 설정을 조직의 요구 사항을 충족 하 고 사용 하 여 Gpo 구성 설정을 적용 하려면 구현 보안 구성 마법사 출력을 검토 해야 합니다.  
  
### <a name="preventing-web-browsing-from-domain-controllers"></a>방지 도메인 컨트롤러에서 웹 검색  
AppLocker 구성과 "블랙홀" 프록시 구성을 WFAS 구성 조합해 도메인 컨트롤러 인터넷에 액세스 하 않도록 하 고 도메인 컨트롤러의 웹 브라우저의 사용을 방지 하기 위해 사용할 수 있습니다.  
  


