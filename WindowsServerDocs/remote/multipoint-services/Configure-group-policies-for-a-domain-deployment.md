---
title: 도메인 배포를 위한 그룹 정책 구성
description: MultiPoint 서비스에서 그룹 정책을 설정 하는 방법 알아보기
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: 13e5fa90-d330-4155-a6b8-78eb650cbbfa
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: e851d12dad29de8b3498aad220354d31917fadee
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80862186"
---
# <a name="configure-group-policies-for-a-domain-deployment"></a>도메인 배포를 위한 그룹 정책 구성
MultiPoint 서비스의 도메인 배포가 제대로 작동 하도록 하려면 MultiPoint 서비스 시스템의 WMSshell 사용자 계정에 다음 그룹 정책 설정을 적용 합니다.  
  
> [!IMPORTANT]  
> 일부 그룹 정책 설정에 따라 필수 구성 설정이 MultiPoint 서비스에 적용 되는 것을 방지할 수 있습니다. MultiPoint 서비스에서 제대로 작동 하도록 그룹 정책 설정을 이해 하 고 정의 해야 합니다. 예를 들어 자동 로그온을 방지 하는 그룹 정책 설정은 MultiPoint 서비스 로그온 동작에 문제가 있을 수 있습니다.  
  
## <a name="update-group-policies-for-the-wmsshell-user-account"></a>WMSshell 사용자 계정에 대 한 그룹 정책 업데이트 
WMSshell 사용자 계정은 MultiPoint 서비스에서 콘솔에 로그인 하는 데 사용 하는 시스템 계정으로, 실제 스테이션이 생성 됩니다. 이 계정은 다중 포인트 관리자를 통해 관리 되지 않습니다.
  
> [!NOTE]  
> 그룹 정책을 업데이트 하는 방법에 대 한 자세한 내용은 [로컬 그룹 정책 편집기](https://technet.microsoft.com/library/dn265982.aspx)를 참조 하세요.  
  
**정책:** 사용자 구성 > 관리 템플릿 > 제어판 > **개인 설정**  
  
다음 값을 할당 합니다.  
  
|설정|값|  
|-----------|----------|  
|화면 보호기 사용|사용 안 함|  
|화면 보호기 시간 제한|사용 안 함<p>초: xxx|  
|암호로 화면 보호기 보호|사용 안 함|  
  
**정책:** 컴퓨터 구성 > Windows 설정 > 보안 설정 > 로컬 정책 > 사용자 권한 할당 > 로컬 **로그온 허용**  
  
|설정|값|  
|-----------|----------|  
|로컬 로그온 허용|계정 목록에 WMSshell 계정이 포함 되어 있는지 확인 합니다.<p>**참고:** 기본적으로 WMSshell 계정은 Users 그룹의 구성원입니다. 사용자 그룹이 목록에 있고 WMSshell가 Users 그룹의 구성원 인 경우에는 WMSshell 계정을 목록에 추가할 필요가 없습니다.|  
  
> [!IMPORTANT]  
> 그룹 정책을 설정 하는 경우 해당 정책이 MultiPoint 서버에서 자동 업데이트 및 오류 Windows 오류 보고를 방해 하지 않는지 확인 합니다. 이러한 설정은 **자동으로 업데이트 설치** 및 자동 **Windows 오류 보고** 설정에 의해 설정 되며,이 설정은 **서버 설정 편집**을 사용 하 여 Multipoint Manager에서 구성 되거나, 디스크 보호를 위해 예약 된 업데이트에서 구성 된 Windows multipoint server 설치 중에 선택 되었습니다.  
  
## <a name="update-the-registry"></a>레지스트리 업데이트  
MultiPoint 서비스의 도메인 배포의 경우 다음 레지스트리 하위 키를 업데이트 해야 합니다.  
  
> [!IMPORTANT]  
> 레지스트리를 잘못 편집하면 시스템이 크게 손상될 수 있습니다. 따라서 레지스트리를 변경하기 전에 컴퓨터의 중요한 데이터를 백업해 두어야 합니다.  
  
#### <a name="to-update-registry-subkeys-for-a-domain-deployment-of-multipoint-services"></a>MultiPoint 서비스의 도메인 배포에 대 한 레지스트리 하위 키를 업데이트 하려면  
  
1.  레지스트리 편집기를 엽니다. 명령 프롬프트에서 **regedit.exe**를 입력 하 고 enter 키를 누릅니다.  
  
2.  왼쪽 창에서 다음 레지스트리 하위 키를 찾아 선택 합니다.  
  
    HKEY_USERS\<SIDofWMSshell > \Software\Policies\Microsoft\Windows\Control Panel\Desktop  
  
    여기서 '<SIDofWMSshell>'는 WMSshell 계정에 대 한 SID (보안 식별자)입니다. SID를 식별 하는 방법에 대 한 자세한 내용은 [사용자 이름을 sid (보안 식별자)와 연결 하는 방법](https://support.microsoft.com/kb/154599)을 참조 하세요.  
  
3.  오른쪽 목록에서 다음 하위 키를 업데이트 합니다.  
  
    |하위 키|값 이름|값 데이터|  
    |----------|--------------|--------------|  
    |ScreenSaveActive|REG_SZ|0 (영)|  
    |ScreenSaveTimeout|REG_SZ|120|  
    |ScreenSaverIsSecure|REG_SZ|0 (영)|  
  
    레지스트리 하위 키를 업데이트 하려면:  
  
    1.  왼쪽 창에서 선택한 레지스트리 키를 사용 하 여 오른쪽 창에서 하위 키를 마우스 오른쪽 단추로 클릭 한 다음 **수정**을 클릭 합니다.  
  
    2.  문자열 편집 대화 상자에서 **값 데이터**에 새 값을 입력 한 다음 **확인**을 클릭 합니다.  
  
4.  레지스트리 하위 키 업데이트를 완료 한 후 컴퓨터를 다시 시작 하 여 변경 내용을 활성화 합니다. 
