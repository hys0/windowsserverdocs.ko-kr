---
title: 관리 도구를 사용하여 네트워크 정책 서버 관리
description: 이 항목을 사용 하 여 Windows Server 2016에서 네트워크 정책 서버를 관리 하는 데 사용할 수 있는 도구에 대해 알아볼 수 있습니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 5de80dc0-53be-42b7-8e5b-24d213bf2b25
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 527fbf52d68f36d198068514476868bcba930a68
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71396454"
---
# <a name="network-policy-server-management-with-administration-tools"></a>관리 도구를 사용하여 네트워크 정책 서버 관리

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목을 사용 하 여 NPSs를 관리 하는 데 사용할 수 있는 도구에 대해 알아볼 수 있습니다.

NPS를 설치한 후 NPSs를 관리할 수 있습니다.

- 로컬에서 NPS Microsoft Management Console \(MMC @ no__t 스냅인, 관리 도구의 정적 NPS 콘솔, Windows PowerShell 명령 또는 NPS에 대 한 네트워크 셸 \(Netsh @ no__t-3 명령을 사용 합니다.
- Nps MMC 스냅인, nps에 대 한 Netsh 명령, NPS 용 Windows PowerShell 명령 또는 원격 데스크톱 연결를 사용 하 여 원격 NPS를 사용 합니다.
- 원격 워크스테이션에서 원격 데스크톱 연결를 사용 하 여 NPS MMC 또는 Windows PowerShell과 같은 다른 도구와 함께 사용 합니다.

>[!NOTE]
>Windows Server 2016에서는 NPS 콘솔을 사용 하 여 로컬 NPS를 관리할 수 있습니다. 원격 및 로컬 NPSs를 모두 관리 하려면 NPS MMC snap @ no__t-0in을 사용 해야 합니다.

다음 섹션에서는 로컬 및 원격 NPSs를 관리 하는 방법에 대 한 지침을 제공 합니다.

## <a name="configure-the-local-nps-by-using-the-nps-console"></a>NPS 콘솔을 사용 하 여 로컬 NPS 구성

NPS를 설치한 후에는이 절차를 사용 하 여 NPS MMC를 통해 로컬 NPS를 관리할 수 있습니다.

**관리 자격 증명** 

이 절차를 완료 하려면 Administrators 그룹의 멤버 여야 합니다.

### <a name="to-configure-the-local-nps-by-using-the-nps-console"></a>NPS 콘솔을 사용 하 여 로컬 NPS를 구성 하려면

1. 서버 관리자에서 클릭 **도구**, 를 클릭 하 고 **네트워크 정책 서버**합니다. NPS 콘솔이 열립니다.

2. NPS 콘솔에서 NPS \(Local @ no__t-1을 클릭 합니다. 세부 정보 창에서 **표준 구성** 또는 **고급 구성**을 선택 하 고 선택 사항에 따라 다음 중 하나를 수행 합니다.
    - **표준 구성**을 선택 하는 경우 목록에서 시나리오를 선택 하 고 지침에 따라 구성 마법사를 시작 합니다.
    - **고급 구성**을 선택 하는 경우 화살표를 클릭 하 여 **고급 구성 옵션**을 확장 한 다음 원하는 NPS 기능 (radius 서버, radius 프록시 또는 둘 다)을 기반으로 사용 가능한 옵션을 검토 하 고 구성 합니다.

## <a name="manage-multiple-npss-by-using-the-nps-mmc-snap-in"></a>NPS MMC Snap @ no__t-0in을 사용 하 여 여러 NPSs 관리

이 절차를 사용 하 여 NPS MMC snap @ no__t-0in을 사용 하 여 로컬 NPS 및 여러 원격 NPSs를 관리할 수 있습니다.

아래 절차를 수행 하기 전에 로컬 컴퓨터와 원격 컴퓨터에 NPS를 설치 해야 합니다.

네트워크 조건 및 NPS MMC snap @ no__t-0in을 사용 하 여 관리 하는 NPSs의 수에 따라 MMC snap @ no__t-1in의 응답이 느릴 수 있습니다. 또한 nps 구성 트래픽은 원격 관리 세션 중에 NPS snap @ no__t-0in을 사용 하 여 네트워크를 통해 전송 됩니다. 네트워크가 물리적으로 안전 하 고 악의적인 사용자가이 네트워크 트래픽에 액세스할 수 없는지 확인 합니다.

**관리 자격 증명** 

이 절차를 완료 하려면 Administrators 그룹의 멤버 여야 합니다.

### <a name="to-manage-multiple-npss-by-using-the-nps-snap-in"></a>NPS snap @ no__t-0in을 사용 하 여 여러 NPSs를 관리 하려면

1. MMC를 열려면 관리자 권한으로 Windows PowerShell을 실행 합니다. Windows PowerShell에서 **mmc**를 입력 한 다음 enter 키를 누릅니다. Microsoft Management Console이 열립니다.
2. MMC의 **파일** 메뉴에서 **추가/제거 Snap @ no__t-2in**을 클릭 합니다. **Add 또는 Remove Snap @ no__t-1ins** 대화 상자가 열립니다.
3. **Add 또는 Remove snap @ no__t-1**. **사용 가능한 snap @ no__t-3ins**에서 목록을 아래로 스크롤하고 **네트워크 정책 서버**를 클릭 한 다음 **추가**를 클릭 합니다. **컴퓨터 선택** 대화 상자가 열립니다.
4. **컴퓨터 선택**에서 **이 콘솔이 실행 되 고 있는 컴퓨터의 로컬 컴퓨터 \(** 가 선택 되어 있는지 확인 한 다음 **확인**을 클릭 합니다. 로컬 NPS에 대 한 snap @ no__t-0in이 **선택한 snap @ no__t-2 ins**의 목록에 추가 됩니다.
5. **Add 또는 Remove snap @ no__t-1ins**에서 **Available snap @ no__t-3Ins**에서 **네트워크 정책 서버** 가 선택 되어 있는지 확인 한 다음 **추가**를 클릭 합니다. **컴퓨터 선택** 대화 상자가 다시 열립니다.
6. **컴퓨터 선택**에서 **다른 컴퓨터**를 클릭 한 후 nps snap @ no__t-4in을 사용 하 여 관리 하려는 원격 NPS의 IP 주소 또는 정규화 된 도메인 이름 \(fqdn @ no__t-3을 입력 합니다. 원하는 경우 **찾아보기** 를 클릭 하 여 추가할 컴퓨터의 디렉터리를 정독 수 있습니다. **확인**을 클릭합니다.
7. 5 단계와 6 단계를 반복 하 여 NPSs를 NPS snap @ no__t-0in에 추가 합니다. 관리 하려는 모든 NPSs를 추가 했으면 **확인**을 클릭 합니다.
8. 나중에 사용할 수 있도록 NPS 스냅인을 저장 하려면 **파일**을 클릭 한 다음 **저장**을 클릭 합니다. 다른 이름 **으로 저장** 대화 상자에서 파일을 저장 하려는 하드 디스크 위치를 찾아 Microsoft Management Console @no__t -1 @ no__t 파일에 대 한 이름을 입력 한 다음 **저장**을 클릭 합니다. 

## <a name="manage-an-nps-by-using-remote-desktop-connection"></a>원격 데스크톱 연결를 사용 하 여 NPS 관리

원격 데스크톱 연결를 사용 하 여 원격 NPS를 관리 하려면이 절차를 사용할 수 있습니다.

원격 데스크톱 연결를 사용 하 여 Windows Server 2016를 실행 하는 NPSs를 원격으로 관리할 수 있습니다. Windows 10 또는 이전 버전의 Windows 클라이언트 운영 체제를 실행 하는 컴퓨터에서 NPSs를 원격으로 관리할 수도 있습니다.

두 가지 방법 중 하나를 사용 하 여 원격 데스크톱 연결을 사용 하 여 여러 NPSs를 관리할 수 있습니다.

1. 각 NPSs에 개별적으로 원격 데스크톱 연결을 만듭니다.
2. 원격 데스크톱을 사용 하 여 하나의 NPS에 연결한 다음 해당 서버의 NPS MMC를 사용 하 여 다른 원격 서버를 관리 합니다. 자세한 내용은 이전 섹션인 **NPS MMC Snap @ no__t-1in를 사용 하 여 여러 NPSs 관리**를 참조 하세요.

**관리 자격 증명** 

이 절차를 완료 하려면 NPS에서 Administrators 그룹의 구성원 이어야 합니다.

### <a name="to-manage-an-nps-by-using-remote-desktop-connection"></a>원격 데스크톱 연결를 사용 하 여 NPS를 관리 하려면

1. 원격으로 관리 하려는 각 NPS의 서버 관리자에서 **로컬 서버**를 선택 합니다. 서버 관리자 세부 정보 창에서 **원격 데스크톱** 설정을 확인 하 고 다음 중 하나를 수행 합니다. 
    1. **원격 데스크톱** 설정 값을 **사용**하는 경우이 절차의 일부 단계를 수행할 필요가 없습니다. 4 단계로 건너뛰어 원격 데스크톱 사용자 권한 구성을 시작 합니다.
    2. **원격 데스크톱** 설정을 **사용 하지**않는 경우 **사용 안 함**이라는 단어를 클릭 합니다. **시스템 속성** 대화 상자가 **원격** 탭에서 열립니다.
2. **원격 데스크톱**에서 **이 컴퓨터에 대 한 원격 연결 허용**을 클릭 합니다. **원격 데스크톱 연결** 대화 상자가 열립니다. 다음 중 하나를 수행합니다.
    1. 허용 되는 네트워크 연결을 사용자 지정 하려면 **고급 보안이 포함 된 Windows 방화벽**을 클릭 하 고 허용할 설정을 구성 합니다. 
    2. 컴퓨터의 모든 네트워크 연결에 대해 원격 데스크톱 연결을 사용 하도록 설정 하려면 **확인**을 클릭 합니다.
3. **시스템 속성**의 **원격 데스크톱**에서 **네트워크 수준 인증로 원격 데스크톱을 실행 하는 컴퓨터 에서만 연결 허용**을 사용 하도록 설정할지 여부를 결정 하 고 선택 합니다.
4. 클릭 **사용자 선택**합니다. **원격 데스크톱 사용자** 대화 상자가 열립니다.
5. **원격 데스크톱 사용자**에서 NPS에 원격으로 연결할 수 있는 권한을 사용자에 게 부여 하려면 **추가**를 클릭 한 다음 사용자 계정에 대 한 사용자 이름을 입력 합니다. **확인**을 클릭합니다.
6. NPS에 대 한 원격 액세스 권한을 부여 하려는 각 사용자에 대해 5 단계를 반복 합니다. 사용자 추가가 완료 되 면 **확인** 을 클릭 하 여 **원격 데스크톱 사용자** 대화 상자를 닫고 **확인** 을 다시 클릭 하 여 **시스템 속성** 대화 상자를 닫습니다.
7. 이전 단계를 사용 하 여 구성한 원격 NPS에 연결 하려면 **시작**을 클릭 하 고 사전순 목록을 스크롤한 다음 **Windows 보조 프로그램**을 클릭 하 고 **원격 데스크톱 연결**를 클릭 합니다. **원격 데스크톱 연결** 대화 상자가 열립니다.
8. **원격 데스크톱 연결** 대화 상자의 **컴퓨터**에 NPS 이름 또는 IP 주소를 입력 합니다. 원하는 경우 **옵션**을 클릭 하 고 추가 연결 옵션을 구성한 후 **저장** 을 클릭 하 여 반복 사용을 위해 연결을 저장 합니다.
9. **연결**을 클릭 하 고 메시지가 표시 되 면 로그인 하 여 NPS를 구성할 수 있는 권한이 있는 계정에 대 한 사용자 계정 자격 증명을 제공 합니다.

## <a name="use-netsh-nps-commands-to-manage-an-nps"></a>Netsh NPS 명령을 사용 하 여 NPS 관리

Netsh NPS 컨텍스트의 명령을 사용 하면 NPS 및 원격 액세스 서비스 둘 다에서 사용 되는 인증, 권한 부여, 계정 및 감사 데이터베이스의 구성을 표시 하 고 설정할 수 있습니다. Netsh NPS 컨텍스트의 명령을 사용 하 여 다음을 수행 합니다.

- Windows 인터페이스의 NPS 콘솔을 사용 하 여 구성에도 사용할 수 있는 NPS의 모든 측면을 포함 하 여 NPS를 구성 하거나 다시 구성 합니다.
- 레지스트리 키와 NPS 구성 저장소를 포함 하 여 한 NPS (원본 서버)의 구성을 Netsh 스크립트로 내보냅니다.
- Netsh 스크립트와 원본 NPS에서 내보낸 구성 파일을 사용 하 여 다른 NPS로 구성을 가져옵니다.

이러한 명령은 Windows Server 2016 명령 프롬프트 또는 Windows PowerShell에서 실행할 수 있습니다. 스크립트 및 배치 파일에서 netsh nps 명령을 실행할 수도 있습니다.

**관리 자격 증명** 

이 절차를 수행하려면 로컬 컴퓨터에서 Administrators 그룹의 구성원이어야 합니다.

### <a name="to-enter-the-netsh-nps-context-on-an-nps"></a>NPS에서 Netsh NPS 컨텍스트를 입력 하려면

1. 명령 프롬프트 또는 Windows PowerShell을 엽니다.
2. **Netsh**를 입력 하 고 enter 키를 누릅니다.
3. **Nps**를 입력 한 다음 enter 키를 누릅니다.
4. 사용 가능한 명령 목록을 보려면 물음표 \(? \)을 입력 하 고 ENTER 키를 누릅니다.


Netsh NPS 명령에 대 한 자세한 내용은 [Windows Server 2008의 네트워크 정책 서버용 Netsh 명령](https://technet.microsoft.com/library/cc754428(v=ws.10).aspx)또는 TechNet 갤러리에서 전체 [netsh 기술 참조](https://gallery.technet.microsoft.com/Netsh-Technical-Reference-c46523dc?redir=0) 다운로드를 참조 하세요. 이 다운로드는 Windows Server 2008 및 Windows Server 2008 r 2에 대 한 전체 네트워크 셸 기술 참조입니다. 형식은 zip 파일의 Windows 도움말 \( * .chm @ no__t-1입니다. 이러한 명령은 Windows Server 2016 및 Windows 10에 계속 제공 되므로 이러한 환경에서는 netsh를 사용할 수 있지만 Windows PowerShell을 사용 하는 것이 좋습니다.

## <a name="use-windows-powershell-to-manage-npss"></a>Windows PowerShell을 사용 하 여 NPSs 관리

Windows PowerShell 명령을 사용 하 여 NPSs를 관리할 수 있습니다. 자세한 내용은 다음 Windows PowerShell 명령 참조 항목을 참조 하세요.

- [Windows PowerShell의 NPS (네트워크 정책 서버) cmdlet](https://technet.microsoft.com/library/jj872739(v=wps.630).aspx). 이러한 netsh 명령은 Windows Server 2012 R2 이상 운영 체제에서 사용할 수 있습니다.
- [NPS 모듈](https://technet.microsoft.com/itpro/powershell/windows/nps/index). 이러한 netsh 명령은 Windows Server 2016에서 사용할 수 있습니다.

NPS 관리에 대 한 자세한 내용은 [nps (네트워크 정책 서버) 관리](nps-manage-top.md)를 참조 하세요.
