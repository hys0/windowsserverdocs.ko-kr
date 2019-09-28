---
title: OTP 사용 문제 해결
description: 이 항목은 Windows Server 2016에서 OTP 인증을 사용 하 여 원격 액세스 배포 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b58252ca-4c1d-4664-a3c4-7301e2121517
ms.author: pashort
author: shortpatti
ms.openlocfilehash: a1c18f264a6a8d263f3e9f50bc325ef97f4240af
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366920"
---
# <a name="troubleshooting-enabling-otp"></a>OTP 사용 문제 해결

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에는 **DAOtpAuthentication** PowerShell Cmdlet 또는 원격 액세스 관리 콘솔을 사용 하 여 DirectAccess OTP 인증을 사용 하는 것과 관련 된 문제에 대 한 문제 해결 정보가 포함 되어 있습니다.
  
## <a name="failed-to-enroll-the-otp-signing-certificate"></a>OTP 서명 인증서를 등록 하지 못했습니다.  
**오류를 받았습니다** (서버 이벤트 로그). 인증서 템플릿 < OTP_signing_template_name를 사용 하 여 OTP 서명 인증서를 등록할 수 없습니다 >  
  
**가능한 원인**  
  
이 오류의 가능한 원인은 세 가지가 있습니다.  
  
-   템플릿이 없습니다.  
  
-   템플릿에 설정 된 권한으로는 DirectAccess 서버를 등록할 수 없습니다.  
  
-   발급 CA (인증 기관)에 네트워크로 연결 되어 있지 않습니다.  
  
**해결 방법**  
  
1.  지정 된 이름의 OTP 서명 인증서 템플릿이 있는지 확인 합니다.  
  
    1.  가 있으며 적절 한 사용 권한이 있습니다.  
  
    2.  는 DirectAccess 서버에 대 한 인증서를 발급할 수 있는 하나 이상의 CA에서 발급 됨으로 설정 됩니다.  
  
2.  템플릿이 존재 하지 않는 경우 3.3 등록 기관 인증서 계획에 설명 된 대로 만들거나, 일치 하는 다른 템플릿이 새 템플릿 이름을 사용 하 여 DirectAccess OTP를 다시 구성 합니다.  
  
## <a name="failed-to-enable-directaccess-otp-when-webdav-is-installed"></a>WebDAV가 설치 될 때 DirectAccess OTP를 사용 하도록 설정 하지 못함  
**시나리오**. 원격 액세스 관리 콘솔에서 또는 `Enable-DAOtpAuthentication` PowerShell cmdlet을 사용 하 여 DirectAccess OTP 구성을 적용 하려고 하면 작업이 실패 합니다.  
  
**오류를 받았습니다** (서버 이벤트 로그). WebDAV IIS 확장이 서버에서 실행 중 이므로 DirectAccess OTP 설정을 적용할 수 없습니다. WebDAV를 제거 하 고 설정을 다시 적용 합니다.  
  
**가능한 원인**  
  
DirectAccess OTP 서비스는 WebDAV 게시 기능과 호환 되지 않으며 WebDAV가 설치 되어 있는 동안에는 사용 하도록 설정할 수 없습니다.  
  
**해결 방법**  
  
WebDAV 역할을 제거 합니다.  
  
1.  서버 관리자 콘솔의 왼쪽 창에서 **IIS**를 클릭 합니다.  
  
2.  기본 창에서 **역할 및 기능**으로 스크롤합니다.  
  
3.  **WebDAV 게시**를 마우스 오른쪽 단추로 클릭 한 다음 **역할 또는 기능 제거**를 클릭 합니다.  
  
4.  역할 및 기능 제거 마법사를 완료 합니다.  
  
5.  DirectAccess OTP 구성을 다시 적용 합니다.  
  
## <a name="no-templates-available-in-the-remote-access-management-console"></a>원격 액세스 관리 콘솔에서 사용할 수 있는 템플릿이 없습니다.  
**시나리오**. 원격 액세스 관리 콘솔을 사용 하 여 OTP 또는 등록 기관 인증서 템플릿을 구성 하는 동안 선택 창에 일부 또는 모든 템플릿이 누락 됩니다.  
  
**가능한 원인**  
  
이 오류의 가능한 원인은 두 가지입니다.  
  
-   템플릿은 DirectAccess OTP 요구 사항에 따라 구성 되지 않으므로 선택할 수 없습니다.  
  
-   **OTP CA 서버** 아래에서 선택한 ca는 필수 템플릿을 발급 하도록 구성 되지 않습니다.  
  
**해결 방법**  
  
1.  3\.2 OTP 인증서 템플릿 계획 및 3.3 등록 기관 인증서 계획에 설명 된 대로 OTP 로그온 템플릿 및 OTP 서명 인증서 템플릿이 올바르게 구성 되어 있는지 확인 합니다.  
  
2.  **OTP CA Servers** 목록에 구성 된 ca가 관련 템플릿을 발급 하도록 구성 되어 있는지 확인 합니다.  
  
    1.  CA 서버에서 인증 기관 콘솔을 엽니다.  
  
    2.  왼쪽 창에서 선택한 CA 서버를 확장 합니다.  
  
    3.  **인증서 템플릿** 을 클릭 하 고 필요한 템플릿이 사용 하도록 설정 되었는지 확인 합니다. 그렇지 않으면 **인증서 템플릿**을 마우스 오른쪽 단추로 클릭 하 고 **새로 만들기**를 클릭 한 다음 **발급할 인증서 템플릿**을 클릭 하 고 사용 하도록 설정할 템플릿을 선택 합니다.  
  
## <a name="cannot-set-renewal-period-of-otp-template-to-1-hour"></a>OTP 템플릿의 갱신 기간을 1 시간으로 설정할 수 없음  
**시나리오**. Windows 2003 CA를 사용 하 여 DirectAccess OTP 로그온 템플릿을 구성 하는 경우 템플릿의 갱신 기간을 1 시간으로 설정할 수 없습니다.  
  
**가능한 원인**  
  
Windows Server 2003의 인증서 템플릿 MMC 스냅인을 사용 하면 템플릿의 갱신 기간을 1 시간으로 설정할 수 없습니다.  
  
**해결 방법**  
  
Windows Server 2003 서버에서 인증서 템플릿 스냅인을 설치 하 고이를 사용 하 여 OTP 로그온 템플릿을 구성 합니다. [인증서 템플릿 스냅인 설치](https://technet.microsoft.com/library/cc732445.aspx)를 참조 하세요.  
  


