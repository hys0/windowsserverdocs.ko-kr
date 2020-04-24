---
title: 연결 시 "원격 데스크톱 서비스가 현재 사용 중입니다" 메시지가 수신됨
description: 사용자가 원격 데스크톱 연결을 시작할 때의 "원격 데스크톱 서비스가 현재 사용 중입니다" 오류를 해결합니다.
ms.reviewer: rklemen
ms.topic: troubleshooting
author: kaushika-msft
manager: dcscontentpm
ms.author: delhan
ms.date: 07/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: c345833ee63a1286a5615998649e8aa9d25896a6
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2020
ms.locfileid: "80857166"
---
# <a name="on-connecting-user-receives-remote-desktop-service-is-currently-busy-message"></a>사용자가 연결하면 "원격 데스크톱 서비스가 현재 사용 중입니다" 메시지가 수신됨

이 문제를 해결하기 위한 적절한 대응 방법을 확인하려면 다음을 참조하세요.

- 원격 데스크톱 서비스가 응답하지 않습니다(예: 시작 화면에서 원격 데스크톱 클라이언트가 "중지"된 것으로 표시됨).  
   - 서비스가 응답하지 않는 경우 [RDSH 서버 메모리 이슈](#rdsh-server-memory-issue)를 참조하세요.
   - 클라이언트가 정상적으로 서비스와 상호 작용하는 것으로 표시되면 다음 단계를 진행합니다.
- 한 명 이상의 사용자가 원격 데스크톱 세션을 종료하는 경우 사용자가 다시 연결할 수 있나요?  
   - 세션을 종료하는 사용자가 몇 명이든 서비스에서 연결을 계속 거부하면 [RD 수신기 이슈](#rd-listener-issue)를 참조하세요.
   - 수많은 사용자가 세션을 종료한 후 서비스에서 다시 연결을 수락하는 경우 [연결 제한 정책을 확인](#check-the-connection-limit-policy)합니다.

## <a name="rdsh-server-memory-issue"></a>RDSH 서버 메모리 이슈

일부 Windows Server 2012 R2 RDSH 서버에서 메모리 누수가 발견되었습니다. 이러한 서버는 시간이 지남에 따라 다음과 같은 메시지와 함께 원격 데스크톱 연결 및 로컬 콘솔 로그인을 모두 거부하기 시작합니다.

> 원격 데스크톱 서비스가 현재 사용 중이므로 수행하려는 작업을 완료할 수 없습니다. 몇 분 후에 다시 시도하세요. 다른 사용자는 여전히 로그인할 수 있어야 합니다.

또한 연결하려는 원격 데스크톱 클라이언트에서도 응답하지 않습니다.

이 이슈를 해결하려면 RDSH 서버를 다시 시작합니다.

이 문제를 해결하려면 KB 4093114([2018년 4월 10일 - KB4093114(매월 롤업)](https://support.microsoft.com/help/4093114/))를 RDSH 서버에 적용합니다.

## <a name="rd-listener-issue"></a>RD 수신기 이슈

Windows Server 2008 R2에서 Windows Server 2012 R2 또는 Windows Server 2016으로 바로 업그레이드된 일부 RDSH 서버에서 이슈가 발견되었습니다. 원격 데스크톱 클라이언트가 RDSH 서버에 연결되면 RDSH 서버에서 사용자 세션에 대한 RD 수신기를 만듭니다. 영향을 받는 서버는 사용자가 연결할 때 RD 수신기 수를 늘리기만 하고 줄이지는 않습니다.

이 문제는 다음과 같은 방법으로 해결할 수 있습니다.

  - RDSH 서버를 다시 시작하여 RD 수신기 수를 초기화합니다.
  - 연결 제한을 매우 큰 값으로 설정하여 정책을 수정합니다. 연결 제한 정책 관리에 대한 자세한 내용은 [연결 제한 정책 확인](#check-the-connection-limit-policy)을 참조하세요.

이 이슈를 해결하려면 다음 업데이트를 RDSH 서버에 적용합니다.

  - Windows Server 2012 R2: KB 4343891, [2018년 8월 30일 - KB4343891(월별 롤업 미리 보기)](https://support.microsoft.com/help/4343891/windows-81-update-kb4343891)
  - Windows Server 2016: KB 4343884, [2018년 8월 30일 - KB4343884(OS 빌드 14393.2457)](https://support.microsoft.com/help/4343884/windows-10-update-kb4343884)

## <a name="check-the-connection-limit-policy"></a>연결 제한 정책 확인

개별 컴퓨터 수준에서 또는 GPO(그룹 정책 개체)를 구성하여 동시 원격 데스크톱 연결 수 제한을 설정할 수 있습니다. 기본적으로 제한은 설정되지 않습니다.

RDSH 서버의 현재 설정을 확인하고 기존 GPO를 파악하려면 관리자 권한으로 명령 프롬프트 창을 열고 다음 명령을 입력합니다.
  
```cmd
gpresult /H c:\gpresult.html
```
   
이 명령이 완료되면 **gpresult.html** 파일을 엽니다. **컴퓨터 구성\\관리 템플릿\\Windows 구성 요소\\원격 데스크톱 서비스\\원격 데스크톱 세션 호스트\\연결**에서 **연결 수 제한** 정책을 찾습니다.

  - 이 정책을 **사용 안 함**으로 설정하면 그룹 정책이 RDP 연결을 제한하지 않습니다.
  - 이 정책이 **사용**으로 설정된 경우 **최우선 GPO**를 확인합니다. 연결 제한을 제거 또는 변경해야 하는 경우 이 GPO를 편집합니다.

정책 변경 내용을 적용하려면 영향을 받는 컴퓨터에서 명령 프롬프트 창을 열고 다음 명령을 입력합니다.
  
```cmd
gpupdate /force
```
  
