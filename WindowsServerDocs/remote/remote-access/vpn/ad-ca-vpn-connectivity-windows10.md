---
title: Azure AD를 사용한 VPN 연결에 대한 조건부 액세스
description: 이 선택적 단계에서는 권한 있는 VPN 사용자가 Azure Active Directory (Azure AD) 조건부 액세스를 사용 하 여 리소스에 액세스 하는 방법을 미세 조정할 수 있습니다.
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.localizationpriority: medium
ms.author: lizross
author: eross-msft
ms.date: 06/28/2019
ms.reviewer: deverette
ms.openlocfilehash: 1a26f19cee5c6b6faf551633fd1739b1103c6ddf
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80313389"
---
# <a name="step-7-optional-conditional-access-for-vpn-connectivity-using-azure-ad"></a>7단계. 필드 Azure AD를 사용 하 여 VPN 연결에 대 한 조건부 액세스

- [**이전:** 6 단계. Windows 10 클라이언트 Always On VPN 연결 구성](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md)
- [**다음:** 7.1 단계. EAP-TLS를 구성 하 여 CRL (인증서 해지 목록) 검사 무시](vpn-config-eap-tls-to-ignore-crl-checking.md)

이 선택적 단계에서는 VPN 사용자가 [Azure Active Directory (AZURE AD) 조건부 액세스](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)를 사용 하 여 리소스에 액세스 하는 방법을 세밀 하 게 조정할 수 있습니다. Vpn (가상 사설망) 연결에 대 한 Azure AD 조건부 액세스를 사용 하 여 VPN 연결을 보호할 수 있습니다. 조건부 액세스는 Azure AD(Azure Active Directory)에 연결된 애플리케이션에 대한 액세스 규칙을 만드는 데 사용되는 정책 기반 평가 엔진입니다.

## <a name="prerequisites"></a>필수 조건

다음 항목에 대해 잘 알고 있습니다.

- [Azure Active Directory의 조건부 액세스](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)
- [VPN 및 조건부 액세스](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access)

VPN 연결에 대 한 조건부 액세스 Azure Active Directory 구성 하려면 다음을 구성 해야 합니다.

- [서버 인프라](always-on-vpn/deploy/vpn-deploy-server-infrastructure.md)
- [Always On VPN에 대 한 원격 액세스 서버](always-on-vpn/deploy/vpn-deploy-ras.md)
- [네트워크 정책 서버](always-on-vpn/deploy/vpn-deploy-nps.md)
- [DNS 및 방화벽 설정](always-on-vpn/deploy/vpn-deploy-dns-firewall.md)
- [Windows 10 클라이언트 Always On VPN 연결](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md)

## <a name="step-71-configure-eap-tls-to-ignore-certificate-revocation-list-crl-checking"></a>[7.1 단계. EAP-TLS를 구성 하 여 CRL (인증서 해지 목록) 검사 무시](vpn-config-eap-tls-to-ignore-crl-checking.md)

이 단계에서는 **Ignorenorevocationcheck** 를 추가 하 고 인증서에 CRL 배포 지점이 포함 되지 않은 경우 클라이언트 인증을 허용 하도록 설정할 수 있습니다. 기본적으로 IgnoreNoRevocationCheck는 0 (사용 안 함)으로 설정 됩니다.

인증서 체인 (루트 인증서 포함)의 해지 검사를 수행 하지 않는 한 EAP-TLS 클라이언트는 연결할 수 없습니다. Azure AD에서 사용자에 게 발급 한 클라우드 인증서는 수명이 1 시간인 수명이 짧은 인증서 이기 때문에 CRL이 없습니다. NPS의 EAP는 CRL이 없음을 무시 하도록 구성 해야 합니다. 인증 방법이 EAP-TLS 이므로이 레지스트리 값은 **Eap\13**에서만 필요 합니다. 다른 EAP 인증 방법을 사용 하는 경우 레지스트리 값도 그 아래에 추가 해야 합니다.

## <a name="step-72-create-root-certificates-for-vpn-authentication-with-azure-ad"></a>[7.2 단계. Azure AD를 사용 하 여 VPN 인증에 대 한 루트 인증서 만들기](vpn-create-root-cert-for-vpn-auth-azure-ad.md)

이 단계에서는 테 넌 트에서 VPN 서버 클라우드 앱을 자동으로 만드는 Azure AD를 사용 하 여 VPN 인증에 대 한 루트 인증서를 구성 합니다.  

VPN 연결에 대 한 조건부 액세스를 구성 하려면 다음을 수행 해야 합니다.

1. Azure Portal에서 VPN 인증서를 만듭니다.
2. VPN 인증서를 다운로드 합니다.
3. VPN 서버에 인증서를 배포 합니다.

> [!IMPORTANT]
> Azure Portal에서 VPN 인증서가 만들어지면 Azure AD는 VPN 클라이언트에 수명이 짧은 인증서를 즉시 발급 하는 데 사용 하기 시작 합니다. Vpn 클라이언트의 자격 증명 유효성 검사 문제를 방지 하기 위해 vpn 인증서를 VPN 서버에 즉시 배포 하는 것이 중요 합니다.

## <a name="step-73-configure-the-conditional-access-policy"></a>[7.3 단계. 조건부 액세스 정책 구성](vpn-config-conditional-access-policy.md)

이 단계에서는 VPN 연결에 대 한 조건부 액세스 정책을 구성 합니다.

조건부 액세스 정책을 구성 하려면 다음을 수행 해야 합니다.

1. VPN 사용자에 게 할당 되는 조건부 액세스 정책을 만듭니다.
2. 클라우드 앱을 **VPN 서버로**설정 합니다.
3. **Multi-factor authentication을 요구**하도록 Grant (access control)를 설정 합니다.  필요에 따라 다른 컨트롤을 사용할 수 있습니다.

## <a name="step-74-deploy-conditional-access-root-certificates-to-on-premises-ad"></a>[7.4 단계. 온-프레미스 AD에 조건부 액세스 루트 인증서 배포](vpn-deploy-cond-access-root-cert-to-on-premise-ad.md)

이 단계에서는 VPN 인증을 위해 신뢰할 수 있는 루트 인증서를 온-프레미스 AD에 배포 합니다.

신뢰할 수 있는 루트 인증서를 배포 하려면 다음을 수행 해야 합니다.

1. 다운로드 한 인증서를 *VPN 인증에 대 한 신뢰할 수 있는 루트 CA*로 추가 합니다.
2. VPN 서버 및 VPN 클라이언트로 루트 인증서를 가져옵니다.
3. 인증서가 있고 신뢰할 수 있는 것으로 표시 되는지 확인 합니다.

## <a name="step-75-create-oma-dm-based-vpnv2-profiles-to-windows-10-devices"></a>[7.5 단계. Windows 10 장치에 대 한 OMA DM 기반 VPNv2 프로필 만들기](vpn-create-oma-dm-based-vpnv2-profiles.md)

이 단계에서는 Intune을 사용 하 여 VPN 장치 구성 정책을 배포 하는 OMA DM 기반 VPNv2 프로필을 만들 수 있습니다. Configuration Manager 또는 PowerShell 스크립트를 사용 하 여 VPNv2 프로필을 만들려면 [VPNV2 CSP 설정](https://docs.microsoft.com/windows/client-management/mdm/vpnv2-csp) 에서 자세한 내용을 참조 하세요.

## <a name="next-steps"></a>다음 단계

[7.1 단계. 인증서 해지 목록 (CRL) 검사를 무시 하도록 EAP-TLS 구성](vpn-config-eap-tls-to-ignore-crl-checking.md):이 단계에서는 **Ignorenorevocationcheck** 를 추가 하 고 인증서에 crl 배포 지점이 포함 되지 않은 경우 클라이언트의 인증을 허용 하도록 설정 해야 합니다. 기본적으로 IgnoreNoRevocationCheck는 0 (사용 안 함)으로 설정 됩니다.

## <a name="related-topics"></a>관련 항목

- [VPNv2 프로필 구성](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access): 이제 VPN 클라이언트를 클라우드 기반 조건부 액세스 플랫폼과 통합 하 여 원격 클라이언트에 대 한 장치 준수 옵션을 제공할 수 있습니다. 이 단계에서는\<DeviceCompliance >를 사용 하 여 VPNv2 프로필을 구성 합니다. **\<> true\</sh>**

- [자동 vpn 프로필을 사용 하 여 Windows 10에서 원격 액세스 향상](https://www.microsoft.com/itshowcase/Article/Content/894/Enhancing-remote-access-in-Windows-10-with-an-automatic-VPN-profile): MICROSOFT에서 vpn 연결에 대 한 조건부 액세스를 구현 하는 방법을 알아봅니다. VPN 프로필에는 장치가 회사 네트워크에 연결 하는 데 필요한 모든 정보 (지원 되는 인증 방법 및 장치를 연결 해야 하는 VPN 서버 포함)가 포함 됩니다. 조건부 액세스 및 Single Sign-On을 포함 하 여 Windows 10 기념일 업데이트를 변경 하는 경우 항상 VPN 연결 프로필을 만들 수 있었습니다.

- [Azure Active Directory의 조건부 액세스](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal): 보안은 클라우드를 사용 하는 조직에서 가장 중요 한 문제입니다. 클라우드 보안의 주요 측면은 클라우드 리소스를 관리 하는 데 사용 되는 id 및 액세스입니다. 모바일 우선, 클라우드 우선 세계에서 사용자는 어디서 나 다양 한 장치 및 앱을 사용 하 여 조직의 리소스에 액세스할 수 있습니다. 따라서 리소스에 액세스할 수 있는 사용자에 게 더 이상 충분 하지 않습니다. 보안과 생산성 간의 균형을 유지 하기 위해 IT 전문가는 리소스에 액세스 하는 방법도 액세스 제어 결정에 고려해 야 합니다.

- [Vpn 및 조건부 액세스](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access): 이제 vpn 클라이언트를 클라우드 기반 조건부 액세스 플랫폼과 통합 하 여 원격 클라이언트에 대 한 장치 준수 옵션을 제공할 수 있습니다. 조건부 액세스는 Azure AD(Azure Active Directory)에 연결된 애플리케이션에 대한 액세스 규칙을 만드는 데 사용되는 정책 기반 평가 엔진입니다.
