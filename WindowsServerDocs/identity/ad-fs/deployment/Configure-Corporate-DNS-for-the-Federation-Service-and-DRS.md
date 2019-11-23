---
ms.assetid: aca4a4fa-b12c-4eed-a499-f9aedb7d2fd6
title: 페더레이션된 서비스와 DRS에 대해 회사 DNS 구성
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 9f0b04f9dc050117fdefc630759c86d2b1bb1ecc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408448"
---
# <a name="configure-corporate-dns-for-the-federation-service-and-drs"></a>페더레이션된 서비스와 DRS에 대해 회사 DNS 구성
  
## <a name="step-6-add-a-host-a-and-alias-cname-resource-record-to-corporate-dns-for-the-federation-service-and-drs"></a>6 단계: 페더레이션 서비스 및 DRS에 대 한\) 및 별칭 \(CNAME\) 리소스 레코드를 회사 DNS에 추가 하 \(호스트를 추가 합니다.  
이전 단계에서 구성한 페더레이션 서비스 및 장치 등록 서비스에 대 한 DNS\) \(회사 도메인 이름 시스템에 다음 리소스 레코드를 추가 해야 합니다.  
  
|항목|형식|주소|  
|---------|--------|-----------|  
|페더레이션\_서비스\_이름|\) \(호스트|AD FS 서버 팜 앞에 구성 된 AD FS 서버의 IP 주소 또는 부하 분산 장치의 IP 주소|  
|enterpriseregistration|CNAME \(별칭\)|페더레이션\_서버\_name.contoso.com|  
  
다음 절차를 사용 하 여\) 및 별칭 \(CNAME\) 리소스 레코드를 페더레이션 서버 및 장치 등록 서비스에 대 한 회사 DNS에 \(하는 호스트를 추가할 수 있습니다.  
  
이 절차를 완료 하려면 최소한 **Administrators**그룹의 구성원 이거나 이와 동등한 자격이 필요 합니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
#### <a name="to-add-a-host-a-and-alias-cname-resource-records-to-dns-for-your-federation-server"></a>\(호스트를 추가 하려면 페더레이션 서버에 대 한 DNS에\) 및 별칭 \(CNAME\) 리소스 레코드를 추가 합니다.  
  
1.  도메인 컨트롤러의 서버 관리자에 있는 **도구** 메뉴에서 **dns** 를 클릭 하 여의 dns 맞춤\-를 엽니다.  
  
2.  콘솔 트리에서 **도메인\_컨트롤러\_이름** 노드, **전방 조회 영역**, 오른쪽\-**도메인\_이름**을 차례로 확장 한 다음 **새 호스트 \(A 또는 AAAA\)를** 클릭 합니다.  
  
3.  **이름** 상자에 AD FS 팜에 사용할 이름을 입력 합니다.  
  
4.  **IP 주소** 상자에 페더레이션 서버의 IP 주소를 입력합니다. **호스트 추가**를 클릭합니다.  
  
5.  \-**도메인\_이름** 노드를 마우스 오른쪽 단추로 클릭 한 다음 **새 별칭 \(CNAME\)** 을 클릭 합니다.  
  
6.  **새 리소스 레코드** 대화 상자의 **별칭 이름** 상자에 **enterpriseregistration**을 입력합니다.  
  
7.  FQDN (정규화 된 도메인 이름) \(FQDN\)의 대상 호스트 상자에 **federation\_service\_farm\_name. domain\_name.com**를 입력 한 다음 **확인**을 클릭 합니다.  
  
    > [!IMPORTANT]  
    > 실제 배포에서는 회사에 여러 UPN (사용자 계정 이름 \(UPN\) 접미사가 있는 경우 DNS의 각 UPN 접미사에 대해 여러 CNAME 레코드를 만들어야 합니다.  
  
## <a name="see-also"></a>참고 항목 

[AD FS 배포](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS 배포 가이드](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[페더레이션 서버 팜 배포](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  

