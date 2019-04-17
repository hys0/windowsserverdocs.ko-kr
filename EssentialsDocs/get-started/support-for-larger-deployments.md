---
title: "큰 배포에 대 한 지원"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
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
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
#<a name="support-for-larger-deployments"></a>큰 배포에 대 한 지원

>Windows Server 2016 Essentials에 적용 됩니다.

> [!IMPORTANT]  
> 이 여기에 설명 된 기능 Windows Server 2016 Essentials SKU 및 하지를 사용 하도록 설정 Essentials 경험 역할와 Windows Server 2016에만 작동 합니다.


이제 Windows Server Essentials 큰 배포를 지원합니다.

- 여러 도메인
- 여러 도메인 컨트롤러
- 지정 된 도메인 컨트롤러를 지정 하는 기능
- 사용자가 최대 500 및 500 장치에 대 한 지원

##<a name="support-for-multiple-domains"></a>여러 도메인에 대 한 지원

Windows server 2012 R2 Essentials 서버를 필요에 따라 하나만 도메인 지원 하 고 Essentials 서버 숲 루트 해야 합니다. 도메인 및 숲은 계속 필요, Windows Server 2016 Essentials 경험 역할 여러 도메인 지원 하기 위해 Windows Server 2016 표준 또는 데이터 센터에 배포 이제 수 있습니다.

## <a name="support-for-multiple-domain-controllers"></a>여러 도메인 컨트롤러에 대 한 지원

 Windows Server Essentials 2012 r 2는 Azure Active Directory, Office 365를 여러 개 도메인 컨트롤러 배포 될 등을 활용 하는 모든 서비스를 차단 합니다. 그 이유는 계정 및 암호 동기화 로컬 도메인 컨트롤러와 Azure Active Directory 계정 자격 증명 동기화는 암호를 사용 될 수 있습니다. 이 제한은 Windows Server 2016 Essentials에서 제거 되었습니다.

##<a name="ability-to-specify-a-designated-domain-controller"></a>지정 된 도메인 컨트롤러를 지정 하는 기능

이제는 도메인 Active Directory 개체를 검색 시간이 개선 뿐만 아니라 도메인에 있는 다른 도메인 컨트롤러에서 동기화 된 계정 변경 조정 하는 지정 된 도메인 컨트롤러를 선택할 수 있습니다.

지정 된 도메인 컨트롤러 기본 Windows Server Essentials 경험 서버 역할을 실행 하는 서버 됩니다. 해당 서버 구성원 서버를는 도메인 컨트롤러를 하지 즉 다음 지정된 도메인 컨트롤러를 자동으로 확인할 도메인에 있는 도메인 컨트롤러 테스트를 진행에 따라 기본에 경험 서버 역할을 실행 하는 서버에 최저 네트워크 대기입니다. 수동으로 지정 된 도메인 컨트롤러 서버를 변경 하려면 할 수 있는 **설정** 에 **Windows Server Essentials 대시보드** 다음과 같이 합니다.

![설정을 보여 주는 스크린샷 포그라운드에서 패널 및 Windows Server Essentials 대시보드 백그라운드에서 제어 됩니다. 설정 제어판의 지정 된 도메인 컨트롤러 페이지에서 현재 선택 됩니다.](media/larger-deployments-1.PNG)

##<a name="support-for-500-users-and-500-devices"></a>사용자가 500 및 500 장치에 대 한 지원
-------------------------------------

지원 되는 사용자 및 Windows Server 2012 R2 Essentials에서 디바이스의 최대 50 및 25 각각입니다. Windows Server Essentials 경험 서버 역할 도입 100 사용자와 200 장치에 해당 제한 된 증가 합니다.

Windows Server 2016 필수 패키지 500 사용자 및 500 장치를 지원 합니다. 이 가능한 공급자 프레임 워크에 대 한 업데이트는 개체 목록 캐시 큰 사용자와 디바이스가 개체 목록 신속 하 게 렌더링 므 컨트롤을 알아봅니다. 또한, 검색 및 필터 기능을 빨리 찾는 사용자 또는 디바이스 (참조 그림 5 2)에 대 한 일 수 있습니다 추가 되었습니다. 검색 및 필터 기능을 찾을 수는 **Windows Server Essentials 대시보드**, **원격 Web Access**, 및 Windows 및 Windows Phone 스토어 **내 서버** 응용 프로그램입니다.

![Windows Server Essentials 대시보드 문자열 "d5c."을 검색 하려면의 검색 기능을 사용을 보여 주는 스크린샷 두 파일 및 폴더 및 사용자가 두이 검색 결과 포함 되어 있습니다.](media/larger-deployments-2.PNG)

Windows Server Essentials 대시보드 문자열 "d5c"을 검색 하려면의 검색 기능을 사용을 보여 주는 스크린샷 합니다. 두 파일 및 폴더 및 사용자가 두이 검색 결과 포함 되어 있습니다.

> [!NOTE]  
> Windows Server Essentials 서버 역할을 75 클라이언트 백업 유지에 대 한 지원 되는 제한에 대 한 지원 되는 사용자와 디바이스 제한에 증가 합니다.

<a name="see-also"></a>참조 하십시오
--------
[Windows Server Essentials 시작](get-started.md)