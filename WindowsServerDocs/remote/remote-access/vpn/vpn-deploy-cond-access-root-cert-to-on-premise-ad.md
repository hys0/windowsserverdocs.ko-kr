---
title: 온-프레미스 AD에 조건부 액세스 루트 인증서 배포
description: ''
services: active-directory
ms.prod: windows-server-threshold
ms.technology: networking-ras
documentationcenter: ''
ms.assetid: ''
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2018
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.reviewer: deverette
ms.openlocfilehash: 210540846f5d62dfc74a2e629a6b7675ccf9894d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837374"
---
# <a name="step-74-deploy-conditional-access-root-certificates-to-on-premises-ad"></a>7.4단계. 온-프레미스에 조건부 액세스 루트 인증서를 배포할 AD

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10

이 단계에서는 조건부 액세스 루트 인증서와 VPN 인증에 대 한 신뢰할 수 있는 루트 인증서에 배포한 온-프레미스 AD입니다.

&#171;  [**이전:** 7.3단계. 조건부 액세스 정책 구성](vpn-config-conditional-access-policy.md)<br>
&#187;[ **다음:** 7.5단계. 만들 8.1(OMA-DM 기반 VPNv2 프로 파일을 Windows 10 장치](vpn-create-oma-dm-based-vpnv2-profiles.md)

1. 에 **VPN 연결** 페이지에서 클릭 **인증서 다운로드**합니다. 
   
    ![조건부 액세스에 대 한 인증서를 다운로드 합니다.](../../media/Always-On-Vpn/06.png)

    >[!NOTE]
    >합니다 **base64 인증서 다운로드** 옵션은 배포에 대 한 base64 인증서를 필요로 하는 몇 가지 구성을 사용할 수 있습니다. 

2. 엔터프라이즈 관리자 권한 및 클라우드를 추가 하려면 다음이 명령을 관리자 권한 명령 프롬프트에서 루트 인증서에는 실행을 사용 하 여 도메인에 가입 된 컴퓨터에 로그온 합니다 *Enterprise NTauth* 저장 합니다.

    >[!NOTE]
    >VPN 서버는 Active Directory 도메인에 가입 되지는 환경에 대 한 클라우드 루트 인증서에 추가 해야 합니다 _신뢰할 수 있는 루트 인증 기관_ 수동으로 저장 합니다.

    |Command  |설명  |  
    |---------|-------------| 
    |`certutil -dspublish -f VpnCert.cer RootCA`     |두 개 만듭니다 **Microsoft VPN 루트 CA gen 1** 에서 컨테이너를 **CN = AIA** 및 **CN = 인증 기관** 컨테이너에서 값으로 각 루트 인증서를 게시 하 고 합니다 _cACertificate_ 특성을 둘 다 **Microsoft VPN 루트 CA gen 1** 컨테이너입니다.|  
    |`certutil -dspublish -f VpnCert.cer NTAuthCA`   |하나 만듭니다 **CN = NTAuthCertificates** 컨테이너를 **CN = AIA** 및 **CN = 인증 기관** 컨테이너에서 값으로 각 루트 인증서를 게시 하 고 합니다 _cACertificate_ 특성을 **CN = NTAuthCertificates** 컨테이너입니다. |  
    |`gpupdate /force`     |Windows 서버 및 클라이언트 컴퓨터에 루트 인증서 추가 속도 높여 줍니다.  |

3.  엔터프라이즈 NTauth 저장소에 신뢰할 수 있는 상태로 표시 된 루트 인증서 있는지 확인 합니다.

    a.  있는 엔터프라이즈 관리자 권한으로 서버에 로그온 합니다 **인증서 기관 관리 도구** 설치 합니다.

    >[!NOTE]
    >기본적으로는 **인증서 기관 관리 도구** 인증 기관 서버를 설치 합니다. 일부로 다른 멤버 서버에 설치 합니다 **역할 관리 도구** 서버 관리자에서.

    b.  시작 메뉴에서 VPN 서버에서 입력 **pkiview.msc** 엔터프라이즈 PKI 대화 상자를 엽니다.

    다.  시작 메뉴에서 입력 **pkiview.msc** 엔터프라이즈 PKI 대화 상자를 엽니다.

    d.  마우스 오른쪽 단추로 클릭 **엔터프라이즈 PKI** 선택한 **AD 관리 컨테이너**합니다.

    d.  아래에 있는 각 Microsoft VPN 루트 CA gen 1 인증서 있는지 확인 합니다.<ul><li>NTAuthCertificates</li><li>AIA 컨테이너</li><li>인증서 기관 컨테이너</li></ul>

    
## <a name="next-step"></a>다음 단계
[7.5 단계입니다. 만들 8.1(OMA-DM Windows 10 장치에 VPNv2 프로필 기반](vpn-create-oma-dm-based-vpnv2-profiles.md): 이 단계에서는 OMA-DM를 만들 수 있습니다 기반 VPN 장치 구성 정책을 배포 하려면 Intune을 사용 하 여 VPNv2 프로 파일입니다. VPNv2 프로필을 만드는 SCCM 또는 PowerShell 스크립트를 원한다 면 참조 [VPNv2 CSP 설정이](https://docs.microsoft.com/windows/client-management/mdm/vpnv2-csp) 대 한 자세한 내용은 합니다.

---
