---
ms.assetid: 133474ee-316d-4b1c-acc6-ad5434a064d5
title: DNS 개념 검토
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/08/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: d077ecc30caca9b8f3b382af624121fec729afae
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890504"
---
# <a name="reviewing-dns-concepts"></a>DNS 개념 검토

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

도메인 이름 시스템 (DNS)는 네임 스페이스를 나타내는 분산된 데이터베이스. 네임 스페이스 모든 클라이언트가 모든 이름을 조회 하는 데 필요한 정보를 포함 합니다. 모든 DNS 서버는 해당 네임 스페이스 내에서 모든 이름에 대 한 쿼리에 응답할 수 있습니다. 다음 방법 중 하나에서 쿼리에 응답 하는 DNS 서버:  
  
- 사용 중인 캐시 하는 경우 캐시에서 쿼리를 응답 합니다.  
- 사용 중인 DNS 서버에서 호스트 된 영역에 있는 경우 해당 영역에서 쿼리에 응답 합니다. 영역에는 DNS 서버에 저장 하는 DNS 트리의 한 부분입니다. 해당 영역에 있는 이름에 대 한 권한이 있는 DNS 서버에서 영역을 호스트 하는 경우 (즉, DNS 서버 대답할 수 쿼리 영역에서 모든 이름에 대 한). 예를 들어 영역 contoso.com을 호스팅하는 서버에서 contoso.com의 모든 이름에 대 한 쿼리에 응답할 수 있습니다.  
- 서버는 캐시 또는 영역에서 쿼리에 응답할 수 없는, 답을 다른 서버를 쿼리 합니다.  

것은 Active Directory 논리 구조 디자인에 직접적인 영향을 했기 때문에 Active Directory 통합 DNS 영역 위임, 재귀적 이름 확인 등, DNS의 핵심 기능을 이해 하는 것이 중요 합니다.  
  
DNS 및 Active Directory 도메인 서비스 (AD DS)에 대 한 자세한 내용은 참조 [DNS 및 AD DS](../../ad-ds/plan/DNS-and-AD-DS.md)합니다.  
  
## <a name="delegation"></a>위임

모든 이름에 대 한 쿼리에 응답 하기 위해 DNS 서버에 대 한 네임 스페이스의 모든 영역에 직접 또는 간접 경로 있어야 합니다. 이러한 경로 위임을 사용 하 여 생성 됩니다. 위임을 계층 구조의 다음 수준에 영역에 대 한 권한이 있는 이름 서버를 나열 하는 부모 영역의 레코드입니다. 위임 있게 한 영역의 다른 영역에는 서버에 클라이언트를 참조 하는 서버에 대 한 합니다. 다음 그림에서는 위임의 한 가지 예를 보여 줍니다.  
  
![DNS 개념](../../media/Reviewing-DNS-Concepts/0c24b576-d41a-4e5d-ad3d-6be81e095835.gif)  
  
DNS 루트 서버 호스트 점으로 표시 하는 루트 영역 (합니다. ). 루트 영역에는 다음 수준의 com 영역 계층 구조를 사용 하 여 영역에 대 한 위임을 포함 되어 있습니다. 루트 영역에 위임, com 영역을 찾으려면이 서버에 연결 해야 Com DNS 루트 서버를 알려 줍니다. 마찬가지로, com 영역에서 위임을 Com 서버에 알립니다, contoso.com 영역을 찾으려면를 연결 해야는 Contoso 서버.  
  
> [!NOTE]  
> 위임을 두 종류의 레코드를 사용합니다. 이름 서버 (NS) 리소스 레코드에는 신뢰할 수 있는 서버의 이름을 제공합니다. 호스트 (A) 및 호스트 (AAAA) 리소스 레코드 IP 버전 4 (IPv4) 및 IP 버전 6 (IPv6)의 제공 권한이 있는 서버.  
  
이 시스템의 영역 및 위임 DNS 네임 스페이스를 나타내는 계층적 트리를 만듭니다. 각 영역 계층 구조에서는 계층을 나타내며 각 위임 트리의 분기를 나타냅니다.  
  
영역 및 위임의 계층 구조를 사용 하 여 DNS 루트 서버 DNS 네임 스페이스에 임의의 이름을 찾을 수 있습니다. 루트 영역 계층 구조에서 다른 모든 영역에 직접 또는 간접적으로 이어지는 위임이 포함 되어 있습니다. DNS 루트 서버를 쿼리할 수 있습니다. 있는 모든 서버 네임 스페이스에서 모든 이름을 찾는 데 위임이에서 정보를 사용할 수 있습니다.  
  
## <a name="recursive-name-resolution"></a>재귀적 이름 확인

재귀적 이름 확인은 DNS 서버를 사용 하는 영역 및 위임의 계층 구조 권한을 보유 하지 않은 쿼리에 응답 하는 프로세스입니다.  
  
일부 구성에서는 DNS 서버는 DNS 루트 서버를 쿼리할 수 있도록 루트 힌트 (즉, 이름 및 IP 주소 목록)을 포함 합니다. 다른 구성 서버를 다른 서버로 답할 수 없는 모든 쿼리를 전달 합니다. 전달 및 루트 힌트에 DNS 서버를 없는 신뢰할 수 없는 쿼리를 해결 하는 데 사용할 수 있는 두 가지가 있습니다.  
  
### <a name="resolving-names-by-using-root-hints"></a>루트 힌트를 사용 하 여 이름 확인

DNS 루트 서버를 찾을 수 있는 DNS 서버를 사용 하는 루트 힌트. DNS 서버에서 DNS 루트 서버를 찾은 후 해당 네임 스페이스에 대 한 모든 쿼리를 확인할 수 있습니다. 다음 그림에 루트 힌트를 사용 하 여 DNS 이름을 확인 하는 방법에 대해 설명 합니다.  
  
![DNS 개념](../../media/Reviewing-DNS-Concepts/1c044845-b104-4262-a7af-474ba3558a85.gif)  
  
이 예제에서는 다음과 같은 이벤트가 발생합니다.  
  
1. 클라이언트 이름 ftp.contoso.com에 해당 하는 IP 주소를 요청 하는 DNS 서버에 재귀 쿼리를 보냅니다. 재귀 쿼리 클라이언트 쿼리에 대 한 명확한 응답을 원한다는 것을 나타냅니다. 재귀 쿼리에 대 한 응답에는 유효한 주소 또는 주소를 찾을 수 없다는 메시지 이어야 합니다.  
2. DNS 서버 이름에 대 한 권한을 보유 하지 않은 하 고 해당 캐시에서 답변 없는 때문에 DNS 서버 루트 힌트를 사용 하 여 DNS 루트 서버 IP 주소를 찾을 수 있습니다.  
3. DNS 서버 이름 ftp.contoso.com를 해결 하려면 DNS 루트 서버를 요청 하는 반복 쿼리를 사용 합니다. 반복 쿼리는 쿼리에 대 한 명확한 응답 대신 다른 서버에 대 한 참조는 서버에 수락 함을 나타냅니다. 레이블으로 끝나는 이름 ftp.contoso.com 때문에 com, DNS 루트 서버 조회 com 영역을 호스팅하는 Com 서버에 반환 합니다.  
4. DNS 서버 이름 ftp.contoso.com를 해결 하려면 Com 서버를 요청 하는 반복 쿼리를 사용 합니다. 이름 ftp.contoso.com 이름이 contoso.com으로 끝나는 때문에 Com 서버 contoso.com 영역을 호스트 하는 Contoso 서버에 대 한 조회를 반환 합니다.  
5. DNS 서버는 Contoso 서버 이름을 ftp.contoso.com 해결에 요청을 반복 쿼리를 사용 합니다. Contoso 서버 영역 데이터에서 답변을 찾은 다음 서버에 대 한 답을 반환 합니다.  
6. 다음 서버는 클라이언트에 결과 반환 합니다.  
  
### <a name="resolving-names-by-using-forwarding"></a>전달을 사용 하 여 이름 확인

전달 루트 힌트를 사용 하는 대신 특정 서버를 통해 경로 이름 확인을 수 있습니다. 다음 그림에 전달을 사용 하 여 DNS 이름을 확인 하는 방법에 대해 설명 합니다.  
  
![DNS 개념](../../media/Reviewing-DNS-Concepts/05bc2eb0-1033-4e53-ae30-244fa247d000.gif)  
  
이 예제에서는 다음과 같은 이벤트가 발생합니다.  
  
1. 클라이언트 이름 ftp.contoso.com에 대 한 DNS 서버를 쿼리합니다.  
2. DNS 서버 전달자 라고 하는 다른 DNS 서버에 쿼리를 전달 합니다.  
3. 전달자 이름에 대 한 권한이 이며 캐시에서 답변 없는, 때문에 루트 DNS 서버 IP 주소를 찾기 위해 루트 힌트를 사용 합니다.  
4. 전달자 이름 ftp.contoso.com를 해결 하려면 DNS 루트 서버를 요청 하는 반복 쿼리를 사용 합니다. 이름으로 끝나는 이름을 ftp.contoso.com 때문에 com, DNS 루트 서버 조회 com 영역을 호스팅하는 Com 서버에 반환 합니다.  
5. 전달자 이름 ftp.contoso.com를 해결 하려면 Com 서버를 요청 하는 반복 쿼리를 사용 합니다. 이름 ftp.contoso.com 이름이 contoso.com으로 끝나는 때문에 Com 서버 contoso.com 영역을 호스트 하는 Contoso 서버에 대 한 조회를 반환 합니다.  
6. 전달자는 Contoso 서버 이름을 ftp.contoso.com 해결에 요청을 반복 쿼리를 사용 합니다. Contoso 서버 답변을 찾아서 해당 영역 파일에 다음 서버에 대 한 답을 반환 합니다.  
7. 전달자 원래 DNS 서버에 결과 반환합니다.  
8. 원본 DNS 서버는 다음 클라이언트에 결과 반환 합니다.  
