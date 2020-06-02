---
title: Windows 데스크톱 클라이언트의 새로운 기능
description: Windows 데스크톱용 원격 데스크톱 클라이언트의 최근 변경 내용에 대해 알아봅니다.
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.topic: article
author: heidilohr
manager: lizross
ms.author: helohr
ms.date: 05/27/2020
ms.localizationpriority: medium
ms.openlocfilehash: 0d49c49def8b110f42a6d56354c73e5a75b04b7e
ms.sourcegitcommit: 4fec7d82f0772d03a9e8cac20092a4309b0f796e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/27/2020
ms.locfileid: "84025514"
---
# <a name="whats-new-in-the-windows-desktop-client"></a>Windows 데스크톱 클라이언트의 새로운 기능

Windows 데스크톱 클라이언트에 대한 자세한 내용은 [Windows 데스크톱 클라이언트 시작](windowsdesktop.md)에서 확인할 수 있습니다. 여기서는 클라이언트에 대한 최신 업데이트를 확인할 수 있습니다.

## <a name="latest-client-versions"></a>최신 클라이언트 버전

클라이언트는 서로 다른 [ 사용자 그룹](windowsdesktop-admin.md#configure-user-groups)에 대해 구성할 수 있습니다. 다음 표에는 각 사용자 그룹에 사용할 수 있는 현재 버전이 나와 있습니다.

|사용자 그룹 |Version  |
|-----------|---------|
|공용     |1.2.1026 |
|참가자    |1.2.1026 |

## <a name="updates-for-version-121026"></a>1\.2.1026 버전에 대한 업데이트

*게시 날짜: 2020/05/27*

다운로드: [Windows 64비트](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4xsGB), [Windows 32비트](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4xd8P), [Windows ARM64](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4xq7m)

- 구독하는 경우 이메일 주소를 입력하는 대신 이제 계정을 선택할 수 있습니다.
- 구독 중인 작업 영역의 URL을 지정하거나 리소스를 자동으로 찾을 수 없는 경우 [이메일 검색](../rds-email-discovery.md)을 활용할 수 있는 새로운 **URL로 구독** 옵션이 추가되었습니다. 이는 다른 원격 데스크톱 클라이언트의 구독 프로세스와 유사합니다. 이는 WVD Spring 2020 Update 작업 영역을 직접 구독하는 데 사용할 수 있습니다.
- 사용자에게 이메일로 보내거나 지원 웹 사이트에 추가할 수 있는 새로운 [URI 스키마](remote-desktop-uri.md)를 사용하여 작업 영역의 구독 지원을 추가했습니다.
- 데스크톱 및 애플리케이션 세션에 대한 클라이언트, 네트워크 및 서버 세부 정보를 제공하는 새로운 **연결 정보** 대화 상자가 추가되었습니다. 이 대화 상자는 전체 화면 모드의 연결 표시줄 또는 창 모드의 시스템 메뉴에서 액세스할 수 있습니다.
- 창 모드에서 시작된 데스크톱 세션은 이제 창을 최대화할 경우 전체 화면으로 전환되지 않고 항상 최대화됩니다. 전체 화면으로 전환하려면 시스템 메뉴에서 **전체 화면** 옵션을 사용하세요.
- 이제 구독 취소 프롬프트에 경고 아이콘이 표시되고 작업 영역 이름이 글머리 기호 목록으로 표시됩니다.
- 문제를 진단하는 데 도움이 되는 추가 오류 대화 상자에 세부 정보 섹션이 추가되었습니다.
- 오류 대화 상자의 세부 정보 섹션에 타임스탬프가 추가되었습니다.
- **데스크톱 크기 ID**라는 RDP 파일 설정이 제대로 작동하지 않는 문제가 해결되었습니다.
- 세션을 시작한 후 **크기 조정 시 해상도 업데이트** 디스플레이 설정이 적용되지 않는 문제가 해결되었습니다.
- 데스크톱 설정 패널의 지역화 문제가 해결되었습니다.
- 데스크톱 설정 패널에서 컨트롤을 탭하여 이동할 때 포커스 상자의 크기가 수정되었습니다.
- 고대비 모드에서 리소스 이름이 잘 보이지 않는 문제가 해결되었습니다.
- 작업 센터의 업데이트 알림이 하루에 두 번 이상 표시되는 문제가 해결되었습니다.

## <a name="updates-for-version-12945"></a>1\.2.945 버전에 대한 업데이트

*게시 날짜: 2020/04/28*

다운로드: [Windows 64비트](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4vhNM), [Windows 32비트](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4vhNO), [Windows ARM64](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4vuSV)

- 연결 센터에서 데스크톱 아이콘을 마우스 오른쪽 단추로 클릭하면 제공되는 데스크톱 연결에 대한 새 표시 설정 옵션이 추가되었습니다.
  - 이제 **모든 디스플레이**, **단일 디스플레이** 및 **디스플레이 선택**이라는 세 가지 표시 구성 옵션이 있습니다.
  - 이제 디스플레이 구성을 선택할 경우에만 사용 가능한 설정이 표시됩니다.
  - 디스플레이 선택 모드에서는 **현재 디스플레이에 맞게 최대화**라는 새 옵션을 사용하여 다시 연결하지 않고 세션에 사용되는 디스플레이를 동적으로 변경할 수 있습니다. 사용하도록 설정하면 세션을 최대화할 경우 세션 창이 열리는 모든 디스플레이에서 해당 세션이 전체 화면으로 표시됩니다.
  - 모든 디스플레이와 디스플레이 선택 모드에 대한 **창 모드인 경우 단일 디스플레이**라는 새 옵션이 추가되었습니다. 이 옵션은 전체 화면 모드를 종료할 때 세션을 자동으로 단일 디스플레이로 전환하고 창을 최대화하면 자동으로 다중 디스플레이로 돌아갑니다.
- 창 모드 데스크톱 세션의 제목 표시줄을 마우스 오른쪽 단추로 클릭하면 표시되는 시스템 메뉴에 **디스플레이 설정**이라는 새 그룹이 추가되었습니다. 이를 사용하면 세션 중에 일부 설정을 동적으로 변경할 수 있습니다. 예를 들어 새로운 **창 모드인 경우 단일 디스플레이 모드** 및 **현재 디스플레이에 맞게 최대화** 설정을 변경할 수 있습니다.
- 전체 화면을 종료하면 세션 창이 처음 전체 화면으로 전환되기 전 원래 위치로 돌아갑니다.
- 작업 영역의 백그라운드 새로 고침 간격이 1시간마다에서 4시간마다로 변경되었습니다. 클라이언트를 시작할 때 이제 새로 고침이 자동으로 수행됩니다.
- 이제 정보 페이지에서 사용자 데이터를 다시 설정하면 완료 시 클라이언트를 닫지 않아도 연결 센터로 리디렉션됩니다.
- 데스크톱 연결에 대한 시스템 메뉴의 항목이 다시 정렬되고 도움말 항목이 이제 클라이언트 설명서를 가리킵니다.
- 탭 탐색 및 화면 읽기 프로그램과 관련된 몇 가지 내게 필요한 옵션 문제가 해결되었습니다.
- 세션 창 뒤에 Azure Active Directory 인증 대화 상자가 나타나는 문제가 해결되었습니다.
- 여러 배율 디스플레이 사이에서 데스크톱 세션 창을 끌 때의 깜박임 및 축소 문제가 해결되었습니다.
- 카메라를 리디렉션하는 동안 발생하는 오류가 해결되었습니다.
- 안정성 개선을 위해 여러 크래시가 해결되었습니다.

## <a name="updates-for-version-12790"></a>1\.2.790 버전에 대한 업데이트

*게시 날짜: 2020/03/24*

다운로드: [Windows 64비트](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4siSh), [Windows 32비트](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4siSi), [Windows ARM64](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4sllb)

- 다른 원격 데스크톱 클라이언트와 일치하도록 작업 영역에 대한 "업데이트" 작업의 이름이 "새로 고침"으로 변경되었습니다.
- 이제 컨텍스트 메뉴에서 작업 영역을 직접 새로 고칠 수 있습니다.
- 이제 작업 영역을 수동으로 새로 고치면 모든 로컬 콘텐츠가 업데이트됩니다.
- 이제 앱을 제거할 필요 없이 [정보] 페이지에서 클라이언트의 사용자 데이터를 다시 설정할 수 있습니다.
- 프롬프트를 건너뛰기 위해 선택적 /f 매개 변수가 포함된 msrdcw.exe /reset을 사용하여 클라이언트의 사용자 데이터를 다시 설정할 수도 있습니다.
- 이제 [정보] 페이지로 이동하면 클라이언트 업데이트를 자동으로 찾습니다.
- 단추의 색이 일치하도록 업데이트되었습니다.

## <a name="updates-for-version-12675"></a>1\.2.675 버전에 대한 업데이트

*게시 날짜: 2020/02/25*

다운로드: [Windows 64비트](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4qeak), [Windows 32비트](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4qm7h), [Windows ARM64](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4qm7g)

- RDP 파일에 서명이 없거나 signscope 속성 중 하나가 수정된 경우 Windows 가상 데스크톱에 대한 연결이 차단됩니다.
- 작업 영역이 비어 있거나 제거되면 연결 센터가 더 이상 비어있는 것으로 나타나지 않습니다.
- 문제 해결을 개선하기 위해 연결 해제 메시지에 활동 ID와 오류 코드를 추가했습니다. **Ctrl+C**를 사용하여 대화 상자 메시지를 복사할 수 있습니다.
- 데스크톱 연결 설정이 디스플레이를 감지하지 못하게 하는 문제를 수정했습니다.
- 클라이언트를 업데이트해도 더 이상 PC가 자동으로 다시 시작되지 않습니다.
- 창 없는 아이콘이 작업 표시줄에 더 이상 나타나지 않습니다.

## <a name="updates-for-version-12605"></a>1\.2.605 버전에 대한 업데이트

*게시 날짜: 2020/01/29*

다운로드: [Windows 64비트](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4oHrD), [Windows 32비트](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4oJZs), [Windows ARM64](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4oXhD)

- 이제 데스크톱 연결에 사용할 디스플레이를 선택할 수 있습니다. 이 설정을 변경하려면 데스크톱 연결의 아이콘을 마우스 오른쪽 단추로 클릭하고 **설정**을 선택합니다.
- 연결 설정에서 사용 가능한 크기 조정 요소를 올바르게 표시하지 않는 문제가 해결되었습니다.
- 연결을 시작하는 동안 내레이터에서 표시된 대화를 읽을 수 없는 문제가 해결되었습니다.
- Azure Active Directory와 Active Directory 이름이 일치하지 않을 경우 잘못된 사용자 이름이 표시되는 문제가 해결되었습니다.
- 네트워크에 연결되지 않은 상태에서 연결을 시작할 때 클라이언트가 응답하지 않는 문제가 해결되었습니다.
- 헤드셋을 연결할 때 클라이언트가 응답하지 않는 문제가 해결되었습니다.

## <a name="updates-for-version-12535"></a>1\.2.535 버전에 대한 업데이트

*게시 날짜: 2019년 12월 4일*

다운로드: [Windows 64비트](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4k7jH), [Windows 32비트](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4k7jL), [Windows ARM64](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4k27O)

- 이제는 클라이언트 상단의 명령 모음에 있는 추가 옵션 버튼에서 직접 업데이트에 대한 정보에 액세스할 수 있습니다.
- 이제는 클라이언트의 명령 모음에서 피드백을 보고할 수 있습니다.
- 피드백 옵션은 이제 피드백 허브를 사용할 수 있는 경우에만 표시됩니다.
- 정책을 통해 알림을 사용하지 않도록 설정하면 업데이트 알림이 표시되지 않습니다.
- 일부 RDP 파일이 시작되지 않는 문제가 해결되었습니다.
- 일부 영구 설정이 손상되어 클라이언트 시작 시 작동이 중단되는 문제가 해결되었습니다.

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
