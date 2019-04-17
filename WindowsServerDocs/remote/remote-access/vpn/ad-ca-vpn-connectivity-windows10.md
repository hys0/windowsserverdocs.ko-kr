---
title: Azure AD를 사용한 VPN 연결에 대한 조건부 액세스
description: 이 선택적 단계에서 VPN 사용자 액세스 방법을 권한이 Azure Active Directory (Azure AD) 조건부 액세스를 사용 하 여 리소스를 조정할 수 있습니다.
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
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2018
ms.locfileid: "6067298"
---
# 7단계. (선택 사항) Azure AD를 사용 하 여 VPN 연결에 대 한 조건부 액세스

& #171;  [ **이전:** 6 단계입니다. VPN 연결에서 Windows 10 클라이언트를 항상 구성](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md)<br>
& #187; [ **다음:** 7.1 단계입니다. EAP-TLS 인증서 해지 목록 (CRL) 검사 무시 하도록 구성](vpn-config-eap-tls-to-ignore-crl-checking.md)

이 선택적 단계에서 VPN 사용자가 [Azure Active Directory (Azure AD) 조건부 액세스](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)를 사용 하 여 리소스를 액세스 하는 방식을 조정할 수 있습니다. Azure AD 가상 사설망 (VPN) 연결에 대 한 조건부 액세스를 사용 하 여 VPN 연결을 보호할 수 있습니다. 조건부 액세스는 Azure AD(Azure Active Directory)에 연결된 응용 프로그램에 대한 액세스 규칙을 만드는 데 사용되는 정책 기반 평가 엔진입니다. 

## 사전 요구 사항

다음 항목을 잘 알고 있다면:
- [Azure Active Directory 조건부 액세스](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)
- [VPN 및 조건부 액세스](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access)

VPN 연결에 대 한 Azure Active Directory 조건부 액세스를 구성 하려면는 다음과 같은 구성 해야 합니다.
- [서버 인프라](always-on-vpn/deploy/vpn-deploy-server-infrastructure.md)
- [원격 액세스 서버에 대 한 VPN에 항상](always-on-vpn/deploy/vpn-deploy-ras.md)
- [네트워크 정책 서버](always-on-vpn/deploy/vpn-deploy-nps.md)
- [DNS 및 방화벽 설정](always-on-vpn/deploy/vpn-deploy-dns-firewall.md)
- [VPN 연결에서 항상 Windows 10 클라이언트](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md)

## [7.1단계. EAP-TLS를 사용하여 CRL(인증서 해지 목록) 확인 무시](vpn-config-eap-tls-to-ignore-crl-checking.md)

이 단계에서는 **IgnoreNoRevocationCheck** 추가 하 고 인증서 CRL 배포 지점 포함 되지 않은 경우 클라이언트 인증을 허용 하도록 설정할 수 있습니다. 기본적으로 IgnoreNoRevocationCheck (사용 안 함) 0으로 설정 됩니다.

NPS 서버 인증서 체인 (루트 인증서 포함)의 해지 확인을 완료 하지 않는 한 EAP-TLS 클라이언트 연결할 수 없습니다. 사용자에 게 Azure AD에서 발급 하는 클라우드 인증서 CRL가 없는 1 시간의 수명이 일시적인 인증서 이기 때문입니다. NPS에서 EAP CRL의 부재 무시 하도록 구성 해야 합니다. 인증 방법 EAP-TLS 이므로 **EAP\13**에서이 레지스트리 값만 필요 합니다. 다른 EAP 인증 방법을 사용 하는 경우 다음 레지스트리 값 추가할지에서 이러한도 합니다. 




## [7.2단계. Azure AD를 사용하여 VPN 인증에 대한 루트 인증서 만들기](vpn-create-root-cert-for-vpn-auth-azure-ad.md)

이 단계에서 Azure AD 테 넌 트에 자동으로 VPN 서버 클라우드 응용 프로그램을 만드는와 VPN 인증에 대 한 루트 인증서를 구성 합니다.  

VPN 연결에 대 한 조건부 액세스를 구성 하려면 해야 합니다.
1. (인증서를 여러 개 만들 수 있습니다) Azure portal에서 VPN 인증서를 만듭니다.
2. VPN 인증서를 다운로드 합니다.
3. VPN 서버에 인증서를 배포 합니다.

## [7.3단계. 조건부 액세스 정책 구성](vpn-config-conditional-access-policy.md)

이 단계에서 VPN 연결에 대 한 조건부 액세스 정책을 구성할 수 있습니다. 

조건부 액세스 정책을 구성 하려면 해야 합니다.
1. VPN 사용자에 게 할당 하는 조건부 액세스 정책을 만듭니다.
2. **VPN 서버**에 클라우드 응용 프로그램을 설정 합니다.
3. **다단계 인증을 요구**하도록 허용 (액세스 제어)를 설정 합니다.  필요에 따라 다른 컨트롤을 사용할 수 있습니다.

## [7.4단계. 온-프레미스에 조건부 액세스 루트 인증서를 배포 광고](vpn-deploy-cond-access-root-cert-to-on-premise-ad.md)

이 단계에서는 온-프레미스에 VPN 인증에 대 한 신뢰할 수 있는 루트 인증서를 배포할 광고입니다.

신뢰할 수 있는 루트 인증서를 배포 하려면 해야 합니다.
1. *신뢰할 수 있는 루트 CA VPN 인증에 대 한*다운로드 한 인증서를 추가 합니다.
2. VPN 서버와 VPN 클라이언트에 루트 인증서를 가져옵니다.
3. 확인 인증서 있는 표시 하는 신뢰할 수 있는 합니다.


## [7.5단계. Windows 10 장치에 대한 OMA-DM 기반 VPNv2 프로필 만들기](vpn-create-oma-dm-based-vpnv2-profiles.md)

이 단계에서는 OMA DM 생성할 수 VPNv2 프로필 Intune을 사용 하 여 VPN 장치 구성 정책 배포를 기반으로 합니다. VPNv2 프로필을 만드는 SCCM 또는 PowerShell 스크립트를 사용 하려는 경우 [VPNv2 CSP 설정](https://docs.microsoft.com/windows/client-management/mdm/vpnv2-csp) 에 대 한 자세한 내용은 참조 하세요. 


## 다음 단계
[단계 7.1입니다. EAP-TLS 인증서 해지 목록 (CRL) 검사 무시 하도록 구성](vpn-config-eap-tls-to-ignore-crl-checking.md):이 단계에서 추가 **IgnoreNoRevocationCheck** 및 인증서 CRL 배포 지점 포함 되지 않은 경우 클라이언트 인증을 허용 하도록 설정 해야 합니다. 기본적으로 IgnoreNoRevocationCheck (사용 안 함) 0으로 설정 됩니다.

---

## 관련 항목
- [VPNv2 프로필 구성](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access): 이제 VPN 클라이언트를 사용 하 여 원격 클라이언트에 대 한 장치 준수 옵션을 제공 하는 클라우드 기반 조건부 액세스 플랫폼과 통합 수 있습니다. VPNv2 프로필과이 단계에서 구성한 **\ < DeviceCompliance > \ < 사용 > true\ < / 활성화 >** 합니다. 
 
- [자동 VPN 프로필을 사용 하 여 Windows 10에 원격 액세스 강화](https://www.microsoft.com/itshowcase/Article/Content/894/Enhancing-remote-access-in-Windows-10-with-an-automatic-VPN-profile): Microsoft VPN 연결에 대 한 조건부 액세스를 구현 하는 방법을 알아봅니다. VPN 프로필 장치 지원 되는 인증 방법 및 장치에 연결 해야 하는 VPN 서버를 포함 하 여 회사 네트워크에 연결 하는 데 필요한 모든 정보를 포함 합니다. 조건부 액세스 및 single sign-on을 포함 하 여 Windows 10 1 주년 업데이트의 변경 내용을 우리의 Always-On VPN 연결 프로필을 만들 수 있습니다. 연결 프로필을 만든 도메인 가입 및 System Center Configuration Manager 콘솔을 사용 하 여 Microsoft Intune에서 관리 하는 장치. 

- [Azure Active Directory에 액세스 하는 조건부](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal): 보안은 클라우드를 사용 하 여 조직에 대 한 최우선 합니다. 클라우드 리소스를 관리 하는 데 있어 클라우드 보안의 주요 측면은 id 및 액세스 합니다. 모바일 우선, 클라우드 중심 세계에서 사용자가 조직의 리소스 어디에서 다양 한 장치 및 앱을 사용 하 여 액세스할 수 있습니다. 결과적으로 리소스에 액세스할 수 있는 사람 초점 충분 하지 않은 더 이상. 마스터 보안과 생산성 간의 균형을 위해 IT 전문가 필요 리소스 액세스 제어 결정에 액세스 하는 방법을 고려 합니다.

- [VPN 및 조건부 액세스](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access): 이제 VPN 클라이언트를 사용 하 여 원격 클라이언트에 대 한 장치 준수 옵션을 제공 하는 클라우드 기반 조건부 액세스 플랫폼과 통합 수 있습니다. 조건부 액세스는 Azure AD(Azure Active Directory)에 연결된 응용 프로그램에 대한 액세스 규칙을 만드는 데 사용되는 정책 기반 평가 엔진입니다. 

---