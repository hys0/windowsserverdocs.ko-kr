---
title: 관리 템플릿 NPS
description: 이 항목 만들고, 적용을 내보내고, Windows Server 2016에 네트워크 정책 서버에 대 한 NPS 서식 가져오기 하는 방법에 대해 설명 합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 989b00c5-4767-4081-ace5-6321f8b2c55e
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 0a7f4c50d87c155c1adcd445eae8df23aab7730b
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="manage-nps-templates"></a>관리 템플릿 NPS

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

네트워크 정책 서버 \(NPS\) 템플릿 구성 요소 같은 RADIUS(Remote Authentication Dial-In User Service) \(RADIUS\) 클라이언트 또는 로컬 NPS 서버 또는 다른 NPS 서버에서 사용할 수 있도록 내보내기 다시 사용할 수 있는 공유 암호 만들기를 사용할 수 있습니다. 

관리 템플릿 있는 하면, 수정, 삭제, 중복을 만들고 볼 수 NPS 템플릿 사용 NPS 콘솔 노드를 제공 합니다. NPS 템플릿 시간과 비용을 하나 이상의 서버의 NPS 구성 하는 데 걸리는의 양을 줄일 하도록 설계 되었습니다.

관리 템플릿 구성에 대 한 다음 NPS 서식 파일 형식을 사용할 수 있습니다.

- **공유 암호**합니다. 이와 같은 서식 쉽게 처리할 수 공유 암호 다시 사용할 수 있습니다 (템플릿 NPS 콘솔에서 해당 위치에 선택)를 지정할 수 있도록 RADIUS 클라이언트 및 서버를 구성할 때 합니다. 

- **RADIUS 클라이언트**합니다. 이와 같은 서식 템플릿을 NPS 콘솔에서 해당 위치에 선택 하 여 다시 사용할 수 있는 RADIUS 클라이언트 설정을 구성할 수 있습니다.

- **원격 RADIUS 서버**합니다. 이 템플릿의 템플릿을 NPS 콘솔에서 해당 위치에 선택 하 여 다시 사용할 수 있는 원격 RADIUS 서버 설정을 구성할 수 있습니다. 

- **IP 필터**합니다. 이 템플릿의 사용 하면 인터넷 프로토콜 버전 4 (IPv4)을 만들 수 없음 및 인터넷 프로토콜 버전 6 \(IPv6\) 필터를 다시 사용할 수 \ 템플릿을 NPS console\에서 해당 위치 선택) (하면 네트워크 정책 구성 하는 경우 합니다.

## <a name="create-an-nps-template"></a>NPS 템플릿 만들기

템플릿 구성 다른 직접 NPS 서버 구성 하는 것입니다. 템플릿 만들기 NPS 서버 기능 영향을 주지 않습니다. 것이 템플릿을 NPS 콘솔에서 해당 위치에 선택 하 고 템플릿을 NPS 서버 기능에 영향을 템플릿을 적용 있습니다. 

예를 들어, RADIUS 클라이언트 NPS 콘솔에서 구성한 경우 **RADIUS 클라이언트 및 서버**, NPS 서버 구성을 변경 하 고 NPS 통신할 액세스 서버 네트워크 중 하나를 구성 한 단계를 수행 합니다. \ (네트워크 액세스 서버 구성 하려면 다음 단계는 \(NAS\) NPS와 통신 하도록 합니다. \) 

그러나 새 구성한 경우 **RADIUS 클라이언트** 아래 NPS 콘솔에 템플릿으로 **관리 템플릿** 아래에서 새 RADIUS 클라이언트 만드는 대신 **RADIUS 클라이언트 및 서버**, 서식 만든 있지만 하지 변경한 NPS 서버 기능이 아직 합니다. NPS 서버 기능을 변경 하려면 템플릿을 NPS 본체의 정확한 위치에서 적용 해야 합니다.

다음 절차 새 템플릿을 만드는 방법에 대해 설명 합니다.

회원 **관리자**, 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.

### <a name="to-create-an-nps-template"></a>NPS 템플릿 만들기


1. 서버 관리자에서 NPS 서버에서 클릭 **도구**을 차례로 클릭 하 고 **네트워크 정책 서버**합니다. NPS console을 엽니다. 

2. NPS 본체에서 확장 **관리 템플릿**과 같은 서식 파일 형식 마우스 오른쪽 단추로 클릭 **RADIUS 클라이언트**을 차례로 클릭 하 고 **새로**합니다.

3. 템플릿을 구성할 사용할 수 있는 새로운 템플릿 속성 대화 상자를 엽니다.

## <a name="apply-an-nps-template"></a>NPS 템플릿을 적용합니다

만든 템플릿을 사용 하면 **관리 템플릿** NPS 콘솔에서 템플릿을 적용할 수 있는 위치로 이동 하 여 합니다. 예를 들어, 공유 암호 템플릿 RADIUS 클라이언트 구성 적용 하려는 경우 다음 절차를 사용할 수 있습니다.

회원 **관리자**, 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.

### <a name="to-apply-an-nps-template"></a>NPS 템플릿을 적용 하려면

1. 서버 관리자에서 NPS 서버에서 클릭 **도구**을 차례로 클릭 하 고 **네트워크 정책 서버**합니다. NPS console을 엽니다.

2. NPS 본체에서 확장 **RADIUS 클라이언트 및 서버**를 확장 한 다음 **RADIUS 클라이언트**합니다.

3.에서 **RADIUS 클라이언트**, 세부 정보 창에서 마우스 오른쪽 단추로 클릭 NPS 템플릿을 적용를 클릭 한 다음 원하는 RADIUS 클라이언트 **속성**합니다.

4. 속성 대화 상자에서 RADIUS 클라이언트에 대 한에 **기존 공유 암호 템플릿 선택**, 템플릿 목록에서 적용 하려면 템플릿을 선택 합니다.

## <a name="export-or-import-nps-templates"></a>NPS 템플릿 내보내기 또는 가져오기

다른 NPS 서버에서 사용할 수 있도록 템플릿 내보낼 수 하거나 템플릿으로 가져올 수 있습니다 **관리 템플릿** 로컬 컴퓨터에서 사용할 수 있도록 합니다. 

회원 **관리자**, 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.

### <a name="to-export-or-import-nps-templates"></a>내보내거나 NPS 서식 가져오기

1. 내보낼 NPS 템플릿 NPS 콘솔에서 마우스 오른쪽 단추로 클릭 **관리 템플릿**, 클릭 한 다음 **내보내려면 템플릿 파일에**합니다.

2. NPS 콘솔에서 NPS 서식 가져오기를 마우스 오른쪽 단추로 클릭 **관리 템플릿**을 차례로 클릭 하 고 **컴퓨터에서 서식 가져오기** 또는 **파일에서 서식 가져오기**합니다.


