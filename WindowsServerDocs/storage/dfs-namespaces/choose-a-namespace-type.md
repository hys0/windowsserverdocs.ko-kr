---
title: 네임스페이스 형식 선택
description: 이 문서에서는 네임 스페이스 유형을 선택 하는 방법을 설명 합니다.
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: b4addd18629bd54cd9d5fc2df5c660c621e735de
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85473790"
---
# <a name="choose-a-namespace-type"></a>네임 스페이스 유형 선택

> 적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

네임 스페이스를 만들 때 독립 실행형 네임 스페이스 또는 도메인 기반 네임 스페이스 중 하나를 선택 해야 합니다. 또한 도메인 기반 네임 스페이스를 선택 하는 경우에는 Windows 2000 서버 모드 또는 Windows Server 2008 모드의 네임 스페이스 모드를 선택 해야 합니다.

## <a name="choosing-a-namespace-type"></a>네임 스페이스 유형 선택

다음 조건 중 하나라도 해당 환경에 적용 되는 경우 독립 실행형 네임 스페이스를 선택 합니다.

-   조직에서 Active Directory Domain Services (AD DS)를 사용 하지 않습니다.
-   장애 조치 (failover) 클러스터를 사용 하 여 네임 스페이스의 가용성을 높이 려 고 합니다.
-   이 항목의 뒷부분에서 설명 하는 도메인 기반 네임 스페이스 (Windows Server 2008 모드)에 대 한 요구 사항을 충족 하지 않는 도메인에서 5000 개 이상의 DFS 폴더를 사용 하 여 단일 네임 스페이스를 만들어야 합니다.

> [!NOTE]
> 네임 스페이스의 크기를 확인 하려면 DFS 관리 콘솔 트리에서 네임 스페이스를 마우스 오른쪽 단추로 클릭 하 고 **속성**을 클릭 한 다음 **네임 스페이스 속성** 대화 상자에서 네임 스페이스 크기를 확인 합니다. DFS 네임 스페이스 확장성에 대 한 자세한 내용은 Microsoft 웹 사이트 [파일 서비스](https://technet.microsoft.com/library/cc771548.aspx)를 참조 하세요.

다음 조건 중 하나라도 해당 환경에 적용 되는 경우 도메인 기반 네임 스페이스를 선택 합니다.

-   여러 네임 스페이스 서버를 사용 하 여 네임 스페이스의 가용성을 보장 하려고 합니다.
-   사용자의 네임 스페이스 서버 이름을 숨기려는 경우 이렇게 하면 네임 스페이스 서버를 쉽게 대체 하거나 네임 스페이스를 다른 서버로 마이그레이션할 수 있습니다.

## <a name="choosing-a-domain-based-namespace-mode"></a>도메인 기반 네임 스페이스 모드 선택

도메인 기반 네임 스페이스를 선택 하는 경우 Windows 2000 서버 모드를 사용할지 아니면 Windows Server 2008 모드를 사용할지를 선택 해야 합니다. Windows Server 2008 모드에는 액세스 기반 열거 및 향상 된 확장성에 대 한 지원이 포함 되어 있습니다. 이제 Windows 2000 서버에 도입 된 도메인 기반 네임 스페이스를 "도메인 기반 네임 스페이스 (Windows 2000 서버 모드)" 라고 합니다.

Windows Server 2008 모드를 사용 하려면 도메인 및 네임 스페이스가 다음 최소 요구 사항을 충족 해야 합니다.

-   포리스트는 Windows Server 2003 이상 포리스트 기능 수준을 사용 합니다.
-   도메인은 Windows Server 2008 이상 도메인 기능 수준을 사용 합니다.
-   모든 네임 스페이스 서버는 Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 또는 Windows Server 2008을 실행 합니다.

환경에서 지원 되는 경우 새 도메인 기반 네임 스페이스를 만들 때 Windows Server 2008 모드를 선택 합니다. 이 모드는 추가 기능 및 확장성을 제공 하 고 Windows 2000 서버 모드에서 네임 스페이스를 마이그레이션할 필요가 없습니다.

네임 스페이스를 Windows Server 2008 모드로 마이그레이션하는 방법에 대 한 자세한 내용은 [Windows server 2008 모드로 도메인 기반 네임 스페이스 마이그레이션](migrate-a-domain-based-namespace-to-windows-server-2008-mode.md)을 참조 하세요.

사용자 환경에서 Windows Server 2008 모드의 도메인 기반 네임 스페이스를 지원 하지 않는 경우 네임 스페이스에 대 한 기존 Windows 2000 서버 모드를 사용 합니다.

## <a name="comparing-namespace-types-and-modes"></a>네임 스페이스 형식 및 모드 비교

각 네임 스페이스 형식 및 모드의 특성은 다음 표에 설명 되어 있습니다.

|특성|독립 실행형 네임 스페이스|도메인 기반 네임 스페이스 (Windows 2000 서버 모드) |도메인 기반 네임 스페이스 (Windows Server 2008 모드) |
|---|---|---|---|
|네임 스페이스 경로|\\\ *ServerName\RootName* |\\\ *NetBIOSDomainName\RootName* <br />\\\ *DNSDomainName\RootName*|\\\ *NetBIOSDomainName\RootName* <br /> \\\ *DNSDomainName\RootName*|
|네임 스페이스 정보 저장소 위치|레지스트리 및 네임 스페이스 서버의 메모리 캐시|각 네임 스페이스 서버의 메모리 캐시 및 AD DS|각 네임 스페이스 서버의 메모리 캐시 및 AD DS|
|네임 스페이스 크기 권장 사항|네임 스페이스에는 대상이 인 5000 개 이상의 폴더가 포함 될 수 있습니다. 권장 제한은 대상이 있는 5만 폴더입니다.|Windows Server 2008를 실행 하 고 있지 않은 도메인 컨트롤러와의 호환성을 유지 하려면 AD DS의 네임 스페이스 개체 크기가 5mb 미만 이어야 합니다. 즉, 대상이 인 약 5000 개의 폴더가 있습니다.|네임 스페이스에는 대상이 인 5000 개 이상의 폴더가 포함 될 수 있습니다. 권장 제한은 대상이 있는 5만 폴더입니다. |
|최소 AD DS 포리스트 기능 수준|AD DS 필요 하지 않음|Windows 2000|Windows Server 2003|
|최소 AD DS 도메인 기능 수준|AD DS 필요 하지 않음|Windows 2000 혼합|Windows Server 2008|
|지원 되는 최소 네임 스페이스 서버|Windows 2000 Server|Windows 2000 Server|Windows Server 2008|
|액세스 기반 열거 지원 (사용 되는 경우)|예, Windows Server 2008 네임 스페이스 서버가 필요 합니다.|아니요|예|
|네임 스페이스 가용성을 보장 하는 지원 되는 메서드|장애 조치 (failover) 클러스터에 독립 실행형 네임 스페이스를 만듭니다.|여러 네임 스페이스 서버를 사용 하 여 네임 스페이스를 호스팅합니다. 네임 스페이스 서버는 동일한 도메인에 있어야 합니다.|여러 네임 스페이스 서버를 사용 하 여 네임 스페이스를 호스팅합니다. 네임 스페이스 서버는 동일한 도메인에 있어야 합니다.|
|DFS 복제를 사용 하 여 폴더 대상을 복제할 수 있도록 지원|AD DS 도메인에 가입 된 경우 지원 됨|지원됨|지원됨|

## <a name="additional-references"></a>추가 참조

-   [DFS 네임스페이스 배포](deploying-dfs-namespaces.md)
-   [도메인 기반 네임스페이스를 Windows Server 2008 모드로 마이그레이션](migrate-a-domain-based-namespace-to-windows-server-2008-mode.md)


