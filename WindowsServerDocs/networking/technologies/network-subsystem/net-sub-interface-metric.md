---
title: 네트워크 인터페이스의 순서 구성
description: 이 항목은 Windows Server 2016에 대 한 네트워크 하위 시스템 성능 튜닝 지침의 일부입니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 3266328c-ca82-40d2-90ca-854b7088ccaa
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 18bc9a268b4e69e4b87b6b1e310f1162473adb10
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59821774"
---
# <a name="configure-the-order-of-network-interfaces"></a>네트워크 인터페이스의 순서 구성

>적용 대상: Windows Server (반기 채널), Windows Server 2016

Windows Server 2016 및 Windows 10에서 네트워크 인터페이스의 순서를 구성 하려면 인터페이스 메트릭을 사용할 수 있습니다.

이 이전 버전의 Windows 및 Windows Server 사용자 인터페이스 또는 명령을 사용 하 여 네트워크 어댑터의 바인딩 순서를 구성할 수 있는 다릅니다 **INetCfgComponentBindings::MoveBefore**하 고 **INetCfgComponentBindings::MoveAfter**합니다. 네트워크 인터페이스를 순서에 대 한 이러한 두 가지 방법 Windows Server 2016 및 Windows 10에서 사용할 수 없는 경우

대신, 각 어댑터의 인터페이스 메트릭을 구성 하 여 네트워크 어댑터의 열거 된 순서를 설정 하는 것에 대 한 새 메서드를 사용할 수 있습니다. 사용 하 여 인터페이스 메트릭을 구성할 수 있습니다 합니다 [집합 NetIPInterface](https://docs.microsoft.com/powershell/module/nettcpip/set-netipinterface) Windows PowerShell 명령입니다.

때 네트워크 트래픽을 경로 선택 되 고 구성 합니다 **InterfaceMetric** 의 매개 변수를 **집합 NetIPInterface** 명령을 인터페이스를 확인 하는 데 사용 되는 전체 메트릭 기본 설정 경로 메트릭 및 인터페이스 메트릭을의 합계가 표시 됩니다. 일반적으로 인터페이스 메트릭을 모두 유선 및 무선 사용할 경우 연결을 사용 하는 등의 특정 인터페이스에 우선 순위를 제공 합니다.

다음 Windows PowerShell 명령 예제는이 매개 변수 사용 방법을 보여 줍니다.

    Set-NetIPInterface -InterfaceIndex 12 -InterfaceMetric 15

어댑터 목록에 표시 되는 순서는 IPv4 또는 IPv6 인터페이스 메트릭을 기준으로 결정 됩니다.  자세한 내용은 [GetAdaptersAddresses 함수](https://msdn.microsoft.com/library/windows/desktop/aa365915%28v=vs.85%29.aspx?f=255&MSPPError=-2147217396)합니다.

이 가이드의 모든 항목에 대 한 링크를 참조 하세요 [네트워크 하위 시스템 성능 튜닝](net-sub-performance-top.md)합니다.
