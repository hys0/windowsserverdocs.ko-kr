---
ms.assetid: 026747c7-4c34-41c7-b7ea-27f9a7f64a35
title: "회사 dns 호스트 (A) 리소스 레코드 Federation 서버에 대 한 추가"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 425cfe794095f1515eb3fae2f1a5e5db90ba3d00
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="add-a-host-a-resource-record-to-corporate-dns-for-a-federation-server"></a>회사 dns 호스트 (A) 리소스 레코드 Federation 서버에 대 한 추가

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


클라이언트 회사에서 사용 하 여 Windows 통합 인증 federation 서버 성공적으로 액세스를 네트워크, 호스트 \(A\) 리소스 기록 먼저 만들어야 호스트 계정 federation 서버의 이름을 확인 하는 회사 Domain Name System \(DNS\) \ (예: fs.fabrikam.com\) federation 서버 또는 federation 서버 클러스터의 IP 주소를 합니다. 호스트 \(A\) 리소스 레코드 federation 서버에 대 한 회사 DNS를 추가 하려면 다음 절차에 사용할 수 있습니다.  
  
회원 **관리자**, 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.  해당 계정을 사용에 대 한 세부 정보를 검토 및 그룹 구성원에 [로컬와 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
### <a name="to-add-a-host-a-resource-record-to-corporate-dns-for-a-federation-server"></a>호스트 \(A\) 리소스 레코드 federation 서버에 대 한 회사 DNS를 추가 하려면  
  
1.  회사 네트워크에 대 한 DNS 서버를 snap\에서 DNS을 엽니다.  
  
2.  콘솔에서 나무 right\ 클릭 해당 앞으로 조회 영역이 한 다음 **새 호스트 \(A or AAAA\)**합니다.  
  
3.  **이름**만 해당 federation 서버 또는 federation 서버 클러스터;의 컴퓨터 이름을 입력 예를 들어 정식된 도메인에 대 한 \(FQDN\) 입력 fs.fabrikam.com 이름을 **fs**합니다.  
  
4.  **IP 주소**, federation 서버 또는 federation 서버 클러스터 192.168.1.4 예를 들어, IP 주소를 입력 합니다.  
  
5.  클릭 **호스트 추가**합니다.  
  
## <a name="additional-references"></a>추가 참조  
[Federation 서버 설정 검사:](Checklist--Setting-Up-a-Federation-Server.md)  
  
[이름 Federation 서버에 대 한 확인 요구 사항](https://technet.microsoft.com/library/dd807055.aspx)  
  

