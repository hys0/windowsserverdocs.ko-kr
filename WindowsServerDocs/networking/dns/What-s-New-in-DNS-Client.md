---
title: DNS 클라이언트 Windows Server에서의 새로운 기능
description: 이 항목에서는 Windows Server 및 Windows 10에서 DNS 클라이언트의 새로운 기능을 소개
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: 6edaba84-4595-4fd8-95d7-64d4d975a38a
ms.author: pashort
author: shortpatti
ms.openlocfilehash: defe88fe2a1e4f5393be4d5d5938d9f5bfbfb5d6
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="whats-new-in-dns-client-in-windows-server-2016"></a>DNS 클라이언트 Windows Server 2016에서 새로운 기능

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 항목에서는 새로운 또는 변경 된 Windows 10 및 Windows Server 2016와이의 최신 버전의 시스템 DNS (도메인 이름) 클라이언트 기능 설명 운영 체제입니다.
  
## <a name="updates-to-dns-client"></a>DNS 클라이언트에 대 한 업데이트

**DNS 클라이언트 서비스 구속력**: Windows 10에서 DNS 클라이언트 서비스 네트워크 인터페이스 하나 이상을 사용 하는 컴퓨터에 대 한 향상 된 지원을 제공 합니다. 다중 홈 컴퓨터에 대 한 DNS 해상도 다음과 같은 방법으로 최적화 되어 다음과 같습니다.  
  
-   DNS 쿼리에 해결 하기 위해 특정 인터페이스에서 구성 된 DNS 서버를 사용 하면 DNS 클라이언트 서비스 DNS 쿼리에 보내기 전에이 인터페이스에 연결 됩니다.  
  
    결합 하 여 특정 인터페이스 DNS 클라이언트 캔을 명확 하 게 인터페이스 이름 확인 발생 하는 위치를 지정,이 통해 DNS 클라이언트와의 커뮤니케이션 최적화 하기 위해 사용 응용 프로그램 네트워크 인터페이스 합니다.  
  
-   사용 되는 DNS 서버 그룹 정책 설정을에서 이름 정책 테이블 (NRPT 확인) 하 여 지정 하는 경우 DNS 클라이언트 서비스가 특정 인터페이스에 연결 되지 않습니다.  
  
> [!NOTE]  
> Windows Server 2016 및 최신 버전을 실행 하는 컴퓨터에 Windows 10에서 DNS 클라이언트 서비스에 대 한 변경 수도 있습니다.  
  
## <a name="see-also"></a>참조 하십시오  
  
-   [DNS 서버를 Windows Server 2016 새로운 기능](What-s-New-in-DNS-Server.md)  
  

