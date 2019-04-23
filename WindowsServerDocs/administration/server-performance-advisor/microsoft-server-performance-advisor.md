---
title: Microsoft Server Performance Advisor
description: Microsoft Server Performance Advisor
ms.assetid: 468ebcb3-9eaf-477c-ab10-e3f1b3ce63dc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: manage
ms.openlocfilehash: ab124f3efabf2ac3ae8904157a81587c0c21ebb5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856334"
---
# <a name="microsoft-server-performance-advisor"></a>Microsoft Server Performance Advisor

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Microsoft 서버 성능 Advisor (SPA) Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 또는 Windows Server 2008 배포에서 성능 문제를 진단 하기 위해 다운로드 합니다. SPA는 종합 진단 보고서와 차트를 생성 하 고 문제를 분석 하 고 수정 작업을 개발 하기 위한 권장 사항을 신속 하 게를 제공 합니다.

-   [Server Performance Advisor 개요](#bkmk-aboutspa)

-   [Server Performance Advisor를 다운로드 합니다.](#bkmk-downloadspa)

-   [서버 성능 관리자 사용자 가이드](server-performance-advisor-users-guide.md)

-   [서버 성능 Advisor 팩 개발 가이드](server-performance-advisor-pack-development-guide.md)

## <a href="" id="bkmk-aboutspa"></a>Server Performance Advisor 개요

Server Performance Advisor SPA Advisor 팩, SPA 프레임 워크와 두 부분으로 구성 됩니다.

### <a name="the-server-performance-advisor-framework"></a>Server Performance Advisor 프레임 워크

Advisor 팩이 지정 하는 데이터를 수집, Microsoft SQL Server 데이터베이스에 수집 된 데이터를 작성, SPA Advisor 팩에 대 한 스크립트를 실행 하는 IT에 게 친숙 한 환경 만들기 및 최종 보고서를 표시 하는 일을 담당 하는 엔진입니다. SPA 콘솔에 SPA 프레임 워크를 설치 하기만 하면 됩니다. SPA 콘솔은 독립 실행형 컴퓨터에 원격으로 테스트 대상 서버를 액세스 하거나 테스트 중인 서버에 설치 하거나 설치할 수 있습니다.

### <a name="server-performance-advisor-packs"></a>Server Performance Advisor 팩

SPA Advisor 팩에는 일련의 메타 데이터 및 SQL 스크립트 파일의 구성 된 모든 튜닝 규칙의 중심 이므로 합니다. SPA 다음 Advisor 팩 함께 제공 됩니다.

-   핵심 OS advisor 팩 일반 운영 체제 기능을 특수 한 서버 역할의 독립의 성능을 분석합니다.

-   인터넷 정보 서버 (IIS) 관리자 팩에는 IIS의 성능을 추적합니다.

-   Hyper-v 관리자 팩에는 Hyper-v 서버 역할의 일반 성능을 분석합니다.

    **참고** The Hyper-v 관리자 팩 게스트 운영 체제를 분석 하지 않습니다.

     

-   Active directory advisor 팩에는 active directory 역할의 일반 성능을 분석합니다.

또한 SPA를 필요에 맞게 advisor 팩을 작성 하는 타사 개발자를 위한 확장 가능한 모델을 제공 합니다.

**참고** SPA 모든 하드웨어 및 사용자 시나리오 컨텍스트를 이해할 수 없습니다. 서버에 대 한 잠재적 변경 결과 이해 하 고 결정을 내릴 수 있도록 도구를 통해 제공 되는 권장 사항을 사용 해야 합니다.

 

## <a href="" id="bkmk-downloadspa"></a>Server Performance Advisor를 다운로드 합니다.


다음 링크를 사용 하 여 서버 성능 관리자에 대 한 Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 또는 Windows Server 2008을 다운로드 하려면:

-   [Microsoft Server Performance Advisor 3.1 (32 비트)](https://go.microsoft.com/fwlink/p/?linkid=327751)

-   [Microsoft Server Performance Advisor 3.1 (64 비트)](https://go.microsoft.com/fwlink/p/?linkid=327752)

다음 명령을 사용 하 여 CAB 파일에 있는 파일을 추출할 수 있습니다.

-   x86 버전: `extrac32.exe /e /a /l  d:\SPA   d:\SPA\SPAPlus\_x86.cab`

-   x64 버전: `extrac32.exe /e /a /l  d:\SPA   d:\SPA\SPAPlus\_amd64.cab`

**주의** .cab 파일을 추출 하면 SPA 제대로 작동 하려면 계층 디렉터리 구조를 유지 해야 합니다. 서버에 설치 된 CAB 도구에 따라 작동 하지 않는 디렉터리 구조에서 추출 될 수 있습니다. 계층 디렉터리 구조를 유지 하려면 파일 디렉터리 구조를 추출 하는 CAB 추출 유틸리티 도구를 사용할 수 있습니다.

CAB 추출 도구 제대로 파일의 압축을 푼 경우 추출 대상 폴더에 하위 폴더가 자동으로 나타납니다.

### <a name="spa-prerequisites"></a>SPA 필수 구성 요소

SPA 콘솔에 다음 소프트웨어가 설치 되어 있는지 필요 합니다.

-   Microsoft.NET Framework 4

-   SQL Server 2008 R2 SP1 또는 Microsoft SQL Server 2008 R2 SP1 Express

최신 버전은 호환 수 있습니다. 알려진된 제품 비 호환성 SPA 콘솔에 표시 됩니다.
