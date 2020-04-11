---
title: WSUS(Windows Server Update Services) 시작
description: WSUS(Windows Server Update Service) 항목 - 서버 역할 및 실제 애플리케이션 개요
ms.prod: windows-server
ms.technology: manage-wsus
ms.topic: get-started article
ms.assetid: 90e3464c-49d8-4861-96db-ee6f8a09ec5b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 5/22/2017
ms.openlocfilehash: 3bb365c627840d4152b0dc450e24dd83d82103ca
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80828636"
---
# <a name="windows-server-update-services-wsus"></a>WSUS(Windows Server Update Services)

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

WSUS(Windows Server Update Services)를 사용하면 정보 기술 관리자가 최신 Microsoft 제품 업데이트를 배포할 수 있습니다. WSUS 네트워크에 있는 컴퓨터에 Microsoft Update를 통해 릴리스되는 업데이트의 배포를 완벽 하 게 관리를 사용할 수 있습니다. 이 항목에서는 이 서버 역할에 대한 개요와 WSUS를 배포 및 관리하는 방법을 자세히 설명합니다.

## <a name="wsus-server-role-description"></a>WSUS 서버 역할 설명
WSUS 서버를 관리 하 고 관리 콘솔을 통해 업데이트를 배포 하는 데 사용할 수 있는 기능을 제공 합니다. WSUS 서버는 조직 내 다른 WSUS 서버의 업데이트 원본이 수도 있습니다. 업데이트 원본으로 사용되는 WSUS 서버를 업스트림 서버라고 합니다. WSUS 구현에서 하나 이상의 WSUS 서버를 네트워크에서 사용 가능한 업데이트 정보를 얻으려면 Microsoft 업데이트에 연결할 수 있어야 합니다. 관리자로 서 확인할 수 있습니다-네트워크 보안 및 구성-에 따라 다른 WSUS 서버의 수에 직접 연결 Microsoft Update.

### <a name="practical-applications"></a>유용한 팁
업데이트 관리란 프로덕션 환경으로 향하는 중간 소프트웨어 릴리스의 배포 및 유지 보수를 제어하는 프로세스입니다. 이 프로세스를 통해 보안 취약점을 극복하고 운영 효율성과 프로덕션 환경의 안정성을 유지 관리할 수 있습니다. 조직에서 해당 운영 체제 및 애플리케이션 소프트웨어 내에 알려진 트러스트 수준을 결정하고 유지 관리할 수 없는 경우 악용되면 수익과 지적 재산의 손실로 이어질 수 있는 여러 가지 보안 취약점이 발생할 수 있습니다. 이와 같은 위협을 최소화하려면 시스템을 적절히 구성하고 최신 소프트웨어를 사용하며 권장 소프트웨어 업데이트를 설치해야 합니다.

WSUS를 통해 사업의 가치를 높일 수 있는 핵심 시나리오는 다음과 같습니다.

-   중앙 집중식 업데이트 관리

-   업데이트 관리 자동화

### <a name="new-and-changed-functionality"></a>새로운 기능 및 변경된 기능

> [!NOTE]
> 모든 버전의 Windows Server 2012 r 2로 WSUS 3.2를 지 원하는 Windows Server에서 업그레이드 WSUS 3.2를 먼저 제거 해야 합니다.
> 
> Windows Server 2012에서 WSUS 3.2가 설치 된 Windows Server의 모든 버전에서 업그레이드 차단 됩니다 설치 프로세스 중 WSUS 3.2가 검색 된 경우. 이 경우 먼저 서버를 업그레이드 하기 전에 Windows Server Update Services를 제거 하 라는 메시지가 됩니다.
> 
> 그러나이 버전의 Windows Server 및 Windows Server 2012 R2, Windows Server 및 WSUS 3.2의 모든 버전에서 업그레이드 하면 변경으로 인해 설치가 차단 되지 않습니다. Windows Server 2012 R2 업그레이드를 수행 하기 전에 WSUS 3.2를 제거 하지 않으면 실패를 Windows Server 2012 r 2에 게시물 WSUS에 대 한 설치 작업을 발생 합니다. 이 경우에 유일한 알려진 해결 방법은 하드 드라이브를 포맷 하 여 Windows Server를 다시 설치 합니다.

Windows Server Update Services는 기본 제공되는 서버 역할로, 다음과 같이 기능이 향상되었습니다.

-   서버 관리자를 사용해 추가 및 제거할 수 있는 기능

-   WSUS에서 가장 중요 한 관리 작업을 관리 하는 Windows PowerShell cmdlet 포함

-   SHA256 해시 기능 추가하여 보안 강화

-   클라이언트와 서버 구분: WUA(Windows 업데이트 에이전트) 버전을 WSUS와 별도로 제공할 수 있습니다.

### <a name="using-windows-powershell-to-manage-wsus"></a>Windows PowerShell을 사용해 WSUS 관리
시스템 관리자가 자신의 작업을 자동화하려면 명령줄 자동화 전반에 대한 지식을 갖추어야 합니다. 이 기능의 주요 목적은 시스템 관리자가 자신의 일상 작업을 자동화할 수 있도록 해 편리하게 WSUS를 관리하는 데 있습니다.

**이와 같은 변경을 통해 더해지는 가치**

Windows PowerShell을 통해 핵심 WSUS 작업을 표시함으로써 시스템 관리자는 생산성을 늘리고, 새로운 도구를 배워야 할 필요성이 줄어들며, 유사 작업 간의 일관성이 결여되어 실패한 예상 사항에서 비롯된 오류를 줄일 수 있습니다.

**달라진 기능**

이전 버전의 Windows Server 운영 체제에는 Windows PowerShell cmdlet이 없어 업데이트 관리를 자동화하기 어려웠습니다. 시스템 관리자는 WSUS 작업용 Windows PowerShell cmdlet을 통해 더욱 유연하고 민첩하게 작업할 수 있습니다.

## <a name="in-this-collection"></a>이 컬렉션에
WSUS 계획, 배포 및 관리를 위한 다음 가이드가 포함되어 있습니다.

-   [Windows Server Update Services 배포](../deploy/deploy-windows-server-update-services.md)

-   [Windows Server Update Services를 사용하여 업데이트 관리](../manage/update-management-with-windows-server-update-services.md)


