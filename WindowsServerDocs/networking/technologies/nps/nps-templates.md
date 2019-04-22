---
title: NPS 템플릿
description: 이 항목에서는 Windows Server 2016에서 네트워크 정책 서버 템플릿의 개요를 제공합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: fdfc0df1-21c7-492c-9fad-38fe9c7d935a
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 0647dbf0f99a01e32ba68475b439501e2dbeebfe
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823314"
---
# <a name="nps-templates"></a>NPS 템플릿

>적용 대상: Windows Server (반기 채널), Windows Server 2016

네트워크 정책 서버 \(NPS\) 템플릿을 사용 하면 원격 인증 전화 접속 사용자 서비스 같은 구성 요소를 만들려면 \(RADIUS\) 클라이언트 또는 로컬에서 재사용할 수 있는 공유 암호 NPS 및 기타 NPSs에서 사용 하기 위해 내보내기입니다.

NPS 템플릿은 시간 및 비용에는 하나 이상의 서버에 NPS를 구성 하는 데 걸리는 시간을 줄이도록 설계 되었습니다. 구성 템플릿 관리에 대 한 사용 가능한 다음 NPS 템플릿 형식은 다음과 같습니다.

- 공유 암호
- RADIUS 클라이언트
- 원격 RADIUS 서버
- IP 필터
- 업데이트 관리 서버 그룹

템플릿을 구성 하는 것은 NPS를 직접 구성 다릅니다. 템플릿을 만드는 NPS의 기능 영향을 주지 않습니다. 선택한 경우에 템플릿의 템플릿을 NPS 기능에 영향을 준다는 NPS 콘솔에서 해당 위치에서 이며 

예를 들어, RADIUS 클라이언트 및 서버에서 NPS 콘솔에서 RADIUS 클라이언트를 구성 하는 경우 NPS 구성을 변경할 수 있고 한 네트워크 액세스 서버와 통신 하는 NPS를 구성 하는 하나의 단계를 수행 \(NAS의\) . \(NPS와 통신 하는 NAS를 구성 하려면 다음 단계를 것입니다.\) 그러나 아래에서 [NPS] 콘솔에서 새 RADIUS 클라이언트 템플릿을 구성한 경우 **템플릿 관리** 아래의 새 RADIUS 클라이언트를 만드는 대신 **RADIUS 클라이언트 및 서버**, 만든를 하지만 템플릿을 변경 되지 NPS 기능을 아직입니다. NPS 기능을 변경 하려면 NPS 콘솔의 올바른 위치에서 템플릿을 선택 해야 합니다.

## <a name="creating-templates"></a>템플릿 만들기

템플릿을 만들려면 NPS 콘솔을 열고 같은 템플릿 유형을 마우스 오른쪽 단추로 **IP 필터**를 클릭 하 고 **새로 만들기**합니다. 새 템플릿 속성 대화 상자 템플릿을 구성할 수 있도록 열립니다.

## <a name="using-templates-locally"></a>로컬 템플릿을 사용 하 여

만든 템플릿을 사용할 수 있습니다 **템플릿 관리** 템플릿을 적용할 수 있는 NPS 콘솔에서 위치로 이동 하 여 합니다. 예를 들어, 하는 새 공유 암호 템플릿을 만드는 경우 원하는에서 RADIUS 클라이언트 구성에 적용할 **RADIUS 클라이언트 및 서버** 하 고 **RADIUS 클라이언트**, RADIUS 클라이언트 속성을 엽니다. **기존 공유 비밀 템플릿을 선택할**, 사용 가능한 템플릿 목록에서 이전에 만든 템플릿을 선택 합니다.

NPS에 대 한 자세한 내용은 참조 하세요. [네트워크 정책 (NPS 서버)](nps-top.md)합니다.
