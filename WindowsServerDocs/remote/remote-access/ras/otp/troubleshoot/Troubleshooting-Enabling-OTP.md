---
title: OTP 사용 문제 해결
description: 이 항목은 Windows Server 2016에서 OTP 인증을 사용 하 여 원격 액세스 배포 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b58252ca-4c1d-4664-a3c4-7301e2121517
ms.author: pashort
author: shortpatti
ms.openlocfilehash: d789671a0425974e560e5f4a43ebcba4c1741c76
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819464"
---
# <a name="troubleshooting-enabling-otp"></a>OTP 사용 문제 해결

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 DirectAccess OTP 인증을 사용 하 여 사용과 관련 된 문제에 대 한 문제 해결 정보는 **사용 DAOtpAuthentication** PowerShell cmdlet 또는 원격 액세스 관리 콘솔.
  
## <a name="failed-to-enroll-the-otp-signing-certificate"></a>OTP 서명 인증서를 등록 하지 못함  
**수신 된 오류** (서버 이벤트 로그). < OTP_signing_template_name > 인증서 템플릿을 사용 하는 OTP 서명 인증서를 등록할 수 없습니다.  
  
**가능한 원인**  
  
이 오류에 대 한 가능한 원인 세 가지 있습니다.  
  
-   템플릿에 존재 하지 않습니다.  
  
-   서식 파일에서 설정 된 사용 권한에 DirectAccess 서버를 등록을 허용 하지 않습니다.  
  
-   발급 인증 기관 (CA)에 네트워크 연결이 없습니다.  
  
**해결 방법**  
  
1.  지정 된 이름의 템플릿을 인증서 OTP 서명 되었는지 확인 합니다.  
  
    1.  존재 하 고 적절 한 사용 권한이 있습니다.  
  
    2.  DirectAccess 서버에 인증서를 발급할 수 있는 하나 이상의 CA에서 발급 한 수로 설정 됩니다.  
  
2.  경우 서식 파일 하지, 등록 기관 인증서 3.3 계획에 설명 된 대로 만듭니다 없거나 다른 일치 하는 템플릿이 있으면 DirectAccess OTP 새 템플릿 이름으로 다시 구성 합니다.  
  
## <a name="failed-to-enable-directaccess-otp-when-webdav-is-installed"></a>WebDAV를 설치할 때에 DirectAccess OTP를 사용 하도록 설정 하지 못했습니다.  
**시나리오**합니다. 원격 액세스 관리 콘솔에서 또는 사용 하 여 DirectAccess OTP 구성을 적용 하는 동안는 `Enable-DAOtpAuthentication` PowerShell cmdlet, 작업이 실패 합니다.  
  
**수신 된 오류** (서버 이벤트 로그). IIS WebDAV 확장을 서버에서 실행 되므로 DirectAccess OTP 설정은 적용할 수 없습니다. WebDAV를 제거 하 고 설정을 다시 적용 합니다.  
  
**가능한 원인**  
  
DirectAccess OTP 서비스 WebDAV 게시 기능과 호환 되지 않으며 WebDAV가 설치 되는 동안 사용할 수 없습니다.  
  
**해결 방법**  
  
WebDAV 역할을 제거 합니다.  
  
1.  왼쪽 창에서 서버 관리자 콘솔에서 클릭 **IIS**합니다.  
  
2.  주 창에서 스크롤하여 **역할 및 기능**합니다.  
  
3.  마우스 오른쪽 단추로 클릭 **WebDAV 게시**를 클릭 하 고 **역할 또는 기능 제거**합니다.  
  
4.  제거 역할 및 기능 마법사를 완료 합니다.  
  
5.  DirectAccess OTP 구성을 다시 적용 합니다.  
  
## <a name="no-templates-available-in-the-remote-access-management-console"></a>원격 액세스 관리 콘솔에서 사용 가능한 템플릿이 없습니다  
**시나리오**합니다. 선택 창에서 구성 일부 원격 액세스 관리 콘솔을 사용 하 여 OTP 또는 등록 기관 인증서 템플릿 또는 템플릿의 모든는 없습니다.  
  
**가능한 원인**  
  
이 오류의 가능한 원인은 두 가지 있습니다.  
  
-   템플릿을 DirectAccess OTP 요구 사항에 따라 구성 되지 않으며 따라서 선택할 수 없습니다.  
  
-   아래에서 선택한 Ca **OTP CA 서버** 하면 필요한 파일을 실행 하도록 구성 되지 않습니다.  
  
**해결 방법**  
  
1.  OTP 로그온 템플릿과 OTP 서명 인증서 템플릿에 3.2 계획 OTP 인증서 템플릿 및 3.3 계획 등록 기관 인증서에에서 설명 된 대로 올바르게 구성 되어 있는지 확인 합니다.  
  
2.  확인에서 구성 된 CAs를 **OTP CA 서버** 목록 관련 템플릿 문제를 구성:  
  
    1.  CA 서버에서 인증 기관 콘솔을 엽니다.  
  
    2.  왼쪽된 창에서 선택한 CA 서버를 확장 합니다.  
  
    3.  클릭 **인증서 템플릿** 필수 템플릿에 설정 되어 있는지 확인 합니다. 그렇지 않은 경우 마우스 오른쪽 단추로 클릭 **인증서 템플릿**, 클릭 **새로 만들기**, 클릭 **발급할 인증서 템플릿**를 선택한 다음 사용 하려는 템플릿.  
  
## <a name="cannot-set-renewal-period-of-otp-template-to-1-hour"></a>OTP 템플릿의 갱신 기간 1 시간을 설정할 수 없습니다.  
**시나리오**합니다. Windows 2003 CA를 사용 하 여 DirectAccess OTP 로그온 템플릿을 구성 하는 경우 템플릿의 갱신 기간 1 시간으로 설정 하는 것이 불가능 합니다.  
  
**가능한 원인**  
  
인증서 템플릿 MMC 스냅인을 Windows Server 2003에서 허용 하지 않습니다 템플릿의 갱신 기간 1 시간을 설정할 수 없습니다.  
  
**해결 방법**  
  
인증서 템플릿 스냅인 후 Windows Server 2003 서버에 설치 하 고 사용 하 여 OTP 로그온 템플릿을 구성 참조를 [인증서 템플릿 스냅인 설치](https://technet.microsoft.com/library/cc732445.aspx)합니다.  
  


