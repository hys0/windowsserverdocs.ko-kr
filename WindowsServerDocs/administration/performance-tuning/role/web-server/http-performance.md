---
title: HTTP 1.1/2를 위한 성능 튜닝
description: 성능 튜닝 권장 사항에 대 한 HTTP 1.1/2
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: IvanPash; GMonte
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: bf85efa88e377966135c23a548119f19c39cceba
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59866374"
---
# <a name="performance-tuning-http-112"></a>성능 튜닝 HTTP 1.1/2

HTTP/2 (예를 들어, 페이지 로드 시간을 브라우저에서) 클라이언트 쪽에서 성능을 향상 시키는 것입니다. 서버에서 CPU 비용이 약간의 증가 나타낼 수 있습니다. 서버 모든 요청에 대 한 하나의 TCP 연결에서 더 이상 요구 하는 반면 해당 상태의 일부 이제에 보관 됩니다 HTTP 계층입니다. 또한 HTTP/2에 추가 CPU 로드를 나타내는 헤더 압축 합니다.

일부 경우는 HTTP/1.1 (HTTP/2 연결을 다시 설정 하 고 대신 HTTP/1.1을 사용 하 여 새 연결을 설정) 대체 (fallback) 필요 합니다. 특히, TLS 협상 및 HTTP 인증 (기본 및 다이제스트) 이외에 HTTP/대체 (fallback) 1.1 필요합니다. 오버 헤드를 추가 하는 경우에 이러한 작업 이미 약간의 지연이 의미 하 고 특히 성능 구분 되지 않아.

## <a name="see-also"></a>참조
- [웹 서버 성능 조정](index.md) 
- [IIS 10.0 성능 튜닝](tuning-iis-10.md)