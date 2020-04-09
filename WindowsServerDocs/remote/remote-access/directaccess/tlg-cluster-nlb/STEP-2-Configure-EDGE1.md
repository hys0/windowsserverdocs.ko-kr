---
title: 2 단계 EDGE1 구성
description: 이 항목은 테스트 랩 가이드-windows Server 2016 용 Windows NLB를 사용 하는 클러스터의 DirectAccess 시연에 포함 되어 있습니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: 84457351-1ca7-4e7c-8e2c-53d55b1fcdc0
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 8705e69debec2f0a19f5cc010ed5ca254cc56741
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80819316"
---
# <a name="step-2-configure-edge1"></a>2 단계 EDGE1 구성

>적용 대상: Windows Server(반기 채널), Windows Server 2016

DirectAccess 서버에서 수행 되는 절차는 다음과 같습니다.

## <a name="to-configure-directaccess-on-edge1"></a>EDGE1에서 DirectAccess를 구성 하려면
  
1.  **시작** 화면에서**ramgmtui.exe**를 입력 한 다음 enter 키를 누릅니다. **사용자 계정 컨트롤** 대화 상자가 표시되면 원하는 작업이 표시되어 있는지 확인하고 **예**를 클릭합니다.  
  
2.  원격 액세스 관리 콘솔의 왼쪽 창에서 **구성**을 클릭 합니다.  
  
3.  콘솔의 가운데 창에 있는 **2 단계 원격 액세스 서버** 영역에서 **편집**을 클릭 합니다.  
  
4.  **원격 액세스 서버 설치** 마법사에서 **접두사 구성**을 클릭 합니다. **접두사 구성** 페이지의 **DirectAccess 클라이언트 컴퓨터에 할당 된 IPv6 접두사**에 **2001: db8:1: 1000:/59**를 입력 한 후 **다음**을 클릭 합니다.  
  
5.  **마침**을 클릭합니다.  
  
6.  콘솔의 가운데 창에서 클릭 **마침**합니다.  
  
7.  에 **원격 액세스 검토** 대화 상자에서 구성 설정을 검토 하 고 클릭 한 다음 **적용**합니다. **원격 액세스 설정 마법사 설정 적용** 대화 상자에서 **닫기**를 클릭합니다.
