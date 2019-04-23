---
title: 관리 도구를 사용하여 네트워크 정책 서버 관리
description: Windows Server 2016에서 네트워크 정책 서버를 관리 하는 데 사용할 수 있는 도구에 대해 자세히 알아보려면이 항목에서는 사용할 수 있습니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 5de80dc0-53be-42b7-8e5b-24d213bf2b25
ms.author: pashort
author: shortpatti
ms.openlocfilehash: fa1767e49b16f4a55f36e052d4354aaead540f26
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856884"
---
# <a name="network-policy-server-management-with-administration-tools"></a>관리 도구를 사용하여 네트워크 정책 서버 관리

>적용 대상: Windows Server (반기 채널), Windows Server 2016

프로그램 NPSs 관리 하는 데 사용할 수 있는 도구에 대해 자세히 알아보려면이 항목에서는 사용할 수 있습니다.

NPS를 설치한 후 NPSs를 관리할 수 있습니다.

- NPS Microsoft 관리 콘솔을 사용 하 여 로컬로 \(MMC\) 스냅인, 관리 도구, Windows PowerShell 명령 또는 네트워크 셸 정적 NPS 콘솔 \(Netsh\) NPS에 대 한 명령입니다.
- NPS 또는 원격 데스크톱 연결에 대 한 NPS MMC 스냅인, NPS 용 Netsh 명령은, Windows PowerShell 명령을 사용 하 여 원격 NPS 합니다.
- NPS MMC 또는 Windows PowerShell과 같은 다른 도구와 함께에서 원격 데스크톱 연결을 사용 하 여 원격 워크스테이션에서.

>[!NOTE]
>Windows Server 2016에서 NPS 콘솔을 사용 하 여 로컬 NPS를 관리할 수 있습니다. 원격 및 로컬 NPSs를 관리 하려면 NPS MMC 스냅인을 사용 해야\-에서 합니다.

다음 섹션에서는 로컬 및 원격 NPSs 프로그램을 관리 하는 방법에 지침을 제공 합니다.

## <a name="configure-the-local-nps-by-using-the-nps-console"></a>NPS 콘솔을 사용 하 여 로컬 NPS를 구성

NPS를 설치한 후에 NPS MMC를 사용 하 여 로컬 NPS를 관리 하려면이 절차를 사용할 수 있습니다.

**관리자 자격 증명** 

이 절차를 완료 하려면 Administrators 그룹의 멤버 여야 합니다.

### <a name="to-configure-the-local-nps-by-using-the-nps-console"></a>NPS 콘솔을 사용 하 여 로컬 NPS를 구성 하려면

1. 서버 관리자에서 클릭 **도구**, 를 클릭 하 고 **네트워크 정책 서버**합니다. NPS 콘솔이 열립니다.

2. NPS 콘솔에서 클릭 NPS \(로컬\)합니다. 세부 정보 창에서 하나를 선택 **표준 구성** 또는 **고급 구성**, 다음 선택 항목에 따라 다음 중 하나를 수행 합니다.
    - 선택 하면 **표준 구성**시나리오 목록에서 선택 하 고 구성 마법사를 시작 하 고 지침을 따릅니다.
    - 선택 하면 **고급 구성**를 확장 하 고 화살표를 클릭 **고급 구성 옵션**, 차례로 검토 하 고 원하는-NPS 기능에 따라 사용 가능한 옵션 구성 RADIUS 서버, RADIUS 프록시 또는 둘 다입니다.

## <a name="manage-multiple-npss-by-using-the-nps-mmc-snap-in"></a>NPS MMC 스냅인을 사용 하 여 여러 NPSs 관리\-에서

이 절차를 사용 하 여 NPS MMC 스냅인을 사용 하 여 로컬 NPS 및 원격 NPSs 여러 관리 하\-에서 합니다.

다음 절차를 수행 하기 전에 컴퓨터의 로컬 및 원격 컴퓨터에 NPS를 설치 해야 합니다.

NPS MMC 스냅인을 사용 하 여 관리 하는 네트워크 상태 및 NPSs 수에 따라\-MMC 스냅인의 응답에서\-의 속도가 느려질 수 있습니다. 또한 NPS 구성 트래픽은 보내집니다 네트워크를 통해 원격 관리 세션 중 NPS 스냅인을 사용 하 여\-에서 합니다. 네트워크를 물리적으로 안전 하 고 악의적인 사용자가이 네트워크 트래픽에 대 한 액세스 없는 확인 합니다.

**관리자 자격 증명** 

이 절차를 완료 하려면 Administrators 그룹의 멤버 여야 합니다.

### <a name="to-manage-multiple-npss-by-using-the-nps-snap-in"></a>NPS 스냅인을 사용 하 여 여러 NPSs를 관리할\-에서

1. MMC를 열려면 관리자 권한으로 Windows PowerShell을 실행 합니다. Windows PowerShell에서 입력 **mmc**, 한 다음 ENTER를 누릅니다. Microsoft Management Console이 열립니다.
2. Mmc에서에 **파일** 메뉴에서 클릭 **추가/제거 스냅인\-에서**합니다. 합니다 **스냅인 추가 / 제거\-기능** 대화 상자가 열립니다.
3. **스냅인 추가 / 제거\-기능**의 **사용 가능한 스냅인\-기능**목록 아래로 스크롤하여, 클릭 **네트워크 정책 서버**, 클릭및 **추가**합니다. **컴퓨터 선택** 대화 상자가 열립니다.
4. **컴퓨터 선택**를 확인 하는 **로컬 컴퓨터 \(이 콘솔이 실행 되는 컴퓨터\)**  를 선택한 다음 클릭 **확인**합니다. 스냅인\-로컬 nps에 추가 됩니다 목록 **선택한 스냅인\-기능**합니다.
5. **스냅인 추가 / 제거\-기능**의 **사용 가능한 스냅인\-기능**, 되도록 **네트워크 정책 서버** 는 여전히을 선택한 다음 클릭  **추가**합니다. 합니다 **컴퓨터 선택** 대화 상자가 다시 열립니다.
6. **컴퓨터 선택**, 클릭 **다른 컴퓨터로**, IP 주소 또는 정규화 된 도메인 이름을 입력 합니다 \(FQDN\) NPS를 사용 하 여 관리 하려는 원격 NPS의 맞춤\-에서 합니다. 필요에 따라 눌러도 **찾아보기** 을 추가 하려는 컴퓨터에 대 한 디렉터리입니다. **확인**을 클릭합니다.
7. 자세한 NPSs NPS 스냅인에 추가할 5-6 단계를 반복\-에서 합니다. 관리 하려는 모든 NPSs 추가 했으면 **확인**합니다.
8. 나중에 사용할 NPS 스냅인을 저장 하려면 클릭 **파일**를 클릭 하 고 **저장**합니다. 에 **다른 이름으로 저장** 대화 상자에서 파일을 저장 하려는 하드 디스크 위치에 Microsoft Management Console에 대 한 이름을 입력 \(.msc\) 파일을 선택한 다음 클릭 **저장**. 

## <a name="manage-an-nps-by-using-remote-desktop-connection"></a>원격 데스크톱 연결을 사용 하 여 NPS 관리

원격 데스크톱 연결을 사용 하 여 원격 NPS를 관리 하려면이 절차를 사용할 수 있습니다.

원격 데스크톱 연결을 사용 하 여 Windows Server 2016을 실행 하 여 NPSs를 원격으로 관리할 수 있습니다. Windows 10 또는 Windows 클라이언트 운영 체제를 실행 하는 컴퓨터에서 NPSs를 원격으로 관리할 수 있습니다.

두 가지 방법 중 하나를 사용 하 여 여러 NPSs를 관리 하려면 원격 데스크톱 연결을 사용할 수 있습니다.

1. 개별적으로 각 프로그램 NPSs에 원격 데스크톱 연결을 만듭니다.
2. 원격 데스크톱을 사용 하 여 하나의 NPS에 연결할 하 고 다른 원격 서버 관리 하려면 해당 서버의 NPS MMC를 사용 합니다. 자세한 내용은 이전 섹션을 참조 하세요 **NPS MMC 스냅인을 사용 하 여 여러 NPSs 관리할\-에서**합니다.

**관리자 자격 증명** 

이 절차를 완료 하려면 NPS에서 Administrators 그룹의 멤버 여야 합니다.

### <a name="to-manage-an-nps-by-using-remote-desktop-connection"></a>원격 데스크톱 연결을 사용 하 여 NPS 관리

1. 서버 관리자에서 원격으로 관리 하려는 각 NPS에서 선택 **로컬 서버**합니다. 서버 관리자 세부 정보 창에서 보기를 **원격 데스크톱** 설정 및 다음 중 하나를 수행 합니다. 
    1. 경우 값을 **원격 데스크톱** 설정은 **Enabled**,이 절차의 단계 중 일부를 수행할 필요가 없습니다. 원격 데스크톱 사용자 사용 권한을 구성 하려면 4 단계를 건너뛸 합니다.
    2. 경우는 **원격 데스크톱** 설정은 **사용 안 함**, 이라는 단어를 클릭 **비활성**합니다. 합니다 **시스템 속성** 대화 상자가 열리고 합니다 **원격** 탭 합니다.
2. **원격 데스크톱**, 클릭 **이 컴퓨터에 원격 연결 허용**합니다. 합니다 **원격 데스크톱 연결** 대화 상자가 열립니다. 다음 중 하나를 수행합니다.
    1. 허용 되는 네트워크 연결을 사용자 지정 하려면 클릭 **Windows Firewall with Advanced Security**를 허용 하려는 설정을 구성 합니다. 
    2. 모든 네트워크 컴퓨터에서 연결에 대 한 원격 데스크톱 연결을 사용 하려면 **확인**합니다.
3. **시스템 속성**의 **원격 데스크톱**를 사용할지 여부를 결정할 **네트워크수준인증을사용하여원격데스크톱을실행하는컴퓨터에서만에서연결허용**를 선택 하 고 있습니다.
4. 클릭 **사용자 선택**합니다. 합니다 **Remote Desktop Users** 대화 상자가 열립니다.
5. **Remote Desktop Users**, 클릭에 NPS를 원격으로 연결할 사용자 권한을 부여 하기 **추가**, 사용자의 계정에 대 한 사용자 이름을 입력 합니다. **확인**을 클릭합니다.
6. NPS로 원격 액세스 권한을 부여 하려는 각 사용자에 대해 5 단계를 반복 합니다. 추가 사용자 작업이 완료 되 면 **확인** 닫으려면 합니다 **Remote Desktop Users** 대화 상자 및 **확인** 를 다시는 **시스템 속성**대화 상자.
7. 이전 단계를 사용 하 여 구성 된 원격 NPS에 연결 하려면 클릭 **시작**사전순 목록 아래로 스크롤하여을 클릭 한 다음 **Windows Accessories**를 클릭 하 고 **원격 데스크톱 연결**합니다. 합니다 **원격 데스크톱 연결** 대화 상자가 열립니다.
8. 에 **원격 데스크톱 연결** 대화 상자의 **컴퓨터**, NPS 이름 또는 IP 주소를 입력 합니다. 원하는 경우 클릭 **옵션**에서 추가 연결 옵션을 구성 하 고 클릭 **저장** 반복 해 서 사용에 대 한 연결을 저장 합니다.
9. 클릭 **Connect**, 메시지가 표시 되 면 및에 로그온 하 고 NPS를 구성 하는 권한이 있는 계정의 사용자 계정 자격 증명을 제공 합니다.

## <a name="use-netsh-nps-commands-to-manage-an-nps"></a>Netsh NPS 명령을 사용 하 여 NPS 관리

표시 하 고 계정 및 둘 다 NPS 및 원격 액세스 서비스에서 사용 되는 데이터베이스 감사는 인증, 권한 부여의 구성을 설정 명령은 Netsh NPS 컨텍스트에서 사용할 수 있습니다. Netsh NPS 컨텍스트에서 사용 하 여 명령:

- 구성 하거나 Windows 인터페이스에서 NPS 콘솔을 사용 하 여도 구성에 사용할 수 있는 NPS의 모든 측면을 포함 하는 NPS를 다시 구성 합니다.
- Netsh 스크립트로 NPS 구성과 레지스트리 키를 포함 하 여 NPS (원본 서버)를 저장 한 구성을 내보냅니다.
- 원본 NPS에서에서 Netsh 스크립트 및 내보낸된 구성 파일을 사용 하 여 다른 NPS 구성을 가져와야 합니다.

Windows Server 2016 명령 프롬프트에서 또는 Windows PowerShell에서 다음이 명령을 실행할 수 있습니다. 또한 배치 파일과 스크립트에서 netsh nps 명령을 실행할 수 있습니다.

**관리자 자격 증명** 

이 절차를 수행하려면 로컬 컴퓨터에서 Administrators 그룹의 구성원이어야 합니다.

### <a name="to-enter-the-netsh-nps-context-on-an-nps"></a>Netsh NPS 컨텍스트에서 NPS에서 입력

1. 명령 프롬프트 또는 Windows PowerShell을 엽니다.
2. 형식 **netsh**, 한 다음 ENTER를 누릅니다.
3. 형식 **nps**, 한 다음 ENTER를 누릅니다.
4. 사용 가능한 명령 목록을 보려면, 물음표 \(?\) ENTER 키를 누릅니다.


Netsh NPS 명령에 대 한 자세한 내용은 참조 하십시오 [Windows Server 2008에서 네트워크 정책 서버용 Netsh 명령](https://technet.microsoft.com/library/cc754428(v=ws.10).aspx), 또는 전체를 다운로드 [Netsh 기술 참조](https://gallery.technet.microsoft.com/Netsh-Technical-Reference-c46523dc?redir=0) TechNet 갤러리에서. 이 다운로드는 전체 네트워크 셸 기술 참조에 대 한 Windows Server 2008 및 Windows Server 2008 R2는입니다. 형식은 Windows 도움말 \(*.chm\) zip 파일에 있습니다. 이러한 명령은 Windows Server 2016 및 Windows 10에서 계속 제공 되므로 netsh 이러한 환경에서는 사용할 수 있지만 Windows PowerShell을 사용 하는 것이 좋습니다.

## <a name="use-windows-powershell-to-manage-npss"></a>Windows PowerShell을 사용 하 여 NPSs 관리

NPSs를 관리 하려면 Windows PowerShell 명령을 사용할 수 있습니다. 자세한 내용은 다음 Windows PowerShell 명령 참조 항목을 참조 하세요.

- [네트워크 정책 (NPS) 서버 Cmdlet Windows PowerShell에서](https://technet.microsoft.com/library/jj872739(v=wps.630).aspx)합니다. 이 netsh 명령은 Windows Server 2012 R2 또는 이후 운영 체제에서 사용할 수 있습니다.
- [NPS 모듈](https://technet.microsoft.com/itpro/powershell/windows/nps/index)합니다. 이 netsh 명령은 Windows Server 2016에서 사용할 수 있습니다.

NPS 관리에 대 한 자세한 내용은 참조 하세요. [관리 서버 NPS (네트워크 정책)](nps-manage-top.md)합니다.
