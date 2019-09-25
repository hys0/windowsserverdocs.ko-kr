---
title: Windows 데스크톱 클라이언트 시작
description: Windows 데스크톱 클라이언트에 대한 기본 정보입니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
author: heidilohr
manager: daveba
ms.author: helohr
ms.date: 09/13/2019
ms.localizationpriority: medium
ms.openlocfilehash: c864ba0e51054a553bfd53f845bd4d1c9ff3c8ba
ms.sourcegitcommit: 61767c405da44507bd3433967543644e760b20aa
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70988241"
---
# <a name="get-started-with-the-windows-desktop-client"></a>Windows 데스크톱 클라이언트 시작

>적용 대상: Windows 10 및 Windows 7

Windows 데스크톱용 원격 데스크톱 클라이언트를 사용하여 다른 Windows 디바이스에서 원격으로 Windows 앱 및 데스크톱에 액세스할 수 있습니다.

> [!NOTE]
> - 이 설명서는 Windows와 함께 제공되는 원격 데스크톱 연결(MSTSC) 클라이언트를 위한 것이 아니라 새로운 원격 데스크톱(MSRDC) 클라이언트를 위한 것입니다.
> - 이 클라이언트는 현재 [Windows Virtual Desktop](https://aka.ms/wvd)에서 원격 앱 및 데스크톱에만 액세스하도록 지원합니다.
> - Windows 데스크톱 클라이언트의 새 릴리스가 궁금하신가요? [Windows 데스크톱 클라이언트의 새로운 기능](windowsdesktop-whatsnew.md)을 확인하세요.

## <a name="install-the-client"></a>클라이언트 설치

현재 Windows 64비트용 클라이언트를 다운로드할 수 있습니다. 더 많은 Windows 버전에서 클라이언트를 사용할 수 있게 되면 다음 목록을 업데이트할 것입니다.

- [Windows 64비트 클라이언트](https://go.microsoft.com/fwlink/?linkid=2068602)

관리자 권한이 필요하지 않은 현재 사용자의 클라이언트를 설치하거나, 디바이스의 모든 사용자가 클라이언트에 액세스할 수 있도록 관리자가 클라이언트를 설치 및 구성할 수 있습니다.

설치가 완료되면 **원격 데스크톱**을 검색하여 시작 메뉴에서 클라이언트를 시작할 수 있습니다.

## <a name="feeds"></a>피드

관리자가 제공한 피드를 구독하여 앱 및 데스크톱과 같이 액세스할 수 있는 관리형 리소스의 목록을 가져옵니다. 구독하면 로컬 PC에서 리소스를 사용할 수 있게 됩니다. Windows 데스크톱 클라이언트는 현재 Windows Virtual Desktop에서 게시된 리소스를 지원합니다.

### <a name="subscribe-to-a-feed"></a>피드 구독

1. 연결 센터라고도 하는 클라이언트의 기본 페이지에서 **구독**을 탭합니다.
2. 메시지가 표시되면 사용자 계정으로 로그인합니다.
3. 해당 리소스가 작업 영역별로 그룹화된 연결 센터에 표시됩니다.

리소스는 다음 방법 중 하나를 사용하여 시작할 수 있습니다.

- [연결 센터]로 이동하여 시작할 리소스를 두 번 클릭합니다.
- [시작] 메뉴로 이동하여 작업 영역 이름이 있는 폴더를 찾거나 검색 창에서 리소스 이름을 입력할 수도 있습니다.

### <a name="workspace-details"></a>작업 영역 세부 정보

구독하면 작업 영역에 대한 추가 정보가 [세부 정보] 패널에 표시됩니다.

- 작업 영역의 이름
- 구독하는 데 사용되는 URL 및 사용자 이름
- 앱 및 데스크톱의 수
- 마지막 업데이트 날짜/시간
- 마지막 업데이트의 상태

[세부 정보] 패널에 액세스하려면 다음을 수행합니다.

1. 연결 센터에서 [작업 영역] 옆에 있는 오버플로 메뉴( **...** )를 탭합니다.
2. 드롭다운 메뉴에서 **세부 정보**를 선택합니다.
3. [세부 정보] 패널이 클라이언트의 오른쪽에 표시됩니다.

구독이 완료되면 작업 영역이 정기적으로 자동으로 업데이트됩니다. 관리자가 변경한 내용에 따라 리소스를 추가, 변경 또는 제거할 수 있습니다.

또한 필요한 경우 [세부 정보] 패널에서 **지금 업데이트**를 선택하여 리소스에 대한 업데이트를 수동으로 찾을 수도 있습니다.

### <a name="unsubscribe-from-a-feed"></a>피드에서 구독 취소

이 섹션에서는 피드에서 구독을 취소하는 방법을 설명합니다. 구독을 취소하여 다른 계정으로 다시 구독하거나 시스템에서 리소스를 제거할 수 있습니다.

1. 연결 센터에서 [작업 영역] 옆에 있는 오버플로 메뉴( **...** )를 탭합니다.
2. 드롭다운 메뉴에서 **구독 취소**를 선택합니다.
3. 대화 상자를 검토하고 **계속**을 선택합니다.

## <a name="update-the-client"></a>클라이언트 업데이트

관리자가 사용하지 않도록 설정한 경우를 제외하고는 새 버전의 클라이언트를 사용할 수 있을 때 알림을 받습니다. 이 알림은 연결 센터 또는 Windows 알림 센터에 직접 표시될 수 있습니다. 업데이트 프로세스를 시작하려면 알림을 선택합니다.

또한 클라이언트에 대한 새 업데이트를 수동으로 검색할 수도 있습니다.

1. 연결 센터에서 클라이언트 위쪽의 명령 표시줄에 있는 오버플로 메뉴( **...** )를 탭합니다.
2. 드롭다운 메뉴에서 **정보**를 선택합니다.
3. **업데이트 확인**을 탭합니다.
4. 사용할 수 있는 업데이트가 있으면 **업데이트 설치**를 탭하여 해당 클라이언트를 업데이트합니다.

## <a name="providing-feedback"></a>사용자 의견 제공

기능을 제안하거나 문제를 보고하려고 하나요? 클라이언트에서도 액세스할 수 있는 [피드백 허브](feedback-hub://?tabid=2&contextid=883)를 사용하여 알려주세요.

1. 연결 센터에서 클라이언트 위쪽의 명령 표시줄에 있는 오버플로 메뉴( **...** )를 탭합니다.
2. 드롭다운 메뉴에서 **피드백**을 선택하여 [피드백 허브]를 엽니다.