---
title: NPS 템플릿
description: 이 항목에서는 Windows Server 2016의 네트워크 정책 서버 템플릿에 대해 간략하게 설명 합니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: fdfc0df1-21c7-492c-9fad-38fe9c7d935a
ms.author: pashort
author: shortpatti
ms.openlocfilehash: bafff7a6a15312ab1bdca2e7b98307bc94731d3a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405321"
---
# <a name="nps-templates"></a>NPS 템플릿

>적용 대상: Windows Server(반기 채널), Windows Server 2016

네트워크 정책 서버 \(NPS @ no__t 템플릿을 사용 하면 RADIUS(Remote Authentication Dial-In User Service) \(RADIUS @ no__t-3 클라이언트 또는 공유 암호와 같은 구성 요소를 만들어 로컬 NPS에서 다시 사용 하 고 다른 컴퓨터에서 사용 하기 위해 내보낼 수 있습니다. NPSs.

NPS 템플릿은 하나 이상의 서버에서 NPS를 구성 하는 데 소요 되는 시간과 비용을 줄이도록 설계 되었습니다. 다음 NPS 템플릿 유형은 템플릿 관리에서 구성에 사용할 수 있습니다.

- 공유 암호
- RADIUS 클라이언트
- 원격 RADIUS 서버
- IP 필터
- 업데이트 관리 서버 그룹

템플릿을 구성 하는 것은 NPS를 직접 구성 하는 것과는 다릅니다. 템플릿을 만들면 NPS의 기능에 영향을 주지 않습니다. NPS 콘솔의 해당 위치에서 템플릿을 선택 하는 경우에만 템플릿이 NPS 기능에 영향을 줍니다. 

예를 들어 NPS 콘솔의 RADIUS 클라이언트 및 서버에서 RADIUS 클라이언트를 구성 하는 경우 nps 구성을 변경 하 고 NPS에서 네트워크 액세스 @no__t 서버 중 하 나와 통신 하도록 NPS 구성 (0NAS's @ no__t-1)의 한 단계를 수행 합니다. @no__t-다음 단계는 NPS와 통신 하도록 NAS를 구성 하는 것입니다. \) 그러나 **Radius 클라이언트 및 서버**에서 새 radius 클라이언트를 만들지 않고 **템플릿 관리** 의 NPS 콘솔에서 새 radius 클라이언트 템플릿을 구성 하는 경우에는 템플릿을 만들었지만 nps를 변경 하지 않은 것입니다. 기능이 아직 없습니다. NPS 기능을 변경 하려면 NPS 콘솔의 올바른 위치에서 템플릿을 선택 해야 합니다.

## <a name="creating-templates"></a>템플릿 만들기

템플릿을 만들려면 NPS 콘솔을 열고 **IP 필터**와 같은 템플릿 유형을 마우스 오른쪽 단추로 클릭 한 다음 **새로 만들기**를 클릭 합니다. 템플릿을 구성할 수 있는 새 템플릿 속성 대화 상자가 열립니다.

## <a name="using-templates-locally"></a>로컬에서 템플릿 사용

템플릿을 적용할 수 있는 NPS 콘솔의 위치로 이동 하 여 **템플릿 관리** 에서 만든 템플릿을 사용할 수 있습니다. 예를 들어 radius 클라이언트 구성에 적용할 새 공유 비밀 템플릿을 만든 경우 **radius 클라이언트 및 서버** 와 **RADIUS 클라이언트**에서 radius 클라이언트 속성을 엽니다. **기존 공유 비밀 템플릿 선택**의 사용 가능한 템플릿 목록에서 이전에 만든 템플릿을 선택 합니다.

NPS에 대 한 자세한 내용은 [nps (네트워크 정책 서버)](nps-top.md)를 참조 하세요.
