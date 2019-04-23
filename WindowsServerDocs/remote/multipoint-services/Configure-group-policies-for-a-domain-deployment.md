---
title: 도메인 배포를 위한 그룹 정책 구성
description: MultiPoint 서비스에서 그룹 정책을 설정 하는 방법 알아보기
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 13e5fa90-d330-4155-a6b8-78eb650cbbfa
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: f661fbdc40fd7dd2562d51756bc7642c8e9a4a82
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59888044"
---
# <a name="configure-group-policies-for-a-domain-deployment"></a>도메인 배포를 위한 그룹 정책 구성
MultiPoint 서비스에 도메인 배포가 제대로 작동 되도록 MultiPoint 서비스 시스템에서 WMSshell 사용자 계정에 다음 그룹 정책 설정을 적용 합니다.  
  
> [!IMPORTANT]  
> 일부 그룹 정책 설정에 필요한 구성 설정에서 MultiPoint 서비스에 적용 되 고 방지할 수 있습니다. 이해 하 고 MultiPoint 서비스에서 제대로 작동 되도록 그룹 정책 설정을 정의 해야 합니다. 예를 들어, 자동 로그온을 방지 하는 그룹 정책 설정 MultiPoint 서비스 로그온 동작을 사용 하 여 문제를 제공할 수도 있습니다.  
  
## <a name="update-group-policies-for-the-wmsshell-user-account"></a>WMSshell 사용자 계정에 대 한 그룹 정책 업데이트 
WMSshell 사용자는 MultiPoint 서비스를 사용 하 여 로그인 콘솔로 actuall 스테이션 생성 되는 위치를 시스템 계정이입니다. 이 계정은 수집과 다중 포인트 관리자에서 관리 합니다.
  
> [!NOTE]  
> 참조 그룹 정책을 업데이트 하는 방법을 알아보려면 [로컬 그룹 정책 편집기](https://technet.microsoft.com/library/dn265982.aspx)합니다.  
  
**정책:** 사용자 구성 > 관리 템플릿 > 제어판 > **개인 설정**  
  
다음 값을 할당 합니다.  
  
|설정|값|  
|-----------|----------|  
|화면 보호기를 사용 하도록 설정|사용 안 함|  
|화면 보호기 시간 제한|사용 안 함<br /><br />시간 (초): xxx|  
|화면 보호기 암호로 보호|사용 안 함|  
  
**정책:** 컴퓨터 구성 > Windows 설정 > 보안 설정 > 로컬 정책 > 사용자 권한 할당 > **로컬 로그온 허용**  
  
|설정|값|  
|-----------|----------|  
|로컬 로그온 허용|계정 목록 WMSshell 계정에 포함 되도록 합니다.<br /><br />**참고:** 기본적으로 WMSshell 계정은 사용자 그룹의 구성원입니다. 목록에서 사용자 그룹은 WMSshell Users 그룹의 멤버인 경우 WMSshell 계정 목록에 추가할 필요가 없습니다.|  
  
> [!IMPORTANT]  
> 모든 그룹 정책으로 설정 하면 정책이 자동 업데이트 및 오류 Windows MultiPoint server에 대 한 보고를 사용 하 여 방해 하지 있는지 확인 합니다. 이러한 속성은 설정 하 여를 **업데이트를 자동으로 설치** 하 고 **자동 Windows 오류 보고** MultiPoint에 구성 된 Windows MultiPoint Server 설치 중에 선택한 설정 관리자를 사용 하 여 **서버 설정 편집**, 또는 디스크 보호에 대해 예약 된 업데이트에서 구성 합니다.  
  
## <a name="update-the-registry"></a>레지스트리 업데이트  
MultiPoint 서비스의 도메인 배포의 경우 다음 레지스트리 하위 키를 업데이트 해야 합니다.  
  
> [!IMPORTANT]  
> 레지스트리를 잘못 편집하면 시스템에 심각한 손상을 줄 수 있습니다. 따라서 레지스트리를 변경하기 전에 컴퓨터의 중요한 데이터를 백업해 두어야 합니다.  
  
#### <a name="to-update-registry-subkeys-for-a-domain-deployment-of-multipoint-services"></a>MultiPoint 서비스의 도메인 배포를 위한 레지스트리 하위 키를 업데이트 하려면  
  
1.  레지스트리 편집기를 엽니다. (명령 프롬프트에서 입력 **regedit.exe**, ENTER 키를 누릅니다.)  
  
2.  왼쪽된 창에서 찾아 다음 레지스트리 하위 키를 선택 합니다.  
  
    HKEY_USERS\<SIDofWMSshell>\Software\Policies\Microsoft\Windows\Control Panel\Desktop  
  
    여기서 '<SIDofWMSshell>' WMSshell 계정에 대 한 보안 식별자 (SID)입니다. SID를 식별 하는 방법을 알아보려면 참조 [사용자 이름 보안 식별자 (SID) 사용 하 여 연결 하는 방법을](https://support.microsoft.com/kb/154599)합니다.  
  
3.  오른쪽의 목록에서 다음 하위 키를 업데이트 합니다.  
  
    |하위 키|값 이름|값 데이터|  
    |----------|--------------|--------------|  
    |ScreenSaveActive|REG_SZ|0 (영)|  
    |ScreenSaveTimeout|REG_SZ|120|  
    |ScreenSaverIsSecure|REG_SZ|0 (영)|  
  
    레지스트리 하위 키를 업데이트 합니다.  
  
    1.  왼쪽된 창에서 선택한 레지스트리 키를 사용 하 여 오른쪽 창에서 하위 키를 마우스 오른쪽 단추로 누른 **수정**합니다.  
  
    2.  문자열 편집 대화 상자에 새 값을 입력 **값 데이터**를 클릭 하 고 **확인**합니다.  
  
4.  레지스트리 하위 키를 업데이트를 마친 후 변경 내용을 활성화 하려면 컴퓨터를 다시 시작 합니다. 