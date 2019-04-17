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
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2018
ms.locfileid: "6067306"
---
# 7.4단계. 온-프레미스에 조건부 액세스 루트 인증서를 배포 광고

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10

이 단계에서 조건부 액세스 루트 인증서 VPN 인증 인증서를 신뢰할 수 있는 루트 인증서로에 배포할 온-프레미스 AD 합니다.

& #171;  [ **이전:** 7.3 단계입니다. 조건부 액세스 정책 구성](vpn-config-conditional-access-policy.md)<br>
& #187; [ **다음:** 7.5 단계입니다. 만들기 OMA DM Windows 10 디바이스에 VPNv2 프로필 기반](vpn-create-oma-dm-based-vpnv2-profiles.md)

1. **VPN 연결** 페이지에서 **인증서를 다운로드**를 클릭 합니다. 
   
    ![조건부 액세스에 대 한 인증서를 다운로드 합니다.](../../media/Always-On-Vpn/06.png)

    >[!NOTE]
    >**Base64 인증서 다운로드** 옵션은 배포에 대 한 base64 인증서를 필요로 하는 일부 구성에 사용할 수 있습니다. 

2. 엔터프라이즈 관리자 권한 가진 도메인에 가입 된 컴퓨터에 로그온 하 고 *엔터프라이즈 NTauth* 저장소로 클라우드 루트 인증서를 추가 하려면 관리자 명령 프롬프트에서 다음이 명령을 실행 합니다.

    >[!NOTE]
    >VPN 서버는 Active Directory 도메인에 가입 되지 않은 환경에서는 클라우드 루트 인증서는 _신뢰할 수 있는 루트 인증 기관_ 저장소에 수동으로 추가 되어야 합니다.

    |명령  |설명  |  
    |---------|-------------| 
    |`certutil -dspublish -f VpnCert.cer RootCA`     |아래 두 **Microsoft VPN 루트 CA 생성 1** 컨테이너를 만들고 합니다 **CN AIA =** 및 **CN = 인증 기관** 컨테이너, 모두 Microsoft VPN **루트의 _cACertificate_ 특성 값으로 각 루트 인증서를 게시 하 고 CA 생성 1** 컨테이너입니다.|  
    |`certutil -dspublish -f VpnCert.cer NTAuthCA`   |하나의 **CN = NTAuthCertificates** 아래에서 컨테이너는 **CN AIA =** 및 **CN = 인증 기관** 컨테이너, 각 루트 인증서의 CN ** _cACertificate_ 특성 값으로 게시 하 고 = NTAuthCertificates** 컨테이너입니다. |  
    |`gpupdate /force`     |Windows 서버와 클라이언트 컴퓨터에 루트 인증서 추가 신속 하 게 처리 합니다.  |

3.  루트 인증서 엔터프라이즈 NTauth 저장소에 신뢰할 수 있는 것으로 표시 되는지 확인 합니다.

    a.  **인증서 인증 기관 관리 도구가** 설치 되어 있는 엔터프라이즈 관리자 권한으로 서버에 로그온 합니다.

    >[!NOTE]
    >기본적으로 **인증서 기관 관리 도구** 는 설치 된 인증 기관 서버입니다. **역할 관리 도구** 에서 서버 관리자 일부로 다른 구성원 서버에 설치할 수 있습니다.

    b.  VPN 서버에서 시작 메뉴에서 엔터프라이즈 PKI 대화 상자를 열려면 **pkiview.msc** 입력 합니다.

    c.  시작 메뉴에서 엔터프라이즈 PKI 대화 상자를 열려면 **pkiview.msc** 입력 합니다.

    d.  **엔터프라이즈 PKI** 를 마우스 오른쪽 단추로 클릭 하 고 **AD 컨테이너 관리를**선택 합니다.

    d.  아래에 있는 Microsoft VPN 루트 CA 생성 1 인증서 각 인지 확인 합니다.<ul><li>NTAuthCertificates</li><li>AIA 컨테이너</li><li>인증서 기관 컨테이너</li></ul>

    
## 다음 단계
[단계 7.5입니다. 만들기 OMA DM Windows 10 디바이스에 VPNv2 프로필 기반](vpn-create-oma-dm-based-vpnv2-profiles.md):이 단계에서 OMA DM를 만들 수 있습니다 VPNv2 프로필 Intune을 사용 하 여 VPN 장치 구성 정책 배포를 기반으로 합니다. VPNv2 프로필을 만드는 SCCM 또는 PowerShell 스크립트를 만들려는 경우 [VPNv2 CSP 설정](https://docs.microsoft.com/windows/client-management/mdm/vpnv2-csp) 에 대 한 자세한 내용은 참조 하세요.

---
