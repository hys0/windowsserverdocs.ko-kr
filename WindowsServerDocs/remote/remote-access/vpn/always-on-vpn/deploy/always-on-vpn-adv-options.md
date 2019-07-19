---
title: Always On VPN 고급 기능
description: 이 배포에 제공 된 배포 시나리오 외에도 다른 고급 VPN 기능을 추가 하 여 VPN 연결의 보안 및 가용성을 향상 시킬 수 있습니다.
ms.assetid: 51a1ee61-3ffe-4f65-b8de-ff21903e1e74
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.date: 11/05/2018
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.reviewer: deverette
ms.openlocfilehash: c238e44b538a31be7b21d2e75f41ebbf7ec7a1c8
ms.sourcegitcommit: 1bc3c229e9688ac741838005ec4b88e8f9533e8a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68314329"
---
# <a name="advanced-features-of-always-on-vpn"></a>Always On VPN의 고급 기능

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**선행** Always On VPN 기술에 대해 알아보기](../always-on-vpn-technology-overview.md)
- [**그런** Always On VPN 배포 계획 시작](always-on-vpn-deploy-planning.md)

제공 된 배포 시나리오 외에도 다른 고급 VPN 기능을 추가 하 여 VPN 연결의 보안 및 가용성을 향상 시킬 수 있습니다. 예를 들어 이러한 구성 요소는 연결을 허용 하기 전에 연결 하는 클라이언트가 정상 상태 인지 확인 하는 데 도움이 될 수 있습니다.

## <a name="high-availability"></a>고가용성

고가용성을 위한 추가 옵션은 다음과 같습니다.

|옵션  |설명  |
|---------|---------|
|서버 복원 력 및 부하 분산     |고가용성을 요구 하거나 많은 수의 요청을 지 원하는 환경에서는 NPS (네트워크 정책 서버)를 실행 하 고 원격을 사용 하도록 설정 하는 여러 서버 간의 부하 분산을 사용 하 여 원격 액세스의 성능 및 복원 력을 높일 수 있습니다. 서버 클러스터링에 액세스 합니다.<p>관련 문서:<ul><li>[NPS 프록시 서버 부하 분산](../../../../../networking/technologies/nps/nps-manage-proxy-lb.md)</li><li>[클러스터에 원격 액세스 배포](https://docs.microsoft.com/windows-server/remote/remote-access/ras/cluster/deploy-remote-access-in-cluster)</li></ul>        |
|지리적 사이트 복원 력     |IP 기반 지리적 위치에 대해 Windows Server 2016에서 DNS와 함께 글로벌 Traffic Manager를 사용할 수 있습니다. 보다 강력한 지리적 부하 분산을 위해 Microsoft Azure Traffic Manager와 같은 글로벌 서버 부하 분산 솔루션을 사용할 수 있습니다.<p>관련 문서:<ul><li>[Traffic Manager 개요](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview)</li><li>[Microsoft Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager)</li></ul>         |

## <a name="advanced-authentication"></a>고급 인증

다음은 인증에 대 한 추가 옵션입니다.

|옵션  |설명  |
|---------|---------|
|비즈니스용 Windows Hello     |Windows 10에서는 비즈니스용 Windows Hello가 PC 및 모바일 디바이스에서 암호를 강력한 2단계 인증으로 바꿉니다. 이 인증은 장치에 연결 되 고 생체 인식 또는 PIN (개인 식별 번호)을 사용 하는 새로운 유형의 사용자 자격 증명으로 구성 됩니다.<p>Windows 10 VPN 클라이언트는 비즈니스용 Windows Hello와 호환 됩니다. 사용자가 제스처를 사용 하 여 로그인 한 후 VPN 연결은 인증서 기반 인증에 비즈니스용 Windows Hello 인증서를 사용 합니다.<p>관련 문서:<ul><li>[비즈니스용 Windows Hello](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-identity-verification)</li><li>기술 사례 연구: [Windows 10에서 비즈니스용 Windows Hello를 사용 하 여 원격 액세스를 사용 하도록 설정](https://msdn.microsoft.com/library/mt728163.aspx)</li></ul>         |
|Azure MFA (다단계 인증)     |Azure MFA에는 Windows VPN 인증 메커니즘과 통합할 수 있는 클라우드 및 온-프레미스 버전이 있습니다.<p>이 메커니즘의 작동 방식에 대 한 자세한 내용은 [Azure Multi-factor Authentication 서버와 RADIUS 인증 통합](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-server-radius)을 참조 하세요.         |

## <a name="advanced-vpn-features"></a>고급 VPN 기능

고급 기능에 대 한 추가 옵션은 다음과 같습니다.

|옵션  |설명  |
|---------|---------|
|트래픽 필터링     |VPN 클라이언트가 액세스할 수 있는 응용 프로그램을 적용 해야 하는 경우 VPN 트래픽 필터를 사용 하도록 설정할 수 있습니다.<p>자세한 내용은 [VPN 보안 기능](https://docs.microsoft.com/windows/access-protection/vpn/vpn-security-features)을 참조 하세요.         |
|앱 트리거 VPN     |특정 응용 프로그램이 나 응용 프로그램 유형을 시작할 때 자동으로 연결 되도록 VPN 프로필을 구성할 수 있습니다.<p>이 및 기타 트리거 옵션에 대 한 자세한 내용은 [VPN 자동 트리거 프로필 옵션](https://docs.microsoft.com/windows/access-protection/vpn/vpn-auto-trigger-profile)을 참조 하세요.         |
|VPN 조건부 액세스   |조건부 액세스 및 장치 규정 준수는 VPN에 연결 하기 전에 관리 장치가 표준을 충족 하도록 요구할 수 있습니다. VPN 조건부 액세스에 대 한 고급 기능 중 하나를 사용 하면 클라이언트 인증 인증서가 ' 1.3.6.1.4.1.311.87 '의 ' AAD 조건부 액세스 ' OID를 포함 하는 경우에만 VPN 연결을 제한할 수 있습니다.<p>VPN 연결을 제한 하려면 다음을 수행 해야 합니다.<ol><li>NPS 서버에서 **네트워크 정책 서버** 스냅인을 엽니다.</li><li>**정책** > **네트워크 정책**을 확장 합니다.</li><li>**VPN (가상 사설망) 연결** 네트워크 정책을 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택 합니다.</li><li>**설정** 탭을 선택 합니다.</li><li>**공급 업체 관련** 을 선택 하 고 **추가**를 선택 합니다.</li><li>**허용-인증서-OID** 옵션을 선택한 다음 **추가**를 선택 합니다.</li><li>**1.3.6.1.4.1.311.87** 의 AAD 조건부 액세스 OID를 특성 값으로 붙여넣은 다음 **확인** 을 두 번 선택 합니다.</li><li>**닫기** 및 **적용**을 차례로 선택 합니다.<p>이제 VPN 클라이언트가 단기 클라우드 인증서 이외의 다른 인증서를 사용 하 여 연결 하려고 하면 연결이 실패 합니다.</li></ol>조건부 액세스에 대 한 자세한 내용은 [VPN 및 조건부 액세스](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access)를 참조 하세요.   |


---
## <a name="blocking-vpn-clients-that-use-revoked-certificates"></a>해지 된 인증서를 사용 하는 VPN 클라이언트 차단
  
업데이트를 설치한 후 RRAS 서버는 인증을 위해 IKEv2 및 컴퓨터 인증서를 사용 하는 Vpn (예: 장치 터널 항상 사용 Vpn)에 대해 인증서 해지를 적용할 수 있습니다. 즉, 이러한 Vpn의 경우 RRAS 서버가 해지 된 인증서를 사용 하려고 하는 클라이언트에 대 한 VPN 연결을 거부할 수 있습니다.

**가용성**

다음 표에는 각 버전의 Windows에 대 한 수정 사항의 대략적인 릴리스 날짜가 나와 있습니다.

|운영 체제 버전 |릴리스 또는 릴리스 날짜 * |
|---------|---------|
|Windows Server, 버전 1903  |[KB4501375](https://support.microsoft.com/help/4501375/windows-10-update-kb4501375)  |
|Windows Server 2019<br />Windows Server, 버전 1809  |Q3, 2019  |
|Windows Server, 버전 1803  |Q3, 2019  |
|Windows Server, 버전 1709  |Q3, 2019  |
|Windows Server 2016, 버전 1607  |[KB4503294](https://support.microsoft.com/help/4503294/windows-10-update-kb4503294)  |
  
\*모든 릴리스 날짜는 일정 분기에 나열 됩니다. 날짜는 근사치 이며 예 고 없이 변경 될 수 있습니다. 업데이트를 릴리스할 때 릴리스에 대 한 링크가 릴리스 날짜를 대체 합니다.

**필수 구성 요소를 구성 하는 방법** 

1. Windows 업데이트를 사용할 수 있게 되 면 설치 합니다.
1. 사용 하는 모든 VPN 클라이언트 및 RRAS 서버 인증서에 CDP 항목이 있고 RRAS 서버가 각 Crl에 연결할 수 있는지 확인 합니다.
1. RRAS 서버에서 **VpnAuthProtocol** PowerShell cmdlet을 사용 하 여 **RootCertificateNameToAccept** 매개 변수를 구성 합니다.<br /><br />
   다음 예에서는이 작업을 수행 하는 명령을 나열 합니다. 예제에서 **CN = Contoso Root 인증 기관** 은 루트 인증 기관의 고유 이름을 나타냅니다. 
   ``` powershell
   $cert1 = ( Get-ChildItem -Path cert:LocalMachine\root | Where-Object -FilterScript { $_.Subject -Like "*CN=Contoso Root Certification Authority,*" } )
   Set-VpnAuthProtocol -RootCertificateNameToAccept $cert1 -PassThru
   ```
**IKEv2 컴퓨터 인증서를 기반으로 하는 VPN 연결에 대 한 인증서 해지를 적용 하도록 RRAS 서버를 구성 하는 방법**

1. 명령 프롬프트 창에서 다음 명령을 실행 합니다. 
   ```
   reg add HKLM\SYSTEM\CurrentControlSet\Services\RemoteAccess\Parameters\Ikev2 /f /v CertAuthFlags /t REG_DWORD /d "4"
   ```

1. **라우팅 및 원격 액세스** 서비스를 다시 시작 합니다.
  
이러한 VPN 연결에 대해 인증서 해지를 사용 하지 않도록 설정 하려면 **certauthflags = 2** 를 설정 하거나 **certauthflags** 값을 제거한 후 **라우팅 및 원격 액세스** 서비스를 다시 시작 합니다. 

**IKEv2 컴퓨터 인증서를 기반으로 하는 VPN 연결에 대 한 VPN 클라이언트 인증서를 해지 하는 방법**
1. 인증 기관에서 VPN 클라이언트 인증서를 해지 합니다.
1. 인증 기관에서 새 CRL을 게시 합니다.
1. RRAS 서버에서 관리 명령 프롬프트 창을 열고 다음 명령을 실행 합니다.
   ```
   certutil -urlcache * delete
   certutil -setreg chain\ChainCacheResyncFiletime @now
   ```

**IKEv2 컴퓨터 인증서 기반 VPN 연결에 대 한 인증서 해지가 작동 하는지 확인 하는 방법**  
>[!Note]  
> 이 절차를 사용 하기 전에 CAPI2 작업 이벤트 로그를 사용 하도록 설정 해야 합니다.
1. 이전 단계에 따라 VPN 클라이언트 인증서를 해지 합니다.
1. 해지 된 인증서가 있는 클라이언트를 사용 하 여 VPN에 연결 해 봅니다. RRAS 서버에서 연결을 거부 하 고 "IKE 인증 자격 증명을 사용할 수 없습니다."와 같은 메시지를 표시 해야 합니다.
1. RRAS 서버에서 이벤트 뷰어를 열고 **응용 프로그램 및 서비스 Logs/Microsoft/Windows/CAPI2**로 이동 합니다. 
1. 다음 정보가 있는 이벤트를 검색 합니다.
   * 로그 이름: **Microsoft-CAPI2/운영 CAPI2/Operational**
   * 이벤트ID: **41** 
   * 이 이벤트에는 다음 텍스트가 포함 됩니다. **subject = "*클라이언트 fqdn*"** (*클라이언트 fqdn* 은 해지 된 인증서가 있는 클라이언트의 정규화 된 도메인 이름을 나타냄) 

   이벤트 **<Result>** 데이터의 필드에는 **인증서가 해지 됩니다 .가**포함 되어야 합니다. 예를 들어 이벤트에서 다음 발췌를 참조 하십시오.
   ```xml
   Log Name:      Microsoft-Windows-CAPI2/Operational Microsoft-Windows-CAPI2/Operational  
   Source:        Microsoft-Windows-CAPI2  
   Date:          5/20/2019 1:33:24 PM  
   Event ID:      41  
   ...  
   Event Xml:
   <Event xmlns="http://schemas.microsoft.com/win/2004/08/events/event">
    <UserData>  
     <CertVerifyRevocation>  
      <Certificate fileRef="C97AE73E9823E8179903E81107E089497C77A720.cer" subjectName="client01.corp.contoso.com" />  
      <IssuerCertificate fileRef="34B1AE2BD868FE4F8BFDCA96E47C87C12BC01E3A.cer" subjectName="Contoso Root Certification Authority" />
      ...
      <Result value="80092010">The certificate is revoked.</Result>
     </CertVerifyRevocation>
    </UserData>
   </Event>
   ```

---
## <a name="additional-protection"></a>추가 보호

### <a name="trusted-platform-module-tpm-key-attestation"></a>TPM (신뢰할 수 있는 플랫폼 모듈) 키 증명

TPM-증명 된 키를 사용 하는 사용자 인증서는 내보내기, 공세 및 TPM에서 제공 하는 키 격리에 의해 백업 되는 더 높은 보안 보증을 제공 합니다.

Windows 10의 TPM 키 증명에 대 한 자세한 내용은 [Tpm 키 증명](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/component-updates/tpm-key-attestation)을 참조 하세요.

## <a name="next-step"></a>다음 단계

[ALWAYS ON VPN 배포 계획을 시작 합니다](always-on-vpn-deploy-planning.md). 를 VPN 서버로 사용 하려는 컴퓨터에 원격 액세스 서버 역할을 설치 하기 전에 다음 작업을 수행 합니다. 적절 한 계획 후에 Always On VPN을 배포 하 고, 선택적으로 Azure AD를 사용 하 여 VPN 연결에 대 한 조건부 액세스를 구성할 수 있습니다.  

## <a name="related-topics"></a>관련 항목
- [NPS 프록시 서버 부하 분산](../../../../../networking/technologies/nps/nps-manage-proxy-lb.md): VPN (가상 사설망) 서버 및 무선 액세스 지점과 같은 네트워크 액세스 서버인 RADIUS (원격 인증 전화 접속 사용자 서비스) 클라이언트는 연결 요청을 만들고 NPS와 같은 RADIUS 서버에 보냅니다. 경우에 따라 NPS 서버에서 한 번에 너무 많은 연결 요청을 수신 하 여 성능이 저하 되거나 오버 로드 될 수 있습니다.

- [Traffic Manager 개요](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview): 이 항목에서는 서비스 끝점에 대 한 사용자 트래픽의 배포를 제어할 수 있는 Azure Traffic Manager의 개요를 제공 합니다. Traffic Manager는 DNS (Domain Name System)를 사용 하 여 트래픽 라우팅 메서드 및 끝점의 상태를 기준으로 클라이언트 요청을 가장 적절 한 끝점으로 보냅니다. 

- [비즈니스용 Windows Hello](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-identity-verification): 이 항목에서는 클라우드 전용 배포 및 하이브리드 배포와 같은 필수 구성 요소를 제공 합니다.  또한이 항목에서는 비즈니스용 Windows Hello에 대 한 질문과 대답을 제공 합니다.

- [기술 사례 연구: Windows 10](https://msdn.microsoft.com/library/mt728163.aspx)에서 비즈니스용 windows Hello를 사용 하 여 원격 액세스를 사용 하도록 설정: 이 기술 사례 연구에서는 Microsoft에서 비즈니스용 Windows Hello를 사용 하 여 원격 액세스를 구현 하는 방법에 대해 알아봅니다.  비즈니스용 Windows Hello는 암호를 초과 하는 조직과 소비자를 위한 개인/공개 키 또는 인증서 기반 인증 방법입니다. 이 인증 형태는 암호를 대체 하 고 위반, thefts 및 피싱에 대 한 저항력이 있는 키 쌍 자격 증명에 의존 합니다. 

- [Azure Multi-factor Authentication 서버와 RADIUS 인증 통합](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-server-radius): 이 항목에서는 Azure Multi-factor Authentication 서버를 사용 하 여 RADIUS 클라이언트 인증을 추가 하 고 구성 하는 과정을 안내 합니다. RADIUS는 인증 요청을 받고 해당 요청을 처리하는 표준 프로토콜입니다. Azure Multi-factor Authentication 서버는 RADIUS 서버 역할을 할 수 있습니다. 

- [VPN 보안 기능](https://docs.microsoft.com/windows/access-protection/vpn/vpn-security-features): 이 항목에서는 vpn 잠금, Windows Information Protection (WIP)와 VPN 통합 및 트래픽 필터에 대 한 VPN 보안 지침을 제공 합니다. 

- [VPN 자동 트리거 프로필 옵션](https://docs.microsoft.com/windows/access-protection/vpn/vpn-auto-trigger-profile): 이 항목에서는 앱 트리거, 이름 기반 트리거 및 Always On 같은 VPN 자동 트리거 프로필 옵션을 제공 합니다.

- [VPN 및 조건부 액세스](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access): 이 항목에서는 원격 클라이언트에 대 한 장치 준수 옵션을 제공 하기 위한 클라우드 기반 조건부 액세스 플랫폼의 개요를 제공 합니다. 조건부 액세스는 Azure AD(Azure Active Directory)에 연결된 응용 프로그램에 대한 액세스 규칙을 만드는 데 사용되는 정책 기반 평가 엔진입니다. 

- [TPM 키 증명](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/component-updates/tpm-key-attestation): 이 항목에서는 tpm (신뢰할 수 있는 플랫폼 모듈)에 대 한 개요와 TPM 키 증명을 배포 하는 단계를 제공 합니다. 문제 해결 정보 및 문제를 해결 하는 단계를 찾을 수도 있습니다.
