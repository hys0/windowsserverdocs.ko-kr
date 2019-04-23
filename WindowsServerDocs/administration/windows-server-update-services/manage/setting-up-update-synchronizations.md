---
title: 업데이트 동기화 설정
description: Windows Server Update Service (WSUS) 항목-설정 및 업데이트 동기화를 구성 하는 방법
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-wsus
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ddd5c395-451b-44a0-8e08-a05db26d2282
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e381316372e68d2a43203b8fc90a243af5f40b02
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59869214"
---
# <a name="setting-up-update-synchronizations"></a>업데이트 동기화 설정

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

동기화 하는 동안 WSUS 서버는 업데이트 원본에서 업데이트 (업데이트 메타 데이터 및 파일)을 다운로드 합니다. 또한 다운로드 새 제품 분류 및 범주 있으면 됩니다. WSUS 서버에 처음으로 동기화, 동기화 옵션을 구성할 때 지정한 업데이트를 모두 다운로드 됩니다. 첫 번째 동기화 후 WSUS 서버에 기존 업데이트 및 만료 정책에 대 한 메타 데이터에 대 한 수정 버전 뿐만 아니라 업데이트 원본에서 업데이트에만 업데이트를 다운로드합니다.

업데이트를 다운로드 하는 WSUS 서버를 처음으로 시간이 오래 걸릴 수 있습니다. 여러 WSUS 서버를 설정 하는 경우 있습니다 속도를 높일 수 프로세스 정도 한 WSUS 서버에서 모든 업데이트를 다운로드 하 고 다음 업데이트는 다른 WSUS 서버의 콘텐츠 디렉터리에 복사 하 여 합니다.

다른 한 WSUS 서버의 콘텐츠 디렉터리에서 콘텐츠를 복사할 수 있습니다. 콘텐츠 디렉터리의 위치는 WSUS post 설치 프로세스를 실행할 때 지정 됩니다. WSUS 서버 간에 파일을 업데이트 메타 데이터를 내보내려면 wsusutil.exe 도구를 사용할 수 있습니다. 그런 다음 다른 WSUS 서버에 해당 파일을 가져올 수 있습니다.

## <a name="setting-up-update-synchronizations"></a>업데이트 동기화 설정
**옵션** 페이지는 WSUS 서버에서 업데이트를 동기화 하는 방법을 사용자 지정 하기 위한 WSUS 관리 콘솔에서 중앙 액세스 지점입니다. 업데이트를 자동으로 동기화를 지정할 수 있습니다 서버 업데이트, 연결 설정 및 동기화 일정을 가져오는 하는 위치입니다. 구성 마법사를 사용할 수도 있습니다는 **옵션** 페이지를 구성 하거나 언제 든 지 WSUS 서버를 다시 구성 합니다.

### <a name="synchronizing-update-by-product-and-classification"></a>제품 및 분류 하 여 업데이트를 동기화합니다.
제품 또는 제품군 (예: Windows, 또는 Windows Server 2008 Datacenter edition)에 따라 업데이트를 다운로드 하는 WSUS 서버 및 분류 (예를 들어 중요 업데이트나 보안 업데이트)를 지정 합니다. WSUS 서버를 첫 번째 동기화에서 모든 사용자가 지정한 범주에 사용 가능한 업데이트를 다운로드 합니다. 후속 동기화에서 하면 WSUS 서버 다운로드 최신 업데이트에만 (또는 WSUS 서버에서 이미 사용할 수 있는 업데이트의 변경 사항) 범주에 대해 지정 했습니다.

업데이트 제품 및 분류를 지정할 수는 **옵션** 페이지 **제품 및 분류**합니다. 제품은 제품군 별로 그룹화 된 계층 구조에 나와 있습니다. Windows를 선택 하면 자동으로 해당 제품 계층에 속하는 모든 제품을 선택 합니다. 부모 확인란을 선택 하 여 그 아래 모든 항목 뿐만 아니라 모든 이후 버전을 선택 합니다. 자식 확인란을 선택 하는 부모 확인란은 선택 하지 않습니다. 제품은 모든 Windows 제품 및 분류에 대 한 기본 설정에 대 한 기본 설정 및 보안 업데이트 합니다.

WSUS 서버에서 복제 모드에서을 실행 하는 경우이 작업을 수행할 수 없습니다. 복제 모드에 대 한 자세한 내용은 참조 하세요. [실행 중인 WSUS 복제 모드](running-wsus-replica-mode.md), 및 [1 단계: WSUS 배포 준비](../plan/plan-your-wsus-deployment.md)합니다.

##### <a name="to-specify-update-products-and-classifications-for-synchronization"></a>업데이트 제품 및 동기화에 대 한 분류를 지정 하려면

1.  WSUS 관리 콘솔에서 클릭 된 **옵션** 노드.

2.  클릭 **제품 및 분류**, 를 클릭 하 고는 **제품** 탭 합니다.

3.  제품 또는 제품군 wsus에서 업데이트 한 다음 클릭 하려면 확인란을 선택 **확인**합니다.

4.  에 **분류** 탭에서 WSUS 서버가 동기화 한 클릭 한 다음 업데이트 분류의 확인란을 선택 **확인**합니다.

> [!NOTE]
> 같은 방식으로 제품 또는 분류를 제거할 수 있습니다. WSUS 서버 선택을 취소 한 제품에 대 한 새 업데이트 동기화가 중지 됩니다. 그러나 선택을 취소 하면 전에 해당 제품에 대 한 동기화 된 업데이트 WSUS 서버에 유지 되 고 가능한 항목으로 나열 됩니다.
> 
> 에 설명 된 대로 이러한 제품을 제거 하려면 업데이트를 거부 [업데이트 작업](updates-operations.md)를 사용 하 여 합니다 [The 서버 정리 마법사](the-server-cleanup-wizard.md) 제거 합니다.

### <a name="synchronizing-updates-by-language"></a>언어에 따라 업데이트 동기화
WSUS 서버는 지정한 언어에 따라 업데이트를 다운로드 합니다. 사용 하는 언어의 모든 업데이트를 동기화 할 수 또는 언어 하위 집합을 지정할 수 있습니다. WSUS 서버 계층 있고 서로 다른 언어의 업데이트를 다운로드 해야 하는 경우 업스트림 서버에서 필요한 모든 언어를 지정 해야 합니다. 다운스트림 서버에서 업스트림 서버에서 지정 된 언어의 하위 집합을 지정할 수 있습니다.

### <a name="synchronizing-updates-from-the-microsoft-update-catalog"></a>Microsoft Update 카탈로그에서 업데이트를 동기화합니다.
Microsoft 업데이트 카탈로그 사이트에서 업데이트를 동기화 하는 방법에 대 한 자세한 내용은 다음을 참조 하세요. [WSUS 및 카탈로그 사이트](wsus-and-the-catalog-site.md)합니다.

### <a name="synchronizing-device-updates-by-inventory-inventory-based-synchronization"></a>인벤토리 (인벤토리 기반 동기화)를 통해 장치 업데이트를 동기화합니다.
특정 제품 범주 및 분류 (예: 드라이버)에 매우 많은 업데이트를 포함 하 고 이러한 전체 범주 WSUS 서버를 동기화 하는 것은 권장 되지 않습니다. 이렇게 성능 문제 및 지속적인 유지 관리 문제가 발생할 수 있습니다. WSUS 재고 시스템 클라이언트 장치에서 식별할 수 없는 정보를 수집 하 고 해당 인벤토리 정보를 사용 하 여 Microsoft Update에서 충분 한 업데이트 메타 데이터를 검색 합니다. Microsoft Update 카탈로그를 자동으로 검색 되는 WSUS를 지정 하는 거의 동일한이 메커니즘은 관리 되는 장치에서 검색 된 장치에 대 한 업데이트에만 가져오기.

이 인벤토리 기능을 사용 하면 특정 장치 펌웨어 및 Microsoft Update 카탈로그에 게시 되지 않는 모델 기반 서비스 집합을 지원 되는 유일한 방법 이며

이 방식으로 동기화 하는 업데이트를 검토 하 고 다른 업데이트와 마찬가지로 승인 및도 같은 자동 승인 규칙에 따라 교체 만료 및 기타 동작 연결 되어 있는 기존 업데이트 합니다.

WSUS는 클라이언트 인벤토리를 통해 가져온 업데이트를 포함 하 여 특정 드라이버 및 펌웨어 업데이트를 요청 하는 경우 서버 쪽 필터링을 수행 합니다. 따라서 클라이언트 컴퓨터 또는 장치 메타 데이터 및 드라이버에 대 한 detectoids 및 드라이버 업데이트 실제로 해당 장치에 연결 된 장치에 대해서만 받게 됩니다. 이 동작은 클라이언트 검색 시간을 최소화 하 고 WSUS 서버와 클라이언트 간에 전송 되는 데이터를 감소 됩니다.

> [!NOTE]
> WSUS 장치 단위 별로 장치 인벤토리를 유지 관리 하는 인벤토리 기반 동기화를 사용 하는 경우 업스트림 WSUS 서버에만 요약 롤업 (중복 제거 된 Id 목록이) 적이 보내집니다. 업스트림 WSUS 서버에서 어떤 장치는 어떤 컴퓨터에 연결 하거나 WSUS 계층 내 인스턴스 수가 지정된 된 장치에 존재 하는 방법에 대 한 정보를 받지 않습니다. 일반적으로이 요약 롤업 식별 하거나 WSUS로 관리 되는 네트워크 장치에 계산에 사용할 수 없습니다.

## <a name="configuring-proxy-server-settings"></a>프록시 서버 설정 구성
업스트림 서버 또는 Microsoft Update와 동기화 하는 동안 프록시 서버를 사용 하도록 WSUS 서버를 구성할 수 있습니다. 이 설정은 사용자의 WSUS 동기화를 실행 하는 경우에 적용 됩니다. 기본적으로 WSUS 서버는 Microsoft Update 또는 업스트림 서버에 직접 연결 하려고 합니다.

#### <a name="to-specify-a-proxy-server-for-synchronization"></a>동기화에 대 한 프록시 서버를 지정 하려면

1.  WSUS 관리 콘솔에서 클릭 **옵션**, 를 클릭 하 고 **업데이트 원본 및 프록시 서버**합니다.

2.  에 **프록시 서버** 탭을 선택은 **동기화 할 때 프록시 서버를 사용 하 여** 확인란을 서버 이름을 입력 하 고 포트 번호는 프록시 서버를 합니다.

    > [!NOTE]
    > WSUS 프록시 서버에 구성 된 동일한 포트 번호로 구성를 사용 합니다.

    -   특정 사용자 자격 증명을 사용 하 여 프록시 서버에 연결 하려는 경우 선택 합니다 **사용자 자격 증명을 사용 하 여 프록시 서버에 연결할** 확인란을 선택한 다음 해당 상자에 사용자 이름, 도메인 및 사용자의 암호를 입력 .

    -   프록시 서버에 연결 하는 사용자에 대 한 기본 인증을 사용 하도록 설정 하려는 경우는 **기본 인증 허용 (암호를 일반 텍스트로 보냄)** 확인란 합니다.

3.  **확인**을 클릭합니다.

    > [!NOTE]
    > 없기 때문에 WSUS를 시작 하는 네트워크 트래픽을 모두, Microsoft update에 직접 연결 된 WSUS 서버에서 Windows 방화벽을 구성할 필요가 없습니다.

## <a name="configuring-the-update-source"></a>업데이트 원본 구성
소스 업데이트는 WSUS 서버를 해당 업데이트를 가져옵니다 위치 및 메타 데이터를 업데이트 합니다. Microsoft Update 또는 다른 WSUS 서버 (업데이트 원본을 업스트림 서버 이며 서버에는 다운스트림 서버 한 대로 작업을 수행 하는 WSUS 서버)를 업데이트 원본이 되도록 지정할 수 있습니다.

WSUS 서버의 업데이트 소스와 동기화 하는 방법을 사용자 지정 하기 위한 옵션은 다음과 같습니다.

-   동기화에 대 한 사용자 지정 포트를 지정할 수 있습니다. 포트를 구성 하는 방법에 대 한 내용은 [3 단계: WSUS 구성](../deploy/2-configure-wsus.md) WSUS 배포 가이드에서입니다.

-   보안 동기화 WSUS 서버 간에 업데이트 정보를 보안 소켓 레이어 (SSL)를 사용할 수 있습니다. SSL을 사용 하는 방법에 대 한 자세한 내용은 "3.5 섹션을 참조 하십시오. 보안 WSUS Secure Sockets Layer 프로토콜을 사용 하 여"의 [3 단계: WSUS 구성](../deploy/2-configure-wsus.md) WSUS 배포 가이드에서입니다.

## <a name="synchronizing-manually-or-automatically"></a>수동 또는 자동으로 동기화합니다.
WSUS 서버를 수동으로 동기화 하거나 자동으로 동기화 하는 시간을 지정할 수 있습니다.

#### <a name="to-manually-synchronize-the-wsus-server"></a>WSUS 서버를 수동으로 동기화 하려면

1.  WSUS 관리 콘솔에서 클릭 **옵션**, 를 클릭 하 고 **동기화 일정**합니다.

2.  클릭 **수동으로 동기화**, 를 클릭 하 고 **확인**합니다.

#### <a name="to-set-up-an-automatic-synchronization-schedule"></a>자동 동기화 일정을 설정 하려면

1.  WSUS 관리 콘솔에서 클릭 **옵션**, 를 클릭 한 다음 **동기화 일정**합니다.

2.  클릭 **자동으로 동기화**합니다.

3.  에 대 한 **첫 번째 동기화**, 동기화를 매일 시작 시간을 선택 합니다.

4.  에 대 한 **하루 동기화**을 매일 수행 하려는 동기화의 수를 선택 합니다. 예를 들어 원할 경우 4 개의 동기화를 시작 해 서 매일 오전 3 시에 다음 동기화 작업이 수행 됩니다 오전 오전 9시 3 시에서 오후 3 시와 오후 9시 각 날짜입니다. (Microsoft Update에 대 한 서버 연결 아웃 공간 하기 위해 임의 시간 오프셋 예약 된 동기화 시간에 추가할 수는 note).

5.  **확인**을 클릭합니다.

#### <a name="to-synchronize-your-wsus-server-immediately"></a>WSUS 서버를 즉시 동기화 하려면

1.  WSUS 관리 콘솔에서 해당 상위 서버 노드를 선택 합니다.

2.  에 **개요** 창 아래에서 **동기화 상태**, 클릭 **지금 동기화**합니다.

> [!NOTE]
> 동기화는 다운스트림 서버에서 시작 됩니다.
