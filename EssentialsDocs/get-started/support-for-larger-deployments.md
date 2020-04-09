---
title: 대규모 배포 지원
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 07d0c4c6-3e92-4969-82b8-105e46ab8d97
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: c54defee45e8950d878ba70f627c1e645a2c8586
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80817826"
---
# <a name="support-for-larger-deployments"></a>대규모 배포 지원

>적용 대상: Windows Server 2016 Essentials

> [!IMPORTANT]  
> 이 항목에서 설명 하는 기능은 Windows server 2016 Essentials SKU가 아니라 Essentials Experience 역할을 사용 하는 Windows Server 2016 에서만 작동 합니다.


이제 Windows Server Essentials는 다음과 같은 대규모 배포를 지원 합니다.

- 여러 도메인
- 여러 도메인 컨트롤러
- 지정 된 도메인 컨트롤러를 지정 하는 기능
- 최대 500 사용자 및 500 장치 지원

## <a name="support-for-multiple-domains"></a>여러 도메인 지원

Windows server 2012 R2 Essentials는 서버당 하나의 도메인만 지원 하며, Essentials 서버는 포리스트의 루트 여야 합니다. 도메인 및 포리스트가 아직 필요 하지만 이제 windows server 2016 Essentials Experience 역할을 Windows Server 2016 Standard 또는 Datacenter에 배포 하 여 여러 도메인을 지원할 수 있습니다.

## <a name="support-for-multiple-domain-controllers"></a>여러 도메인 컨트롤러에 대 한 지원

 Windows Server Essentials 2012 R2에서는 두 개 이상의 도메인 컨트롤러를 배포 하는 Office 365와 같은 Azure Active Directory를 활용 하는 모든 서비스를 차단 합니다. 그 이유는 로컬 도메인 컨트롤러와 Azure Active Directory 간의 계정 및 암호 동기화로 인해 암호가 동기화 되지 않은 경우 계정 자격 증명을 사용할 수 있기 때문입니다. 이러한 제한 사항은 Windows Server 2016 Essentials에서 제거 되었습니다.

## <a name="ability-to-specify-a-designated-domain-controller"></a>지정 된 도메인 컨트롤러를 지정 하는 기능

이제 지정 된 도메인 컨트롤러를 선택 하 여 Active Directory 도메인 개체에 대 한 검색 시간을 개선 하 고 도메인의 다른 도메인 컨트롤러에 대 한 계정 변경의 동기화를 조정할 수 있습니다.

지정 된 기본 도메인 컨트롤러는 Windows Server Essentials Experience 서버 역할을 실행 하는 서버와 동일 합니다. 해당 서버가 구성원 서버인 경우 도메인 컨트롤러가 아닌 것을 의미 하며, 기본 지정 된 도메인 컨트롤러는 도메인의 도메인 컨트롤러에서 네트워크 대기 시간이 가장 낮은 테스트를 실행 하는 서버에 대 한 테스트를 기반으로 Windows Server Experience 서버 역할입니다. 지정 된 도메인 컨트롤러의 서버를 수동으로 변경 하려면 아래와 같이 **Windows Server Essentials 대시보드의** **설정** 에서이 작업을 수행할 수 있습니다.

![전경의 설정 제어판 및 백그라운드의 Windows Server Essentials 대시보드를 보여 주는 스크린샷 설정 제어판의 지정 된 도메인 컨트롤러 페이지가 현재 선택 되어 있습니다.](media/larger-deployments-1.PNG)

## <a name="support-for-500-users-and-500-devices"></a>500 사용자 및 500 장치 지원
-------------------------------------

Windows Server 2012 R2 Essentials에서 지원 되는 사용자 및 장치의 최대 수는 각각 25 및 50입니다. Windows Server Essentials Experience 서버 역할이 도입 되면서 해당 제한이 100 사용자 및 200 장치로 늘어났습니다.

Windows Server 2016 Essentials는 500 사용자 및 500 장치를 지원 합니다. 이러한 작업을 가능 하 게 하는 것은 공급자 프레임 워크 및 개체 목록 컨트롤에 대 한 업데이트로, 크게 사용자 및 장치 개체 목록을 캐시 하 고 신속 하 게 렌더링 합니다. 또한 검색 및 필터 기능이 추가 되어 찾고 있는 사용자 또는 장치를 신속 하 게 찾을 수 있습니다 (그림 5-2 참조). **Windows Server Essentials 대시보드**, **원격 웹 액세스**및 Windows 및 Windows Phone **My server** 응용 프로그램에서 검색 및 필터 기능을 찾을 수 있습니다.

![Windows Server Essentials 대시보드의 검색 기능을 사용 하 여 "d5c" 문자열을 검색 하는 방법을 보여 주는 스크린샷 이 검색 결과에는 두 개의 파일과 폴더 및 두 명의 사용자가 포함 됩니다.](media/larger-deployments-2.PNG)

Windows Server Essentials 대시보드의 검색 기능을 사용 하 여 문자열 "d5c"를 검색 하는 방법을 보여 주는 스크린샷 이 검색 결과에는 두 개의 파일과 폴더 및 두 명의 사용자가 포함 됩니다.

> [!NOTE]  
> Windows Server Essentials 서버 역할에 대해 지원 되는 사용자 및 장치 한도가 증가 했지만 클라이언트 백업에 대해 지원 되는 한도는 75에 그대로 남아 있습니다.

<a name="see-also"></a>참고 항목
--------
[Windows Server Essentials 시작](get-started.md)