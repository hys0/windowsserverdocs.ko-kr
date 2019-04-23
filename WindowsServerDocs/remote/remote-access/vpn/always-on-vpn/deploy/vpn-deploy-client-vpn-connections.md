---
title: Windows 10 클라이언트 Always On VPN 연결 구성
description: 이 단계에서는 ProfileXML 옵션 및 스키마에 대해 알아봅니다 및 VPN 연결을 사용 하 여 해당 인프라와 통신 하는 Windows 10 클라이언트 컴퓨터를 구성 합니다.
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865894"
---
# <a name="step-6-configure-windows-10-client-always-on-vpn-connections"></a>6단계. Windows 10 클라이언트 Always On VPN 연결 구성

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10


&#171;  [**이전:** 5단계. DNS 및 방화벽 설정 구성](vpn-deploy-dns-firewall.md)<br>
&#187;[ **다음:** 7단계. (선택 사항) Azure AD를 사용 하 여 VPN 연결에 대 한 조건부 액세스](../../ad-ca-vpn-connectivity-windows10.md)

이 단계에서는 ProfileXML 옵션 및 스키마에 대해 알아봅니다 및 VPN 연결을 사용 하 여 해당 인프라와 통신 하는 Windows 10 클라이언트 컴퓨터를 구성 합니다. 

Always On VPN 클라이언트 PowerShell, SCCM 또는 Intune을 통해 구성할 수 있습니다. 세 가지 모두 적절 한 VPN 설정을 구성 하는 XML VPN 프로필을 필요 합니다. PowerShell 자동화 없는 조직 SCCM 또는 Intune에 대 한 등록이 가능 합니다.

>[!NOTE]
>그룹 정책 관리 템플릿 Windows 10 원격 액세스 Always On VPN 클라이언트 구성에 포함 되지 않습니다.  그러나 로그온 스크립트를 사용할 수 있습니다.

## <a name="profilexml-overview"></a>ProfileXML 개요

ProfileXML은 VPNv2 csp URI 노드입니다. 각 VPNv2 CSP 노드를 개별적으로 구성 하는 대신-트리거와 같은 경로 목록 및 인증 프로토콜-단일 CSP 노드를 단일 XML 블록으로 모든 설정을 제공 하 여 Windows 10 VPN 클라이언트를 구성 하려면이 노드를 사용 합니다. ProfileXML 스키마 거의 동일 하 게 VPNv2 CSP 노드의 스키마와 일치 하지만 몇 가지 용어는 약간 다릅니다.

Windows PowerShell, System Center Configuration Manager 및 Intune을 포함 하 여이 배포를 설명 하는 모든 배달 방법 ProfileXML 사용 합니다. 이 배포에서 ProfileXML VPNv2 CSP 노드를 구성 하는 방법은 두 가지 있습니다.

- **OMA-DM**. 첫 번째 방법은 앞 섹션에서 설명한 대로 OMA-DM를 사용 하 여 MDM 공급자를 사용 하도록 [VPNv2 CSP 노드](../always-on-vpn-technology-overview.md#vpnv2-csp-nodes)합니다. 이 메서드를 사용 하 여 쉽게 삽입할 수 있습니다 VPN 프로필 구성 XML 태그 ProfileXML CSP 노드로 Intune을 사용 하는 경우.

- **Windows Management Instrumentation (WMI) CSP 브리지-에-** 합니다. ProfileXML CSP 노드 구성의 두 번째 방법은 WMI-CSP 브리지를 사용 하는 것, WMI 클래스 라고 **MDM_VPNv2_01**-ProfileXML 노드와 VPNv2 CSP 액세스할 수 있는 합니다. 해당 WMI 클래스의 새 인스턴스를 만든 경우 WMI CSP를 사용 하 여 Windows PowerShell 및 System Center Configuration Manager를 사용 하는 경우 VPN 프로필을 만듭니다.

이러한 구성 방법 다를 경우에 올바른 형식의 XML VPN 프로필을 둘 모두 필요 합니다. ProfileXML VPNv2 CSP 설정을 사용 하려면 ProfileXML 스키마를 사용 하 여 간단한 배포 시나리오에 필요한 태그를 구성 하 여 XML을 생성 합니다. 자세한 내용은 [ProfileXML XSD](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/vpnv2-profile-xsd)합니다.

다음 필요한 설정과 해당 ProfileXML 태그의 각 찾습니다. 특정 태그가 ProfileXML 스키마 내에서 각 설정을 구성 하 고 기본 프로필 아래에 나와 있는 것은 모든 키를 누릅니다. 추가 태그 배치 ProfileXML 스키마를 참조 하세요.

[!INCLUDE [important-lower-case-true-include](../../../includes/important-lower-case-true-include.md)]

**연결 형식:** Native IKEv2

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


**트리거:** Always On이 고 신뢰할 수 있는 네트워크 검색

ProfileXML 요소:

    <AlwaysOn>true</AlwaysOn>
    <TrustedNetworkDetection>corp.contoso.com</TrustedNetworkDetection>


**인증:** TPM으로 보호 된 사용자 인증서를 사용 하 여에 PEAP TLS

ProfileXML 요소:

    <Authentication>
    <UserMethod>Eap</UserMethod>
    <Eap>
    <Configuration>...</Configuration>
    </Eap>
    </Authentication>

일부 VPN 인증 메커니즘을 구성 하려면 간단한 태그를 사용할 수 있습니다. 그러나 EAP 및 PEAP는 더 복잡 합니다. EAP 설정을 사용 하 여 VPN 클라이언트를 구성 하 고 다음 구성을 XML로 내보내기를 방법은 하는 XML 태그를 만들기 위한 가장 쉬운 방법입니다. 

EAP 설정에 대 한 자세한 내용은 참조 하십시오 [EAP 구성](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/eap-configuration)합니다. 

## <a name="bkmk_profile"></a>템플릿 연결 프로필을 수동으로 만들기

이 단계를 사용 하 여 Protected Extensible Authentication Protocol \(PEAP\) 클라이언트와 서버 간의 통신을 보호할 수 있습니다. 간단한 사용자 이름 및 암호와 달리이 연결에 작동 하도록 VPN 프로필의 고유한 EAPConfiguration 섹션에 필요 합니다. 

XML 태그를 처음부터 새로 만드는 방법을 설명 하는 대신 사용 하 여 설정을 Windows의 VPN 프로필 템플릿 만들기. 템플릿 VPN 프로필을 만든 후 Windows PowerShell를 사용 하 여 배포에 나중에 배포 하는 최종 ProfileXML를 만들려면 해당 템플릿에서 EAPConfiguration 부분을 사용 하도록 합니다.

### <a name="record-nps-certificate-settings"></a>레코드 NPS 인증서 설정

서식 파일을 만들기 전에 호스트 이름 또는 서버 인증서의 NPS 서버의 정규화 된 도메인 이름 (FQDN) 및 인증서를 발급 한 CA의 이름을 기록해 둡니다.

**절차:**

1.  NPS 서버에서 네트워크 정책 서버를 엽니다.

2.  정책에서 NPS 콘솔에서 클릭 **네트워크 정책**합니다.

3.  마우스 오른쪽 단추로 클릭 **가상 사설망 \(VPN\) 연결**를 클릭 하 고 **속성**합니다.

4.  클릭 합니다 **제약 조건** 탭을 클릭 **인증 방법을**합니다.

5.  EAP 종류에서 **Microsoft: 보호 된 EAP (PEAP)**, 클릭 **편집**합니다.

6.  에 대 한 값을 기록 **에 발급 된 인증서** 하 고 **발급자**합니다.<p>예정 된 VPN 템플릿 구성에서 이러한 값을 사용합니다. 예를 들어 서버의 FQDN이 nps01.corp.contoso.com 경우 호스트 이름은 NPS01 인증서 이름은 서버의-nps01.corp.contoso.com 예를 들어, FQDN 또는 DNS 이름을 기반으로 합니다.

7.  보호 된 EAP 속성 편집 대화 상자를 취소 합니다.

8.  가상 개인 네트워크 (VPN) 연결 속성 대화 상자를 취소 합니다.

9.  네트워크 정책 서버를 닫습니다.

>[!NOTE]
>여러 NPS 서버를 설정한 경우 VPN 프로필을 확인할 수 있도록 각 할 각각에서 이러한 단계를 완료 합니다.

### <a name="configure-the-template-vpn-profile-on-a-domain-joined-client-computer"></a>도메인에서 VPN 프로필 템플릿 구성\-가입 된 클라이언트 컴퓨터

되었으니 이제 도메인에 가입 된 클라이언트 컴퓨터에서 VPN 프로필 템플릿을 구성 하는 데 필요한 정보입니다. 사용할 사용자 계정의 유형을 \(표준 사용자나 관리자,\) 프로세스의이 부분에 상관 없이 대 한 합니다. 

그러나 인증서 자동 등록을 구성한 후 컴퓨터를 다시 시작 하지 않은 경우 이렇게 템플릿 등록에 사용 가능한 인증서를 확인 하기 위해 VPN 연결을 구성 하기 전에 합니다.

>[!NOTE]
>VPN, Always On NRPT 규칙 등의 고급 속성을 수동으로 추가할 방법이 있으면 네트워크 검색 등을 신뢰할 수 있는 합니다. 다음 단계에서는, VPN 서버의 구성을 확인 하려면 테스트 VPN 연결을 만들고는 서버에 VPN 연결을 설정할 수 있습니다.

**단일 테스트 VPN 연결을 수동으로 만들기**

1.  멤버인 도메인에 가입 된 클라이언트 컴퓨터에 로그인 합니다 **VPN 사용자** 그룹입니다.

2.  시작 메뉴에서 입력 **VPN**, Enter 키를 누릅니다.

3.  세부 정보 창에서 클릭 **VPN 연결 추가**합니다.

4.  VPN 공급자 목록에서 클릭 **Windows (기본 제공)** 합니다.

5.  연결 이름 입력 **템플릿**합니다.

6.  서버 이름 또는 주소를 입력 합니다 **외부** VPN 서버의 FQDN \(예를 들어 **vpn.contoso.com**\)합니다.

7.  **저장**을 클릭합니다.

8.  관련 설정에서 클릭 **어댑터 옵션을 변경**합니다.

9.  마우스 오른쪽 단추로 클릭 **템플릿을**, 클릭 **속성**합니다.

10. 에 **보안** 탭의 **VPN 종류**, 클릭 **IKEv2**합니다.

11. 데이터 암호화, 클릭 **최대 강력한 암호화**합니다.

12. 클릭 **확장 인증 프로토콜 (EAP)**; 그런 **사용 하 여 확장 인증 프로토콜 (EAP)**, 클릭 **Microsoft: 보호 된 EAP (PEAP) (암호화 사용)** 합니다.

13. 클릭 **속성** 보호 된 EAP 속성 대화 상자를 열고 다음 단계를 완료 합니다.

    a. 에 **이러한 서버에 연결** NPS 서버 인증 설정 (예를 들어 NPS01)이이 섹션 앞부분에서에서 검색 하는 NPS 서버의 이름을 입력 합니다.

    >[!NOTE]
    >서버 이름을 입력 하는 인증서의 이름과 일치 해야 합니다. 이 섹션의 앞부분에이 이름은 복구할 수 있습니다. 이름이 일치 하지 않는 경우 연결이 실패를 알리는 "연결 하지 못했습니다 RAS/VPN 서버에서 구성 된 정책으로 인해."

    b.  신뢰할 수 있는 루트 인증 기관에서 루트 (예: contoso-CA) NPS 서버의 인증서를 발급 한 CA를 선택 합니다.

    다.  연결 전에 알림, 클릭 **새 서버 또는 신뢰할 수 있는 Ca를 허가 하도록 사용자를 묻지**합니다.

    d.  인증 방법 선택, 클릭 **스마트 카드 또는 기타 인증서**, 클릭 **구성**합니다. 스마트 카드 또는 기타 인증서 속성 대화 상자를 엽니다.

    e.  클릭 **이 컴퓨터에 인증서를 사용 하 여**입니다.

    f.  이러한 서버 상자에 대 한 연결을 이전 단계에서 NPS 서버 인증 설정에서 검색 하는 NPS 서버 이름을 입력 합니다.

    g.  신뢰할 수 있는 루트 인증 기관에서 루트 NPS 서버의 인증서를 발급 한 CA를 선택 합니다.

    h.  선택 된 **새 서버를 허가 하도록 사용자를 묻지 신뢰할 수 있는 인증 기관 또는** 확인란 합니다.

    i.  클릭 **확인** 를 스마트 카드 또는 기타 인증서 속성 대화 상자를 닫습니다.

    j.  클릭 **확인** 보호 된 EAP 속성 대화 상자를 닫습니다.

10. 클릭 **확인** 템플릿 속성 대화 상자를 닫습니다.

11. 네트워크 연결 창을 닫습니다.

12. 클릭 하 여 VPN 설정에서 테스트 **템플릿을**를 클릭 하 고 **Connect**합니다.

>[!IMPORTANT]
>템플릿 VPN 서버에 VPN 연결 성공 인지 확인 합니다. 이렇게 하면 다음 예제에서 사용 하기 전에 EAP 설정이 정확한 지. 계속 하기 전에 한 번 이상 연결 해야 합니다. 그렇지 않으면 프로필에서 VPN에 연결 하는 데 필요한 모든 정보가 포함 되지 않습니다.

## <a name="bkmk_ProfileXML"></a>ProfileXML 구성 파일 만들기

이 섹션을 완료 하기 전에 템플릿 VPN 연결을 테스트를 만들고 있는지 확인 하는 섹션 [템플릿 연결 프로필을 수동으로 만들](#bkmk_profile) 에 대해 설명 합니다. 프로필에서 VPN에 연결 하는 데 필요한 모든 정보가 포함 되어 있는지 확인 해야 하는 VPN 연결을 테스트 합니다.

목록 1에서 Windows PowerShell 스크립트는 둘 다 포함 바탕 화면에서 두 파일을 만듭니다 **EAPConfiguration** 이전에 만든 템플릿 연결 프로필을 기반으로 하는 태그:

-   **VPN_Profile.xml.** 이 파일 VPNv2 CSP에 ProfileXML 노드를 구성 하는 데 필요한 XML 태그를 포함 합니다. Intune 같은 MDM OMA DM 호환 서비스를 사용 하 여이 파일을 사용 합니다.

-   **VPN_Profile.ps1.** 이 파일은 실행할 수 있는 Windows PowerShell 스크립트를 VPNv2 CSP에 ProfileXML 노드를 구성 하려면 클라이언트 컴퓨터입니다. 또한이 스크립트를 통해 System Center Configuration Manager를 배포 하 여 CSP를 구성할 수 있습니다. 향상 된 Hyper-v가 세션을 포함 하 여 원격 데스크톱 세션에서이 스크립트를 실행할 수 없습니다.

>[!IMPORTANT]
>아래 예제에서는 명령에는 Windows 10 빌드 1607 이상 필요합니다.

**VPN_Profile.xml 만들고 VPN_Proflie.ps1**

1. 동일한 사용자를 사용 하 여 VPN 프로필 템플릿이 포함 된 도메인에 가입 된 클라이언트 컴퓨터에 로그인 계정을 섹션 "수동으로 만들기 템플릿 연결 프로필을" 설명 합니다.

2. Windows PowerShell 통합된 스크립팅 환경에 코드 1을 붙여 넣습니다 \(ISE\), 및 설명에 설명 된 매개 변수를 사용자 지정 합니다. 다음은 $Template, $ProfileName, $Servers, $DnsSuffix, $DomainName, $TrustedNetwork, $DNSServers입니다. 각 설정에 대 한 전체 설명은 주석입니다.

3.  생성 스크립트를 실행 **VPN_Profile.xml** 하 고 **VPN_Profile.ps1** 바탕 화면입니다.

#### <a name="listing-1-understanding-makeprofileps1"></a>목록 1. Understanding MakeProfile.ps1

이 섹션에서는 VPNv2 CSP에 ProfileXML 구성 VPN 프로필을 만드는 방법의 이해를 갖추기 위해 사용할 수 있는 예제 코드를 설명 합니다.

이 예제에서는 코드에서 스크립트를 조합 하 고 스크립트를 실행 한 후 스크립트에서는 두 개의 파일을 생성 합니다. VPN_Profile.xml 및 VPN_Profile.ps1 합니다. VPN_Profile.xml를 사용 하 여 8.1(OMA-DM 규격 MDM 서비스에서 Microsoft Intune과 같은 ProfileXML를 구성 합니다.

사용 된 **VPN_Profile.ps1** Windows PowerShell 또는 System Center Configuration Manager Windows 10 데스크톱에서 ProfileXML를 구성 하는 스크립트.

>[!NOTE]
>전체 예제 스크립트를 보려면 섹션을 참조 하세요 [MakeProfile.ps1 전체 스크립트](#bkmk_fullscript)합니다.

#### <a name="parameters"></a>매개 변수

다음 매개 변수를 구성 합니다.

**$Template**합니다. EAP 구성을 검색 하는 템플릿의 이름입니다.

**$ProfileName**. 프로필의 고유한 영숫자 식별자입니다. 프로필 이름은 슬래시 (/)를 포함할 수 없습니다. 프로필 이름에 공백이 나 다른 영숫자가 아닌 문자가 있으면이 적절히 이스케이프 되어야 URL 인코딩 표준에 따라 합니다.

**$Servers**합니다. 공용 또는 라우팅 가능 IP 주소 또는 VPN gateway에 대 한 DNS 이름입니다. 이 게이트웨이의 IP 또는 서버 팜에 대 한 가상 IP를 외부 가리킬 수 있습니다. 예제를 208.147.66.130 또는 vpn.contoso.com입니다.

**$DnsSuffix**. DNS 접미사를 구분 하는 하나 이상의 쉼표가 지정 합니다. 목록의 첫 번째도 VPN 인터페이스에 대 한 기본 연결에 대 한 DNS 접미사로 사용 됩니다. 목록 전체를 SuffixSearchList에도 추가 됩니다.

**$DomainName**. 정책이 적용 되는 네임 스페이스를 나타내는 데 사용 합니다. 이름 쿼리를 실행 하면 DNS 클라이언트에 일치 항목을 찾지 DomainNameInformationList에서 네임 스페이스의 모든 쿼리에 이름을 비교 합니다. 이 매개 변수는 다음 형식 중 하나일 수 있습니다.

- FQDN-정규화 된 도메인 이름
- 접미사-도메인 접미사를 DNS 확인을 위해 짧은 이름이 쿼리에 추가 됩니다. 접미사를 지정 하려면 마침표 앞에 추가 \(.) DNS 접미사에 있습니다.

**$DNSServers**합니다. 네임 스페이스에 사용할 목록을 쉼표로 구분 된 DNS 서버 IP 주소입니다.

**$TrustedNetwork**. 신뢰할 수 있는 네트워크를 식별 하려면 쉼표로 구분 된 문자열입니다. VPN은 사용자가 보호 된 리소스가 장치에 직접 액세스할 수 있는 회사 무선 네트워크에 자동으로 연결 하지 않습니다.

다음은 예제 값 아래 명령에서 사용 된 매개 변수입니다. 사용자 환경에 대 한 이러한 값을 변경 하는 것을 확인 합니다.

    $TemplateName = 'Template'
    $ProfileName = 'Contoso AlwaysOn VPN'
    $Servers = 'vpn.contoso.com'
    $DnsSuffix = 'corp.contoso.com'
    $DomainName = '.corp.contoso.com'
    $DNSServers = '10.10.0.2,10.10.0.3'
    $TrustedNetwork = 'corp.contoso.com'


### <a name="prepare-and-create-the-profile-xml"></a>프로필 XML을 만들고 준비

다음 예제 명령은 템플릿 프로필에서 EAP 설정을 가져오려면


    $Connection = Get-VpnConnection -Name $TemplateName
    if(!$Connection)
    {
    $Message = "Unable to get $TemplateName connection profile: $_"
    Write-Host "$Message"
    exit
    }
    $EAPSettings= $Connection.EapConfigXmlStream.InnerXml


### <a name="create-the-profile-xml"></a>XML 프로필 만들기

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


### <a name="output-vpnprofilexml-for-intune"></a>Intune에 대 한 출력 VPN_Profile.xml

프로필 XML 파일을 저장 하려면 다음 예제에서는 명령을 사용할 수 있습니다.

    $ProfileXML | Out-File -FilePath ($env:USERPROFILE + '\desktop\VPN_Profile.xml')

### <a name="output-vpnprofileps1-for-the-desktop-and-system-center-configuration-manager"></a>데스크톱 및 System Center Configuration Manager에 대 한 출력 VPN_Profile.ps1

다음 예제 코드 VPNv2 CSP에 ProfileXML 노드를 사용 하 여 AlwaysOn IKEv2 VPN 연결을 구성 합니다.

Windows 10 데스크톱 또는 System Center Configuration Manager에서이 스크립트를 사용할 수 있습니다.

### <a name="define-key-vpn-profile-parameters"></a>키의 VPN 프로필 매개 변수를 정의 합니다.

    $Script = '$ProfileName = ''' + $ProfileName + '''
    $ProfileNameEscaped = $ProfileName -replace ' ', '%20'

## <a name="define-vpn-profilexml"></a>VPN ProfileXML 정의

    $ProfileXML = ''' + $ProfileXML + '''
    
### <a name="escape-special-characters-in-the-profile"></a>프로필의 이스케이프 특수 문자

    $ProfileXML = $ProfileXML -replace '<', '&lt;'
    $ProfileXML = $ProfileXML -replace '>', '&gt;'
    $ProfileXML = $ProfileXML -replace '"', '&quot;'
    
### <a name="define-wmi-to-csp-bridge-properties"></a>WMI-CSP 브리지 속성 정의

    $nodeCSPURI = "./Vendor/MSFT/VPNv2"
    $namespaceName = "root\cimv2\mdm\dmmap"
    $className = "MDM_VPNv2_01"

### <a name="determine-user-sid-for-vpn-profile"></a>VPN 프로필에 대 한 사용자 SID를 결정 합니다.

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
    

### <a name="define-wmi-session"></a>WMI 세션을 정의 합니다.

    $session = New-CimSession
    $options = New-Object Microsoft.Management.Infrastructure.Options.CimOperationOptions
    $options.SetCustomOption("PolicyPlatformContext_PrincipalContext_Type", "PolicyPlatform_UserContext", $false)
    $options.SetCustomOption("PolicyPlatformContext_PrincipalContext_Id", "$SidValue", $false)


### <a name="detect-and-delete-previous-vpn-profile"></a>검색 및 이전 VPN 프로필을 삭제 합니다.

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
    

### <a name="create-the-vpn-profile"></a>VPN 프로필을 만듭니다.

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

### <a name="save-the-profile-xml-file"></a>프로필 XML 파일 저장

    $Script | Out-File -FilePath ($env:USERPROFILE + '\desktop\VPN_Profile.ps1')
    
    $Message = "Successfully created VPN_Profile.xml and VPN_Profile.ps1 on the desktop."
    Write-Host "$Message"

## <a name="bkmk_fullscript"></a>MakeProfile.ps1 Full Script

대부분의 예제 ProfileXML MDM_VPNv2_01 WMI 클래스의 새 인스턴스를 삽입할 Set-wmiinstance Windows PowerShell cmdlet을 사용 합니다. 

그러나이 작동 하지 않습니다 System Center Configuration Manager에서 최종 사용자의 컨텍스트에서 패키지를 실행할 수 없으므로 있습니다. 따라서이 스크립트는 사용자의 컨텍스트에서 WMI 세션을 만들려면 Common Information Model을 사용 하 고 그런 다음 해당 세션에서 MDM_VPNv2_01 WMI 클래스의 새 인스턴스를 만듭니다. 이 WMI 클래스 VPNv2 CSP를 구성 하는 WMI-CSP 브리지를 사용 합니다. 따라서 클래스 인스턴스를 추가 하 여 CSP 구성 합니다. 

>[!IMPORTANT]
>WMI-CSP 브리지 디자인 하 여 로컬 관리자 권한이 필요합니다. 당 사용자 VPN 프로필 배포를 사용 해야 SCCM 또는 MDM.

>[!NOTE]
>현재 사용자의 SID를 사용 하 여 사용자의 컨텍스트를 식별 하는 VPN_Profile.ps1 스크립트입니다. 원격 데스크톱 세션에서 사용할 수 없는 SID 이기 때문에 원격 데스크톱 세션에서 스크립트가 작동 하지 않습니다. 마찬가지로, 향상 된 Hyper-v 세션에서 작동 하지 않습니다. 원격 액세스 Always On VPN, 가상 컴퓨터에서 테스트 하려는 경우이 스크립트를 실행 하기 전에 클라이언트 Vm에서 고급 세션을 사용 하지 않도록 설정 합니다.

다음 예제 스크립트는 모든 이전 섹션의 코드 예제를 포함합니다. 환경에 적합 한 값으로 예제 값을 변경 하는 것을 확인 합니다.
    
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

## <a name="configure-the-vpn-client-by-using-windows-powershell"></a>Windows PowerShell을 사용 하 여 VPN 클라이언트 구성

VPNv2 CSP는 Windows 10 클라이언트 컴퓨터를 구성 하려면에서 만든 VPN_Profile.ps1 Windows PowerShell 스크립트를 실행 합니다 [XML 프로필을 만들](#create-the-profile-xml) 섹션입니다. 관리자 권한으로 Windows PowerShell을 엽니다. 그렇지 않으면 말했다는 거 야 하는 오류를 받게 _액세스가 거부 되었습니다_합니다.

VPN 프로필을 구성 하는 VPN_Profile.ps1를 실행 한 후 언제 든 지 확인할 수 있습니다 성공 Windows PowerShell ISE에서 다음 명령을 실행 하 여:

    Get-WmiObject -Namespace root\cimv2\mdm\dmmap -Class MDM_VPNv2_01

**Get-wmiobject cmdlet에서 성공적인 결과**


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

ProfileXML 구성 구조, 맞춤법 검사, 구성 및 경우에 따라 대/소문자에서 정확 해야 합니다. 목록 1에 구조 내의 다른 항목을 표시 하는 경우 가능성이 ProfileXML 태그에 오류가 있습니다.

태그의 문제를 해결 하는 경우에 Windows PowerShell ISE에서 해결 하는 보다 XML 편집기에 삽입할 쉽습니다. 두 경우 모두에서 프로필의 가장 간단한 버전을 사용 하 여 시작 구성 요소를 추가 다시 문제까지 한 번에 하나씩 다시 발생 합니다.

## <a name="vpn-deploy-client-sccm"></a>System Center Configuration Manager를 사용 하 여 VPN 클라이언트 구성

System Center Configuration Manager에서 Windows PowerShell에서 했던 것과 마찬가지로 ProfileXML CSP 노드를 사용 하 여 VPN 프로필을 배포할 수 있습니다. 섹션에서 만든 VPN_Profile.ps1 Windows PowerShell 스크립트를 사용 하는 이때 [ProfileXML 구성 파일을 만들](#bkmk_ProfileXML)합니다.

Windows 10 클라이언트 컴퓨터에 원격 액세스 Always On VPN 프로필을 배포 하려면 System Center Configuration Manager를 사용 하려면 컴퓨터 또는 사용자에 게 부여한 프로필을 배포할 그룹을 만들어 시작 해야 합니다. 이 시나리오에서는 구성 스크립트를 배포할 사용자 그룹을 만듭니다.

### <a name="create-a-user-group"></a>사용자 그룹 만들기

1.  Configuration Manager 콘솔에서 자산 및 준수를 열고\\사용자 컬렉션입니다.

2.  에 **홈** 리본의 합니다 **만들기** 그룹에서 클릭 **사용자 컬렉션 만들기**합니다.

3.  일반 페이지에서 다음 단계를 수행 합니다.

    a. **이름을**, 형식 **VPN 사용자**합니다.

    b. 클릭 **찾아보기**, 클릭 **모든 사용자** 누릅니다 **확인**합니다.

    다. **다음**을 클릭합니다.

4.  멤버 관리 규칙 페이지에서 다음 단계를 수행 합니다.

    a.  **멤버 관리 규칙**, 클릭 **규칙 추가**를 클릭 하 고 **직접 규칙**합니다. 이 예제에서는 사용자 컬렉션에 개별 사용자를 추가 하는 합니다. 그러나 대규모 배포에 대해 동적으로이 컬렉션에 사용자를 추가 하려면 쿼리 규칙을 사용할 수 있습니다.

    b.  **시작** 페이지에서 **다음**을 클릭합니다.

    다.  리소스 페이지에 대 한 검색에서 **값**를 추가 하려는 사용자의 이름을 입력 합니다. 리소스 이름에는 사용자의 도메인이 포함 됩니다. 부분 일치를 기준으로 결과 포함 하려면 삽입 합니다 **%** 검색 기준의 한쪽 끝에서 문자입니다. 예를 들어, 입력 "lori" 문자열이 포함 된 모든 사용자를 찾으려면 **%lori%** 합니다. **다음**을 클릭합니다.

    d.  리소스 선택 페이지에서 그룹에 추가 하 고 클릭 하려는 사용자를 선택 **다음**합니다.

    e.  요약 페이지에서 클릭 **다음**합니다.

    f.  완료 페이지에서 클릭 **닫기**합니다.

6.  사용자 컬렉션 만들기 마법사의 멤버 자격 규칙 페이지에서 다시 **다음**합니다.

7.  요약 페이지에서 클릭 **다음**합니다.

8.  완료 페이지에서 클릭 **닫기**합니다.

패키지 및 프로그램 배포 섹션에서 만든 Windows PowerShell 구성 스크립트를 만들면 VPN 프로필을 받을 사용자 그룹을 만든 후 [ProfileXML 구성 파일을 만들](#bkmk_ProfileXML)합니다.

### <a name="create-a-package-containing-the-profilexml-configuration-script"></a>ProfileXML 구성 스크립트가 포함 된 패키지 만들기

1.  사이트 서버 컴퓨터 계정에 액세스할 수 있는 네트워크 공유에 VPN_Profile.ps1 스크립트를 호스트 합니다.

2.  Configuration Manager 콘솔에서 엽니다 **소프트웨어 라이브러리\\응용 프로그램 관리\\패키지**합니다.

3.  에 **홈** 리본의 **만들기** 그룹에서 클릭 **패키지 만들기** 만들 패키지 및 프로그램 마법사를 시작 합니다.

4.  패키지 페이지에서 다음 단계를 수행 합니다.

    a. **이름을**, 형식 **Windows 10 Always On VPN 프로필**합니다.

    b. 선택 된 **이 패키지에 원본 파일이** 확인란을 클릭 **찾아보기**합니다.

    다. 원본 폴더 설정 대화 상자에서 클릭 **찾아보기**VPN_Profile.ps1, 포함 된 파일 공유를 선택 하 고 클릭 **확인**합니다.<p>로컬 경로가 아닌 네트워크 경로 선택 했는지 확인 합니다. 즉, 경로와 같아야  *\\fileserver\\vpnscript*아니라 *c:\\vpnscript*합니다.

1.  **다음**을 클릭합니다.

2.  프로그램 유형 페이지에서 클릭 **다음**합니다.

3.  표준 프로그램 페이지에서 다음 단계를 수행 합니다.

    a.  **이름을**, 형식 **VPN 프로필 스크립트**합니다.

    b.  **명령줄**, 형식 **PowerShell.exe-ExecutionPolicy 무시-파일 "VPN_Profile.ps1"** 합니다.

    다.  **실행 모드**, 클릭 **관리자 권한으로 실행**합니다.

    d.  **다음**을 클릭합니다.

4.  요구 사항 페이지에서 다음 단계를 수행 합니다.

    a.  선택 **지정 된 플랫폼 에서만이 프로그램 실행**합니다.

    b.  선택 된 **모든 Windows 10 (32 비트)** 하 고 **모든 Windows 10 (64 비트)** 확인란 합니다.

    다.  **예상 디스크 공간**, 형식 **1**합니다.

    d.  **최대 허용 실행된 시간 (분)**, 형식 **15**합니다.

    e.  **다음**을 클릭합니다.

5.  요약 페이지에서 클릭 **다음**합니다.

6.  완료 페이지에서 클릭 **닫기**합니다.

패키지 및 만든 프로그램을 사용 하 여 배포 해야 합니다 **VPN 사용자** 그룹입니다.

### <a name="deploy-the-profilexml-configuration-script"></a>ProfileXML 구성 스크립트를 배포 합니다.

1.  Configuration Manager 콘솔에서 소프트웨어 라이브러리를 엽니다\\응용 프로그램 관리\\패키지 있습니다.

2.  **패키지**, 클릭 **Windows 10 Always On VPN 프로필**합니다.

3.  에 **프로그램** 세부 정보 창의 맨 아래에 있는 탭을 마우스 오른쪽 단추로 클릭 **VPN 프로필 스크립트**, 클릭 **속성**, 다음 단계를 완료 하 고:

    a.  에 **고급** 탭의 **이 프로그램이 컴퓨터에 할당 된 경우**, 클릭 **로그온 하는 모든 사용자에 한 번씩**합니다.

    b.  **확인**을 클릭합니다.

4.  마우스 오른쪽 단추로 클릭 **VPN 프로필 스크립트** 누릅니다 **배포** 소프트웨어 배포 마법사를 시작 합니다.

5.  일반 페이지에서 다음 단계를 수행 합니다.

    a.  옆에 있는 **컬렉션**, 클릭 **찾아보기**합니다.

    b.  에 **컬렉션 형식을** 목록 (왼쪽 위)를 클릭 **사용자 컬렉션**합니다.

    다.  클릭 **VPN 사용자**, 클릭 **확인**합니다.

    d.  **다음**을 클릭합니다.

6.  콘텐츠 페이지에서 다음 단계를 수행 합니다.

    a.  클릭 **추가**, 클릭 **배포 지점**합니다.

    b.  **사용 가능한 배포 지점**를 클릭 하 여 ProfileXML 구성 스크립트를 배포 하려는 배포 지점을 선택 **확인**합니다.

    다.  **다음**을 클릭합니다.

7.  배포 설정 페이지에서 클릭 **다음**합니다.

8.  일정 페이지에서 다음 단계를 수행 합니다.

    a.  클릭 **새로 만들기** 할당 일정 대화 상자를 엽니다.

    b.  클릭 **이 이벤트 직후 할당**, 클릭 **확인**합니다.

    다.  **다음**을 클릭합니다.

9.  사용자 환경 페이지에서 다음 단계를 수행 합니다.

    1.  선택 된 **소프트웨어 설치** 확인란 합니다.

    2.  클릭 **요약**합니다.

10. 요약 페이지에서 클릭 **다음**합니다.

11. 완료 페이지에서 클릭 **닫기**합니다.

배포 ProfileXML 구성 스크립트를 사용 하 여 사용자 컬렉션을 빌드할 때 선택한 사용자 계정 사용 하 여 Windows 10 클라이언트 컴퓨터에 로그인 합니다. VPN 클라이언트 구성을 확인 합니다.

>[!NOTE]
>원격 데스크톱 세션에서 스크립트 VPN_Profile.ps1 작동 하지 않습니다. 마찬가지로, 향상 된 Hyper-v 세션에서 작동 하지 않습니다. 원격 액세스 Always On VPN, 가상 컴퓨터에서 테스트 하려는 경우 계속 하기 전에 클라이언트 Vm에서 고급 세션을 사용 하지 않도록 설정 합니다.

### <a name="verify-the-configuration-of-the-vpn-client"></a>VPN 클라이언트 구성 확인

1.  제어판에서 아래 **시스템\\Security**, 클릭 **Configuration Manager**합니다. 

2.  Configuration Manager 속성 대화 상자에서에 **작업** 탭에서 다음 단계를 완료 합니다.

    a.  클릭 **컴퓨터 정책 검색 및 평가 주기**, 클릭 **지금 실행**를 클릭 하 고 **확인**합니다.

    b.  클릭 **사용자 정책 검색 및 평가 주기**, 클릭 **지금 실행**를 클릭 하 고 **확인**합니다.

    다.  **확인**을 클릭합니다.

3.  제어판을 닫습니다.

곧 새로운 VPN 프로필이 표시 됩니다.

## <a name="configure-the-vpn-client-by-using-intune"></a>Intune을 사용 하 여 VPN 클라이언트 구성

Windows 10 원격 액세스 Always On VPN 프로필을 배포 하려면 Intune을 사용 하려면 ProfileXML CSP 노드 섹션에서 만든 VPN 프로필을 사용 하 여 구성할 수 있습니다 [ProfileXML 구성 파일을 만들](#bkmk_ProfileXML), 기본 EAP를 사용할 수 있습니다 아래에 제공 된 XML 샘플입니다.

>[!NOTE]
>Intune은 이제 Azure AD 그룹을 사용 합니다. Azure AD Connect 동기화는 온-프레미스에서 Azure AD에 VPN 사용자 그룹의 VPN 사용자 그룹에 할당 된 사용자를 진행할 준비가 되었습니다.

그룹에 추가 하는 모든 사용자에 대 한 Windows 10 클라이언트 컴퓨터를 구성 하려면 VPN 장치 구성 정책을 만듭니다. VPN 매개 변수를 제공 하는 Intune 템플릿, 때문만 복사 합니다 \<EapHostConfig > \</EapHostConfig > VPN_ProfileXML 파일의 부분입니다. 


### <a name="create-the-always-on-vpn-configuration-policy"></a>Always On VPN 구성 정책 만들기

1.  [Azure 포털](https://portal.azure.com/)할 수 있습니다.

2.  로 이동 **Intune** > **장치 구성을** > **프로필**합니다.

3.  클릭 **프로필 만들기** 만들기 프로필 마법사를 시작 합니다.

4.  입력을 **이름을** VPN 프로필 및 (선택 사항)을 설명 합니다.

5.   아래 **플랫폼**를 선택 **Windows 10 이상**를 선택 하 고 **VPN** 프로필 유형 드롭다운 목록에서.

     >[!TIP]
     >사용자 지정 VPN profileXML를 만들려는 경우 참조 [Intune을 사용 하 여 적용 ProfileXML](https://docs.microsoft.com/windows/security/identity-protection/vpn/vpn-profile-options#apply-profilexml-using-intune) 지침에 대 한 합니다.

6. 아래는 **기본 VPN** 탭, 확인 또는 다음 설정을 지정 합니다.

    - **연결 이름:** 클라이언트 컴퓨터에 표시 된 대로 VPN 연결의 이름을 입력 합니다 **VPN** 탭에서 **설정**, 예를 들어 _Contoso AutoVPN_합니다.  
    
    - **서버:** 클릭 하 여 하나 이상의 VPN 서버를 추가할 **추가 합니다.**
    
    - **설명을** 고 **IP 주소 또는 FQDN:** 설명 및 IP 주소 또는 VPN 서버의 FQDN을 입력 합니다. 이러한 값은 VPN 서버 인증 인증서의 주체 이름을 사용 하 여 정렬 되어야 합니다. 
    
    - **기본 서버:** 로 설정 하는 기본 VPN 서버 이면 **True**합니다. 이 수행 하 고 연결을 사용 하 여 장치를 기본 서버로이 서버 수 있습니다. 
    
    - **연결 형식:** 로 **IKEv2**합니다.  
    
    - **Always On:** 로 **사용** 로그인 다음 사람에 자동으로 VPN에 연결 하 고 사용자 연결을 끊습니다 수동으로 연결을 유지 합니다.
    
    - **로그온 할 때마다 자격 증명 기억**:  자격 증명을 캐시에 대 한 부울 값 (true 또는 false) 가능 하면 true, 자격 증명 집합 캐시 되 면 합니다.

7.  텍스트 편집기에 다음 XML 문자열을 복사 합니다.<p>
 
    [!INCLUDE [important-lower-case-true-include](../../../includes/important-lower-case-true-include.md)]
    <p>
    
    ```XML
    <EapHostConfig xmlns="https://www.microsoft.com/provisioning/EapHostConfig"><EapMethod><Type xmlns="https://www.microsoft.com/provisioning/EapCommon">25</Type><VendorId xmlns="https://www.microsoft.com/provisioning/EapCommon">0</VendorId><VendorType xmlns="https://www.microsoft.com/provisioning/EapCommon">0</VendorType><AuthorId xmlns="https://www.microsoft.com/provisioning/EapCommon">0</AuthorId></EapMethod><Config xmlns="https://www.microsoft.com/provisioning/EapHostConfig"><Eap xmlns="https://www.microsoft.com/provisioning/BaseEapConnectionPropertiesV1"><Type>25</Type><EapType xmlns="https://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV1"><ServerValidation><DisableUserPromptForServerValidation>true</DisableUserPromptForServerValidation><ServerNames>NPS.contoso.com</ServerNames><TrustedRootCA>5a 89 fe cb 5b 49 a7 0b 1a 52 63 b7 35 ee d7 1c c2 68 be 4b </TrustedRootCA></ServerValidation><FastReconnect>true</FastReconnect><InnerEapOptional>false</InnerEapOptional><Eap xmlns="https://www.microsoft.com/provisioning/BaseEapConnectionPropertiesV1"><Type>13</Type><EapType xmlns="https://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV1"><CredentialsSource><CertificateStore><SimpleCertSelection>true</SimpleCertSelection></CertificateStore></CredentialsSource><ServerValidation><DisableUserPromptForServerValidation>true</DisableUserPromptForServerValidation><ServerNames>NPS.contoso.com</ServerNames><TrustedRootCA>5a 89 fe cb 5b 49 a7 0b 1a 52 63 b7 35 ee d7 1c c2 68 be 4b </TrustedRootCA></ServerValidation><DifferentUsername>false</DifferentUsername><PerformServerValidation xmlns="https://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2">true</PerformServerValidation><AcceptServerName xmlns="https://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2">true</AcceptServerName></EapType></Eap><EnableQuarantineChecks>false</EnableQuarantineChecks><RequireCryptoBinding>false</RequireCryptoBinding><PeapExtensions><PerformServerValidation xmlns="https://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV2">true</PerformServerValidation><AcceptServerName xmlns="https://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV2">true</AcceptServerName></PeapExtensions></EapType></Eap></Config></EapHostConfig>
    ```

8.  대체는  **\<TrustedRootCA > 5a 89 fe cb 5b 49 a7 0b 1a 52 63 b7 35 ee d 7 1c c2 68 4b 수 <\/TrustedRootCA >** 온-프레미스 루트 인증 기관 인증서 지문 사용 하 여 샘플 양쪽 모두에서.
  
    >[!Important]
    >샘플 지문을 사용 하지 않는 합니다 \<TrustedRootCA >\</TrustedRootCA > 섹션 아래.  TrustedRootCA NPS 및 RRAS 서버에 대 한 서버 인증 인증서를 발급 한 온-프레미스 루트 인증 기관의 인증서 지문 이어야 합니다. **클라우드 루트 인증서 또는 중간 발급 CA 인증서 지문을 아니어야**합니다.

10. 대체는  **\<servernames에 대 > NPS.contoso.com\</ServerNames >** 인증이 발생 하는 도메인에 가입 된 NPS의 FQDN 사용 하 여 XML 샘플에서입니다. 

11. 수정 된 XML 문자열을 복사 및 붙여 합니다 **EAP Xml** 기본 VPN 탭 아래에서 상자 하 고 클릭 **확인**합니다.<p>EAP를 사용 하 여 Always On VPN 장치 구성 정책에는 Intune에서 생성 됩니다.


### <a name="sync-the-always-on-vpn-configuration-policy-with-intune"></a>Intune 사용 하 여 Always On VPN 구성 정책을 동기화합니다

구성 정책을 테스트 하려면 Windows 10 클라이언트 컴퓨터에 사용자로 로그인을 추가할 수는 **항상에서 VPN 사용자** 그룹 및 Intune과 동기화 합니다.

1.  시작 메뉴에서 클릭 **설정을**합니다.

2.  설정에서 클릭 **계정을**, 클릭 **회사 또는 학교 액세스**합니다.

3.  MDM 프로필을 클릭 하 고 클릭 **정보**합니다.

4.  클릭 **동기화** Intune 정책 평가 및 검색을 강제 합니다.

5.  설정을 닫습니다. 동기화 후 컴퓨터에 사용할 수 있는 VPN 프로필이 나타납니다.

## <a name="next-step"></a>다음 단계
배포 Always On VPN 수행 됩니다.  구성할 수 있습니다 다른 기능에 대 한 아래 표를 참조 합니다.

|하려는 경우...  |다음을 참조 하는 중...  |
|---------|---------|
|VPN에 대 한 조건부 액세스를 구성 합니다.    |[7 단계입니다. (선택 사항) Azure AD를 사용 하 여 VPN 연결에 대 한 조건부 액세스를 구성](../../ad-ca-vpn-connectivity-windows10.md): 이 단계에서는 미세 조정할 수 있습니다 어떻게 권한이 부여 된 VPN 사용자 액세스를 사용 하 여 리소스 [Azure Active Directory (Azure AD) 조건부 액세스](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)합니다. 가상 사설망 (VPN) 연결에 대 한 Azure AD 조건부 액세스를 사용 하 여 VPN 연결을 보호할 수 있습니다. 조건부 액세스는 Azure AD(Azure Active Directory)에 연결된 응용 프로그램에 대한 액세스 규칙을 만드는 데 사용되는 정책 기반 평가 엔진입니다.         |
|고급 VPN 기능에 자세히 알아보기  |[고급 VPN 기능](always-on-vpn-adv-options.md#advanced-vpn-features): 이 페이지는 VPN 트래픽 필터를 사용 하는 방법, 앱 트리거를 사용 하 여 자동 VPN 연결을 구성 하는 방법만 Azure AD에서 발급 한 인증서를 사용 하 여 클라이언트에서 VPN 연결을 허용 하도록 NPS를 구성 하는 방법에 지침을 제공 합니다.        |


---
