---
title: NPS 템플릿
description: 이 항목에서는 네트워크 정책 서버 템플릿 Windows Server 2016에 대 한 개요입니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: fdfc0df1-21c7-492c-9fad-38fe9c7d935a
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 2835959b8c076ef7b6aeb1fca31a62717ef95037
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="nps-templates"></a>NPS 템플릿

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

네트워크 정책 서버 \(NPS\) 템플릿을 사용 RADIUS(Remote Authentication Dial-In User Service) \(RADIUS\) 클라이언트 또는 공유 암호 로컬 NPS 서버 또는 다른 NPS 서버에서 사용할 수 있도록 내보내기 다시 사용할 수 있는 등 구성 요소를 만들 수 있습니다.

NPS 템플릿 시간과 비용을 하나 이상의 서버의 NPS 구성 하는 데 걸리는의 양을 줄일 하도록 설계 되었습니다. 다음 NPS 템플릿 종류 관리 템플릿 구성에 맞게 사용할 수 있습니다.

- 공유 암호
- RADIUS 클라이언트
- 원격 RADIUS 서버
- IP 필터
- 서버 그룹 개선

템플릿 구성 다른 직접 NPS 서버 구성 하는 것입니다. 템플릿 만들기 NPS 서버 기능 영향을 주지 않습니다. 선택한 경우에 템플릿의 템플릿을 NPS 서버 기능에 영향을 NPS 콘솔에서 해당 위치에입니다. 

예를 들어, NPS RADIUS 클라이언트 및 서버에서 콘솔에서 RADIUS 클라이언트 구성, NPS 서버 구성 변경을 NPS 통신할 네트워크에 대 한 액세스 서버 \(NAS's\) 중 하나를 구성 첫 단계가 완료 합니다. 그러나 \ (NPS.와 통신 하도록 NAS 구성 하려면 다음 단계 것 \) NPS 콘솔 아래에서 새 RADIUS 클라이언트 템플릿을 경우 구성 **관리 템플릿** 아래에서 새 RADIUS 클라이언트 만드는 대신 **RADIUS 클라이언트 및 서버**, 서식 만든 있지만 NPS 서버 기능이 아직 변경 하지 했습니다. NPS 서버 기능을 변경 하려면 템플릿을 NPS 본체의 정확한 위치에서 선택 해야 합니다.

## <a name="creating-templates"></a>템플릿 만들기

템플릿의 만들려는 NPS 콘솔과 같은 서식 파일 형식 마우스 오른쪽 단추로 클릭 **IP 필터**을 차례로 클릭 하 고 **새로**합니다. 새 템플릿 속성 대화 상자가 템플릿을 구성할 수 있도록 해 주는 열립니다.

## <a name="using-templates-locally"></a>로컬 템플릿을 사용

만든 템플릿을 사용 하면 **관리 템플릿** NPS 콘솔에서 템플릿을 적용 될 수 있는 위치로 이동 하 여 합니다. 예를 들어, 새로운 공유 암호 템플릿을 만든 경우 하려는 RADIUS 클라이언트 구성에 적용 **RADIUS 클라이언트 및 서버** 및 **RADIUS 클라이언트**, RADIUS 클라이언트 속성을 엽니다. **기존 공유 암호 템플릿 선택**를 사용할 수 있는 템플릿 목록에서 이전에 만든 템플릿을 선택 합니다.

NPS에 대 한 자세한 내용은 참조 [네트워크 NPS 정책 서버 ()](nps-top.md)합니다.
