---
title: AD FS 문제 해결-AD FS 끝점
description: 이 문서에서는 AD FS 끝점 문제를 해결 하는 방법을 설명 합니다.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/03/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 807b5c5de14bf6a43419d0b9d2d3a4e6953d0075
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366216"
---
# <a name="ad-fs-troubleshooting---ad-fs-metadata-endpoints"></a>AD FS 문제 해결-메타 데이터 끝점 AD FS
끝점은 페더레이션 메타 데이터 게시와 같은 AD FS의 페더레이션 서버 기능에 대 한 액세스를 제공 합니다.  AD FS 서버가 웹 요청에 응답 하는지 확인 하기 위해 다양 한 끝점을 확인할 수 있습니다.


## <a name="federation-metadata-test"></a>페더레이션 메타 데이터 테스트
수동 페더레이션은 브라우저가 AD FS 로그인 페이지로 다시 리디렉션되는 시나리오를 나타냅니다.  메타 데이터 끝점을 테스트 하 여 이러한 수동 시나리오에서 AD FS 서버가 웹 요청에 응답 하는지 확인할 수 있습니다.  다음 절차를 사용 하 여 끝점을 테스트 합니다.

1.  웹 브라우저를 사용 하 여 AD FS 페더레이션 메타 데이터 끝점으로 이동 합니다.  예를 들어  https://sts.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml
2. Xml 파일은 컴퓨터에 로컬로 다운로드 되어야 합니다.
3. 이 파일을 열고 아래 내용은 비슷한 정보가 포함 되어 있는지 확인 합니다. ![Passive](media/ad-fs-tshoot-endpoints/meta2.png)

## <a name="ws-mex-test-active-test"></a>WS MEX 테스트 (활성 테스트)
Ws-metadataexchange는 웹 서비스 프로토콜 이며 WS-FEDERATION 로드맵의 일부입니다.  SOAP 메시지를 사용 하 여 메타 데이터를 요청 합니다.  끝점을 테스트 하 여 AD FS 서버가 Ws-metadataexchange에 대 한 웹 요청에 응답 하는지 확인할 수 있습니다.  다음 절차를 사용 하 여 끝점을 테스트 합니다.
1.  웹 브라우저를 사용 하 여 AD FS 페더레이션 메타 데이터 끝점으로 이동 합니다.  예를 들어  https://sts.contoso.com/adfs/services/trust/mex
2. Xml 파일이 브라우저에 자동으로 표시 됩니다.  아래 이미지와 같습니다.

![활성](media/ad-fs-tshoot-endpoints/meta3.png)


## <a name="next-steps"></a>다음 단계

- [AD FS 문제 해결](ad-fs-tshoot-overview.md)