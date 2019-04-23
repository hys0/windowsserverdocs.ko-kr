---
title: Azure AD를 사용한 VPN 연결에 대한 조건부 액세스
description: 이 선택적 단계에서는 어떻게 권한이 부여 된 VPN 사용자 액세스 Azure Active Directory (Azure AD) 조건부 액세스를 사용 하 여 리소스를 조정할 수 있습니다.
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: ''
ms.localizationpriority: medium
ms.author: pashort
author: shortpatti
ms.date: 07/13/2018
ms.reviewer: deverette
ms.openlocfilehash: c9104a5d9ae3069e753b8b771270502c4264db96
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59885274"
---
# <a name="step-7-optional-conditional-access-for-vpn-connectivity-using-azure-ad"></a>7단계. (선택 사항) Azure AD를 사용 하 여 VPN 연결에 대 한 조건부 액세스

&#171;  [**이전:** 6단계. Windows 10 클라이언트를 VPN 연결에 always On 구성](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md)<br>
&#187;[ **다음:** 7.1단계. 인증서 해지 목록 (CRL) 검사를 무시 하도록 EAP-TLS 구성](vpn-config-eap-tls-to-ignore-crl-checking.md)

이 선택적 단계에서는 미세 조정할 수 있습니다 VPN 사용자가 사용 하 여 리소스를 액세스 하는 방식을 [Azure Active Directory (Azure AD) 조건부 액세스](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)합니다. 가상 사설망 (VPN) 연결에 대 한 Azure AD 조건부 액세스를 사용 하 여 VPN 연결을 보호할 수 있습니다. 조건부 액세스는 Azure AD(Azure Active Directory)에 연결된 응용 프로그램에 대한 액세스 규칙을 만드는 데 사용되는 정책 기반 평가 엔진입니다. 

## <a name="prerequisites"></a>사전 요구 사항

다음 항목에 잘 알고 있다면:
- [Azure Active Directory의 조건부 액세스](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)
- [VPN 및 조건부 액세스](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access)

VPN 연결에 대 한 Azure Active Directory 조건부 액세스를 구성 하려면 다음을 구성 했으며 해야 합니다.
- [서버 인프라](always-on-vpn/deploy/vpn-deploy-server-infrastructure.md)
- [VPN Always On에 대 한 원격 액세스 서버](always-on-vpn/deploy/vpn-deploy-ras.md)
- [네트워크 정책 서버](always-on-vpn/deploy/vpn-deploy-nps.md)
- [DNS 및 방화벽 설정](always-on-vpn/deploy/vpn-deploy-dns-firewall.md)
- [VPN 연결에 Always On Windows 10 클라이언트](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md)

## <a name="step-71-configure-eap-tls-to-ignore-certificate-revocation-list-crl-checkingvpn-config-eap-tls-to-ignore-crl-checkingmd"></a>[7.1 단계입니다. 인증서 해지 목록 (CRL) 검사를 무시 하도록 EAP-TLS 구성](vpn-config-eap-tls-to-ignore-crl-checking.md)

이 단계에서 추가할 수 있습니다 **IgnoreNoRevocationCheck** 인증서에 CRL 배포 지점 포함 되지 않은 경우 클라이언트 인증을 허용 하도록 설정 합니다. 기본적으로 IgnoreNoRevocationCheck 0 (해제)으로 설정 됩니다.

NPS 서버 (루트 인증서 포함)의 인증서 체인의 해지 확인을 완료 하지 않으면 EAP-TLS 클라이언트를 연결할 수 없습니다. 1 시간 동안 유지를 사용 하 여 단기 인증서 이기 때문에 클라우드 인증서를 Azure AD에서 사용자에 게 발급 된 CRL을 갖지 않습니다. NPS에서 EAP CRL의 부재를 무시 하도록 구성 해야 합니다. 이 레지스트리 값에만 필요 EAP-TLS 인증 방법 이므로 **EAP\13**합니다. 다른 EAP 인증 방법을 사용 하는 경우 다음 레지스트리 값을 추가 해야 해당 아래도 합니다. 




## <a name="step-72-create-root-certificates-for-vpn-authentication-with-azure-advpn-create-root-cert-for-vpn-auth-azure-admd"></a>[7.2 단계입니다. Azure AD를 사용 하 여 VPN 인증에 대 한 루트 인증서 만들기](vpn-create-root-cert-for-vpn-auth-azure-ad.md)

이 단계에서는 자동으로 테 넌 트에서 VPN 서버 클라우드 앱을 만드는 Azure AD와 VPN 인증에 대 한 루트 인증서를 구성 합니다.  

VPN 연결에 대 한 조건부 액세스를 구성 하려면:
1. (둘 이상의 인증서를 만들 수)는 Azure 포털에서 VPN 인증서를 만듭니다.
2. VPN 인증서를 다운로드 합니다.
3. VPN 서버에 인증서를 배포 합니다.

## <a name="step-73-configure-the-conditional-access-policyvpn-config-conditional-access-policymd"></a>[7.3 단계입니다. 조건부 액세스 정책 구성](vpn-config-conditional-access-policy.md)

이 단계에서는 VPN 연결에 대 한 조건부 액세스 정책을 구성할 수 있습니다. 

조건부 액세스 정책을 구성 하려면:
1. VPN 사용자에 게 할당 되는 조건부 액세스 정책을 만듭니다.
2. 클라우드 앱 설정 **VPN 서버**합니다.
3. (액세스 제어) 권한 부여로 **multi-factor authentication 요구**합니다.  필요에 따라 다른 컨트롤을 사용할 수 있습니다.

## <a name="step-74-deploy-conditional-access-root-certificates-to-on-premises-advpn-deploy-cond-access-root-cert-to-on-premise-admd"></a>[7.4 단계입니다. 온-프레미스에 조건부 액세스 루트 인증서를 배포할 AD](vpn-deploy-cond-access-root-cert-to-on-premise-ad.md)

이 단계에서는 온-프레미스 VPN 인증에 대 한 신뢰할 수 있는 루트 인증서를 배포할 AD입니다.

신뢰할 수 있는 루트 인증서를 배포 하려면를 지정 해야 합니다.
1. 다운로드 한 인증서로 추가 *VPN 인증에 대 한 신뢰할 수 있는 루트 CA*합니다.
2. VPN 서버 및 VPN 클라이언트 루트 인증서를 가져옵니다.
3. 인증서 표시 되며 표시를 확인 합니다. 신뢰할 수 있는 합니다.


## <a name="step-75-create-oma-dm-based-vpnv2-profiles-to-windows-10-devicesvpn-create-oma-dm-based-vpnv2-profilesmd"></a>[7.5 단계입니다. 만들 8.1(OMA-DM 기반 VPNv2 프로 파일을 Windows 10 장치](vpn-create-oma-dm-based-vpnv2-profiles.md)

이 단계에서는 OMA-DM를 만들 수 있습니다 기반 VPN 장치 구성 정책을 배포 하려면 Intune을 사용 하 여 VPNv2 프로 파일입니다. SCCM 또는 PowerShell 스크립트를 사용 하 여 VPNv2 프로필 만들기를 참조 하려는 경우 [VPNv2 CSP 설정이](https://docs.microsoft.com/windows/client-management/mdm/vpnv2-csp) 대 한 자세한 내용은 합니다. 


## <a name="next-step"></a>다음 단계
[7.1 단계입니다. 인증서 해지 목록 (CRL) 검사를 무시 하도록 EAP-TLS 구성](vpn-config-eap-tls-to-ignore-crl-checking.md): 이 단계에서는 추가 해야 합니다 **IgnoreNoRevocationCheck** 인증서에 CRL 배포 지점 포함 되지 않은 경우 클라이언트 인증을 허용 하도록 설정 합니다. 기본적으로 IgnoreNoRevocationCheck 0 (해제)으로 설정 됩니다.

---

## <a name="related-topics"></a>관련 항목
- [VPNv2 프로필 구성](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access): 이제 VPN 클라이언트를 클라우드 기반 조건부 액세스 플랫폼과 통합하여 원격 클라이언트에 대한 디바이스 준수 옵션을 제공할 수 있습니다. 이 단계에서는 사용 하 여 VPNv2 프로필 구성한  **\<DeviceCompliance > \<사용 > true\</활성화 >** 합니다. 
 
- [자동 VPN 프로필을 사용 하 여 Windows 10에서 원격 액세스 향상](https://www.microsoft.com/itshowcase/Article/Content/894/Enhancing-remote-access-in-Windows-10-with-an-automatic-VPN-profile): Microsoft에서 VPN 연결에 대 한 조건부 액세스를 구현 하는 방법에 대해 알아봅니다. VPN 프로필에 장치를 지원 되는 인증 방법 및 장치에 연결 해야 하는 VPN 서버를 포함 하 여 회사 네트워크에 연결 하는 데 필요한 모든 정보가 포함 됩니다. 조건부 액세스 및 single sign-on을 포함 하 여 Windows 10 1 주년 업데이트의 변경 내용을를 Always-On VPN 연결 프로필을 만들 수 있게 되었습니다. 에 대 한 연결 프로필을 만들었습니다 도메인에 가입 된 장치와 Microsoft Intune에서 관리 하는 System Center Configuration Manager 콘솔을 사용 합니다. 

- [Azure Active Directory의 조건부 액세스](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal): 보안은 클라우드를 사용 하 여 조직에 대 한 관심사입니다. 클라우드 리소스를 관리 하는 데 있어 클라우드 보안의 주요 측면은 id 및 액세스 합니다. 모바일 우선, 클라우드 우선 세계에서 사용자는 어디에서 나 다양 한 장치 및 앱을 사용 하 여 조직의 리소스를 액세스할 수 있습니다. 결과적으로 리소스를 액세스할 수 있는 사용자에 초점을 두 충분 하지 않습니다 더 이상. 보안과 생산성 간의 균형을 이루기 위해 IT 전문가 게 필요한 액세스 제어 결정에 리소스 액세스 되는 방법을 고려해.

- [VPN 및 조건부 액세스](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access): 이제 VPN 클라이언트를 클라우드 기반 조건부 액세스 플랫폼과 통합하여 원격 클라이언트에 대한 디바이스 준수 옵션을 제공할 수 있습니다. 조건부 액세스는 Azure AD(Azure Active Directory)에 연결된 응용 프로그램에 대한 액세스 규칙을 만드는 데 사용되는 정책 기반 평가 엔진입니다. 

---