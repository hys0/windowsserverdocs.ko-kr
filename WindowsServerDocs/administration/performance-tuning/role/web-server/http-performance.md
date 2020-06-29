---
title: HTTP 1.1/2에 대 한 성능 조정
description: HTTP 1.1/2에 대 한 성능 튜닝 권장 사항
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: ivanpash; gmonte
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: a0a4464d7a13911ec9cc7d104b6fe9292a64586e
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85471248"
---
# <a name="performance-tuning-http-112"></a>성능 튜닝 HTTP 1.1/2

HTTP/2는 클라이언트 쪽의 성능을 향상 시키기 위한 것입니다 (예: 브라우저의 페이지 로드 시간). 서버에서는 CPU 비용이 약간 증가 하는 것을 나타낼 수 있습니다. 서버는 모든 요청에 대해 더 이상 단일 TCP 연결을 요구 하지 않지만 이제는 이러한 상태 중 일부가 HTTP 계층에 유지 됩니다. 또한 h t t p/2에는 추가 CPU 로드를 나타내는 헤더 압축이 있습니다.

일부 상황에서는 http/1.1 대체 (http/2 연결을 다시 설정 하 고 대신 HTTP/1.1을 사용 하도록 새 연결을 설정) 해야 합니다. 특히 TLS 재협상 및 HTTP 인증 (기본 및 다이제스트 제외)에는 HTTP/1.1 대체가 필요 합니다. 이로 인해 오버 헤드가 발생 하는 경우에도 이러한 작업에는 약간의 지연이 포함 되어 있으므로 특히 성능이 중요 하지 않습니다.

## <a name="additional-references"></a>추가 참조
- [웹 서버 성능 조정](index.md)
- [IIS 10.0 성능 튜닝](tuning-iis-10.md)