---
title: DNS (Domain Name System) 문제 해결
description: 이 문서에서는 DNS 문제가 발생 했을 때 데이터를 수집 하는 방법을 소개 합니다.
manager: dcscontentpm
ms.prod: ''
ms.technology: networking-dns
ms.topic: article
ms.author: delhan
ms.date: 8/8/2019
author: Deland-Han
ms.openlocfilehash: 11c52b3beca3afcc0a6bfc8cecee2143dce0f023
ms.sourcegitcommit: c5709021aa98abd075d7a8f912d4fd2263db8803
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2020
ms.locfileid: "76265835"
---
# <a name="troubleshooting-domain-name-system-dns-issues"></a>DNS (Domain Name System) 문제 해결
 
도메인 이름 확인 문제는 클라이언트 쪽 및 서버 쪽 문제로 나눌 수 있습니다. 일반적으로 서버 쪽에서 문제가 발생 하는 것을 확인 하는 경우를 제외 하 고는 클라이언트 쪽 문제 해결을 시작 해야 합니다.

- [DNS 클라이언트 문제 해결](troubleshoot-dns-client.md)

- [DNS 서버 문제 해결](troubleshoot-dns-server.md)
 
## <a name="data-collection"></a>데이터 수집
 
문제가 발생 하는 경우 클라이언트와 서버 쪽 모두에서 동시에 데이터를 수집 하는 것이 좋습니다. 그러나 실제 문제에 따라 DNS 클라이언트 또는 DNS 서버에서 단일 데이터 집합으로 컬렉션을 시작할 수 있습니다.
 
영향을 받는 클라이언트 및 구성 된 DNS 서버에서 Windows 네트워킹 진단을 수집 하려면 다음 단계를 수행 합니다.

1. 클라이언트 및 서버에서 네트워크 캡처를 시작 합니다.

   ```cmd
   netsh trace start capture=yes tracefile=c:\%computername%_nettrace.etl
   ```

2. 다음 명령을 실행 하 여 DNS 클라이언트에서 DNS 캐시를 지웁니다.

   ```cmd
   ipconfig /flushdns
   ```

3. 문제를 재현합니다.

4. 추적 중지 및 저장:

   ```cmd
   netsh trace stop
   ```

5. 각 컴퓨터에서 Nettrace .cab 파일을 저장 합니다. 이 정보는 Microsoft 지원에 문의할 때 유용 합니다.