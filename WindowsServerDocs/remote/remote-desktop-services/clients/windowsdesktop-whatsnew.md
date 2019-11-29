---
title: Windows 데스크톱 클라이언트의 새로운 기능
description: Windows 데스크톱용 원격 데스크톱 클라이언트의 최근 변경 내용에 대해 알아봅니다.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
author: heidilohr
manager: daveba
ms.author: helohr
ms.date: 11/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: 54994aad08c2f428b429082ed450235ed8bbe7e7
ms.sourcegitcommit: 244b89505c5131dfdb90628857cc7e31741c84c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2019
ms.locfileid: "74265922"
---
# <a name="whats-new-in-the-windows-desktop-client"></a>Windows 데스크톱 클라이언트의 새로운 기능

Windows 데스크톱 클라이언트에 대한 자세한 내용은 [Windows 데스크톱 클라이언트 시작](windowsdesktop.md)에서 확인할 수 있습니다. 여기서는 클라이언트에 대한 최신 업데이트를 확인할 수 있습니다.

## <a name="latest-client-versions"></a>최신 클라이언트 버전

클라이언트는 서로 다른 [ 사용자 그룹](windowsdesktop-admin.md#configure-user-groups)에 대해 구성할 수 있습니다. 다음 표에는 각 사용자 그룹에 사용할 수 있는 현재 버전이 나와 있습니다.

|사용자 그룹 |버전  |
|-----------|---------|
|Public     |1.2.431  |
|Windows 참가자 프로그램    |1.2.524  |

## <a name="updates-for-version-12524"></a>1\.2.524 버전에 대한 업데이트

*게시 날짜: 11/20/2019*

다운로드: [Windows 64비트](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4e7Nj), [Windows 32비트](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4dZCo), [Windows ARM64](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4dX1s)

- 이제는 클라이언트 상단의 명령 모음에 있는 추가 옵션 버튼에서 직접 업데이트에 대한 정보에 액세스할 수 있습니다.
- 이제는 클라이언트의 명령 모음에서 피드백을 보고할 수 있습니다.

## <a name="updates-for-version-12431"></a>1\.2.431 버전에 대한 업데이트

*게시 날짜: 2019/11/12*

다운로드: [Windows 64비트](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE48kow), [Windows 32비트](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE48koA), [Windows ARM64](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE48zYj)

- 이제 32비트 및 ARM64 버전의 클라이언트를 사용할 수 있습니다!
- 이제 클라이언트는 연결 모음에 대한 변경 내용(예: 위치, 크기 및 고정 상태)을 저장하고 이러한 변경 내용을 세션 간에 적용합니다.
- 업데이트된 게이트웨이 정보 및 연결 상태 대화 상자
- Azure Active Directory 토큰이 만료된 후 연결을 시도하는 동안 두 자격 증명을 동시에 표시하는 문제를 해결했습니다.
- 이제 Windows 7에서는 서버에서 자격 증명을 허용하지 않을 때 자격 증명을 저장한 경우 사용자에게 자격 증명을 입력하라는 메시지가 표시됩니다.
- 이제 다시 연결할 때 Azure Active Directory 프롬프트가 연결 창 앞에 표시됩니다.
- 작업 표시줄에 고정된 항목은 이제 피드를 새로 고치는 동안 업데이트됩니다.
- 터치를 사용하는 경우 연결 센터에서 스크롤 기능이 향상되었습니다.
- 해상도 드롭다운 메뉴에서 빈 줄을 제거했습니다.
- Windows 자격 증명 관리자에서 불필요한 항목을 제거했습니다.
- 이제 전체 화면을 종료할 때 데스크톱 세션의 크기가 적절하게 조정됩니다.
- 이제 절전 모드로 들어간 후 세션을 다시 시작하면 RemoteApp 연결 끊기 대화 상자가 전경에 표시됩니다.
- 키보드 탐색과 같은 접근성 문제를 해결했습니다.

## <a name="updates-for-version-12247"></a>1\.2.247 버전에 대한 업데이트

*게시 날짜: 2019년 9월 17일*

다운로드: [Windows 64비트](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE3LkSa)

- 지역화된 버전의 대체 언어가 향상되었습니다. 예를 들어 FR-CA는 영어 대신 프랑스어로 올바르게 표시됩니다.
- 구독을 제거하면 이제 클라이언트의 자격 증명 관리자에서 저장된 자격 증명을 올바르게 제거합니다.
- 클라이언트 업데이트 프로세스가 시작되면 이제 무인 모드로 실행되고, 완료되면 클라이언트가 다시 시작됩니다.
- 클라이언트는 이제 Windows 10에서 S 모드로 사용할 수 있습니다.
- 사용자 이름에 공백이 있는 사용자에 대한 업데이트 프로세스가 실패하는 문제가 해결되었습니다.
- 연결 중에 인증할 때 발생하는 충돌이 해결되었습니다.
- 클라이언트를 닫을 때 발생하는 충돌이 해결되었습니다.
