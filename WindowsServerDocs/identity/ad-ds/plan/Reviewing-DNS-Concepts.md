---
ms.assetid: 133474ee-316d-4b1c-acc6-ad5434a064d5
title: "DNS 개념을 검토"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 29c4c3d1d785d1b3b1fa1926eca8298aab2b3ee3
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="reviewing-dns-concepts"></a>DNS 개념을 검토

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

시스템 DNS (도메인 이름)은 네임 나타내는 분산된 데이터베이스 합니다. 네임 클라이언트가 이름을 조회 하는 데 필요한 정보를 모두 포함 됩니다. DNS 서버 네임 스페이스에서 든 이름에 대 한 쿼리가 응답할 수 있습니다. DNS 서버 다음 방법 중 하나에 쿼리에 응답:  
  
-   대답을 해당 캐시에 한 경우 캐시에서 쿼리에 응답 합니다.  
  
-   DNS 서버에서 주최한 영역에 대 한 대답 경우, 해당 영역에서 쿼리에 응답 합니다. 영역에는 DNS 서버에 저장 된 DNS 나무의 일부입니다. 이 이름에 해당 영역에 대 한 권한이 DNS 서버가 영역을 호스트 (즉, DNS 서버 수 쿼리에 응답 모든 이름 영역에 대 한). 예를 들어, 영역 contoso.com 호스트 하는 서버 contoso.com에 모든 이름에 대 한 쿼리가 응답할 수 있습니다.  
  
-   서버에서 캐시 나 영역 쿼리 응답할 수 없는, 다른 서버에 대 한 대답이 쿼리.  
  
되므로 DNS의 핵심 기능 위임, 반복 이름 확인 DNS Active Directory 통합 영역 등을 알아야 Active Directory 논리 구조 디자인에 직접적인 영향을 미칠 것입니다.  
  
DNS (AD DS) Active Directory Domain Services에 대 한 자세한 내용은 참조 [DNS 및 AD DS](../../ad-ds/plan/DNS-and-AD-DS.md)합니다.  
  
## <a name="delegation"></a>위임  
쿼리 모든 이름에 대 한 대답 DNS 서버를에 대 한 모든 영역 네임에 직접 경로 있어야 합니다. 이러한 경로 위임을 사용 하 여 만들어집니다. 위임 계층 다음 수준에서 영역에 대 한 권한이 있는 이름을 서버 나열 된 부모 영역에 기록입니다. 위임 수 있도록 서버에 있는 다른 영역 서버에 클라이언트 부르고 한 영역에 대 한 합니다. 다음은 위임 중 한 가지 예입니다.  
  
![DNS 개념](../../media/Reviewing-DNS-Concepts/0c24b576-d41a-4e5d-ad3d-6be81e095835.gif)  
  
DNS 서버의 루트 섬에는 점 표현 루트 영역 (합니다. ). 루트 영역 영역 다음 수준의 계층 com 영역에 위임 포함 되어 있습니다. 루트 영역에서 위임, com 영역을 찾으려면 것 서버에 연결 해야 Com 루트 DNS 서버를 알려 줍니다. 마찬가지로, com 영역에 위임 알려주는 Com 서버를 contoso.com 영역을 찾으려면 것 서버에 연결 해야 Contoso 합니다.  
  
> [!NOTE]  
> 위임 두 가지 유형의 기록 사용합니다. 이름 (NS) 서버 리소스 레코드 권한 있는 서버의 이름을 제공 합니다. 호스트 (는) 및 리소스 레코드 (AAAA) 호스트 IP IPv4 버전 4 () 및 IP 버전 6 (IPv6) 주소 제공 권한 있는 서버 합니다.  
  
이 시스템 영역과 위임 계층 트리 DNS 네임을 만듭니다. 각 영역에에서 계층 나타내며 각 위임 나무의 분기 합니다.  
  
영역과 위임 계층을 사용 하 여 DNS 루트 서버 DNS 네임 스페이스에서 이름을 찾을 수 있습니다. 루트 영역 위임 계층에서 다른 모든 영역을 직접 나 간접 사항이 포함 되어 있습니다. DNS 서버의 루트 쿼리 수 있는 모든 서버 네임에서 든 이름을 찾습니다 위임에서 정보를 사용할 수 있습니다.  
  
## <a name="recursive-name-resolution"></a>반복 이름 확인  
반복 이름 확인 DNS 서버 영역과 위임 계층 신뢰할 수 없는 하지는 쿼리에 응답을 사용 하는 프로세스입니다.  
  
일부 구성 DNS 서버 쿼리 루트 DNS 서버를 사용할 수 있도록 루트 힌트 (즉, 목록이 이름 및 IP 주소)를 포함 합니다. 다른 구성 서버 다른 서버에 응답할 수 있는 모든 쿼리를 전달 합니다. 전달 및 루트 힌트에 DNS 서버 신뢰할 수 없는 하지는 쿼리를 확인 하는 데 사용할 수 있는 두 가지가 있습니다.  
  
### <a name="resolving-names-by-using-root-hints"></a>이름 루트 힌트를 사용 하 여 확인  
루트 힌트 루트 DNS 서버를 찾을 수 있는 DNS 서버를 사용 합니다. DNS 서버 루트 DNS 서버를 찾으면 네임 스페이스 쿼리를 해결할 수 있습니다. 다음 그림에서는 루트 힌트를 사용 하 여 DNS 이름을 확인 하는 방법을 설명 합니다.  
  
![DNS 개념](../../media/Reviewing-DNS-Concepts/1c044845-b104-4262-a7af-474ba3558a85.gif)  
  
여기에서 다음과 같은 이벤트가 발생합니다.  
  
1.  클라이언트 반복 쿼리를 ftp.contoso.com 이름에 해당 하는 IP 주소를 요청할 수 DNS 서버를 보냅니다. 반복 쿼리 쿼리에 대 한 명확한 응답 사실 나타냅니다. 올바른 주소 또는 주소를 찾을 수 없음을 알리는 메시지가 반복 쿼리에 응답 여야 합니다.  
  
2.  DNS 서버가 하지 이름에 대 한 권한을 보유 하 고 해당 캐시에 대 한 답을가지고 있지 않습니다, 있으므로 DNS 서버 루트 힌트를 사용 하 여 DNS 서버의 루트 IP 주소를 찾습니다.  
  
3.  DNS 서버 반복 쿼리를 사용 하 여 이름을 ftp.contoso.com 확인 하기 위해 루트 DNS 서버를 받아야 합니다. 반복 쿼리 서버 쿼리에 대 한 명확한 응답 대신 다른 서버에 문의 수락할 수 있는지를 나타냅니다. 이름을 ftp.contoso.com 레이블으로 끝나는 때문에, com 루트 DNS 서버 조회 com 영역 호스트 하는 Com 서버를 반환 합니다.  
  
4.  DNS 서버가 반복 쿼리를 사용 하 여 Com 서버 ftp.contoso.com 이름을 확인 하기 위해 요청 합니다. 이름이 ftp.contoso.com contoso.com 이름으로 끝나는, Com 서버 반환 조회 Contoso 서버에는 contoso.com 호스트 영역 합니다.  
  
5.  DNS 서버 반복 쿼리를 사용 하 여 ftp.contoso.com 이름을 확인 하려면 Contoso 서버를 받아야 합니다. Contoso 서버 해당 영역 데이터에 대 한 대답을 찾을 하 고 서버에 대 한 대답을 반환 합니다.  
  
6.  서버 결과 클라이언트를 반환합니다.  
  
### <a name="resolving-names-by-using-forwarding"></a>전달을 사용 하 여 이름을 확인  
전달 특정 서버의 루트 힌트를 사용 하는 대신 통해 경로 이름 확인 할 수 있습니다. 다음 그림에서는 전달을 사용 하 여 DNS 이름을 확인 하는 방법을 설명 합니다.  
  
![DNS 개념](../../media/Reviewing-DNS-Concepts/05bc2eb0-1033-4e53-ae30-244fa247d000.gif)  
  
여기에서 다음과 같은 이벤트가 발생합니다.  
  
1.  클라이언트는 ftp.contoso.com 이름에 대 한 DNS 서버를 쿼리.  
  
2.  DNS 서버 쿼리 전달자 이라고 다른 DNS 서버를 전달 됩니다.  
  
3.  이름에 대 한 권한이 전달자를 해당 캐시에 대 한 답을가지고 있지 않습니다 때문 DNS 서버의 루트 IP 주소를 찾습니다 루트 힌트를 사용 합니다.  
  
4.  전달자 반복 쿼리를 사용 하 여 이름을 ftp.contoso.com 확인 하기 위해 루트 DNS 서버를 받아야 합니다. 이름으로 끝나는 ftp.contoso.com 이름 하기 때문에, com 루트 DNS 서버 조회 com 영역 호스트 하는 Com 서버를 반환 합니다.  
  
5.  전달자 반복 쿼리를 사용 하 여 ftp.contoso.com 이름을 확인 하려면 Com 서버를 받아야 합니다. 이름이 ftp.contoso.com contoso.com 이름으로 끝나는, Com 서버 반환 조회 Contoso 서버에는 contoso.com 호스트 영역 합니다.  
  
6.  전달자 반복 쿼리를 사용 하 여 ftp.contoso.com 이름을 확인 하려면 Contoso 서버를 받아야 합니다. Contoso 서버 해당 영역 파일에 대 한 대답을 찾을 하 고 서버에 대 한 대답을 반환 합니다.  
  
7.  전달자 결과 원래 DNS 서버를 반환합니다.  
  
8.  원래 DNS 서버 결과 클라이언트를 반환합니다.  
  


