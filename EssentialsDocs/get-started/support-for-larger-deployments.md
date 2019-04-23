---
title: 대규모 배포 지원
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 07d0c4c6-3e92-4969-82b8-105e46ab8d97
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: c60e5f73c88a225fbd1067992894f9d20da745ad
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59860484"
---
#<a name="support-for-larger-deployments"></a>대규모 배포 지원

>적용 대상: Windows Server 2016 Essentials

> [!IMPORTANT]  
> 이 항목에서 설명 하는 기능은 Essentials Experience 역할이 사용 하도록 설정 하 고 Windows Server 2016 Essentials SKU와 Windows Server 2016에만 작동 합니다.


Windows Server Essentials는 이제 사용 하 여 대규모 배포를 지원합니다.

- 여러 도메인
- 여러 도메인 컨트롤러
- 지정 된 도메인 컨트롤러를 지정 하는 기능
- 최대 500 명의 사용자와 500 개의 장치에 대 한 지원

##<a name="support-for-multiple-domains"></a>여러 도메인 지원

Windows server 2012 R2 Essentials가 필요한 서버당 하나의 도메인을 지원 하 고 Essentials server 포리스트의 루트 여야 합니다. 도메인 및 포리스트는 여전히 필요, Windows Server 2016 Essentials Experience 역할이 Windows Server 2016 Standard 또는 Datacenter 여러 도메인을 지원 하기 위해 이제 배포할 수 있습니다.

## <a name="support-for-multiple-domain-controllers"></a>여러 도메인 컨트롤러에 대 한 지원

 Windows Server Essentials 2012 R2 이상의 도메인 컨트롤러를 배포 하는 Office 365와 같은 Azure Active Directory를 활용 하는 모든 서비스를 차단 합니다. 이유는 로컬 도메인 컨트롤러와 Azure Active Directory 계정 및 암호 동기화 계정 자격 증명 동기화는 암호를 사용 하 여 발생할 수 있습니다. Windows Server 2016 Essentials에서이 제한이 제거 되었습니다.

##<a name="ability-to-specify-a-designated-domain-controller"></a>지정 된 도메인 컨트롤러를 지정 하는 기능

이제는 Active Directory 도메인 개체에 대 한 검색 시간을 향상 시킬 뿐만 아니라 도메인에 다른 도메인 컨트롤러에서 계정 변경의 동기화를 조정 하는 지정 된 도메인 컨트롤러를 선택할 수 있습니다.

도메인 컨트롤러를 지정 된 기본 Windows Server Essentials Experience 서버 역할을 실행 하는 동일한 서버 됩니다. 해당 서버 서버인 경우 멤버를 의미 하는 도메인 컨트롤러가 아닌 다음 테스트에 따라 지정 된 도메인 컨트롤러를 자동으로 결정 됩니다 하는 기본 도메인에서 도메인 컨트롤러를 실행 하는 서버를 가장 낮은 네트워크 대기 시간에는 Windows Server 환경을 서버 역할입니다. 수동으로 서버는 지정 된 도메인 컨트롤러를 변경 하려는 경우 가능 하므로 **설정을** 에 **Windows Server Essentials 대시보드** 아래와 같이 합니다.

![설정을 보여 주는 스크린 샷 포그라운드에서 패널 및 백그라운드에서 Windows Server Essentials 대시보드를 제어 합니다. 제어판의 설정의 도메인 컨트롤러 지정 페이지에서 현재 선택 됩니다.](media/larger-deployments-1.PNG)

##<a name="support-for-500-users-and-500-devices"></a>사용자가 500 및 500 개의 장치에 대 한 지원
-------------------------------------

Windows Server 2012 R2 Essentials에서 지원 되는 사용자 및 장치 수가 최대 각각 25와 50입니다. Windows Server Essentials Experience 서버 역할의 도입으로 100 명의 사용자와 200 대의 장치가 해당 한도 증가 되었습니다.

Windows Server 2016 Essentials 500 명의 사용자와 500 개의 장치를 지원합니다. 이 가능한 공급자 프레임 워크에 대 한 업데이트 이며 개체 목록 컨트롤 캐시 하며 사용자 및 장치 개체 목록 크기를 신속 하 게 렌더링 합니다. 또한, 검색 및 필터링 기능을 추가한 신속 하 게 찾을 사용자 또는 장치 (참조: 그림 5-2) 일 수 있습니다. 검색 및 필터링 기능을 찾을 수 있습니다 합니다 **Windows Server Essentials 대시보드**를 **원격 웹 액세스**, 및 Windows Phone 및 Windows 스토어 **My Server** 응용 프로그램입니다.

![Windows Server Essentials 대시보드 "d5c." 문자열을 검색 하려면 검색 기능의 사용을 보여 주는 스크린샷 이 검색 결과를 두 개의 파일 및 폴더와 두 사용자를 포함 합니다.](media/larger-deployments-2.PNG)

Windows Server Essentials 대시보드 "d5c" 문자열을 검색 하려면 검색 기능의 사용을 보여 주는 스크린샷. 이 검색 결과를 두 개의 파일 및 폴더와 두 사용자를 포함 합니다.

> [!NOTE]  
> Windows Server Essentials 서버 역할의 경우 75 클라이언트 백업 유지에 대 한 지원 되는 제한 지원 되는 사용자 및 장치 제한을 증가 하는 동안.

<a name="see-also"></a>참조
--------
[Windows Server Essentials를 사용 하 여 시작](get-started.md)