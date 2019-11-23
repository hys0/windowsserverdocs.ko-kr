---
title: 네임스페이스 형식 선택
description: 이 문서에서는 네임스페이스 형식을 선택하는 방법을 설명합니다.
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: becaab1b4c35492200ad3d75d5f31829d85e10f8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402195"
---
# <a name="choose-a-namespace-type"></a>네임스페이스 형식 선택

> 적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

네임스페이스를 만들 때 두 네임스페이스 형식인 독립형 네임스페이스와 도메인 기반 네임스페이스 중 하나를 선택해야 합니다. 또한 도메인 기반 네임 스페이스를 선택 하는 경우에는 Windows 2000 서버 모드 또는 Windows Server 2008 모드의 네임 스페이스 모드를 선택 해야 합니다.

## <a name="choosing-a-namespace-type"></a>네임스페이스 형식 선택

다음 조건 중 하나라도 환경에 해당하는 경우 독립형 네임스페이스를 선택합니다.

-   조직에서 Active Directory Domain Services (AD DS)를 사용 하지 않습니다.
-   장애 조치(failover) 클러스터를 사용하여 네임스페이스의 가용성을 높일 수 있습니다.
-   이 항목의 뒷부분에서 설명 하는 도메인 기반 네임 스페이스 (Windows Server 2008 모드)에 대 한 요구 사항을 충족 하지 않는 도메인에서 5000 개 이상의 DFS 폴더를 사용 하 여 단일 네임 스페이스를 만들어야 합니다.

> [!NOTE]
> 네임스페이스의 크기를 확인하려면 DFS 관리 콘솔 트리에서 네임스페이스를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭한 다음 **네임스페이스 속성** 대화 상자에서 네임스페이스 크기를 봅니다. DFS 네임스페이스 확장성에 대한 자세한 내용은 Microsoft 웹 사이트 [File Services](https://technet.microsoft.com/library/cc771548.aspx)를 참조하세요.

다음 조건 중 하나라도 환경에 해당하는 경우 도메인 기반 네임스페이스를 선택합니다.

-   여러 네임스페이스 서버를 사용하여 네임스페이스의 가용성을 보장할 수 있습니다.
-   사용자에게서 네임스페이스 서버의 이름을 숨길 수 있습니다. 그러면 더 쉽게 네임스페이스 서버를 바꾸거나 네임스페이스를 다른 서버로 마이그레이션할 수 있습니다.

## <a name="choosing-a-domain-based-namespace-mode"></a>도메인 기반 네임스페이스 모드 선택

도메인 기반 네임 스페이스를 선택 하는 경우 Windows 2000 서버 모드를 사용할지 아니면 Windows Server 2008 모드를 사용할지를 선택 해야 합니다. Windows Server 2008 모드에는 액세스 기반 열거 및 향상 된 확장성에 대 한 지원이 포함 되어 있습니다. 이제 Windows 2000 서버에 도입 된 도메인 기반 네임 스페이스를 "도메인 기반 네임 스페이스 (Windows 2000 서버 모드)" 라고 합니다.

Windows Server 2008 모드를 사용 하려면 도메인 및 네임 스페이스가 다음 최소 요구 사항을 충족 해야 합니다.

-   포리스트에서 Windows Server 2003 이상의 포리스트 기능 수준을 사용합니다.
-   도메인은 Windows Server 2008 이상 도메인 기능 수준을 사용 합니다.
-   모든 네임 스페이스 서버는 Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 또는 Windows Server 2008을 실행 합니다.

환경에서 지원 되는 경우 새 도메인 기반 네임 스페이스를 만들 때 Windows Server 2008 모드를 선택 합니다. 이 모드는 추가 기능 및 확장성을 제공 하 고 Windows 2000 서버 모드에서 네임 스페이스를 마이그레이션할 필요가 없습니다.

네임 스페이스를 Windows Server 2008 모드로 마이그레이션하는 방법에 대 한 자세한 내용은 [Windows server 2008 모드로 도메인 기반 네임 스페이스 마이그레이션](migrate-a-domain-based-namespace-to-windows-server-2008-mode.md)을 참조 하세요.

사용자 환경에서 Windows Server 2008 모드의 도메인 기반 네임 스페이스를 지원 하지 않는 경우 네임 스페이스에 대 한 기존 Windows 2000 서버 모드를 사용 합니다.

## <a name="comparing-namespace-types-and-modes"></a>네임스페이스 형식 및 모드 비교

각 네임스페이스 형식과 모드의 특징이 아래 표에 설명되어 있습니다.

|특징|독립형 네임스페이스|도메인 기반 네임스페이스(Windows 2000 Server 모드) |도메인 기반 네임스페이스(Windows Server 2008 모드) | 
|---|---|---|---|
|네임스페이스 경로|\\\ *ServerName\RootName* |\\\ *NetBIOSDomainName\RootName* <br />\\\ *DNSDomainName\RootName*|\\\ *NetBIOSDomainName\RootName* <br /> \\\ *DNSDomainName\RootName*|
|네임스페이스 정보 저장소 위치|레지스트리와 네임스페이스 서버의 메모리 캐시|AD DS와 각 네임스페이스 서버의 메모리 캐시|AD DS와 각 네임스페이스 서버의 메모리 캐시|
|네임스페이스 크기 권장 사항|네임스페이스에 대상을 가진 폴더가 5,000개 이상 포함될 수 있습니다. 권장되는 제한은 대상을 가진 폴더 50,000개입니다.|Windows Server 2008을 실행하지 않는 도메인 컨트롤러와의 호환성 유지를 위해 AD DS의 네임스페이스 개체 크기는 5MB 미만이어야 합니다. 이는 대상을 가진 폴더 약 5,000개 이하를 의미합니다.|네임스페이스에 대상을 가진 폴더가 5,000개 이상 포함될 수 있습니다. 권장되는 제한은 대상을 가진 폴더 50,000개입니다. |
|최소 AD DS 포리스트 기능 수준|AD DS 불필요|Windows 2000|Windows Server 2003|
|최소 AD DS 도메인 기능 수준|AD DS 불필요|Windows 2000 혼합|Windows Server 2008|
|지원되는 최소 네임스페이스 서버|Windows 2000 Server|Windows 2000 Server|Windows Server 2008|
|액세스 기반 열거 지원(사용하도록 설정된 경우)|예, Windows Server 2008 네임스페이스 서버 필요|아니요|예|
|지원되는 네임스페이스 가용성 보장 방법|장애 조치(Failover) 클러스터에 독립형 네임스페이스를 만듭니다.|여러 네임스페이스 서버를 사용하여 네임스페이스를 호스팅합니다. (네임스페이스가 동일한 도메인에 있어야 함)|여러 네임스페이스 서버를 사용하여 네임스페이스를 호스팅합니다. (네임스페이스가 동일한 도메인에 있어야 함)|
|DFS 복제를 사용하여 폴더 대상 복제 지원|AD DS 도메인 가입 시 지원됨|지원함|지원함|

## <a name="see-also"></a>참고 항목

-   [DFS 네임스페이스 배포](deploying-dfs-namespaces.md)
-   [도메인 기반 네임스페이스를 Windows Server 2008 모드로 마이그레이션](migrate-a-domain-based-namespace-to-windows-server-2008-mode.md)


