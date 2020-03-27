---
title: 온-프레미스 AD에 조건부 액세스 루트 인증서 배포
description: ''
services: active-directory
ms.prod: windows-server
ms.technology: networking-ras
ms.workload: identity
ms.topic: article
ms.date: 06/28/2019
ms.author: lizross
author: eross-msft
ms.localizationpriority: medium
ms.reviewer: deverette
ms.openlocfilehash: aeb35d8c3eafd436330b66ca7d5be68d78045df0
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80307844"
---
# <a name="step-74-deploy-conditional-access-root-certificates-to-on-premises-ad"></a>7\.4단계. 온-프레미스 AD에 조건부 액세스 루트 인증서 배포

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10

이 단계에서는 조건부 액세스 루트 인증서를 온-프레미스 AD에 대 한 VPN 인증에 대 한 신뢰할 수 있는 루트 인증서로 배포 합니다.

- [**이전:** 7.3 단계. 조건부 액세스 정책 구성](vpn-config-conditional-access-policy.md)
- [**다음:** 7.5 단계. Windows 10 장치에 대 한 OMA DM 기반 VPNv2 프로필 만들기](vpn-create-oma-dm-based-vpnv2-profiles.md)

1. **VPN 연결** 페이지에서 **인증서 다운로드**를 선택 합니다.

   >[!NOTE]
   >Base64 **인증서 다운로드** 옵션은 배포용 base64 인증서가 필요한 일부 구성에 사용할 수 있습니다.

2. 엔터프라이즈 관리자 권한으로 도메인에 가입 된 컴퓨터에 로그온 하 고 관리자 명령 프롬프트에서 다음 명령을 실행 하 여 *Enterprise NTauth* 스토어에 클라우드 루트 인증서를 추가 합니다.

   >[!NOTE]
   >VPN 서버가 Active Directory 도메인에 가입 되지 않은 환경의 경우 클라우드 루트 인증서를 신뢰할 수 있는 _루트 인증 기관_ 저장소에 수동으로 추가 해야 합니다.

   | 명령 | 설명 |
   | --- | --- |
   | `certutil -dspublish -f VpnCert.cer RootCA` | **Cn = AIA** 및 **Cn = 인증 기관** 컨테이너에 두 개의 **microsoft vpn 루트 ca gen 1** 컨테이너를 만들고 각 루트 인증서를 **Microsoft Vpn 루트 ca gen 1** 컨테이너의 _cACertificate_ 특성 값으로 게시 합니다. |
   | `certutil -dspublish -f VpnCert.cer NTAuthCA` | Cn = **AIA** 및 **Cn = 인증 기관** 컨테이너 아래에 **cn = NTAuthCertificates** 컨테이너를 하나 만들고 **cn = NTAuthCertificates** container의 _cACertificate_ 특성에 값으로 각 루트 인증서를 게시 합니다. |
   | `gpupdate /force` | Windows 서버 및 클라이언트 컴퓨터에 루트 인증서를 추가 하는 것을 신속 하 게 합니다. |

3. 루트 인증서가 Enterprise NTauth 저장소에 있고 신뢰할 수 있는 것으로 표시 되는지 확인 합니다.
   1. **인증 기관 관리 도구가** 설치 되어 있는 엔터프라이즈 관리자 권한으로 서버에 로그온 합니다.

   >[!NOTE]
   >기본적으로 **인증 기관 관리 도구** 는 인증 기관 서버에 설치 됩니다. 서버 관리자에서 **역할 관리 도구의** 일부로 다른 구성원 서버에 설치할 수 있습니다.

   1. VPN 서버의 시작 메뉴에서 **pkiview** 를 입력 하 여 Enterprise PKI 대화 상자를 엽니다.
   1. 시작 메뉴에서 **pkiview** 를 입력 하 여 Enterprise PKI 대화 상자를 엽니다.
   1. **ENTERPRISE PKI** 를 마우스 오른쪽 단추로 클릭 하 고 **AD 컨테이너 관리**를 선택 합니다.
   1. 각 Microsoft VPN 루트 CA gen 1 인증서가 다음 위치에 있는지 확인 합니다.
      - NTAuthCertificates
      - AIA 컨테이너
      - 인증 기관 컨테이너

## <a name="next-steps"></a>다음 단계

[7.5 단계. Windows 10 장치에 대 한 OMA-URI 기반 VPNv2 프로필 만들기](vpn-create-oma-dm-based-vpnv2-profiles.md):이 단계에서는 Intune을 사용 하 여 VPN 장치 구성 정책을 배포 하는 OMA dm 기반 VPNv2 프로필을 만들 수 있습니다. Microsoft Endpoint Configuration Manager 또는 PowerShell 스크립트를 사용 하 여 VPNv2 프로필을 만들려면 [VPNV2 CSP 설정](https://docs.microsoft.com/windows/client-management/mdm/vpnv2-csp) 에서 자세한 내용을 참조 하세요.
