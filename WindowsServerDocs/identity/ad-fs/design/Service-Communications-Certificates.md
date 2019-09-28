---
ms.assetid: 95e82190-68c5-4e40-87b1-f1bd816ef4e9
title: '서비스 통신 인증서:'
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 624d2e26bc0277129e44eee3fdce7c7396b735a0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407902"
---
# <a name="service-communications-certificates"></a>서비스 통신 인증서:

페더레이션 서버는 WCF 메시지 보안이 사용 되는 시나리오에 서비스 통신 인증서를 사용 해야 합니다.  
  
## <a name="service-communication-certificate-requirements"></a>서비스 통신 인증서 요구 사항  
AD FS를 사용 하려면 서비스 통신 인증서가 다음 요구 사항을 충족 해야 합니다.  
  
-   서비스 통신 인증서에는 서버 인증 확장 키 사용 \(EKU @ no__t-1 확장을 포함 해야 합니다.  
  
-   인증서 해지 목록 \(CRLs @ no__t-1은 서비스 통신 인증서에서 루트 CA 인증서로의 체인에 있는 모든 인증서에 액세스할 수 있어야 합니다. 또한이 페더레이션 서버를 신뢰 하는 페더레이션 서버 프록시와 웹 서버에서 루트 CA를 신뢰 해야 합니다.  
  
-   서비스 통신 인증서에 사용 되는 주체 이름은 페더레이션 서비스 속성의 페더레이션 서비스 이름과 일치 해야 합니다.  
  
## <a name="deployment-considerations-for-service-communication-certificates"></a>서비스 통신 인증서에 대 한 배포 고려 사항  
모든 페더레이션 서버에서 동일한 인증서를 사용 하도록 서비스 통신 인증서를 구성 합니다. 페더레이션된 웹 Single @ no__t-0Sign @ no__t \(SSO @ no__t 디자인을 배포 하는 경우 공용 CA에서 서비스 통신 인증서를 발급 하는 것이 좋습니다. 에서 IIS 관리자 snap @ no__t-0in를 통해 이러한 인증서를 요청 하 고 설치할 수 있습니다.  
  
테스트 랩 환경의 페더레이션 서버에서 자체 @ no__t-0 서명 된 서비스 통신 인증서를 사용할 수 있습니다. 그러나 프로덕션 환경에서는 공용 CA에서 서비스 통신 인증서를 가져오는 것이 좋습니다. 다음은 live 배포에 대해 self @ no__t-0signed, 서비스 통신 인증서를 사용 하지 않아야 하는 이유입니다.  
  
-   리소스 파트너 조직의 각 페더레이션 서버에 있는 신뢰할 수 있는 루트 저장소에 self @ no__t-0signed, SSL 인증서를 추가 해야 합니다. 이 만으로 공격자가 리소스 페더레이션 서버를 손상 시킬 수 있는 것은 아니지만 self @ no__t-0signed 인증서를 신뢰 하면 컴퓨터의 공격 노출 영역이 증가 하 고, 인증서 서명자가 없는 경우 보안 취약성이 발생할 수 있습니다. 신뢰성이.  
  
-   잘못 된 사용자 환경을 만듭니다. 클라이언트는 다음 메시지를 표시 하는 페더레이션된 리소스에 액세스 하려고 할 때 보안 경고 메시지를 받게 됩니다. "신뢰 하도록 선택한 회사에서 보안 인증서를 발급 했습니다." 이는 self @ no__t-0signed 된 인증서를 신뢰할 수 없기 때문에 예상 되는 동작입니다.  
  
    > [!NOTE]  
    > 필요한 경우 그룹 정책를 사용 하 여 AD FS 사이트에 액세스를 시도 하는 각 클라이언트 컴퓨터의 신뢰할 수 있는 루트 저장소로 self @ no__t-0signed 인증서를 수동으로 푸시하는 방법으로이 문제를 해결할 수 있습니다.  
  
-   Ca는 자체 @ no__t-1로 서명 된 인증서에서 제공 하지 않는 개인 키 보관, 갱신 및 해지와 같은 추가 인증서 @ no__t-0based 기능을 제공 합니다.  
  

