---
ms.assetid: 026747c7-4c34-41c7-b7ea-27f9a7f64a35
title: 페더레이션 서버에 대한 회사 DNS에 호스트(A) 리소스 레코드 추가
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 5767fa45f8b25680aa1b1d97ddab630923d10fae
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192492"
---
# <a name="add-a-host-a-resource-record-to-corporate-dns-for-a-federation-server"></a>페더레이션 서버에 대한 회사 DNS에 호스트(A) 리소스 레코드 추가



회사에서 클라이언트를 호스트 하는 Windows 통합 인증을 사용 하 여 페더레이션 서버를 성공적으로 액세스 하려면 네트워크에 대 한 \(A\) 회사 도메인 이름 시스템에 리소스 레코드 먼저 만들어야 합니다 \(DNS\) 계정 페더레이션 서버 호스트 이름을 확인 하는 \(예를 들어 fs.fabrikam.com\) 페더레이션 서버 또는 페더레이션 서버 클러스터의 IP 주소를 합니다. 다음 절차를 사용 하 여 호스트를 추가 하려면 \(는\) 페더레이션 서버에 대해 회사 DNS에 리소스 레코드입니다.  
  
멤버 자격이 **관리자**, 또는 이와 동등한 최소한이이 절차를 완료 합니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
### <a name="to-add-a-host-a-resource-record-to-corporate-dns-for-a-federation-server"></a>호스트를 추가 하려면 \(는\) 페더레이션 서버에 대해 회사 DNS에 리소스 레코드  
  
1.  회사 네트워크에 대 한 DNS 서버에서 DNS 스냅인을 열고\-에서 합니다.  
  
2.  콘솔 트리에서 마우스 오른쪽\-적용 가능한 정방향 조회 영역을 클릭 한 다음 클릭 **새 호스트 \(A 또는 AAAA\)** 합니다.  
  
3.  **이름을**에, 예를 들어, 정규화 된 도메인 이름을 페더레이션 서버 또는 페더레이션 서버 클러스터의 컴퓨터 이름만 입력 \(FQDN\) fs.fabrikam.com, 형식 **fs**.  
  
4.  **IP 주소**, 페더레이션 서버 또는 페더레이션 서버 클러스터, 예를 들어 192.168.1.4에 대 한 IP 주소를 입력 합니다.  
  
5.  **호스트 추가**를 클릭합니다.  
  
## <a name="additional-references"></a>추가 참조  
[검사 목록: 페더레이션 서버 설정](Checklist--Setting-Up-a-Federation-Server.md)  
  
[페더레이션 서버에 대한 이름 확인 요구 사항](https://technet.microsoft.com/library/dd807055.aspx)  
  

