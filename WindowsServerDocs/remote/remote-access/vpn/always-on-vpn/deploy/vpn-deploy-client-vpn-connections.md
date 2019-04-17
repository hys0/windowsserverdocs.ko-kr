---
title: Windows 10 클라이언트 Always On VPN 연결 구성
description: 이 단계에서는 ProfileXML 옵션 및 스키마에 대해 및 VPN 연결을 사용 하 여 해당 인프라와 통신 하는 Windows 10 클라이언트 컴퓨터를 구성 합니다.
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.date: 05/29/2018
ms.assetid: d165822d-b65c-40a2-b440-af495ad22f42
ms.localizationpriority: medium
ms.author: pashort
author: shortpatti
ms.reviewer: deverette
ms.openlocfilehash: 6b383076686092e20448977bed3766f7d7d1c2b8
ms.sourcegitcommit: 4147e092d77d9458696e6686bccefe3788c90508
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/28/2019
ms.locfileid: "9031317"
---
# 6단계. Windows 10 클라이언트 Always On VPN 연결 구성

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10


& #171;  [ **이전:** 5 단계입니다. DNS 및 방화벽 설정 구성](vpn-deploy-dns-firewall.md)<br>
& #187; [ **다음:** 7 단계입니다. (선택 사항) Azure AD를 사용 하 여 VPN 연결에 대 한 조건부 액세스](../../ad-ca-vpn-connectivity-windows10.md)

이 단계에서는 ProfileXML 옵션 및 스키마에 대해 및 VPN 연결을 사용 하 여 해당 인프라와 통신 하는 Windows 10 클라이언트 컴퓨터를 구성 합니다. 

PowerShell, SCCM, 또는 Intune을 통해 Always On VPN 클라이언트를 구성할 수 있습니다. 세 가지 모두 적절 한 VPN 설정을 구성 하는 XML VPN 프로필이 필요 합니다. PowerShell 자동화 SCCM 또는 Intune 없이 조직에 대 한 등록 되었을 수 있습니다.

>[!NOTE]
>그룹 정책에 windows 10 원격 액세스 Always On VPN 클라이언트를 구성 하는 관리 템플릿 포함 되지 않습니다.  그러나 로그온 스크립트를 사용할 수 있습니다.

## ProfileXML 개요

ProfileXML은 VPNv2 CSP 내에서 노드 URI입니다. 각 VPNv2 CSP 노드를 개별적으로 구성 하는 대신-트리거 같은 경로 목록 및 인증 프로토콜-이 노드를 사용 하 여 단일 CSP 노드를 단일 XML 블록으로 모든 설정을 제공 하 여 windows 10 VPN 클라이언트를 구성 합니다. ProfileXML 스키마 거의 동일 하 게 VPNv2 CSP 노드의 스키마와 일치 하지만 일부 용어는 약간 다릅니다.

이 배포 설명, Windows PowerShell, System Center Configuration Manager 및 Intune 비롯 한 모든 전달 방법 ProfileXML 사용 합니다. 이 배포에서 ProfileXML VPNv2 CSP 노드를 구성 하는 방법은 두 가지가 있습니다.

- **OMA DM**합니다. 한 가지 방법은 [VPNv2 CSP 노드](../always-on-vpn-technology-overview.md#vpnv2-csp-nodes)섹션의 앞부분에서 설명한 대로 OMA-DM를 사용 하 여 MDM 공급자를 사용 하는 것입니다. 이 메서드를 사용 하 여 삽입할 수 있습니다 쉽게 VPN 프로필 구성 XML 태그 ProfileXML CSP 노드 Intune을 사용 하는 경우.

- **(WMI)---CSP 브리지**입니다. ProfileXML CSP 노드를 구성 하는 두 번째 방법은 CSP를 WMI 브리지를 사용 하는 것-WMI 클래스 라고 **MDM_VPNv2_01**-VPNv2 CSP와 ProfileXML 노드에 액세스할 수 있는 합니다. 해당 WMI 클래스의 새 인스턴스를 만들 때 WMI CSP를 사용 하 여 Windows PowerShell 및 System Center Configuration Manager를 사용 하는 경우 VPN 프로필을 만들 수 있습니다.

이러한 구성 방법 다를 경우에 모두 올바른 형식의 XML VPN 프로필을 필요 합니다. ProfileXML VPNv2 CSP 설정을 사용 하려면, 간단한 배포 시나리오에 필요한 태그를 구성 하는 ProfileXML 스키마를 사용 하 여 XML을 구성 합니다. 자세한 내용은 [ProfileXML XSD](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/vpnv2-profile-xsd)를 참조 하세요.

다음 각 필요한 설정 및 해당 하는 ProfileXML 태그가 찾습니다. ProfileXML 스키마 내에서 특정 태그에 있는 각 설정을 구성 하 고 기본 프로필 아래에 나와 있는 전체 목록은 합니다. 추가 태그 배치 ProfileXML 스키마를 참조 하세요.

[!INCLUDE [important-lower-case-true-include](../../../includes/important-lower-case-true-include.md)]

**연결 형식:** 기본 IKEv2

ProfileXML 요소:

    <NativeProtocolType>IKEv2</NativeProtocolType>

**라우팅:** 분할 터널링

ProfileXML 요소:

    <RoutingPolicyType>SplitTunnel</RoutingPolicyType>

**이름 확인:** 도메인 이름 정보 목록 및 DNS 접미사

ProfileXML 요소:

    <DomainNameInformation>
    <DomainName>.corp.contoso.com</DomainName>
    <DnsServers>10.10.1.10,10.10.1.50</DnsServers>
    </DomainNameInformation>
    
    <DnsSuffix>corp.contoso.com</DnsSuffix>


**트리거:** 항상 설정 및 신뢰할 수 있는 네트워크 검색

ProfileXML 요소:

    <AlwaysOn>true</AlwaysOn>
    <TrustedNetworkDetection>corp.contoso.com</TrustedNetworkDetection>


**인증:** PEAP-TLS TPM 보호 되는 사용자 인증서

ProfileXML 요소:

    <Authentication>
    <UserMethod>Eap</UserMethod>
    <Eap>
    <Configuration>...</Configuration>
    </Eap>
    </Authentication>

일부 VPN 인증 메커니즘을 구성 하려면 간단한 태그를 사용할 수 있습니다. 그러나 PEAP 및 EAP는 훨씬 더 복잡 합니다. XML 태그를 만들 수 있는 가장 쉬운 방법은 해당 EAP 설정을 사용 하 여 VPN 클라이언트를 구성 하 고 다음 해당 구성을 XML로 내보내기 하는 것입니다. 

EAP 설정에 대 한 자세한 내용은 [EAP 구성을](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/eap-configuration)참조 하세요. 

## <a name="bkmk_profile"></a>템플릿 연결 프로필을 수동으로 만들려면

이 단계를 확장할 수 있는 인증 프로토콜 보호 \(PEAP\) 사용 하 여 클라이언트와 서버 간 통신을 보호 합니다. 간단한 사용자 이름 및 암호와 달리이 연결 되려면 VPN 프로필의 고유한 EAPConfiguration 섹션이 필요 합니다. 

처음부터 XML 태그를 만드는 방법을 설명 하는 대신 VPN 프로필 템플릿을 만들려면 Windows의 설정을 사용 합니다. VPN 프로필 템플릿을 만든 후 해당 템플릿을 배포 나중에 배포 하는 최종 ProfileXML 만드는 EAPConfiguration 부분을 사용 하도록 Windows PowerShell을 사용 합니다.

### NPS 인증서 설정 기록

서식 파일을 만들기 전에 호스트 이름 또는 정규화 된 도메인 이름 (FQDN) 서버 인증서에서 NPS 서버와 인증서를 발급 CA의 이름을 기록해 둡니다.

**절차:**

1.  NPS 서버에서 네트워크 정책 서버를 엽니다.

2.  NPS 콘솔에서 정책에서 **네트워크 정책**을 클릭 합니다.

3.  **가상 사설망 \(VPN\) 연결**을 마우스 오른쪽 단추로 클릭 하 고 **속성**을 클릭 합니다.

4.  **제약 조건** 탭을 클릭 하 고 **인증 방법**을 클릭 합니다.

5.  EAP 유형을 클릭 **Microsoft: 보호 된 EAP (PEAP)**, **편집**을 클릭 합니다.

6.  **인증서를 발급** 하 고 **발급자**에 대 한 값을 기록 합니다.<p>예정 된 VPN 템플릿 구성에 이러한 값을 사용 합니다. 예를 들어 서버의 FQDN nps01.corp.contoso.com 이며 호스트 이름 NPS01, 인증서 이름 예를 들어 nps01.corp.contoso.com 서버-의 FQDN 또는 DNS 이름에 기반 합니다.

7.  보호 된 EAP 속성 편집 대화 상자를 취소 합니다.

8.  가상 개인 네트워크 (VPN) 연결 속성 대화 상자를 취소 합니다.

9.  네트워크 정책 서버를 닫습니다.

>[!NOTE]
>여러 NPS 서버가 있는 경우 VPN 프로필 확인할 수 있도록 각각은 사용할지 마다 이러한 단계를 완료 합니다.

### Domain\에 가입 된 클라이언트 컴퓨터에서 VPN 프로필 템플릿 구성

도메인에 가입 된 클라이언트 컴퓨터에서 템플릿 VPN 프로필을 구성 하는 데 필요한 정보 하셨습니다. 사용 하는 사용자 계정 유형의 \ (즉, 표준 사용자 또는 administrator\)에 프로세스의이 부분 중요 하지 않습니다. 

그러나 인증서 자동 등록 구성 후 컴퓨터를 다시 시작 하지 않은 경우 이렇게 템플릿을 사용할 수 있는 인증서를 등록 보장 하기 위해 VPN 연결을 구성 하기 전에 합니다.

>[!NOTE]
>고급 속성 같은 nrpt Always On VPN 수동으로 추가할 방법은 신뢰할 수 있는 네트워크 검색 등. 다음 단계에서 서버에 VPN 연결을 설정할 수 있는지와 VPN 서버 구성을 확인 하려면 테스트 VPN 연결을 만듭니다.

**단일 테스트 VPN 연결을 수동으로 만들려면**

1.  **VPN 사용자** 그룹의 구성원으로 도메인에 가입 된 클라이언트 컴퓨터에 로그인 합니다.

2.  시작 메뉴에서 **VPN**을 입력 하 고 Enter 키를 누릅니다.

3.  세부 정보 창에서 **VPN 연결 추가**클릭 합니다.

4.  VPN 공급자 목록에서 **Windows (기본 제공)를**클릭 합니다.

5.  연결 이름에 **서식 파일**을 입력 합니다.

6.  서버 이름 또는 주소에는 **외부** VPN 서버의 FQDN을 입력 \ (예를 들어**vpn.contoso.com**\).

7.  **저장**을 클릭합니다.

8.  관련 된 설정을 **변경 어댑터 옵션**을 클릭 합니다.

9.  **템플릿**을 마우스 오른쪽 단추로 클릭 하 고 **속성**을 클릭 합니다.

10. **VPN 종류** **보안** 탭에서 **IKEv2**를 클릭 합니다.

11. 데이터 암호화를 **최대 강도 암호화**를 클릭 합니다.

12. **사용 하 여 확장할 수 있는 인증 프로토콜 (EAP)** 클릭 합니다. 그런 다음 **확장할 수 있는 인증 프로토콜 (EAP)** 클릭 **Microsoft: 보호 된 EAP (PEAP) (암호화 사용)**.

13. 보호 된 EAP 속성 대화 상자를 열려면 **속성** 클릭 하 고 다음 단계를 완료 합니다.

    a. **다음이 서버에 연결** 상자에서 NPS 서버 인증 설정 (예를 들어 NPS01)이이 섹션의 앞부분에서 검색 하는 NPS 서버 이름을 입력 합니다.

    >[!NOTE]
    >서버 이름을 입력 하 고 인증서의 이름과 일치 해야 합니다. 이 이름은이 섹션의 앞부분을 복원 하는 경우. 이름이 일치 하지 않으면 연결이 실패 합니다, 내용의 "연결이 차단 된 RAS/VPN 서버에 구성 된 정책으로 인해."

    b.  신뢰할 수 있는 루트 인증 기관에서 루트 NPS 서버 인증서 (예를 들어 contoso CA)를 선택 합니다.

    c.  연결 하기 전에 알림, **새 서버 또는 신뢰할 수 있는 Ca 권한을 부여 하는 사용자를 요청 하지 않도록**를 클릭 합니다.

    d.  인증 방법 선택에서 **스마트 카드 또는 다른 인증서를**클릭 하 고 **구성**합니다. 스마트 카드 또는 다른 인증서 속성 대화 상자가 열립니다.

    e.  **이 컴퓨터에 인증서 사용**을 클릭 합니다.

    f.  이러한 서버 상자에 연결을 이전 단계에서 NPS 서버 인증 설정에서 검색 NPS 서버 이름을 입력 합니다.

    g.  신뢰할 수 있는 루트 인증 기관에서 루트 NPS 서버 인증서를 발급 CA를 선택 합니다.

    h.  선택 합니다 **사용자가 새 서버 권한 부여를 묻는 메시지를 표시 하지 않는 신뢰할 수 있는 인증 기관 또는** 확인란을 선택 합니다.

    i.  스마트 카드 또는 다른 인증서 속성 대화 상자를 닫으려면 **확인** 클릭 합니다.

    j 합니다.  보호 된 EAP 속성 대화 상자를 닫으려면 **확인** 클릭 합니다.

10. 템플릿 속성 대화 상자를 닫으려면 **확인** 클릭 합니다.

11. 네트워크 연결 창을 닫습니다.

12. 설정에서 **서식 파일**을 클릭 하 고 **연결**을 클릭 하 여 VPN을 테스트 합니다.

>[!IMPORTANT]
>VPN 서버에 VPN 연결 템플릿 성공 인지 확인 합니다. 이렇게 하면 다음 예제에서 사용 하기 전에 EAP 설정이 정확한 지. 계속 하기 전에 한 번 이상 연결 해야 합니다. 그렇지 않으면 프로필은 VPN에 연결 하는 데 필요한 모든 정보가 포함 되지 않습니다.

## <a name="bkmk_ProfileXML"></a>ProfileXML 구성 파일 만들기

이 섹션을 완료 하기 전에 생성 하 고 템플릿 [템플릿 연결 프로필을 수동으로 만들](#bkmk_profile) 섹션에서 설명 하는 VPN 연결을 테스트 있는지를 확인 합니다. VPN 연결을 테스트 하는 프로필이 포함 VPN에 연결 하는 데 필요한 모든 정보가 있는지 확인 하려면 필요 합니다.

목록 1에서 Windows PowerShell 스크립트를 이전에 만든 템플릿 연결 프로필에 따라 **EAPConfiguration** 태그를 포함 하는 바탕 화면에 두 개의 파일을 만듭니다.

-   **VPN_Profile.xml 합니다.** 이 파일은 ProfileXML 노드가 VPNv2 CSP에서 구성 하는 데 필요한 XML 태그를 포함 합니다. Intune 같은 OMA DM 호환 MDM 서비스를 사용 하 여이 파일을 사용 합니다.

-   **VPN_Profile.ps1 합니다.** 이 파일은 실행할 수 있는 Windows PowerShell 스크립트 ProfileXML 노드가 VPNv2 CSP에서 구성 하는 클라이언트 컴퓨터에서. 이 스크립트를 통해 System Center Configuration Manager를 배포 하 여 CSP를 구성할 수도 있습니다. Hyper-v 향상 된 세션을 포함 하 여 원격 데스크톱 세션에서이 스크립트를 실행할 수 없습니다.

>[!IMPORTANT]
>아래 예제에서는 명령에는 Windows 10 빌드 1607 이상 필요합니다.

**VPN_Profile.xml 및 VPN_Proflie.ps1 만들기**

1. 섹션에는 동일한 사용자를 사용 하 여 VPN 프로필 템플릿을 포함 하는 도메인에 가입 된 클라이언트 컴퓨터에 로그인 계정이 "템플릿 연결 프로필을 수동으로 만들려면" 설명 합니다.

2. Windows PowerShell 통합된 스크립팅 환경 목록 1 붙여 \(ISE\), 및 설명에 설명 된 매개 변수를 사용자 지정 합니다. $Template, $ProfileName, $Servers, $DnsSuffix, $DomainName, $TrustedNetwork, 및 $DNSServers 사용 됩니다. 각 설정에 대 한 자세한 내용은 의견입니다.

3.  바탕 화면에 **VPN_Profile.xml** 및 **VPN_Profile.ps1** 를 생성 하기 위한 스크립트를 실행 합니다.

#### 1을 나열 합니다. MakeProfile.ps1 이해

이 섹션에서는 ProfileXML VPNv2 CSP의 구성에 대 한 구체적으로 VPN 프로필을 만드는 방법을 파악 하는 데 사용할 수 있는 예제 코드에 설명 합니다.

이 예제 코드에서 스크립트를 조립 하 고 스크립트 두 개의 파일을 생성 스크립트를 실행 한 후: VPN_Profile.xml 및 VPN_Profile.ps1 합니다. VPN_Profile.xml를 사용 하 여 ProfileXML OMA DM 호환 MDM 서비스에서 Microsoft Intune과 같은 구성 합니다.

Windows PowerShell 또는 System Center Configuration Manager에서 **VPN_Profile.ps1** 스크립트를 사용 하 여 Windows 10 데스크톱에서 ProfileXML을 구성할 수 있습니다.

>[!NOTE]
>전체 예제 스크립트를 보려면 [MakeProfile.ps1 전체 스크립트](#bkmk_fullscript)섹션을 참조 하세요.

#### 매개 변수

다음 매개 변수를 구성 합니다.

**$Template**합니다. EAP 구성 검색할 수 있는 서식 파일의 이름입니다.

**$ProfileName**합니다. 프로필에 대 한 고유 영숫자 식별자입니다. 프로필 이름을 슬래시 (/)를 포함 해야 합니다. 프로필 이름에 공백이 나 기타 영숫자가 아닌 문자 있으면, 제대로 이스케이프 표시 해야 하기 URL 인코딩 표준에 따라 합니다.

**$Servers**합니다. 공용 또는 라우팅 가능 IP 주소 또는 VPN 게이트웨이 위한 DNS 이름입니다. 외부 IP 나 서버 팜의 가상 IP 가리킬 수 있습니다. 예, 208.147.66.130 또는 vpn.contoso.com 합니다.

**$DnsSuffix**합니다. 하나 이상의 쉼표 구분 DNS 접미사를 지정 합니다. 목록에서 첫 번째도 VPN 인터페이스에 대 한 기본 연결별 DNS 접미사로 사용 됩니다. 전체 목록은 SuffixSearchList에도 추가 됩니다.

**$DomainName**합니다. 정책이 적용 되는 네임 스페이스를 식별 하는 데 사용 합니다. 한 이름 쿼리에 실행 될 때 DNS 클라이언트 검색 DomainNameInformationList에서 네임 스페이스의 모든 쿼리에서 이름을 비교 합니다. 이 매개 변수는 다음 형식 중 하나일 수 있습니다.

- FQDN-정규화 된 도메인 이름
- 접미사-도메인 접미사를 shortname 쿼리에 DNS 확인에 추가 됩니다. 접미사를 지정 하려면 앞에 마침표 \ (.) DNS 접미사를 합니다.

**$DNSServers**합니다. 쉼표로 구분 된 DNS 서버 IP 주소의 목록입니다 네임 스페이스에 사용 하도록 합니다.

**$TrustedNetwork**합니다. 신뢰할 수 있는 네트워크를 식별 쉼표로 구분 된 문자열입니다. VPN은 사용자가 보호 된 리소스는 장치에 직접 액세스할 수 있는 무선 기업 네트워크에 자동으로 연결 되지 않습니다.

다음은 아래 명령에 사용 되는 매개 변수에 대 한 예제 값입니다. 환경에 대 한 이러한 값을 변경 하는 것을 확인 합니다.

    $TemplateName = 'Template'
    $ProfileName = 'Contoso AlwaysOn VPN'
    $Servers = 'vpn.contoso.com'
    $DnsSuffix = 'corp.contoso.com'
    $DomainName = '.corp.contoso.com'
    $DNSServers = '10.10.0.2,10.10.0.3'
    $TrustedNetwork = 'corp.contoso.com'


### 준비 및 XML 프로필 만들기

다음 예제에서는 명령을 템플릿 프로필의 EAP 설정을 가져오려면:


    $Connection = Get-VpnConnection -Name $TemplateName
    if(!$Connection)
    {
    $Message = "Unable to get $TemplateName connection profile: $_"
    Write-Host "$Message"
    exit
    }
    $EAPSettings= $Connection.EapConfigXmlStream.InnerXml


### XML 프로필 만들기

[!INCLUDE [important-lower-case-true-include](../../../includes/important-lower-case-true-include.md)]

    $ProfileXML =
    '<VPNProfile>
      <DnsSuffix>' + $DnsSuffix + '</DnsSuffix>
      <NativeProfile>
    <Servers>' + $Servers + '</Servers>
    <NativeProtocolType>IKEv2</NativeProtocolType>
    <Authentication>
      <UserMethod>Eap</UserMethod>
      <Eap>
       <Configuration>
     '+ $EAPSettings + '
       </Configuration>
      </Eap>
    </Authentication>
    <RoutingPolicyType>SplitTunnel</RoutingPolicyType>
      </NativeProfile>
     <AlwaysOn>true</AlwaysOn>
     <RememberCredentials>true</RememberCredentials>
     <TrustedNetworkDetection>' + $TrustedNetwork + '</TrustedNetworkDetection>
      <DomainNameInformation>
    <DomainName>' + $DomainName + '</DomainName>
    <DnsServers>' + $DNSServers + '</DnsServers>
    </DomainNameInformation>
    </VPNProfile>'


### Intune에 대 한 출력 VPN_Profile.xml

프로필 XML 파일을 저장 하려면 다음 예제에서는 명령을 사용할 수 있습니다.

    $ProfileXML | Out-File -FilePath ($env:USERPROFILE + '\desktop\VPN_Profile.xml')

### 데스크톱 및 System Center Configuration Manager에 대 한 출력 VPN_Profile.ps1

다음 예제 코드는 ProfileXML 노드가 VPNv2 CSP를 사용 하 여 AlwaysOn IKEv2 VPN 연결을 구성 합니다.

Windows 10 데스크톱 또는 System Center Configuration Manager에서이 스크립트를 사용할 수 있습니다.

### 키 VPN 프로필 매개 변수를 정의 합니다.

    $Script = '$ProfileName = ''' + $ProfileName + '''
    $ProfileNameEscaped = $ProfileName -replace ' ', '%20'

## VPN ProfileXML 정의

    $ProfileXML = ''' + $ProfileXML + '''
    
### 프로필에 특수 문자를 이스케이프

    $ProfileXML = $ProfileXML -replace '<', '&lt;'
    $ProfileXML = $ProfileXML -replace '>', '&gt;'
    $ProfileXML = $ProfileXML -replace '"', '&quot;'
    
### CSP를 WMI 브리지 속성을 정의

    $nodeCSPURI = "./Vendor/MSFT/VPNv2"
    $namespaceName = "root\cimv2\mdm\dmmap"
    $className = "MDM_VPNv2_01"

### VPN 프로필에 대 한 사용자 SID를 확인 합니다.

    try
    {
    $username = Gwmi -Class Win32_ComputerSystem | select username
    $objuser = New-Object System.Security.Principal.NTAccount($username.username)
    $sid = $objuser.Translate([System.Security.Principal.SecurityIdentifier])
    $SidValue = $sid.Value
    $Message = "User SID is $SidValue."
    Write-Host "$Message"
    }
    catch [Exception]
    {
    $Message = "Unable to get user SID. User may be logged on over Remote Desktop: $_"
    Write-Host "$Message"
    exit
    }
    

### WMI 세션을 정의 합니다.

    $session = New-CimSession
    $options = New-Object Microsoft.Management.Infrastructure.Options.CimOperationOptions
    $options.SetCustomOption("PolicyPlatformContext_PrincipalContext_Type", "PolicyPlatform_UserContext", $false)
    $options.SetCustomOption("PolicyPlatformContext_PrincipalContext_Id", "$SidValue", $false)


### 검색 하 고 이전 VPN 프로필을 삭제 합니다.

    try
    {
        $deleteInstances = $session.EnumerateInstances($namespaceName, $className, $options)
        foreach ($deleteInstance in $deleteInstances)
        {
            $InstanceId = $deleteInstance.InstanceID
            if ("$InstanceId" -eq "$ProfileNameEscaped")
            {
                $session.DeleteInstance($namespaceName, $deleteInstance, $options)
                $Message = "Removed $ProfileName profile $InstanceId"
                Write-Host "$Message"
            } else {
                $Message = "Ignoring existing VPN profile $InstanceId"
                Write-Host "$Message"
            }
        }
    }
    catch [Exception]
    {
        $Message = "Unable to remove existing outdated instance(s) of $ProfileName profile: $_"
        Write-Host "$Message"
        exit
    }
    

### VPN 프로필을 만듭니다.

    try
    {
        $newInstance = New-Object Microsoft.Management.Infrastructure.CimInstance $className, $namespaceName
        $property = [Microsoft.Management.Infrastructure.CimProperty]::Create("ParentID", "$nodeCSPURI", "String", "Key")
        $newInstance.CimInstanceProperties.Add($property)
        $property = [Microsoft.Management.Infrastructure.CimProperty]::Create("InstanceID", "$ProfileNameEscaped", "String", "Key")
        $newInstance.CimInstanceProperties.Add($property)
        $property = [Microsoft.Management.Infrastructure.CimProperty]::Create("ProfileXML", "$ProfileXML", "String", "Property")
        $newInstance.CimInstanceProperties.Add($property)
        $session.CreateInstance($namespaceName, $newInstance, $options)
        $Message = "Created $ProfileName profile."


        Write-Host "$Message"
    }
    catch [Exception]
    {
    $Message = "Unable to create $ProfileName profile: $_"
    Write-Host "$Message"
    exit
    }
    
    $Message = "Script Complete"
    Write-Host "$Message"'

### 프로필 XML 파일을 저장

    $Script | Out-File -FilePath ($env:USERPROFILE + '\desktop\VPN_Profile.ps1')
    
    $Message = "Successfully created VPN_Profile.xml and VPN_Profile.ps1 on the desktop."
    Write-Host "$Message"

## <a name="bkmk_fullscript"></a>MakeProfile.ps1 전체 스크립트

대부분의 예제를 ProfileXML MDM_VPNv2_01 WMI 클래스의 새 인스턴스를 삽입 Set-wmiinstance Windows PowerShell cmdlet을 사용 합니다. 

그러나이 작동 하지 않습니다 System Center Configuration Manager에서 되므로 최종 사용자의 컨텍스트에서 패키지를 실행할 수 없습니다. 따라서이 스크립트 공통 정보 모델을 사용 하 여 사용자의 컨텍스트에서 WMI 세션을 만들려면 하 고 그런 다음 해당 세션에서 MDM_VPNv2_01 WMI 클래스의 새 인스턴스를 만듭니다. 이 WMI 클래스 VPNv2 CSP를 구성 하는 CSP를 WMI 브리지를 사용 합니다. 따라서 클래스 인스턴스를 추가 하 여 CSP 구성 합니다. 

>[!IMPORTANT]
>CSP를 WMI 브리지 디자인 하 여 로컬 관리자 권한이 필요합니다. VPN 프로필 사용자 당 배포를 사용 해야 SCCM 또는 MDM.

>[!NOTE]
>현재 사용자의 SID를 사용 하 여 사용자의 컨텍스트를 식별 하는 스크립트 VPN_Profile.ps1 합니다. 원격 데스크톱 세션에서 사용할 수 없는 SID 이기 때문에 스크립트 원격 데스크톱 세션에서 작동 하지 않습니다. 마찬가지로, Hyper-v 향상 된 세션에서 작동 하지 않습니다. 가상 컴퓨터에는 원격 액세스 Always On VPN을 테스트 하는 경우이 스크립트를 실행 하기 전에 클라이언트 Vm에서 고급 세션을 사용 하지 않도록 설정 합니다.

다음 예제 스크립트는 모든 이전 섹션에서 코드 예제를 포함합니다. 환경에 적합 한 값으로 예제 값을 변경 하는 것을 확인 합니다.
    
   ```XML
    $TemplateName = 'Template'
    $ProfileName = 'Contoso AlwaysOn VPN'
    $Servers = 'vpn.contoso.com'
    $DnsSuffix = 'corp.contoso.com'
    $DomainName = '.corp.contoso.com'
    $DNSServers = '10.10.0.2,10.10.0.3'
    $TrustedNetwork = 'corp.contoso.com'

    
    $Connection = Get-VpnConnection -Name $TemplateName
    if(!$Connection)
    {
    $Message = "Unable to get $TemplateName connection profile: $_"
    Write-Host "$Message"
    exit
    }
    $EAPSettings= $Connection.EapConfigXmlStream.InnerXml
    
    $ProfileXML =
    '<VPNProfile>
      <DnsSuffix>' + $DnsSuffix + '</DnsSuffix>
      <NativeProfile>
    <Servers>' + $Servers + '</Servers>
    <NativeProtocolType>IKEv2</NativeProtocolType>
    <Authentication>
      <UserMethod>Eap</UserMethod>
      <Eap>
       <Configuration>
     '+ $EAPSettings + '
       </Configuration>
      </Eap>
    </Authentication>
    <RoutingPolicyType>SplitTunnel</RoutingPolicyType>
      </NativeProfile>
    <AlwaysOn>true</AlwaysOn>
    <RememberCredentials>true</RememberCredentials>
    <TrustedNetworkDetection>' + $TrustedNetwork + '</TrustedNetworkDetection>
      <DomainNameInformation>
    <DomainName>' + $DomainName + '</DomainName>
    <DnsServers>' + $DNSServers + '</DnsServers>
    </DomainNameInformation>
    </VPNProfile>'
    
    $ProfileXML | Out-File -FilePath ($env:USERPROFILE + '\desktop\VPN_Profile.xml')
    
    $Script = '$ProfileName = ''' + $ProfileName + '''
    $ProfileNameEscaped = $ProfileName -replace ' ', '%20'
    
    $ProfileXML = ''' + $ProfileXML + '''
    
    $ProfileXML = $ProfileXML -replace '<', '&lt;'
    $ProfileXML = $ProfileXML -replace '>', '&gt;'
    $ProfileXML = $ProfileXML -replace '"', '&quot;'
    
    $nodeCSPURI = "./Vendor/MSFT/VPNv2"
    $namespaceName = "root\cimv2\mdm\dmmap"
    $className = "MDM_VPNv2_01"
    
    try
    {
    $username = Gwmi -Class Win32_ComputerSystem | select username
    $objuser = New-Object System.Security.Principal.NTAccount($username.username)
    $sid = $objuser.Translate([System.Security.Principal.SecurityIdentifier])
    $SidValue = $sid.Value
    $Message = "User SID is $SidValue."
    Write-Host "$Message"
    }
    catch [Exception]
    {
    $Message = "Unable to get user SID. User may be logged on over Remote Desktop: $_"
    Write-Host "$Message"
    exit
    }
    
    $session = New-CimSession
    $options = New-Object Microsoft.Management.Infrastructure.Options.CimOperationOptions
    $options.SetCustomOption("PolicyPlatformContext_PrincipalContext_Type", "PolicyPlatform_UserContext", $false)
    $options.SetCustomOption("PolicyPlatformContext_PrincipalContext_Id", "$SidValue", $false)
    
        try
    {
        $deleteInstances = $session.EnumerateInstances($namespaceName, $className, $options)
        foreach ($deleteInstance in $deleteInstances)
        {
            $InstanceId = $deleteInstance.InstanceID
            if ("$InstanceId" -eq "$ProfileNameEscaped")
            {
                $session.DeleteInstance($namespaceName, $deleteInstance, $options)
                $Message = "Removed $ProfileName profile $InstanceId"
                Write-Host "$Message"
            } else {
                $Message = "Ignoring existing VPN profile $InstanceId"
                Write-Host "$Message"
            }
        }
    }
    catch [Exception]
    {
        $Message = "Unable to remove existing outdated instance(s) of $ProfileName profile: $_"
        Write-Host "$Message"
        exit
    }
    
    try
    {
        $newInstance = New-Object Microsoft.Management.Infrastructure.CimInstance $className, $namespaceName
        $property = [Microsoft.Management.Infrastructure.CimProperty]::Create("ParentID", "$nodeCSPURI", "String", "Key")
        $newInstance.CimInstanceProperties.Add($property)
        $property = [Microsoft.Management.Infrastructure.CimProperty]::Create("InstanceID", "$ProfileNameEscaped", "String", "Key")
        $newInstance.CimInstanceProperties.Add($property)
        $property = [Microsoft.Management.Infrastructure.CimProperty]::Create("ProfileXML", "$ProfileXML", "String", "Property")
        $newInstance.CimInstanceProperties.Add($property)
        $session.CreateInstance($namespaceName, $newInstance, $options)
        $Message = "Created $ProfileName profile."

        Write-Host "$Message"
    }
    catch [Exception]
    {
        $Message = "Unable to create $ProfileName profile: $_"
        Write-Host "$Message"
        exit
    }
    
    $Message = "Script Complete"
    Write-Host "$Message"'
    
    $Script | Out-File -FilePath ($env:USERPROFILE + '\desktop\VPN_Profile.ps1')
    
    $Message = "Successfully created VPN_Profile.xml and VPN_Profile.ps1 on the desktop."
    Write-Host "$Message"
   ```

## Windows PowerShell을 사용 하 여 VPN 클라이언트를 구성 합니다.

VPNv2 CSP에 Windows 10 클라이언트 컴퓨터를 구성 하려면 [XML 프로필 만들기](#create-the-profile-xml) 섹션에서 만든 VPN_Profile.ps1 Windows PowerShell 스크립트를 실행 합니다. 관리자 권한으로 Windows PowerShell을 엽니다. 그렇지 않으면 라는 _액세스 거부_오류를 받게 됩니다.

언제 든 지 확인할 수 VPN 프로필을 구성 하는 VPN_Profile.ps1를 실행 한 후 Windows PowerShell ISE에서 다음 명령을 실행 하 여 성공적인 것입니다.

    Get-WmiObject -Namespace root\cimv2\mdm\dmmap -Class MDM_VPNv2_01

**Get-wmiobject cmdlet의 성공적인 결과**


    __GENUS : 2
    __CLASS : MDM_VPNv2_01
    __SUPERCLASS:
    __DYNASTY   : MDM_VPNv2_01
    __RELPATH   : MDM_VPNv2_01.InstanceID="Contoso%20AlwaysOn%20VPN",ParentID
      ="./Vendor/MSFT/VPNv2"
    __PROPERTY_COUNT: 10
    __DERIVATION: {}
    __SERVER: WIN01
    __NAMESPACE : root\cimv2\mdm\dmmap
    __PATH  : \\WIN01\root\cimv2\mdm\dmmap:MDM_VPNv2_01.InstanceID="Conto
      so%20AlwaysOn%20VPN",ParentID="./Vendor/MSFT/VPNv2"
    AlwaysOn: True
    ByPassForLocal  :
    DnsSuffix   : corp.contoso.com
    EdpModeId   :
    InstanceID  : Contoso%20AlwaysOn%20VPN
    LockDown:
    ParentID: ./Vendor/MSFT/VPNv2
    ProfileXML  : <VPNProfile><RememberCredentials>true</RememberCredentials>
      <AlwaysOn>true</AlwaysOn><DnsSuffix>corp.contoso.com</DnsSu
      ffix><TrustedNetworkDetection>corp.contoso.com</TrustedNetw
      orkDetection><NativeProfile><Servers>vpn.contoso.com;vpn.co
      ntoso.com</Servers><RoutingPolicyType>SplitTunnel</RoutingP
      olicyType><NativeProtocolType>Ikev2</NativeProtocolType><Au
      thentication><UserMethod>Eap</UserMethod><MachineMethod>Eap
      </MachineMethod><Eap><Configuration><EapHostConfig xmlns="h
      ttp://www.microsoft.com/provisioning/EapHostConfig"><EapMet
      hod><Type xmlns="https://www.microsoft.com/provisioning/EapC
      ommon">25</Type><VendorId xmlns="https://www.microsoft.com/p
      rovisioning/EapCommon">0</VendorId><VendorType xmlns="http:
      //www.microsoft.com/provisioning/EapCommon">0</VendorType><
      AuthorId xmlns="https://www.microsoft.com/provisioning/EapCo
      mmon">0</AuthorId></EapMethod><Config xmlns="https://www.mic
      rosoft.com/provisioning/EapHostConfig"><Eap xmlns="https://w
      ww.microsoft.com/provisioning/BaseEapConnectionPropertiesV1
      "><Type>25</Type><EapType xmlns="https://www.microsoft.com/p
      rovisioning/MsPeapConnectionPropertiesV1"><ServerValidation
      ><DisableUserPromptForServerValidation>true</DisableUserPro
      mptForServerValidation><ServerNames>NPS</ServerNames><Trust
      edRootCA>3f 07 88 e8 ac 00 32 e4 06 3f 30 f8 db 74 25 e1
      2e 5b 84 d1 </TrustedRootCA></ServerValidation><FastReconne
      ct>true</FastReconnect><InnerEapOptional>false</InnerEapOpt
      ional><Eap xmlns="https://www.microsoft.com/provisioning/Bas
      eEapConnectionPropertiesV1"><Type>13</Type><EapType xmlns="
      https://www.microsoft.com/provisioning/EapTlsConnectionPrope
      rtiesV1"><CredentialsSource><CertificateStore><SimpleCertSe
      lection>true</SimpleCertSelection></CertificateStore></Cred
      entialsSource><ServerValidation><DisableUserPromptForServer
      Validation>true</DisableUserPromptForServerValidation><Serv
      erNames>NPS</ServerNames><TrustedRootCA>3f 07 88 e8 ac 00
      32 e4 06 3f 30 f8 db 74 25 e1 2e 5b 84 d1 </TrustedRootCA><
      /ServerValidation><DifferentUsername>false</DifferentUserna
      me><PerformServerValidation xmlns="https://www.microsoft.com
      /provisioning/EapTlsConnectionPropertiesV2">true</PerformSe
      rverValidation><AcceptServerName xmlns="https://www.microsof
      t.com/provisioning/EapTlsConnectionPropertiesV2">true</Acce
      ptServerName></EapType></Eap><EnableQuarantineChecks>false<
      /EnableQuarantineChecks><RequireCryptoBinding>false</Requir
      eCryptoBinding><PeapExtensions><PerformServerValidation xml
      ns="https://www.microsoft.com/provisioning/MsPeapConnectionP
      ropertiesV2">true</PerformServerValidation><AcceptServerNam
      e xmlns="https://www.microsoft.com/provisioning/MsPeapConnec
      tionPropertiesV2">true</AcceptServerName></PeapExtensions><
      /EapType></Eap></Config></EapHostConfig></Configuration></E
      ap></Authentication></NativeProfile><DomainNameInformation>
      <DomainName>corp.contoso.com</DomainName><DnsServers>10.10.
      0.2,10.10.0.3</DnsServers><AutoTrigger>true</AutoTrigger></
      DomainNameInformation></VPNProfile>
    RememberCredentials : True
    TrustedNetworkDetection : corp.contoso.com
    PSComputerName  : WIN01

ProfileXML 구성의 구조, 맞춤법 검사, 구성 및 때로는 대/소문자 여야 합니다. 목록 1 구조와 다른 나타나면 가능성이 ProfileXML 태그 오류가 포함 되어 있습니다.

태그 문제를 해결 해야 할 경우에 Windows PowerShell ISE에서 해결 보다 XML 편집기에 배치 하 쉽습니다. 두 경우 모두 프로필의 가장 간단한 버전으로 시작한 구성 요소를 추가 다시 문제가 될 때까지 한 번에 하나씩 다시 발생 합니다.

## <a name="vpn-deploy-client-sccm"></a>System Center Configuration Manager를 사용 하 여 VPN 클라이언트를 구성 합니다.

System Center Configuration Manager에서 Windows PowerShell에서 했던 것과 마찬가지로 ProfileXML CSP 노드를 사용 하 여 VPN 프로필을 배포할 수 있습니다. 여기에서는 [ProfileXML 구성 파일 만들기](#bkmk_ProfileXML)섹션에서 만든 VPN_Profile.ps1 Windows PowerShell 스크립트를 사용 합니다.

Windows 10 클라이언트 컴퓨터에 원격 액세스 Always On VPN 프로필을 배포 하려면 System Center Configuration Manager를 사용 하려면 컴퓨터 또는 사용자 프로필을 배포 그룹을 만들어 시작 해야 합니다. 이 시나리오에서는 구성 스크립트를 배포 하는 사용자 그룹을 만듭니다.

### 사용자 그룹 만들기

1.  Configuration Manager 콘솔에서 자산 및 Compliance\\User 컬렉션을 엽니다.

2.  **홈** 리본의 **만들기** 그룹 **사용자 컬렉션 만들기**를 클릭 합니다.

3.  일반 페이지에서 다음 단계를 완료 합니다.

    a. **이름** **는 VPN 사용자**를 입력 합니다.

    b. **찾아보기**, **모든 사용자** 를 클릭 하 고 **확인**을 클릭 합니다.

    c. **다음**을 클릭합니다.

4.  구성원 규칙 페이지에서 다음 단계를 완료 합니다.

    a.  **구성원 규칙** **규칙 추가**클릭 하 고 **직접 규칙**을 클릭 합니다. 이 예제에서는 개별 사용자에 게 사용자 컬렉션에 추가할 수 있습니다. 그러나 대규모 배포에 대 한 동적으로이 컬렉션에 사용자를 추가할 쿼리 규칙을 사용할 수 있습니다.

    b.  **시작** 페이지에서 **다음**을 클릭 합니다.

    c.  **값**리소스 페이지에 대 한 검색에 추가 하려는 사용자의 이름을 입력 합니다. 리소스 이름에는 사용자의 도메인에 포함 됩니다. 부분 일치에 따라 결과 포함 하려면 삽입 합니다 **%** 검색 조건의 끝에 문자입니다. 예를 들어 입력 "강 영수" 문자열이 포함 된 모든 사용자를 찾으려면 **% 강 영수 %**. **다음**을 클릭합니다.

    d.  리소스 선택 페이지에서 그룹에 추가 하려는 사용자를 선택 하 고 **** 을 클릭 합니다.

    e.  요약 페이지에서 **다음**을 클릭 합니다.

    f.  Completion(완료) 페이지에서 **Close**(닫기)를 클릭합니다.

6.  다시 사용자 컬렉션 만들기 마법사의 구성원 규칙 페이지에서 **다음**을 클릭 합니다.

7.  요약 페이지에서 **다음**을 클릭 합니다.

8.  Completion(완료) 페이지에서 **Close**(닫기)를 클릭합니다.

VPN 프로필을 수신 하도록 사용자 그룹을 만든 후에 패키지와 [ProfileXML 구성 파일 만들기](#bkmk_ProfileXML)섹션에서 만든 Windows PowerShell 구성 스크립트를 배포 하는 프로그램을 만들 수 있습니다.

### ProfileXML 구성 스크립트를 포함 하는 패키지 만들기

1.  사이트 서버 컴퓨터 계정에 액세스할 수 있는 네트워크 공유에서 VPN_Profile.ps1 스크립트를 호스트 합니다.

2.  Configuration Manager 콘솔에서 **소프트웨어 Library\\Application Management\\Packages**를 엽니다.

3.  **홈** 리본의 그룹 **만들기** , 패키지 만들기 및 프로그램 마법사를 시작 하려면 **패키지 만들기** 클릭 합니다.

4.  패키지 페이지에서 다음 단계를 완료 합니다.

    a. **이름** **Windows 10 항상에서 VPN 프로필**을 입력 합니다.

    b. **이 패키지 소스 파일에 들어** 확인란을 선택 하 고 **찾아보기**를 클릭 합니다.

    c. 원본 폴더 설정 대화 상자에서 **찾아보기**, VPN_Profile.ps1, 포함 된 파일 공유를 선택 하 고 **확인**을 클릭 합니다.<p>로컬 경로 하지 네트워크 경로 선택 했는지 확인 합니다. 즉, 경로 *\\fileserver\\vpnscript*, *c:\\vpnscript*하지 같은 것 이어야 합니다.

1.  **다음**을 클릭합니다.

2.  프로그램 유형 페이지에서 **다음**을 클릭 합니다.

3.  표준 프로그램 페이지에서 다음 단계를 완료 합니다.

    a.  **이름** **VPN 프로필 스크립트**를 입력 합니다.

    b.  **명령줄**입력 **PowerShell.exe ExecutionPolicy 바이패스-파일 "VPN_Profile.ps1"** 합니다.

    c.  **실행 모드**에서 **관리자 권한으로 실행**을 클릭 합니다.

    d.  **다음**을 클릭합니다.

4.  요구 사항 페이지에서 다음 단계를 완료 합니다.

    a.  **이 프로그램은 지정 된 플랫폼에만 실행할 수**를 선택 합니다.

    b.  **모든 Windows 10 (32 비트)** 및 **모든 Windows 10 (64 비트)** 확인란을 선택 합니다.

    c.  **예상 디스크 공간** **1**을 입력 합니다.

    d.  **허용 되는 최대 실행된 시간 (분)** 에서 **15**를 입력 합니다.

    e.  **다음**을 클릭합니다.

5.  요약 페이지에서 **다음**을 클릭 합니다.

6.  Completion(완료) 페이지에서 **Close**(닫기)를 클릭합니다.

패키지 및 만든 프로그램을 사용 하 여 **VPN 사용자** 그룹에 배포 해야 합니다.

### ProfileXML 구성 스크립트를 배포 합니다.

1.  Configuration Manager 콘솔에서 소프트웨어 Library\\Application Management\\Packages를 엽니다.

2.  **패키지** **Windows 10 항상에서 VPN 프로필**을 클릭 합니다.

3.  세부 정보 창 맨 아래에 있는 **프로그램** 탭에서 **VPN 프로필 스크립트**를 마우스 오른쪽 단추로 클릭, **속성**을 클릭 하 고 다음 단계를 완료 합니다.

    a.  **이 프로그램은 컴퓨터에 할당 될 때**에서 **고급** 탭 **에 로그온 하는 모든 사용자에 대해 한 번**클릭 합니다.

    b.  **확인**을 클릭합니다.

4.  **VPN 프로필 스크립트** 를 마우스 오른쪽 단추로 클릭 하 고 소프트웨어 배포 마법사를 시작 하려면 **배포** 클릭 합니다.

5.  일반 페이지에서 다음 단계를 완료 합니다.

    a.  **컬렉션**을 옆 **찾아보기**를 클릭 합니다.

    b.  **컬렉션 형식** 목록 (왼쪽 위)에서 **사용자 컬렉션**을 클릭 합니다.

    c.  **VPN 사용자**를 클릭 하 고 **확인**을 클릭 합니다.

    d.  **다음**을 클릭합니다.

6.  콘텐츠 페이지에서 다음 단계를 완료 합니다.

    a.  **추가**클릭 하 고 **배포 지점**을 클릭 합니다.

    b.  **사용 가능한 배포 지점**ProfileXML 구성 스크립트를 배포 하 고 **확인**을 클릭 하 고 배포 지점을 선택 합니다.

    c.  **다음**을 클릭합니다.

7.  배포 설정 페이지에서 **다음**을 클릭 합니다.

8.  일정 페이지에서 다음 단계를 완료 합니다.

    a.  할당 일정 대화 상자를 열려면 **새** 클릭 합니다.

    b.  **이 이벤트 직후 할당**을 클릭 하 고 **확인**을 클릭 합니다.

    c.  **다음**을 클릭합니다.

9.  사용자 환경 페이지에서 다음 단계를 완료 합니다.

    1.  **소프트웨어 설치** 확인란을 선택 합니다.

    2.  **요약**을 클릭 합니다.

10. 요약 페이지에서 **다음**을 클릭 합니다.

11. Completion(완료) 페이지에서 **Close**(닫기)를 클릭합니다.

ProfileXML 구성 배포 스크립트를 사용 하 여 사용자 컬렉션을 빌드할 때 선택한 사용자 계정 사용 하 여 Windows 10 클라이언트 컴퓨터에 로그인 합니다. VPN 클라이언트의 구성을 확인 합니다.

>[!NOTE]
>스크립트 VPN_Profile.ps1 원격 데스크톱 세션에서 작동 하지 않습니다. 마찬가지로, Hyper-v 향상 된 세션에서 작동 하지 않습니다. 가상 컴퓨터에는 원격 액세스 Always On VPN을 테스트 하는 경우 계속 하기 전에 클라이언트 Vm에서 고급 세션을 사용 하지 않도록 설정 합니다.

### VPN 클라이언트의 구성 확인

1.  제어판에서 **System\\Security** **Configuration Manager**를 클릭 합니다. 

2.  **작업** 탭의 Configuration Manager 속성 대화 상자에서 다음 단계를 완료 합니다.

    a.  **컴퓨터 정책 검색 & 평가 주기를**클릭 하 고 **지금 실행** **확인**을 클릭 합니다.

    b.  **사용자 정책 검색 & 평가 주기를**클릭 하 고 **지금 실행** **확인**을 클릭 합니다.

    c.  **확인**을 클릭합니다.

3.  제어판을 닫습니다.

새 VPN 프로필 곧 표시 됩니다.

## Intune을 사용 하 여 VPN 클라이언트를 구성 합니다.

Windows 10 원격 액세스 Always On VPN 프로필을 배포 하려면 Intune을 사용 하려면 [ProfileXML 구성 파일 만들기](#bkmk_ProfileXML), 섹션에서 만든 VPN 프로필을 사용 하 여 ProfileXML CSP 노드를 구성할 수 있습니다. 하거나 제공 된 기본 EAP XML 샘플을 사용할 수 있습니다. 아래 합니다.

>[!NOTE]
>이제 Intune은 Azure AD 그룹을 사용 합니다. 사용자는 VPN 사용자 그룹에 할당 된 Azure AD Connect 동기화를 Azure AD에 온-프레미스에서 VPN 사용자 그룹을 계속 준비가 되었습니다.

그룹에 추가 하는 모든 사용자에 대 한 Windows 10 클라이언트 컴퓨터를 구성 하려면 VPN 장치 구성 정책을 만듭니다. Intune 템플릿을 VPN 매개 변수를 제공만 VPN_ProfileXML 파일의 \<EapHostConfig> \</EapHostConfig> 부분을 복사 합니다. 


### Always On VPN 구성 정책 만들기

1.  [Azure 포털](https://portal.azure.com/)에 로그인 합니다.

2.  **Intune**로 이동 > **장치 구성** > **프로필**합니다.

3.  **프로필 만들기** 만들기 프로필 마법사를 시작을 클릭 합니다.

4.  VPN 프로필 및 설명 (선택 사항)에 대 한 **이름** 을 입력 합니다.

5.   **플랫폼** **Windows 10 이상**선택 하 고 **VPN** 프로필 유형 드롭다운 목록에서 선택 합니다.

     >[!TIP]
     >사용자 지정 VPN profileXML을 만드는 경우 참조 [Intune을 사용 하 여 ProfileXML 적용](https://docs.microsoft.com/windows/security/identity-protection/vpn/vpn-profile-options#apply-profilexml-using-intune) 합니다.

6. **기본 VPN** 탭에서 확인 하거나 다음 설정을 지정 합니다.

    - **연결 이름:** **설정** **VPN** 탭에서 클라이언트 컴퓨터에 예를 들어 _Contoso AutoVPN_표시 될 때 VPN 연결의 이름을 입력 합니다.  
    
    - **서버:** **추가** 클릭 하 여 하나 이상의 VPN 서버 추가
    
    - **설명** 및 **IP 주소 또는 FQDN:** 설명 및 IP 주소 또는 VPN 서버의 FQDN을 입력 합니다. 이러한 값을 VPN 서버 인증 인증서의 주체 이름으로 정렬 해야 합니다. 
    
    - **기본 서버:** 기본 VPN 서버 이면 **True**로 설정 합니다. 이 작업을 수행 하면 장치 연결을 설정 하는 데 사용 하는 기본 서버로 해당이 서버. 
    
    - **연결 형식:** **IKEv2**로 설정 합니다.  
    
    - **항상:** 로그인 다음 사람에 자동으로 VPN에 연결 하 고 수동으로 끊을 때까지 연락할 **사용** 하도록 설정 합니다.
    
    - **로그온 시 사용자 이름 및 암호 자격 증명**: 자격 증명을 캐시에 대 한 부울 값 (true 또는 false). 가능 하면 true, 자격 증명으로 설정 하 고 캐시 되 면 합니다.

7.  텍스트 편집기를 다음 XML 문자열을 복사 합니다.<p>
 
    [!INCLUDE [important-lower-case-true-include](../../../includes/important-lower-case-true-include.md)]
    <p>
    
    ```XML
    <EapHostConfig xmlns="https://www.microsoft.com/provisioning/EapHostConfig"><EapMethod><Type xmlns="https://www.microsoft.com/provisioning/EapCommon">25</Type><VendorId xmlns="https://www.microsoft.com/provisioning/EapCommon">0</VendorId><VendorType xmlns="https://www.microsoft.com/provisioning/EapCommon">0</VendorType><AuthorId xmlns="https://www.microsoft.com/provisioning/EapCommon">0</AuthorId></EapMethod><Config xmlns="https://www.microsoft.com/provisioning/EapHostConfig"><Eap xmlns="https://www.microsoft.com/provisioning/BaseEapConnectionPropertiesV1"><Type>25</Type><EapType xmlns="https://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV1"><ServerValidation><DisableUserPromptForServerValidation>true</DisableUserPromptForServerValidation><ServerNames>NPS.contoso.com</ServerNames><TrustedRootCA>5a 89 fe cb 5b 49 a7 0b 1a 52 63 b7 35 ee d7 1c c2 68 be 4b </TrustedRootCA></ServerValidation><FastReconnect>true</FastReconnect><InnerEapOptional>false</InnerEapOptional><Eap xmlns="https://www.microsoft.com/provisioning/BaseEapConnectionPropertiesV1"><Type>13</Type><EapType xmlns="https://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV1"><CredentialsSource><CertificateStore><SimpleCertSelection>true</SimpleCertSelection></CertificateStore></CredentialsSource><ServerValidation><DisableUserPromptForServerValidation>true</DisableUserPromptForServerValidation><ServerNames>NPS.contoso.com</ServerNames><TrustedRootCA>5a 89 fe cb 5b 49 a7 0b 1a 52 63 b7 35 ee d7 1c c2 68 be 4b </TrustedRootCA></ServerValidation><DifferentUsername>false</DifferentUsername><PerformServerValidation xmlns="https://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2">true</PerformServerValidation><AcceptServerName xmlns="https://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2">true</AcceptServerName></EapType></Eap><EnableQuarantineChecks>false</EnableQuarantineChecks><RequireCryptoBinding>false</RequireCryptoBinding><PeapExtensions><PerformServerValidation xmlns="https://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV2">true</PerformServerValidation><AcceptServerName xmlns="https://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV2">true</AcceptServerName></PeapExtensions></EapType></Eap></Config></EapHostConfig>
    ```

8.  대체 합니다 **\<TrustedRootCA>5a 89 fe cb 5b 49 a 7 0b 1a 52 63 b7 35 ee d 7 1c c2 68 4b<\/TrustedRootCA> 수** 양쪽에 온-프레미스 루트 인증 기관 인증서 지문 사용 하 여 샘플에서입니다.
  
    >[!Important]
    >샘플 지문 \<TrustedRootCA>\</TrustedRootCA> 섹션 아래에서 사용 하지 마세요.  TrustedRootCA의 RRAS 및 NPS 서버에 대 한 서버 인증 인증서를 발급 한 온-프레미스 루트 인증 기관 인증서 지문 이어야 합니다. **클라우드 루트 인증서와 중간 발급 CA 인증서 지문 안됩니다**.

10. 샘플 XML **\<ServerNames>NPS.contoso.com\</ServerNames>** 인증이 발생 하는 도메인에 가입 된 NPS의 FQDN 바꿉니다. 

11. 수정 된 XML 문자열을 복사 하 고 기본 VPN 탭의 **EAP Xml** 상자에 붙여 넣을 **확인**을 클릭 합니다.<p>EAP를 사용 하 여는 항상에서 VPN 장치 구성 정책 Intune에서 만들어집니다.


### Intune 사용 하 여 Always On VPN 구성 정책을 동기화합니다

구성 정책을 테스트 하려면 **항상 VPN 사용자** 그룹에 추가한 사용자로 windows 10 클라이언트 컴퓨터에 로그인 하 고 Intune로 동기화 합니다.

1.  시작 메뉴 **설정**을 클릭 합니다.

2.  설정에서 **계정**을 클릭 하 고 **회사 또는 학교 액세스를**클릭 합니다.

3.  MDM 프로필을 클릭 하 고 **정보**를 클릭 합니다.

4.  **동기화** 를 강제로 Intune 정책 평가 및 검색을 클릭 합니다.

5.  설정을 닫습니다. 동기화 후 컴퓨터에서 사용할 수 있는 VPN 프로필이 표시 합니다.

## 다음 단계
배포 Always On VPN 수행 됩니다.  구성할 수의 다른 기능에 대 한 아래 표를 참조 하세요.

|하려는 경우...  |다음을 참조 하십시오.  |
|---------|---------|
|VPN에 대 한 조건부 액세스 구성    |7 [단계입니다. (선택 사항) Azure AD를 사용 하 여 VPN 연결에 대 한 조건부 액세스 구성](../../ad-ca-vpn-connectivity-windows10.md):이 단계에서는 미세 조정할 수 VPN 사용자가 액세스 권한이 어떻게 [Azure Active Directory (Azure AD) 조건부 액세스](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)를 사용 하 여 리소스입니다. Azure AD 가상 사설망 (VPN) 연결에 대 한 조건부 액세스를 사용 하 여 VPN 연결을 보호할 수 있습니다. 조건부 액세스는 Azure AD(Azure Active Directory)에 연결된 응용 프로그램에 대한 액세스 규칙을 만드는 데 사용되는 정책 기반 평가 엔진입니다.         |
|고급 VPN 기능에 자세히 알아보기  |[VPN 고급 기능](always-on-vpn-adv-options.md#advanced-vpn-features): VPN 트래픽 필터를 사용 하는 방법, 앱 트리거를 사용 하 여 자동 VPN 연결을 구성 하는 방법 및 NPS만 Azure에서 발급 한 인증서를 사용 하 여 클라이언트에서 VPN 연결을 허용 하도록 구성 하는 방법에 지침을 제공 하는이 페이지 광고 합니다.        |


---
