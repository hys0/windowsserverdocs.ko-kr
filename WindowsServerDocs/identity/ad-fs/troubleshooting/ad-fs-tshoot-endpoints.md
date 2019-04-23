---
title: AD FS 문제 해결-AD FS 끝점
description: 이 문서에서는 AD FS 끝점을 해결 하는 방법 설명
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/03/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 13b830c0317341280bd87499e3abd8dcd1a33fc2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857564"
---
# <a name="ad-fs-troubleshooting---ad-fs-metadata-endpoints"></a>AD FS 문제 해결-AD FS 메타 데이터 끝점
끝점의 페더레이션 메타 데이터 게시와 같은 AD FS 페더레이션 서버 기능에 대 한 액세스를 제공합니다.  AD FS 서버가 웹 요청에 응답 하는지 확인 하려면 다양 한 끝점을 확인할 수 있습니다.


## <a name="federation-metadata-test"></a>페더레이션 메타 데이터 테스트
패시브 페더레이션 시나리오를 브라우저는 AD FS 로그인 페이지로 리디렉션될를 가리킵니다.  메타 데이터 끝점을 테스트 하 여 AD FS 서버에 이러한 수동 시나리오에서 웹 요청에 응답 하는지 확인할 수 있습니다.  끝점을 테스트 하려면 다음 절차를 따르십시오.

1.  웹 브라우저를 사용 하 여 AD FS 페더레이션 메타 데이터 끝점으로 이동 합니다.  예를 들어  https://sts.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml
2. Xml 파일을 컴퓨터에 로컬로 다운로드 해야 합니다.
3. 이 열고 아래 정보 유사한 정보가 포함 되어 있는지 확인 합니다. ![수동](media/ad-fs-tshoot-endpoints/meta2.png)

## <a name="ws-mex-test-active-test"></a>WS-MEX 테스트 (활성 테스트)
Ws-metadataexchange는 웹 서비스 프로토콜 및 Ws-federation 로드맵의 일부입니다.  SOAP 메시지를 사용 하 여 메타 데이터를 요청 합니다.  끝점을 테스트 하 여 Ws-metadataexchange에 대 한 AD FS 서버에 웹 요청에 응답 하는지 확인할 수 있습니다.  끝점을 테스트 하려면 다음 절차를 따르십시오.
1.  웹 브라우저를 사용 하 여 AD FS 페더레이션 메타 데이터 끝점으로 이동 합니다.  예를 들어  https://sts.contoso.com/adfs/services/trust/mex
2. Xml 파일을 자동으로 브라우저에 표시 해야 합니다.  아래 이미지와 같아야 합니다.

![활성](media/ad-fs-tshoot-endpoints/meta3.png)


## <a name="next-steps"></a>다음 단계

- [AD FS 문제 해결](ad-fs-tshoot-overview.md)