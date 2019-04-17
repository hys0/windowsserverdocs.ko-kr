---
title: 네트워크 관리 도구와 정책 서버 관리
description: Windows Server 2016에 네트워크 정책 서버 관리 하는 데 사용할 수 있는 도구에 대 한 자세한 내용은이 항목을 사용할 수 있습니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 5de80dc0-53be-42b7-8e5b-24d213bf2b25
ms.author: pashort
author: shortpatti
ms.openlocfilehash: cdb82c5bc1c541f19b1b2f4c8db837af4a812f81
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="network-policy-server-management-with-administration-tools"></a>네트워크 관리 도구와 정책 서버 관리

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

NPS 서버 관리 하는 데 사용할 수 있는 도구에 대 한 자세한 내용은이 항목을 사용할 수 있습니다.

NPS을 설치한 후 NPS 서버 관리할 수 있습니다.

- 로컬에 NPS Microsoft Management Console \(MMC\) 스냅인, 관리 도구나 Windows PowerShell 명령 셸이 되었습니다 네트워크 \(Netsh\) 명령에 정적 NPS 본체에 대 한 통해 NPS 합니다.
- 원격 NPS 서버, NPS 또는 원격 데스크톱 연결에 대 한 NPS MMC 스냅인, nps Netsh 명령을, Windows PowerShell 명령을 사용 하 여 합니다.
- Windows PowerShell NPS MMC 등의 기타 도구와 함께에서 원격 데스크톱 연결을 사용 하 여 원격 워크스테이션 합니다.

>[!NOTE]
>Windows Server 2016 NPS 콘솔을 사용 하 여 로컬 NPS 서버를 관리할 수 있습니다. 원격 및 로컬 NPS 서버 관리, NPS MMC snap\에서 사용 해야 합니다.

다음 섹션 NPS 지역 및 원격 서버 관리 하는 방법에 지침을 제공 합니다.

## <a name="configure-the-local-nps-server-by-using-the-nps-console"></a>NPS 본체를 사용 하 여 로컬 NPS 서버 구성

NPS을 설치한 후이 절차 NPS MMC 사용 하 여 로컬 NPS 서버 관리에 사용할 수 있습니다.

**관리자 자격 증명** 

이 절차를 수행 하려면 관리자가 그룹의 회원 이어야 합니다.

### <a name="to-configure-the-local-nps-server-by-using-the-nps-console"></a>NPS 본체를 사용 하 여 로컬 NPS 서버 구성 하려면

1. 서버 관리자 클릭 **도구**을 차례로 클릭 하 고 **네트워크 정책 서버**합니다. NPS console을 엽니다.

2. NPS 본체에서 NPS \(Local\)를 클릭 합니다. 세부 정보 창에서 중 하나를 선택 **표준 구성** 또는 **고급 구성**, 선택 항목에 따라 다음 중 하나를 수행 합니다.
    - 원하는 경우 **표준 구성**시나리오를 목록에서 선택한 다음 구성 마법사를 시작 지침을 따릅니다.
    - 원하는 경우 **고급 구성**를 화살표를 클릭 **구성 고급 옵션**, 다음 검토 하 고 RADIUS 서버, RADIUS 프록시 또는 둘 다에서 원하는 NPS 기능에 따라 사용할 수 있는 옵션을 구성 하 고 있습니다.

## <a name="manage-multiple-nps-servers-by-using-the-nps-mmc-snap-in"></a>NPS MMC Snap\에 사용 하 여 여러 NPS 서버 관리

이 절차 NPS MMC snap\에 사용 하 여 로컬 NPS 서버 및 원격 여러 NPS 서버 관리에 사용할 수 있습니다.

아래 절차를 수행 하기 전에 원격 컴퓨터와 로컬 컴퓨터에서 NPS 설치 해야 합니다.

네트워크 상태 NPS 서버 NPS MMC snap\에서 사용 하 여 관리할 수에 따라 mmc snap\에 응답 느려질 수 있습니다. 또한, NPS 서버 구성 교통 전송 네트워크를 통해 원격 관리 세션 동안 NPS snap\에 사용 하 여 합니다. 네트워크 실제로 확실 하 고 있다는 악의적인 사용자가 없는 네트워크 교통이에 대 한 액세스를 확인 합니다.

**관리자 자격 증명** 

이 절차를 수행 하려면 관리자가 그룹의 회원 이어야 합니다.

### <a name="to-manage-multiple-nps-servers-by-using-the-nps-snap-in"></a>NPS snap\에 사용 하 여 여러 NPS 서버 관리 하려면

1. MMC를 열려면 Windows PowerShell을 관리자 권한으로 실행 합니다. Windows PowerShell 입력 **mmc**, ENTER 키를 누릅니다. Microsoft Management Console을 엽니다.
2. MMC에서에 **파일** 메뉴를 클릭 **Snap\에 추가/제거**합니다. **추가 또는 제거 Snap\ 기능** 대화 상자를 엽니다.
3. **추가 또는 제거 Snap\ 기능**에서 **사용 가능한 snap\ 기능**목록 아래로 스크롤하여을 클릭 **네트워크 정책 서버**를 차례로 클릭 하 고 **추가**합니다. **컴퓨터 선택** 대화 상자를 엽니다.
4. **컴퓨터 선택**, 되어 있는지 확인 **로컬 컴퓨터 \ (컴퓨터에는이 콘솔은 running\)** 을 선택한 다음 클릭 **확인**합니다. 로컬 NPS 서버에 대 한으로 snap\ 기능 목록에 추가 **snap\ 기능 선택한**합니다.
5. **추가 또는 제거 Snap\ 기능**에 **사용 가능한 snap\ 기능**, 되도록 **네트워크 정책 서버** 스틸을 선택 하 고 클릭 하면 됩니다 **추가**합니다. **컴퓨터 선택** 대화 상자를 다시 엽니다.
6. **컴퓨터 선택**, 클릭 **다른 컴퓨터**, IP 주소 또는 정식된 도메인 NPS snap\에 사용 하 여 관리할 원격 NPS 서버 \(FQDN\) 이름을 입력 합니다. 클릭 수 있습니다 **찾아보기** 를 추가 하려면 컴퓨터에 대 한 디렉터리 읽습니다. 클릭 **확인**합니다.
7. 5, 6 더 많은 NPS 서버에서 snap\ NPS에 추가 하는 단계를 반복 합니다. 관리 클릭 하려는 모든 NPS 서버 추가한 후 **확인**합니다.
8. 나중을 위해 NPS 스냅인 저장 하려면 **파일**을 차례로 클릭 하 고 **저장**합니다. 에 **다른 이름으로 저장** 대화 상자에서 파일을 저장 하 여 Microsoft Management Console \(.msc\) 파일의 이름을 입력 클릭 한 다음 원하는 하드 디스크 위치를 찾습니다 **저장**합니다. 

## <a name="manage-an-nps-server-by-using-remote-desktop-connection"></a>원격 데스크톱 연결을 사용 하 여 NPS 서버 관리

원격 데스크톱 연결을 사용 하 여 NPS 원격 서버 관리이 절차를 사용할 수 있습니다.

원격 데스크톱 연결을 사용 하 여 Windows Server 2016을 실행 하는 NPS 서버를 원격으로 관리할 수 있습니다. 이전 버전의 Windows 클라이언트 운영 체제 또는 Windows 10을 실행 하는 컴퓨터에서 NPS 서버를 원격으로 관리할 수 있습니다.

두 가지 방법 중 하나를 사용 하 여 여러 NPS 서버 관리 원격 데스크톱 연결을 사용할 수 있습니다.

1. 원격 데스크톱 연결을 각각의 NPS 서버를 개별적으로 만듭니다.
2. 한 NPS 서버에 연결 하려면 원격 데스크톱을 사용 하 고 서버에 NPS MMC 다른 원격 서버 관리를 사용 합니다. 자세한 내용은 참조 이전 섹션 **NPS MMC Snap\에 사용 하 여 여러 NPS 서버 관리**합니다.

**관리자 자격 증명** 

이 절차를 완료 하려면 NPS 서버에 관리자가 그룹의 회원 이어야 합니다.

### <a name="to-manage-an-nps-server-by-using-remote-desktop-connection"></a>원격 데스크톱 연결을 사용 하 여 NPS 서버 관리 하려면

1. 각 NPS 서버를 원격으로 서버 관리자 관리할 선택 **로컬 서버**합니다. 서버 관리자 세부 정보 창에서 보고 있는 **원격 데스크톱** 설정 하 고 다음 중 하나를 수행 합니다. 
    1. 하는 경우의 값은 **원격 데스크톱** 설정이 **사용**,이 절차의 일부의 단계를 수행 해야 합니다. 원격 데스크톱 사용자 권한을 구성 시작 4 단계 나타날 때까지 아래로 건너뜁니다.
    2. 하는 경우는 **원격 데스크톱** 설정이 **사용 안 함**를 단어 클릭 **사용 안 함**합니다. **시스템 속성** 대화 상자에서 열리는 **원격** 탭 합니다.
2. **원격 데스크톱**, 클릭 **이 컴퓨터에 대 한 원격 연결 허용**합니다. **원격 데스크톱 연결** 대화 상자를 엽니다. 다음 중 하나를 수행 합니다.
    1. 허용 되는 네트워크 연결을 사용자 지정 하려면 클릭 **고급 보안이 포함된 Windows 방화벽**, 다음 허용할 설정을 구성 하 고 있습니다. 
    2. 원격 데스크톱 연결을 컴퓨터에 연결 모든 네트워크에 대 한 사용 하도록 설정 하려면 클릭 **확인**합니다.
3. **시스템 속성**에서 **원격 데스크톱**, 사용할지 여부를 결정할 **는 네트워크 수준 인증 원격 데스크톱을 실행 하는 컴퓨터 에서만에서 연결 허용**를 선택 하 고 있습니다.
4. 클릭 **사용자 선택**합니다. **원격 데스크톱 사용자** 대화 상자를 엽니다.
5. **원격 데스크톱 사용자**, NPS 서버를 원격 연결을 클릭 하 여 사용자에 게 권한을 부여 하려면 **추가**, 사용자의 계정에 대 한 사용자 이름을 입력 합니다. 클릭 **확인**합니다.
6. 각 사용자 NPS 서버에 대 한 원격 액세스 권한을 부여 하려는 사람에 대해 5 단계를 반복 합니다. 사용자 추가 마치면 클릭 **확인** 닫을 수 있는 **원격 데스크톱 사용자** 대화 상자 및 **확인** 를 닫습니다는 **시스템 속성** 대화 상자 합니다.
7. 위의 단계를 사용 하 여 구성한 경우 원격 NPS 서버에 연결 하려면 클릭 **시작**사전순 목록을 아래로 스크롤하세요을 클릭 한 다음 **Windows 액세서리**를 클릭 하 고 **원격 데스크톱 연결**합니다. **원격 데스크톱 연결** 대화 상자를 엽니다.
8. 에 **원격 데스크톱 연결** 대화 상자의 **컴퓨터**, NPS 서버 이름 또는 IP 주소를 입력 합니다. 원하는 경우 클릭 **옵션**를 구성 추가 연결 옵션을 클릭 한 다음 **저장** 반복 해 서 사용에 대 한 연결을 저장 합니다.
9. 클릭 **연결**, 메시지가 표시 되 면 하 고 로그온 하 고 NPS 서버 구성 하려면 사용 권한이 있는 계정에 대 한 사용자 계정 자격 증명을 제공 합니다.

## <a name="use-netsh-nps-commands-to-manage-an-nps-server"></a>Netsh NPS 명령 NPS 서버 관리를 사용 하 여

표시 하 고 계정 및 모두 NPS 한 원격 액세스 서비스에서 사용 하는 데이터베이스에 감사 인증, 인증, 구성 설정할 명령을 Netsh NPS 상황에서 사용할 수 있습니다. Netsh NPS 컨텍스트를에 명령을 사용 하 여 다음과 같습니다.

- 구성 또는 NPS 서버, Windows 인터페이스 NPS 콘솔을 사용 하 여도 구성에 맞게 사용할 수 있는 NPS의 모든 측면을 포함 하 여를 다시 구성 합니다.
- 레지스트리 키와 Netsh 본으로 NPS 구성 스토어를 포함 한 NPS 서버 (소스 서버) 구성을 내보냅니다.
- Netsh 스크립트 및 소스 NPS 서버에서 내보낸된 구성 파일을 사용 하 여 다른 NPS 서버로 구성을 가져옵니다.

Windows PowerShell 또는 Windows Server 2016 명령 프롬프트에서 다음이 명령의 실행할 수 있습니다. Netsh nps 명령 스크립트 및 배치 파일의 실행할 수도 있습니다.

**관리자 자격 증명** 

이 절차를 수행 하려면 로컬 컴퓨터에서 관리자가 그룹의 회원 이어야 합니다.

### <a name="to-enter-the-netsh-nps-context-on-an-nps-server"></a>Netsh NPS 컨텍스트 NPS 서버의 입력 하려면

1. Windows PowerShell 또는 명령 프롬프트를 엽니다.
2. 입력 **netsh**, ENTER 키를 누릅니다.
3. 입력 **nps**, ENTER 키를 누릅니다.
4. 사용할 수 있는 명령 목록이 보려면 물음표 \(?\) 입력 하 고 ENTER 키를 누릅니다.


Netsh NPS 명령에 대 한 자세한 내용은 참조 [Windows Server 2008에서 네트워크 정책 서버에 대 한 명령 Netsh](https://technet.microsoft.com/library/cc754428(v=ws.10).aspx), 전체 다운로드 하거나 [Netsh 기술 참조](https://gallery.technet.microsoft.com/Netsh-Technical-Reference-c46523dc?redir=0) TechNet 갤러리에서 합니다. 이 다운로드는 완전 한 네트워크 셸 기술 참조 Windows Server 2008 및 Windows Server 2008 R2. Windows 도움말 \(*.chm\) zip 파일의 형식이.입니다. 이 명령은 Windows 10 및 Windows Server 2016에도 있는 되므로 netsh 이러한 환경에서를 사용할 수 있지만 Windows PowerShell를 사용 하는 것이 좋습니다.

## <a name="use-windows-powershell-to-manage-nps-servers"></a>Windows PowerShell NPS 서버 관리를 사용 하 여

Windows PowerShell 명령을 NPS 서버 관리에 사용할 수 있습니다. 자세한 내용은 다음과 같은 Windows PowerShell 명령 참조 항목을 참조 합니다.

- [네트워크에서 Windows PowerShell 정책 (NPS) 서버 Cmdlet](https://technet.microsoft.com/library/jj872739(v=wps.630).aspx)합니다. Netsh 명령을 Windows Server 2012 r 2 또는 이상 운영 체제에 사용할 수 있습니다.
- [NPS 모듈](https://technet.microsoft.com/itpro/powershell/windows/nps/index)합니다. Netsh 명령을 Windows Server 2016에 사용할 수 있습니다.

NPS 관리에 대 한 자세한 내용은 참조 [관리 네트워크 NPS 정책 서버 ()](nps-manage-top.md)합니다.
