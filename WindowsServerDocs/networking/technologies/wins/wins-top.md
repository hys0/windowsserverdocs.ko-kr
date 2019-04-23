---
title: WINS(Windows Internet Name Service)
description: 이 항목에서는 WINS를 서비스 해제 및 네트워크에서 이름 확인 서비스에 대 한 DNS를 사용 하는 방법에 대 한 정보를 제공 합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 32eabe7d-1130-4001-a79a-8ddb31993e5b
ms.author: pashort
author: shortpatti
ms.openlocfilehash: bbc1871d29021aa3c99f14368a4711dac63f4cee
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59843634"
---
#  <a name="windows-internet-name-service-wins"></a>WINS(Windows Internet Name Service)

>적용 대상: Windows Server (반기 채널), Windows Server 2016

Windows 인터넷 이름 서비스(WINS)는 IP 주소에 NetBIOS 이름을 매핑하는 기존의 컴퓨터 이름 등록 및 확인 서비스입니다.

네트워크에 배포 하는 WINS 아직 없는 경우 수행 하지 대신 WINS-배포, 배포 Domain Name System \(DNS\)합니다. 또한 DNS 컴퓨터 이름 등록 및 확인 서비스를 제공 하 고 Active Directory Domain Services 통합 같은 WINS를 통해 다양 한 추가 이점을 포함 합니다.

자세한 내용은 참조 하세요. [도메인 이름 시스템 (DNS)](https://docs.microsoft.com/windows-server/networking/dns/dns-top)

네트워크에 WINS를 이미 배포한 경우 DNS 배포 후 WINS를 해제 하는 것이 좋습니다.
