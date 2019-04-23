---
title: Windows Admin Center 확장 이해
description: Windows Admin Center SDK 확장 이해(Project Honolulu)
ms.technology: extend
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: b00ee847088d038e59266154bcbbe9499bfe47fa
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850114"
---
# <a name="understanding-windows-admin-center-extensions"></a>Windows Admin Center 확장 이해

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

아직 Windows Admin Center가 작동하는 방식에 익숙하지 않은 경우 개략적인 아키텍처로 시작해 봅니다. Windows Admin Center는 다음의 두 주요 구성 요소로 이루어져있습니다.

- 웹 브라우저 요청에 대해 Windows Admin Center UI 웹 페이지 역할을 하는 경량 **웹 서비스**.
- 웹 페이지의 REST API 요청 수신을 대기하고 대상 서버 또는 클러스터에서 실행할 WMI 호출 또는 PowerShell 스크립트를 릴레이하는 **게이트웨이 구성 요소**.

![Windows Admin Center 아키텍처](../media/understand-extensions/wac-architecture-500px.png)

웹 서비스에서 제공하는 Windows Admin Center UI 웹 페이지에는 확장 가능성 측면에서 확장과 세 번째 확장 형식인 게이트웨이 플러그 인으로 구현되는 솔루션과 도구라는 두 주요 UI 구성 요소가 있습니다.

## <a name="solution-extensions"></a>솔루션 확장

기본적으로 Windows Admin Center 홈 화면에서 Windows Server 연결, Windows PC 연결, 장애 조치 클러스터 연결 및 하이퍼 컨버지드 클러스터 연결의 4가지 연결 유형 중 하나를 추가할 수 있습니다. 연결이 추가되면 연결 이름 및 유형이 홈 화면에 표시됩니다. 연결 이름을 클릭하면 대상 서버 또는 클러스터에 연결과 연결에 대한 UI 로드를 시도합니다.

![Windows Admin Center 아키텍처](../media/understand-extensions/solutions-ui.png)

이러한 각 연결 형식은 솔루션에 연결되고 "솔루션" 확장이라고 하는 확장 유형을 통해 정의됩니다. 일반적으로 솔루션은 서버, PC 또는 장애 조치 클러스터 등의 Windows Admin Center를 통해 관리하고자 하는 개체의 고유한 유형을 정의합니다. 또한 네트워크 스위치 및 Linux 서버와 같은 다른 장치 또는 원격 데스크톱 서비스와 같은 서비스까지에도 연결하고 관리하기 위한 새로운 솔루션을 정의할 수 있습니다.

## <a name="tool-extensions"></a>도구 확장

Windows Admin Center 홈 화면에서 연결을 클릭하면 선택한 연결 형식에 대한 솔루션 확장이 로드되고 왼쪽 탐색 창의 도구 목록을 포함하는 솔루션 UI와 함께 표시됩니다. 도구를 클릭하면 도구 UI가 로드되고 오른쪽 창에 표시됩니다.

![Windows Admin Center UI 아키텍처](../media/understand-extensions/ui-architecture.png)

이러한 각 도구는 "도구" 확장이라고 하는 두 번째 유형의 확장을 통해 정의됩니다. 도구를 로드할 때 대상 서버 또는 클러스터에서 WMI 호출 또는 PowerShell 스크립트를 실행하고 UI에 정보를 표시하거나 사용자 입력에 따라 명령을 실행할 수 있습니다. 도구 확장은 표시할 솔루션을 정의하여 각 솔루션에 대해 다른 도구 집합을 표시합니다. 새로운 솔루션 확장을 만드는 경우 추가적으로 솔루션에 대한 기능을 제공하는 하나 이상의 도구 확장을 작성할 필요가 있을 수 있습니다.

![각 솔루션에 대한 도구 목록](../media/understand-extensions/tools-for-solutions.png)

## <a name="gateway-plugins"></a>게이트웨이 플러그 인

게이트웨이 서비스는 호출할 UI에 대한 REST API를 노출 대상에서 실행되는 명령 및 스크립트를 릴레이합니다. 다른 프로토콜을 지원하는 게이트웨이 플러그 인으로 게이트웨이 서비스를 확장할 수 있습니다. Windows Admin Center는 각각 PowerShell 스크립트 및 WMI 명령을 실행하기 위한 두 게이트웨이 플러그 인으로 미리 패키지됩니다. PowerShell 또는 WMI가 아닌(예: REST) 프로토콜을 통해 대상과 통신해야 하는 경우 이를 위해 게이트웨이 플러그 인을 만들 수 있습니다.

## <a name="next-steps"></a>다음 단계

Windows Admin Center에서 빌드하려는 기능에 따라 기존 서버 또는 클러스터 솔루션에 대해 [도구 확장을 만드는 것](develop-tool.md)만으로 충분할 수 있으며, 확장을 빌드하는 가장 쉬운 첫 번째 단계입니다. 그러나 기능이 서버 또는 클러스터가 아니라 장치, 서비스, 또는 완전히 새로운 것을 관리하기 위한 것이라면 하나 이상의 도구로 [솔루션 확장을 만드는](develop-solution.md) 것을 고려해야 합니다. 마지막으로, WMI 또는 PowerShell이 아닌 프로토콜을 통해 대상과 통신해야 하는 경우 [게이트웨이 플러그 인을 빌드](develop-gateway-plugin.md)해야 할 수 있습니다. 개발 환경 설정 및 첫 번째 확장을 작성하는 방법을 알아보려면 [계속 읽으십시오](developing-extensions.md).
