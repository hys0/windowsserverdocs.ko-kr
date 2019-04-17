---
title: Windows 인터넷 이름 서비스 WINS)
description: 이 항목 제거 WINS 및 DNS 네트워크의 이름 확인 서비스에 대 한 사용에 대 한 정보를 제공 합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 32eabe7d-1130-4001-a79a-8ddb31993e5b
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 5a3d132ada7b1ede83b046499058399a9da12190
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
#  <a name="windows-internet-name-service-wins"></a>Windows 인터넷 이름 서비스 WINS)

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

Windows 이름 WINS (인터넷 서비스) 레거시 컴퓨터 이름 등록 하 고 해결 하는 서비스 IP 주소를 NetBIOS 이름을 컴퓨터 지도입니다.

네트워크에 배포 WINS 아직 없는 경우 수행 하지 배포 WINS-대신, Domain Name System \(DNS\)를 배포 합니다. DNS는 컴퓨터 이름을 등록 및 해상도 서비스를 제공 하 고 많은 다른 이점도 WINS 통해 Active Directory 도메인 서비스와의 통합 같은 수도 있습니다.

자세한 내용은 참조 [시스템 DNS (도메인 이름)](https://docs.microsoft.com/windows-server/networking/dns/dns-top)

네트워크에 이미 WINS를 배포 하는 경우 DNS 배포 WINS을 제거 하는 것이 좋습니다.
