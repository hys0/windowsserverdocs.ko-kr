---
title: WSUS 및 카탈로그 사이트
description: Windows Server Update Service (WSUS) 항목-Microsoft Update 카탈로그 사이트에 액세스 하 여 WSUS에 핫픽스를 가져오는 방법
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-wsus
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f19a8659-5a96-4fdd-a052-29e4547fe51a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 298df36b856cba97ec19126f77456785e5eb6f50
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66810923"
---
# <a name="wsus-and-the-catalog-site"></a>WSUS 및 카탈로그 사이트

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

카탈로그 사이트에는 핫픽스 및 하드웨어 드라이버를 가져올 수 있는 Microsoft 위치입니다.

## <a name="the-microsoft-update-catalog-site"></a>Microsoft Update 카탈로그 사이트
WSUS에 핫픽스를 가져오려면 WSUS 컴퓨터에서 Microsoft Update 카탈로그 사이트에서 액세스 해야 합니다. WSUS 서버인 여부 WSUS 관리 콘솔이 설치 된 모든 컴퓨터 카탈로그 사이트에서 핫픽스를 가져오는 데 사용할 수 있습니다. 핫픽스를 가져오려는 관리자로 컴퓨터에 로그온 해야 합니다.

#### <a name="to-access-the-microsoft-update-catalog-site"></a>Microsoft 업데이트 카탈로그 사이트에 액세스 하려면

1.  WSUS 관리 콘솔에서 상위 서버 노드를 선택 하거나 **업데이트**, 및는 **작업** 창 **업데이트를 가져옵니다**. Microsoft Update 카탈로그 웹 사이트에는 브라우저 창이 열립니다.

2.  이 사이트에서 업데이트에 액세스 하려면 Microsoft Update 카탈로그 activeX 컨트롤을 설치 해야 합니다.

3.  Windows 핫픽스 및 하드웨어 드라이버에 대 한이 사이트를 탐색할 수 있습니다. 요소를 발견 하면 장바구니에 추가 합니다.

4.  탐색 했으면 바구니로 이동 하 고 업데이트 가져오기에 가져오기를 클릭 합니다. 가져오지 않고 업데이트를 다운로드 하려면 선택을 취소 합니다 **Windows Server Update Services로 바로 가져오기** 확인란을 선택 합니다.

승인 된 업데이트가 Microsoft Update 카탈로그 사이트에서 가져온 다음에 WSUS 서버가 동기화 다운로드 됩니다. Microsoft Update 카탈로그 사이트에서 가져오기 시 다운로드 되지 않습니다.

Note는 액세스 해야 Microsoft 업데이트 카탈로그 사이트 하지만 WSUS 호환 형식으로 업데이트를 가져왔는지 확인 하려면 WSUS 콘솔입니다. 모든 다운로드 한 업데이트는 WSUS 서버에 가져오지 않습니다 하지만 대신 개별 다운로드 Microsoft 업데이트 카탈로그 웹 사이트를 직접 액세스 하는 경우 *. MSU 파일입니다. WSUS에서 파일을 가져오기 위해 지원 되는 메커니즘을 현재 되어 있지 않은 \*합니다. MSU 형식입니다.

The 서버 정리 마법사를 실행 하는 경우 WSUS 서버에서 승인 또는 거부 됨으로 설정 되는 Microsoft Update 카탈로그에서 가져온 업데이트를 제거할 수 있습니다. 제거 된 경우은 가져올 수 있습니다 다시 Microsoft Update 카탈로그에서 합니다.

> [!NOTE]
> WSUS 서버 정리 마법사를 실행 하 여 승인 또는 거절으로 설정 되어 있는 Microsoft Update 카탈로그에서 가져온 업데이트를 제거할 수 있습니다. Microsoft Update 카탈로그를 통해 WSUS 시스템에서 제거 된 업데이트를 다시 가져올된 수 있습니다.

## <a name="restricting-access-to-hotfixes"></a>핫픽스에 대 한 액세스 제한
WSUS 관리자가 Microsoft Update 카탈로그 사이트에서 다운로드 한 핫픽스에 대 한 액세스를 제한 고려할 수 있습니다. 이 제한은 다음 단계를 수행 하려면:

#### <a name="to-restrict-access-to-hotfixes"></a>핫픽스를 액세스를 제한 하려면

1.  콘텐츠 IIS vroot에 Windows 인증을 설정 합니다.

    -   IIS 관리자를 시작합니다.

    -   WSUS 관리 웹 사이트 아래에 있는 콘텐츠 노드를 이동 합니다.

    -   에 **콘텐츠 홈** 창에 두 번 클릭은 **인증** 옵션입니다.

    -   선택 **익명 인증** 클릭 **사용 하지 않도록 설정** 에 **작업** 오른쪽 창입니다.

    -   선택 **Windows 인증** 클릭 하 고 **사용** 에 **작업** 오른쪽 창입니다.

2.  핫픽스를 필요로 하는 컴퓨터에 대 한 WSUS 대상 그룹을 만들고 그룹에 추가 합니다. 컴퓨터 및 그룹에 대 한 자세한 내용은 참조 하세요. [WSUS 클라이언트 관리 컴퓨터 및 WSUS 컴퓨터 그룹](managing-wsus-client-computers-and-wsus-computer-groups.md) 이 가이드에서는 및 섹션의 [3.3입니다. WSUS 컴퓨터 그룹 구성](../deploy/2-configure-wsus.md#23-configure-wsus-computer-groups) 3 단계: WSUS 배포 가이드에서 WSUS를 구성 합니다.

3.  핫픽스 파일을 다운로드 합니다.

4.  이러한 컴퓨터의 컴퓨터 계정에만 읽을 수 있도록 이러한 파일의 사용 권한을 설정 합니다. 파일에 네트워크 서비스 계정 전체 액세스를 허용 하도록 해야 합니다.

5.  2 단계에서에서 만든 WSUS 대상 그룹에 대 한 핫픽스를 승인 합니다.

## <a name="importing-updates-in-different-languages"></a>다른 언어의 업데이트 가져오기
Microsoft Update 카탈로그 웹 사이트는 여러 언어를 지 원하는 업데이트가 포함 되어 있습니다. 이 거의 **중요 한** 이러한 업데이트를 지 원하는 언어를 사용 하 여 WSUS 서버를 지 원하는 언어와 일치 하도록 합니다. WSUS 서버는 업데이트에 포함 된 모든 언어를 지원 하지 않으면, 클라이언트 컴퓨터에 업데이트가 배포 되지 않습니다. 마찬가지로, 관리자가 선택 취소 하 고 여러 언어를 지 원하는 업데이트가 WSUS 서버에 다운로드 되었지만 아직 배포 되지 않은 클라이언트 컴퓨터에 업데이트를 포함 하는 언어 중 하나를 클라이언트에 업데이트가 배포 되지 않습니다.
