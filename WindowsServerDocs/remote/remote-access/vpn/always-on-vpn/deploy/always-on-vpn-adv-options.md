---
title: Always On VPN 고급 기능
description: 이 배포에 제공 된 배포 시나리오에서 초과 보안 및 VPN 연결의 가용성을 개선 하기 위해 기타 고급 VPN 기능을 추가할 수 있습니다.
ms.assetid: 51a1ee61-3ffe-4f65-b8de-ff21903e1e74
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.date: 11/05/2018
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.reviewer: deverette
ms.openlocfilehash: 5f43d64dc7642ef67da03fec989909bc4f2f14ae
ms.sourcegitcommit: a3c9a7718502de723e8c156288017de465daaf6b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2019
ms.locfileid: "67263029"
---
# <a name="advanced-features-of-always-on-vpn"></a>Always On VPN의 고급 기능

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**이전:** Always On VPN 기술을 배우고합니다](../always-on-vpn-technology-overview.md)
- [**다음:** Always On VPN 배포 계획 시작](always-on-vpn-deploy-planning.md)

제공 된 배포 시나리오를 넘어 보안 및 VPN 연결의 가용성을 개선 하기 위해 기타 고급 VPN 기능을 추가할 수 있습니다. 예를 들어, 이러한 구성 요소를 사용 하는 연결을 허용 하기 전에 연결 하는 클라이언트가 정상 인지 확인 수 있습니다.

## <a name="high-availability"></a>고가용성

다음은 고가용성을 위한 추가 옵션입니다.

|옵션  |설명  |
|---------|---------|
|서버 복원 력 및 부하 분산     |높은 가용성 또는 지원을 많은 수의 요청을 필요로 하는 환경에서는 늘리려면 성능 및 원격 액세스의 복원 력을 서버 NPS (네트워크 정책)를 실행 하 고 원격을 사용 하도록 설정 하는 여러 서버 간에 부하 분산을 사용 하 여 액세스 서버를 클러스터링 합니다.<p>관련된 문서:<ul><li>[NPS 프록시 서버 부하 분산](../../../../../networking/technologies/nps/nps-manage-proxy-lb.md)</li><li>[클러스터에 원격 액세스 배포](https://docs.microsoft.com/windows-server/remote/remote-access/ras/cluster/deploy-remote-access-in-cluster)</li></ul>        |
|지리적 사이트 복구     |IP 기반 지리적 위치에 대 한 Windows Server 2016에서 DNS를 사용 하 여 Global Traffic Manager를 사용할 수 있습니다. 더 강력한 지리적 부하 분산에 대 한 Microsoft Azure Traffic Manager와 같은 전역 서버 부하 분산 솔루션을 사용할 수 있습니다.<p>관련된 문서:<ul><li>[Traffic Manager 개요](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview)</li><li>[Microsoft Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager)</li></ul>         |

## <a name="advanced-authentication"></a>고급 인증

다음은 인증에 대 한 추가 옵션입니다.

|옵션  |설명  |
|---------|---------|
|비즈니스용 Windows Hello     |Windows 10에서는 비즈니스용 Windows Hello가 PC 및 모바일 디바이스에서 암호를 강력한 2단계 인증으로 바꿉니다. 이 인증의 새로운 유형의 장치에 연결 되 고 사용 하는 생체 인식 하는 사용자 자격 증명이 나 개인 식별 번호 (PIN)으로 구성 됩니다.<p>Windows 10 VPN 클라이언트는 Windows Hello와 호환 됩니다. 사용자 제스처도 로그인 한 후 VPN 연결에 사용 된 Windows Hello 인증서 기반 인증을 위해 비즈니스 인증서에 대 한 합니다.<p>관련된 문서:<ul><li>[비즈니스용 Windows Hello](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-identity-verification)</li><li>기술 사례 연구: [Windows 10에서에서 비즈니스용 Windows Hello 사용 하 여 원격 액세스를 사용 하도록 설정](https://msdn.microsoft.com/library/mt728163.aspx)</li></ul>         |
|Azure MFA (다단계 인증)     |Azure MFA가 클라우드 및 온-프레미스 Windows VPN 인증 메커니즘을 사용 하 여 통합할 수 있는 버전입니다.<p>이 메커니즘 작동 방법에 대 한 자세한 내용은 참조 하세요. [Azure Multi-factor Authentication 서버와 RADIUS 인증 통합](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-server-radius)합니다.         |

## <a name="advanced-vpn-features"></a>고급 VPN 기능

다음은 고급 기능에 대 한 추가 옵션입니다.

|옵션  |설명  |
|---------|---------|
|트래픽 필터링     |클라이언트에서 액세스할 수 있는 응용 프로그램 VPN 적용 해야 할 경우에 VPN 트래픽 필터를 사용할 수 있습니다.<p>자세한 내용은 [VPN 보안 기능](https://docs.microsoft.com/windows/access-protection/vpn/vpn-security-features)합니다.         |
|앱 트리거 VPN     |특정 응용 프로그램 또는 응용 프로그램의 종류를 시작 하는 경우 자동으로 연결 하려면 VPN 프로필을 구성할 수 있습니다.<p>이 및 다른 트리거 옵션에 대 한 자세한 내용은 참조 하세요. [VPN 프로필 자동 트리거 옵션](https://docs.microsoft.com/windows/access-protection/vpn/vpn-auto-trigger-profile)합니다.         |
|VPN 조건부 액세스   |조건부 액세스 및 장치 규정 준수 표준에 맞도록 VPN에 연결 하기 전에 관리 되는 장치를 요구할 수 있습니다. 조건부 액세스를 위한 고급 기능 중 하나를 통해 클라이언트 인증 인증서는 'AAD 조건부 액세스 ' OID ' 1.3.6.1.4.1.311.87의 '를 포함 하는 위치만 VPN 연결을 제한할 수 있습니다.<p>VPN 연결을 제한 해야 합니다.<ol><li>NPS 서버에서 엽니다는 **네트워크 정책 서버** 스냅인입니다.</li><li>확장 **정책을** > **네트워크 정책을**합니다.</li><li>마우스 오른쪽 단추로 클릭 합니다 **가상 개인 네트워크 (VPN) 연결** 네트워크 정책 및 선택 **속성**합니다.</li><li>선택 된 **설정을** 탭 합니다.</li><li>선택 **공급 업체 특정** 선택한 **추가**합니다.</li><li>선택 된 **허용-인증서-OID** 옵션을 선택 합니다 **추가**합니다.</li><li>AAD 조건부 액세스의 OID를 붙여 넣습니다 **1.3.6.1.4.1.311.87** 한 다음 선택한 특성 값으로 **확인** 두 번입니다.</li><li>선택 **닫습니다** 차례로 **적용**합니다.<p>이제 VPN 클라이언트는 수명이 짧은 클라우드 인증서 이외의 인증서를 사용 하 여 연결할 때 연결이 실패 합니다.</li></ol>조건부 액세스에 대 한 자세한 내용은 참조 하세요. [VPN 및 조건부 액세스](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access)합니다.   |


---
## <a name="blocking-vpn-clients-that-use-revoked-certificates"></a>해지 된 인증서를 사용 하는 VPN 클라이언트를 차단 합니다.
  
업데이트를 설치한 후 RRAS 서버 IKEv2를 사용 하는 Vpn에 대 한 인증서 해지를 적용할 수 및 컴퓨터 인증서 인증, 예: 장치에 대 한 Always on Vpn 터널링 합니다. 이 이러한 Vpn에 대 한 RRAS 서버 수 연결을 거부 VPN 클라이언트 해지 된 인증서를 사용 하는 것을 의미 합니다.

**가용성**

다음 표에서 Windows의 각 버전에 대 한 수정 프로그램이 대략적인 출시 날짜를 나열합니다.

|운영 체제 버전 |릴리스 날짜 * |
|---------|---------|
|Windows Server 버전 1903  |Q2, 2019  |
|Windows Server 2019<br />Windows Server 버전 1809  |Q3, 2019  |
|Windows Server, 버전 1803  |Q3, 2019  |
|Windows Server, 버전 1709  |Q3, 2019  |
|Windows Server 2016 버전 1607  |Q2, 2019  |
  
\* 모든 릴리스 날짜는 분기에 나열 됩니다. 날짜는 대략적인 되며 예 고 없이 변경 될 수 있습니다.

**필수 구성 요소를 구성 하는 방법** 

1. 사용 가능 해지면 Windows 업데이트를 설치 합니다.
1. CDP 항목을 모든 VPN 클라이언트 및 사용 하는 RRAS 서버 인증서가 있는 RRAS 서버가 각 Crl를 연결할 수 있는지 확인 합니다.
1. RRAS 서버를 사용 하 여는 **집합 VpnAuthProtocol** PowerShell cmdlet을 구성 합니다 **RootCertificateNameToAccept** 매개 변수입니다.<br /><br />
   다음 예제에서는이 작업을 수행 하는 명령을 나열 합니다. 예에서 **CN = Contoso 루트 인증 기관** 루트 인증 기관의 고유 이름을 나타냅니다. 
   ``` powershell
   $cert1 = ( Get-ChildItem -Path cert:LocalMachine\root | Where-Object -FilterScript { $_.Subject -Like "*CN=Contoso Root Certification Authority,*" } )
   Set-VpnAuthProtocol -RootCertificateNameToAccept $cert1 -PassThru
   ```
**IKEv2 컴퓨터 인증서를 기반으로 하는 VPN 연결에 대 한 인증서 해지를 적용할 RRAS 서버를 구성 하는 방법**

1. 명령 프롬프트 창에서 다음 명령을 실행 합니다. 
   ```
   reg add HKLM\SYSTEM\CurrentControlSet\Services\RemoteAccess\Parameters\Ikev2 /f /v CertAuthFlags /t REG_DWORD /d "4"
   ```

1. 다시 시작 합니다 **라우팅 및 원격 액세스** 서비스입니다.
  
이러한 VPN 연결에 대 한 인증서 해지를 비활성화 하려면 설정 **CertAuthFlags = 2** 하거나 제거 합니다 **CertAuthFlags** 값을 다시는 **라우팅 및 원격 액세스**서비스입니다. 

**IKEv2 컴퓨터 인증서를 기반으로 하는 VPN 연결용 VPN 클라이언트 인증서를 해지 하는 방법**
1. 인증 기관에서 VPN 클라이언트 인증서를 해지 합니다.
1. 인증 기관에서 새 CRL을 게시 합니다.
1. RRAS 서버에서 관리 명령 프롬프트 창을 열고 하 고 다음 명령을 실행 합니다.
   ```
   certutil -urlcache * delete
   certutil -setreg chain\ChainCacheResyncFiletime @now
   ```

**작동은 IKEv2 컴퓨터 인증서 기반 VPN 연결에 대 한 해당 인증서 해지를 확인 하는 방법**  
>[!Note]  
> 이 절차를 사용 하기 전에 CAPI2 operational 이벤트 로그를 사용할 수 있는지 확인 합니다.
1. VPN 클라이언트 인증서를 해지 하려면 이전 단계를 수행 합니다.
1. 해지 된 인증서가 있는 클라이언트를 사용 하 여 VPN에 연결 하려고 합니다. RRAS 서버 연결을 거부 하며 "IKE 인증 자격 증명 허용 되지 않습니다."와 같은 메시지를 표시 합니다.
1. RRAS 서버의 이벤트 뷰어를 열고 이동할 **응용 프로그램 및 서비스 로그/Microsoft/Windows/CAPI2**합니다. 
1. 다음 정보는 이벤트를 검색 합니다.
   * 로그 이름: **Microsoft-Windows-CAPI2/Operational Microsoft-Windows-CAPI2/Operational**
   * 이벤트ID: **41** 
   * 다음 텍스트를 포함 하는 이벤트: **제목 = "*클라이언트 FQDN*"** (*클라이언트 FQDN* 는 해지 된 클라이언트의 정규화 된 도메인 이름을 나타내는 인증서입니다.) 

   합니다 **<Result>** 이벤트 데이터 필드를 포함 해야 **인증서가 해지**합니다. 예를 들어, 이벤트에서 발췌 한 다음 내용 참조:
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

### <a name="trusted-platform-module-tpm-key-attestation"></a>신뢰할 수 있는 플랫폼 모듈 (TPM) 키 증명

TPM 증명 된 키를 사용 하 여 사용자 인증서를 내보내기 아닌, 앤티 만들던 및 TPM에서 제공 하는 키의 격리 하 여 백업 하는 더 높은 보안 보증을 제공 합니다.

Windows 10에서 TPM 키 증명에 대 한 자세한 내용은 참조 하세요. [TPM 키 증명](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/component-updates/tpm-key-attestation)합니다.

## <a name="next-step"></a>다음 단계

[Always On VPN 배포 계획 시작](always-on-vpn-deploy-planning.md): VPN 서버를 사용 하 여 계획 하는 컴퓨터에 원격 액세스 서버 역할을 설치 하기 전에 다음 작업을 수행 합니다. 적절 한 계획 한 후에 Always On VPN을 배포할 수 있으며 필요에 따라 Azure AD를 사용 하 여 VPN 연결에 대 한 조건부 액세스를 구성할 수 있습니다.  

## <a name="related-topics"></a>관련 항목
- [NPS 프록시 서버 부하 분산](../../../../../networking/technologies/nps/nps-manage-proxy-lb.md): 가상 사설망 (VPN) 서버 및 무선 액세스 지점과 같은 네트워크 액세스 서버는 원격 인증 전화 접속 사용자 서비스 (RADIUS) 클라이언트 연결 요청을 만들고 NPS와 같은 RADIUS 서버 보냅니다. 일부 경우에는 NPS 서버 요청을 받을 수 너무 많은 연결 한 번에 성능 저하 또는 오버 로드.

- [Traffic Manager 개요](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview): 이 항목의 Azure Traffic Manager 서비스 끝점에 대 한 사용자 트래픽의 배포를 제어할 수 있는 개요를 제공 합니다. Traffic Manager 도메인 이름 시스템 (DNS)를 사용 하 여 트래픽 라우팅 메서드 및 끝점의 상태에 따라 가장 적합 한 끝점으로 클라이언트 요청을 보냅니다. 

- [비즈니스용 Windows Hello](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-identity-verification): 이 항목에서는 클라우드 전용 배포 및 하이브리드 배포와 같은 필수 구성 요소를 제공합니다.  또한이 항목에 대 한 Windows Hello 비즈니스에 대 한 질문과 대답을 나열합니다.

- [기술 사례 연구: Windows 10에서에서 비즈니스용 Windows Hello 사용 하 여 원격 액세스를 사용 하도록 설정 하면](https://msdn.microsoft.com/library/mt728163.aspx): 이 기술 사례 연구에서는 Microsoft 비즈니스용 Windows Hello와 원격 액세스를 구현 하는 방법을 알아봅니다.  Windows Hello for Business는 개인/공개 키 또는 암호 수준을 넘어서는 조직과 소비자에 대 한 인증서 기반 인증 방법. 이 형태의 인증 암호를 대신할 수 및 위반, 도난 및 피싱에 강한 키 쌍 자격 증명에 의존 합니다. 

- [Azure Multi-factor Authentication 서버와 RADIUS 인증 통합](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-server-radius): 이 항목에서는 안내 추가 하 고 Azure Multi-factor Authentication 서버를 사용 하 여 RADIUS 클라이언트 인증을 구성 합니다. RADIUS는 인증 요청을 받고 해당 요청을 처리하는 표준 프로토콜입니다. Azure Multi-factor Authentication 서버를 RADIUS 서버로 작동할 수 있습니다. 

- [VPN 보안 기능](https://docs.microsoft.com/windows/access-protection/vpn/vpn-security-features): 이 항목에서는 잠금 VPN, VPN 및 트래픽 필터를 사용 하 여 Windows 정보 보호 (WIP) 통합에 대 한 VPN 보안 지침을 제공합니다. 

- [VPN 프로필 자동 트리거 옵션](https://docs.microsoft.com/windows/access-protection/vpn/vpn-auto-trigger-profile): 이 항목에서는 앱 트리거, 트리거 이름 기반 및 Always On 등의 VPN 프로필 자동 트리거 옵션을 제공 합니다.

- [VPN 및 조건부 액세스](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access): 이 항목에서는 원격 클라이언트에 대 한 장치 준수 옵션을 제공 하기 위해 클라우드 기반 조건부 액세스 플랫폼의 개요를 제공 합니다. 조건부 액세스는 Azure AD(Azure Active Directory)에 연결된 응용 프로그램에 대한 액세스 규칙을 만드는 데 사용되는 정책 기반 평가 엔진입니다. 

- [TPM 키 증명](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/component-updates/tpm-key-attestation): 이 항목에서는 모듈 TPM (Trusted Platform) 및 단계는 TPM 키 증명을 배포 하는 개요를 제공 합니다. 또한 문제를 해결 하는 단계 및 문제 해결 정보를 찾을 수 있습니다.
