---
title: WINS(Windows Internet Name Service)
description: 이 항목에서는 WINS를 서비스 해제 하 고 네트워크에서 이름 확인 서비스에 DNS를 사용 하는 방법에 대해 설명 합니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 32eabe7d-1130-4001-a79a-8ddb31993e5b
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 54e3f69500ccb3dbf6b2dfe47f6dd035e0a20511
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80315159"
---
#  <a name="windows-internet-name-service-wins"></a>WINS(Windows Internet Name Service)

>적용 대상: Windows Server(반기 채널), Windows Server 2016

Windows 인터넷 이름 서비스(WINS)는 IP 주소에 NetBIOS 이름을 매핑하는 기존의 컴퓨터 이름 등록 및 확인 서비스입니다.

네트워크에 WINS를 아직 배포 하지 않은 경우 WINS를 배포 하지 말고 DNS\)\(도메인 이름 시스템을 배포 합니다. DNS는 또한 컴퓨터 이름 등록 및 확인 서비스를 제공 하며, Active Directory Domain Services와의 통합과 같이 WINS에 비해 많은 추가 이점을 제공 합니다.

자세한 내용은 [DNS (Domain Name System)](https://docs.microsoft.com/windows-server/networking/dns/dns-top) 를 참조 하세요.

네트워크에 WINS를 이미 배포한 경우에는 DNS를 배포한 다음 WINS를 서비스 해제 하는 것이 좋습니다.
