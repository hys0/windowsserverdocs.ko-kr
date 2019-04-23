---
title: Windows Server에서 DNS 클라이언트의 새로운 기능
description: 이 항목에서는 Windows Server 및 Windows 10에서 DNS 클라이언트의 새로운 기능의 개요를 제공합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: 6edaba84-4595-4fd8-95d7-64d4d975a38a
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 34b1a64465e217fbd7e6b3ae55e89832a7a4e48c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59860564"
---
# <a name="whats-new-in-dns-client-in-windows-server-2016"></a>Windows Server 2016에서에서 DNS 클라이언트의 새로운 기능

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 Windows 10 및 Windows Server 2016 및 이후 버전의 이러한 운영 체제의 새롭거나 변경 된 도메인 이름 시스템 (DNS) 클라이언트 기능을 설명 합니다.
  
## <a name="updates-to-dns-client"></a>DNS 클라이언트에 대 한 업데이트

**DNS 클라이언트 서비스 바인딩을**: Windows 10에서 DNS 클라이언트 서비스는 둘 이상의 네트워크 인터페이스를 사용 하 여 컴퓨터에 대 한 향상 된 지원을 제공합니다. 다중 홈 컴퓨터에 대 한 DNS 확인은 다음과 같은 방법으로 최적화:  
  
-   DNS 쿼리를 확인 하는 특정 인터페이스에 구성 된 DNS 서버를 사용 하면 DNS 클라이언트 서비스는 DNS 쿼리를 보내기 전에이 인터페이스에 바인딩합니다.  
  
    DNS 클라이언트 가능 특정 인터페이스를 명확 하 게 바인딩하여 이름 확인이 수행 하는 인터페이스,이 통해 DNS 클라이언트와의 통신을 최적화 하기 위해 사용 하도록 설정 하면 응용 프로그램 네트워크 인터페이스 포함 됩니다.  
  
-   사용 되는 DNS 서버 이름 확인 정책 테이블 (NRPT)에서 그룹 정책 설정을 통해 지정 되는 경우 DNS 클라이언트 서비스는 특정 인터페이스에 바인딩하지 않습니다.  
  
> [!NOTE]  
> Windows 10에서 DNS 클라이언트 서비스에 Windows Server 2016 및 이후 버전을 실행 하는 컴퓨터에도 있습니다.  
  
## <a name="see-also"></a>참조  
  
-   [Windows Server 2016의에서 DNS 서버의 새로운 기능](What-s-New-in-DNS-Server.md)  
  

