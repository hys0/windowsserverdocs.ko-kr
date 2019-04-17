---
title: 네트워크 인터페이스 순서를 구성
description: 이 항목은 Windows Server 2016 용 네트워크 하위 시스템 성능 조정 가이드의 일부입니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 3266328c-ca82-40d2-90ca-854b7088ccaa
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 2edf9d312e50a0fd8485e0032dee8413675367cf
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="configure-the-order-of-network-interfaces"></a>네트워크 인터페이스 순서를 구성

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

Windows Server 2016 및 Windows 10에서 한 네트워크 인터페이스 순서를 구성 해야 인터페이스 메트릭을 사용할 수 있습니다.

이 이전 버전의 Windows와 허용 사용자 인터페이스 나 명령을 사용 하 여 네트워크 어댑터의 구속력 순서를 구성 하는 Windows Server 다르게 **INetCfgComponentBindings::MoveBefore** 및 **INetCfgComponentBindings::MoveAfter**합니다. 이러한 두 가지 방법을 한 네트워크 인터페이스 주문에 대 한 Windows 10 및 Windows Server 2016에 사용할 수 없는 경우

대신, 새로운 방법에 구성 각 어댑터의 인터페이스 메트릭 하 여 네트워크 어댑터의 열거 순서를 설정 하는 데 사용할 수 있습니다. 사용 하 여 인터페이스 메트릭 구성할 수는 [설정 NetIPInterface](https://docs.microsoft.com/en-us/powershell/module/nettcpip/set-netipinterface) Windows PowerShell 명령 합니다.

네트워크 교통 경로 선택 하는 시간과 구성한 경우는 **InterfaceMetric** 매개는 **설정 NetIPInterface** 명령을 인터페이스 기본 설정을 확인 하는 데 사용 되는 전반적인 메트릭은 경로 미터 및 인터페이스 메트릭 합계 합니다. 일반적으로 인터페이스 메트릭 유선 모두 및 무선 사용할 수 있는 경우 유선 사용 하는 등의 특정 인터페이스에 기본을 제공 합니다.

다음 Windows PowerShell 명령 예제이 매개 변수를 사용 합니다.

    Set-NetIPInterface -InterfaceIndex 12 -InterfaceMetric 15

어댑터 목록에 표시 되는 순서 IPv4 또는 IPv6 인터페이스 메트릭에 의해 결정 됩니다.  자세한 내용은 참조 [GetAdaptersAddresses 기능](https://msdn.microsoft.com/library/windows/desktop/aa365915%28v=vs.85%29.aspx?f=255&MSPPError=-2147217396)합니다.

이 가이드의 모든 항목에 대 한 링크를 참조 하세요. [네트워크 하위 시스템 성능 조정](net-sub-performance-top.md)합니다.
