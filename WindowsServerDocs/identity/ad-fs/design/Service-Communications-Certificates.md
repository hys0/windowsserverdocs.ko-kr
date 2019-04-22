---
ms.assetid: 95e82190-68c5-4e40-87b1-f1bd816ef4e9
title: '서비스 통신 인증서:'
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 32e60f2c2d9e4fced04061ace44882b792e1a3bc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825654"
---
# <a name="service-communications-certificates"></a>서비스 통신 인증서:

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

WCF 메시지 보안이 사용 되는 시나리오에 대 한 서비스 통신 인증서를 사용을 해야 하는 페더레이션 서버입니다.  
  
## <a name="service-communication-certificate-requirements"></a>서비스 통신 인증서 요구 사항  
서비스 통신 인증서는 AD FS와 작동 하도록 다음 요구 사항을 충족 해야 합니다.  
  
-   서비스 통신 인증서 서버의 향상 된 인증 키 사용을 포함 해야 합니다 \(EKU\) 확장 합니다.  
  
-   인증서 해지 목록 \(Crl\) 루트 CA 인증서에서 서비스 통신 인증서 체인에 있는 모든 인증서에 액세스할 수 있어야 합니다. 모든 페더레이션 서버 프록시와 페더레이션 서버에이 신뢰 하는 웹 서버도 루트 CA를 신뢰 해야 합니다.  
  
-   서비스 통신 인증서에 사용 되는 주체 이름에는 페더레이션 서비스의 속성에서 페더레이션 서비스 이름과 일치 해야 합니다.  
  
## <a name="deployment-considerations-for-service-communication-certificates"></a>서비스 통신 인증서에 대 한 배포 고려 사항  
모든 페더레이션 서버는 동일한 인증서를 사용할 수 있도록 서비스 통신 인증서를 구성 합니다. 페더레이션 웹 단일 배포 하는 경우\-기호\-온 \(SSO\) 디자인 권장 공용 CA에서 서비스 통신 인증서를 발행 하는 합니다. 요청 하 고 IIS 관리자 스냅인을 통해 이러한 인증서를 설치할 수 있습니다\-에서 합니다.  
  
자체를 사용할 수 있습니다\-서명 서비스 통신 인증서는 테스트 랩 환경의 페더레이션 서버에서 성공적으로 합니다. 그러나 프로덕션 환경에 대 한 공용 CA에서 서비스 통신 인증서를 가져와야 하는 것이 좋습니다. 다음 가지가 이유를 사용 하지 않아야 자체\-서명 서비스 통신 인증서 라이브 배포:  
  
-   자체\-서명 된 SSL 인증서에 추가 해야 각 리소스 파트너 조직의 페더레이션 서버에서 신뢰할 수 있는 루트 저장소입니다. 이 단독으로 않습니다 하지을 사용 하면 리소스 페더레이션 서버를 손상 시키는 공격자를 자체 신뢰\-서명 된 인증서를 사용 하는 컴퓨터의 공격 표면을 늘어나지 및 서명자 인증서가 없는 경우 보안 취약성이 발생할 수 있습니다 신뢰할 수 있는 합니다.  
  
-   잘못 된 사용자 환경을 만듭니다. 클라이언트는 다음과 같은 메시지가 표시 되는 연결된 된 리소스에 액세스 하려고 할 때 보안 경고 프롬프트 받습니다. "보안 인증서를 신뢰 하도록 선택 하지 않은 회사에서 발급 되었습니다." 예상 되는 동작, 때문에 자체\-서명 된 인증서를 신뢰할 수 없습니다.  
  
    > [!NOTE]  
    > 하는 경우 필요에 따라 해결할 수 있습니다이 조건을 자체 수동으로 밀어 넣는 데 그룹 정책을 사용 하 여\-AD FS 사이트에 액세스 하려고 하는 각 클라이언트 컴퓨터에서 신뢰할 수 있는 루트 저장소에 인증서를 서명 합니다.  
  
-   추가 인증서를 제공 하는 CAs\-등의 기능, 개인 키 보관, 갱신, 해지, 자체에서 제공 되지 않는 기반\-서명 된 인증서입니다.  
  

