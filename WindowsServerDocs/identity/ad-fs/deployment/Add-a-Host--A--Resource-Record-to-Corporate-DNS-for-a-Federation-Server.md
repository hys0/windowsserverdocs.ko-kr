---
ms.assetid: 026747c7-4c34-41c7-b7ea-27f9a7f64a35
title: 페더레이션 서버에 대한 회사 DNS에 호스트(A) 리소스 레코드 추가
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 132e71cec134d17dd73be998683c09f752fdc414
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71360334"
---
# <a name="add-a-host-a-resource-record-to-corporate-dns-for-a-federation-server"></a>페더레이션 서버에 대한 회사 DNS에 호스트(A) 리소스 레코드 추가



회사 네트워크의 클라이언트가 Windows 통합 인증을 사용 하 여 페더레이션 서버에 성공적으로 액세스 하려면 먼저 회사 도메인 이름 @no__t 시스템에서 호스트 \(A @ no__t-1 리소스 레코드를 만들어야 합니다. 페더레이션 서버 또는 페더레이션 서버 클러스터의 IP 주소에 대 한 \(의 계정 페더레이션 서버 호스트 이름입니다. 다음 절차를 사용 하 여 호스트 \(A @ no__t-1 리소스 레코드를 페더레이션 서버에 대 한 회사 DNS에 추가할 수 있습니다.  
  
멤버 자격이 **관리자**, 또는 이와 동등한 최소한이이 절차를 완료 합니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
### <a name="to-add-a-host-a-resource-record-to-corporate-dns-for-a-federation-server"></a>호스트 @no__t를 추가 하려면-0A @ no__t-1 리소스 레코드를 회사 DNS에 페더레이션 서버에 추가 합니다.  
  
1.  회사 네트워크에 대 한 DNS 서버에서 DNS snap @ no__t-0in을 엽니다.  
  
2.  콘솔 트리에서 마우스 오른쪽\-적용 가능한 정방향 조회 영역을 클릭 한 다음 클릭 **새 호스트 \(A 또는 AAAA\)** 합니다.  
  
3.  **이름**에 페더레이션 서버 또는 페더레이션 서버 클러스터의 컴퓨터 이름만 입력 합니다. 예를 들어 정규화 된 도메인 이름 \(FQDN @ no__t-2 fs.fabrikam.com를 입력 하 고 **fs**를 입력 합니다.  
  
4.  **Ip 주소**에 페더레이션 서버 또는 페더레이션 서버 클러스터의 ip 주소 (예: 192.168.1.4)를 입력 합니다.  
  
5.  **호스트 추가**를 클릭합니다.  
  
## <a name="additional-references"></a>추가 참조  
[검사 목록: 페더레이션 서버 설정](Checklist--Setting-Up-a-Federation-Server.md)  
  
[페더레이션 서버에 대한 이름 확인 요구 사항](https://technet.microsoft.com/library/dd807055.aspx)  
  

