---
ms.assetid: ba28bd05-16e6-465f-982b-df49633cfde4
title: 공격으로부터 도메인 컨트롤러 보호
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 06/18/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 6be2899e85b68578518d9de1805c287367608163
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863094"
---
# <a name="securing-domain-controllers-against-attack"></a>공격으로부터 도메인 컨트롤러 보호

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

*법률 숫자 3: 악당 아무런 컴퓨터에 물리적으로 액세스를 제한 없이, 아닙니다 컴퓨터가 더 이상.* - [10 Immutable Laws of Security (버전 2.0)](https://technet.microsoft.com/security/hh278941.aspx)  
  
도메인 컨트롤러 서비스와 엔터프라이즈 서버, 워크스테이션, 사용자 및 응용 프로그램을 효과적으로 관리할 수 있도록 데이터를 제공 하는 것 외에도 AD DS 데이터베이스에 대 한 물리적 저장소를 제공 합니다. 악의적인 사용자가 도메인 컨트롤러에 대 한 권한 있는 액세스를 받은 경우 해당 사용자 수 수정, 손상, 데이터베이스를 삭제 하거나 AD DS 및 Active Directory에서 관리 되는 계정을 확인 하 고 시스템의 모든 확장입니다.  
  
도메인 컨트롤러에서 읽고 AD DS 데이터베이스에 아무 것도 쓸 수, 있으므로 손상 도메인 컨트롤러의 Active Directory 포리스트에 수 하지 수 간주 의미 신뢰할 수 있는 다시 알려진된 성공한 백업을 사용 하 여 복구할 수 있지 않은 경우 및 프로세스에는 이러한 타협을 허용 하는 간격을 닫습니다.  
  
공격자의 준비, 도구 및 기술, 수정 또는 AD DS에도 중대 한 손상을 따라 데이터베이스를 몇 분 일 나 주가 아닌 시간에 완료할 수 있습니다. 문제 되지 않는 사항 가져온 얼마나 공격자가 권한 있는 액세스 하는 경우 현재 계획 되어 있지만 공격자가 Active Directory에 대 한 액세스를 권한 있는 기간입니다. 도메인 컨트롤러를 손상 시 키 지는 광범위 한 전파 액세스에 가장 편리한 경로 또는 구성원 서버, 워크스테이션 및 Active Directory의 소멸을 가장 직접적인 경로 제공할 수 있습니다. 이 인해 도메인 컨트롤러를 개별적으로 및 일반 Windows 인프라 보다 더 엄격 하 게 보호 되어야 합니다.  

## <a name="physical-security-for-domain-controllers"></a>도메인 컨트롤러에 대 한 물리적 보안

이 섹션에서는 도메인 컨트롤러, 도메인 컨트롤러는 실제 인지 또는 데이터 센터 위치, 지점 및 기본 인프라 제어를 사용 하 여 원격 위치에서 가상 컴퓨터를 물리적으로 보호 하는 방법에 대 한 정보를 제공 합니다.  
  
### <a name="datacenter-domain-controllers"></a>데이터 센터 도메인 컨트롤러  
  
#### <a name="physical-domain-controllers"></a>실제 도메인 컨트롤러

데이터 센터의 실제 도메인 컨트롤러는 안전한 전용된 랙 또는 일반 서버 모집단 별도로 케이지도 설치 되어야 합니다. 가능 하면 도메인 컨트롤러 모듈 TPM (Trusted Platform) 칩을 사용 하 여 구성 해야 하 고 BitLocker 드라이브 암호화를 통해 도메인 컨트롤러 서버에서 모든 볼륨을 보호 해야 합니다. BitLocker는 일반적으로 자리 백분율로 성능 오버 헤드가 되지만 서버에서 디스크를 제거 하는 경우에 손상에 대 한 디렉터리를 보호 합니다. BitLocker 부팅 파일을 수정 하면 원본 이진 파일을 로드할 수 있도록 복구 모드로 부팅 서버가 있으므로 루트킷과 같은 공격 으로부터 시스템을 보호할 수 있습니다. 따라서 로컬로 연결 된 저장소 (RAID 하드웨어 없이 또는) 도메인 컨트롤러에 사용할 도메인 컨트롤러 소프트웨어 RAID, serial attached SCSI, SAN/NAS 저장소를 사용 하도록 구성 된 경우 동적 볼륨, BitLocker를 구현할 수 없습니다 때마다 가능 합니다.  
  
#### <a name="virtual-domain-controllers"></a>가상 도메인 컨트롤러 

가상 도메인 컨트롤러를 구현 하는 경우 도메인 컨트롤러에서 다른 가상 컴퓨터 환경에서 보다 별도 물리적 호스트에서 실행 해야 합니다. 타사 가상화 플랫폼을 사용 하는 경우에 Windows Server 2012 또는 공격 노출을 최소를 제공 하 고 호스팅하는 도메인 컨트롤러를 사용 하 여 관리할 수 있습니다 Windows Server 2008 R2에서 Hyper-v 서버의 가상 도메인 컨트롤러 배포를 고려합니다 보다는 가상화 호스트의 나머지 부분을 사용 하 여 관리 되는 합니다. 가상화 인프라의 관리를 위해 System Center Virtual Machine Manager (SCVMM)를 구현 하는 경우 도메인 컨트롤러 가상 머신을 있고 도메인 컨트롤러에 실제 호스트에 대 한 관리를 위임할 수 있습니다. 권한 있는 관리자에 게 자체입니다. 또한 저장소 관리자가 가상 머신 파일에 액세스 하지 못하도록 방지 하기 위해 가상 도메인 컨트롤러의 저장소를 분리 하는 것이 좋습니다.  
  
### <a name="branch-locations"></a>지점 위치  
  
#### <a name="physical-domain-controllers-in-branches"></a>분기에서 실제 도메인 컨트롤러

여러 서버에 하지만 데이터 센터 서버 보안이 유지 되는 정도를 물리적으로 보호 하지 않는 위치에서 모든 서버 볼륨에 대 한 실제 도메인 컨트롤러 TPM 칩과 BitLocker 드라이브 암호화를 사용 하 여 구성 되어야 합니다. 도메인 컨트롤러 방에 자물쇠를 분기 위치에 저장할 수 없습니다, 하는 경우 해당 위치에서 Rodc를 배포 하는 것이 좋습니다.  
  
#### <a name="virtual-domain-controllers-in-branches"></a>분기에서 가상 도메인 컨트롤러

가능 하면 사이트의 다른 가상 컴퓨터 보다 별도 물리적 호스트에 지사에서 가상 도메인 컨트롤러를 실행 해야 합니다. 가상 도메인 컨트롤러 가상 서버 모집단의 나머지 부분에서 별도 물리적 호스트에서 실행할 수 없습니다는 지점의 구현 해야 TPM 칩과 BitLocker 드라이브 암호화 최소한 실행 가상 도메인 컨트롤러를 호스트 하 고 모든 호스트에 가능한 경우 해당 합니다. 지점에 배치의 크기 및 실제 호스트의 보안에 따라 분기 위치에서 Rodc를 배포 해야 합니다.  
  
### <a name="remote-locations-with-limited-space-and-security"></a>제한 된 공간 및 보안을 사용 하 여 원격 위치

인프라만 단일 물리적 서버를 설치할 수 있습니다 위치에 포함 된 경우 가상화 워크 로드를 실행할 수 있는 서버는 원격 위치에서 설치 해야 하며 모든 보호 하도록 BitLocker 드라이브 암호화를 구성 해야 서버에서 볼륨입니다. 서버에 하나의 가상 컴퓨터가 호스트에서 별도 가상 머신으로 실행 하는 다른 서버를 사용 하 여 RODC를 실행 해야 합니다. RODC의 배포에서 제공 됩니다에 대 한 계획에 대 한 정보를 [읽기 전용 도메인 컨트롤러 계획 및 배포 가이드](https://go.microsoft.com/fwlink/?LinkID=135993)합니다. 배포 및 가상화 된 도메인 컨트롤러를 보호 하는 방법에 대 한 자세한 내용은 참조 하세요. [-Hyper-v에서 도메인 컨트롤러 실행](https://technet.microsoft.com/library/dd363553(v=ws.10).aspx) TechNet 웹 사이트입니다. 가상 컴퓨터 관리를 위임 하 고 가상 머신을 보호 참조 자세한 하이퍼-V를 강화 하기 위한 지침은 합니다 [Hyper-v 보안 가이드](https://www.microsoft.com/download/details.aspx?id=16650) Microsoft 웹 사이트는 Solution Accelerator입니다.  
  
## <a name="domain-controller-operating-systems"></a>도메인 컨트롤러 운영 체제

도메인 컨트롤러 채우기의 레거시 운영 체제의 서비스 해제 우선 순위를 지정 하는 조직 내에서 지원 Windows Server의 최신 버전에서 모든 도메인 컨트롤러를 실행 해야 합니다. 도메인 컨트롤러를 제거 하 고 현재 레거시 도메인 컨트롤러 유지, 하 여 자주 새로운 기능 및 보안 되지 사용할 수 있는 도메인 또는 포리스트 레거시 운영 체제를 실행 하는 도메인 컨트롤러를 사용 하 여 활용을 걸릴 수 있습니다. 도메인 컨트롤러 새로 설치 하 고 승격 되지 않고 됩니다 이전 운영 체제 또는 서버 역할 업그레이드 즉, 도메인 컨트롤러의 현재 위치 업그레이드를 수행 하거나 마십시오 운영 체제는 설치 되지 않은 새로 서버에서 AD DS 설치 마법사를 실행. 새로 설치 된 도메인 컨트롤러를 구현 하 여 기존 파일 및 설정 된 도메인 컨트롤러에서 실수로 남아 있지을 일관 되 고 안전한 도메인 컨트롤러 구성의 적용을 간소화를 확인 합니다.  
  
## <a name="secure-configuration-of-domain-controllers"></a>도메인 컨트롤러의 보안 구성

무료로 사용할 수 있는 도구를 Windows에서 기본적으로 설치 되는 일부 여러 Gpo를 통해 이후에 적용할 수 있는 도메인 컨트롤러는 초기 보안 구성 기준을 만드는 데 사용할 수 있습니다. 여기에 이러한 도구 설명 되어 있습니다.  
  
### <a name="security-configuration-wizard"></a>보안 구성 마법사  

모든 도메인 컨트롤러가 초기 빌드 시 잠겨 야 합니다. "기본 빌드" 도메인 컨트롤러에서 서비스, 레지스트리, 시스템 및 WFAS 설정을 구성 하려면 Windows Server에서 기본적으로 제공 되는 보안 구성 마법사를 사용 하 여 수행할 수 있습니다. 설정은 저장 하 고 도메인 컨트롤러의 일관 된 구성을 적용할 포리스트의 각 도메인에 도메인 컨트롤러 OU에 연결할 수 있는 GPO로 내보낼 수 있습니다. 도메인이 여러 버전의 Windows 운영 체제에 있으면 해당 버전의 운영 체제를 실행 하는 도메인 컨트롤러에만 Gpo를 적용 하려면 Windows Management Instrumentation (WMI) 필터를 구성할 수 있습니다.  
  
### <a name="microsoft-security-compliance-toolkit"></a>Microsoft 보안 규정 준수 도구 키트

[Microsoft 보안 규정 준수 도구 키트](https://www.microsoft.com/download/details.aspx?id=55319) 도메인 컨트롤러 설정을 배포 되 고 Gpo가 적용 되는 도메인 컨트롤러에 대 한 포괄적인 구성 기준을 생성 하기 위해 보안 구성 마법사 설정을 사용 하 여 결합할 수 Active Directory 도메인 컨트롤러 OU에 배포 합니다.  
  
### <a name="rdp-restrictions"></a>RDP 제한 사항

모든 도메인 컨트롤러는 포리스트에 있는 Ou에 연결 하는 그룹 정책 개체는 권한이 있는 사용자 및 시스템 (예: 점프 서버)에서 RDP 연결을 허용 하도록 구성 되어야 합니다. 이 WFAS 구성과 사용자 권한 설정의 조합을 통해 수행할 수 있습니다 및 정책을 일관 되 게 적용 되도록 Gpo에서 구현 해야 합니다. 사용 하지 않을 경우 다음 그룹 정책 새로 고침을 적절 한 구성으로 시스템을 반환 합니다.  
  
### <a name="patch-and-configuration-management-for-domain-controllers"></a>패치 및 도메인 컨트롤러에 대 한 구성 관리

들릴 수 있습니다, 있지만 도메인 컨트롤러와 일반 Windows 인프라와 별도로 다른 중요 한 인프라 구성 요소 패치를 적용 하는 것이 좋습니다. 인프라의 모든 컴퓨터에 대 한 엔터프라이즈 구성 관리 소프트웨어를 활용 하는 경우 시스템 관리 소프트웨어의 손상 손상 시키거나 파괴할 해당 소프트웨어에 의해 관리 되는 모든 인프라 구성 요소를 사용할 수 있습니다. 일반적인 인구에서 도메인 컨트롤러에 대 한 패치 및 시스템 관리를 분리 하 여 강력 하 게 관리를 제어 하는 것 외에도 도메인 컨트롤러에 설치 된 소프트웨어의 양을 줄일 수 있습니다.
  
### <a name="blocking-internet-access-for-domain-controllers"></a>도메인 컨트롤러에 대 한 인터넷 액세스를 차단합니다.  

Active Directory 보안 평가의 일부로 수행 되는 검사 중 하나를 사용 하 고 도메인 컨트롤러에서 Internet Explorer의 구성입니다. Internet Explorer (또는 다른 웹 브라우저) 해서는 안 도메인 컨트롤러에서 하지만 수천 개의 도메인 컨트롤러의 분석에 따르면 권한 있는 사용자 조직의 인트라넷 이동할 Internet Explorer를 사용 하는 다양 한 경우 또는 인터넷입니다.  
  
"잘못 된 구성" 섹션에 설명 된 대로 [손상 될 작업 환경](../../../ad-ds/plan/security-best-practices/Avenues-to-Compromise.md), 높은 사용 하 여 Windows 인프라의 가장 강력한 컴퓨터 중 하나에서 인터넷 (또는 감염 된 인트라넷) 검색 계정 (기본적으로 도메인 컨트롤러에 로컬로 로그온 할 수만 계정을은)는 조직의 보안 위험을 별도 작업을 표시 합니다. 또는 맬웨어 감염 된 "유틸리티"의 다운로드를 다운로드 하 여 드라이브를 통한 공격자가 완전히를 손상 시키거나 Active Directory 환경을 삭제 하는 데 필요한 모든 것에 대 한 액세스를 얻을 수 있습니다.  
  
Windows Server 2012, Windows Server 2008 R2, Windows Server 2008 및 현재 버전의 Internet Explorer 다양 한 대부분의 경우에 도메인 컨트롤러 및 권한 있는 계정을 사용한에 악성 다운로드에 대 한 보호를 제공 하지만 인터넷을 찾아보거나 도메인 컨트롤러가 Windows Server 2003 실행 중이 던 최신 운영 체제 및 브라우저에서 제공 하는 보호 의도적으로 해제 되어 있습니다.  
  
정책에 의해 뿐만 아니라 기술적 컨트롤에서 도메인 컨트롤러에서 웹 브라우저를 시작을 금지 되어야 합니다 및 인터넷에 액세스 하려면 도메인 컨트롤러를 허용 해서는 안 됩니다. 도메인 컨트롤러를 사이트 간 복제 해야 하는 경우 사이트 간에 보안 연결을 구현 해야 합니다. 자세한 구성 지침은이 문서의 범위 외부에 있지만 여러 오용 또는 잘못 구성 되어 이후에 손상에 대 한 도메인 컨트롤러의 능력을 제한 하는 컨트롤을 구현할 수 있습니다.  
  
### <a name="perimeter-firewall-restrictions"></a>경계 방화벽 제한 사항

경계 방화벽은 인터넷에 도메인 컨트롤러에서 아웃 바운드 연결을 차단 하도록 구성 되어야 합니다. 경계 방화벽에서 제공한 지침을 수행 하 여 사이트 간 통신을 허용 하도록 구성할 수 있습니다 도메인 컨트롤러에 사이트 경계를 넘어 전달할 필요 수는 없지만 [도메인 및 트러스트에대한방화벽을구성하는방법](https://support.microsoft.com/kb/179442) Microsoft 지원 웹 사이트입니다.  
  
### <a name="dc-firewall-configurations"></a>DC 방화벽 구성  

앞에서 설명한 대로 도메인 컨트롤러에서 고급 보안이 포함 된 Windows 방화벽에 대 한 구성 설정을 캡처하는 데 보안 구성 마법사를 사용 해야 합니다. 방화벽 구성 설정을 조직의 요구 사항을 충족 하 고 다음 Gpo를 사용 하 여 구성 설정을 적용할 되도록 보안 구성 마법사의 출력을 검토 해야 합니다.  
  
### <a name="preventing-web-browsing-from-domain-controllers"></a>도메인 컨트롤러에서 웹 검색 방지

도메인 컨트롤러는 인터넷에 액세스 하지 않도록 설정 하 고 도메인 컨트롤러에서 웹 브라우저 사용을 방지 하기 위해 AppLocker 구성, "블랙홀" 프록시 구성 및 WFAS 구성 조합을 사용할 수 있습니다.
