---
title: 네트워크 인터페이스의 순서 구성
description: 이 항목은 Windows Server 2016에 대 한 네트워크 하위 시스템 성능 조정 가이드의 일부입니다.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 3266328c-ca82-40d2-90ca-854b7088ccaa
manager: dcscontentpm
ms.author: v-tea
author: Teresa-Motiv
ms.openlocfilehash: 9e288908df5f5de70f1e369cff08821b8d178de7
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80862216"
---
# <a name="configure-the-order-of-network-interfaces"></a>네트워크 인터페이스의 순서 구성

>적용 대상: Windows Server(반기 채널), Windows Server 2016

Windows Server 2016 및 Windows 10에서 인터페이스 메트릭을 사용 하 여 네트워크 인터페이스의 순서를 구성할 수 있습니다.

이는 이전 버전의 Windows 및 Windows Server와 다르며, 사용자 인터페이스나 **INetCfgComponentBindings:: MoveBefore** 및 **INetCfgComponentBindings:: movebefore**명령 중 하나를 사용 하 여 네트워크 어댑터의 바인딩 순서를 구성 하는 데 사용할 수 있습니다. 네트워크 인터페이스를 정렬 하는 이러한 두 가지 방법은 Windows Server 2016 및 Windows 10에서 사용할 수 없습니다.

대신 각 어댑터의 인터페이스 메트릭을 구성 하 여 네트워크 어댑터의 열거 순서를 설정 하는 데 새 메서드를 사용할 수 있습니다. [Get-netipinterface](https://docs.microsoft.com/powershell/module/nettcpip/set-netipinterface) Windows PowerShell 명령을 사용 하 여 인터페이스 메트릭을 구성할 수 있습니다.

네트워크 트래픽 경로를 선택 하 고 **get-netipinterface** 명령의 **InterfaceMetric** 매개 변수를 구성한 경우 인터페이스 기본 설정을 결정 하는 데 사용 되는 전체 메트릭은 경로 메트릭과 인터페이스 메트릭의 합계입니다. 일반적으로 인터페이스 메트릭은 유선 및 무선을 모두 사용할 수 있는 경우 유선을 사용 하는 것과 같은 특정 인터페이스에 우선 순위를 부여 합니다.

다음 Windows PowerShell 명령 예제에서는이 매개 변수를 사용 하는 방법을 보여 줍니다.

    Set-NetIPInterface -InterfaceIndex 12 -InterfaceMetric 15

어댑터가 목록에 표시 되는 순서는 IPv4 또는 IPv6 인터페이스 메트릭에 의해 결정 됩니다.  자세한 내용은 [Getadaptersaddresses 함수](https://msdn.microsoft.com/library/windows/desktop/aa365915%28v=vs.85%29.aspx?f=255&MSPPError=-2147217396)를 참조 하세요.

이 가이드의 모든 항목에 대 한 링크는 [네트워크 하위 시스템 성능 튜닝](net-sub-performance-top.md)을 참조 하세요.
