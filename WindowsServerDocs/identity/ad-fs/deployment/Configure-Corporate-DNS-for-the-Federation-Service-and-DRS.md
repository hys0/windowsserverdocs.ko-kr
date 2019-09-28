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
  
## <a name="step-6-add-a-host-a-and-alias-cname-resource-record-to-corporate-dns-for-the-federation-service-and-drs"></a>6단계: 페더레이션 서비스와 DRS에 대해 회사 DNS에 \(A @ no__t-1 및 별칭 \(CNAME no__t 리소스 레코드를 추가 합니다.  
이전 단계에서 구성한 페더레이션 서비스 및 장치 등록 서비스에 대해 회사 도메인 이름 시스템 \(DNS @ no__t-1에 다음 리소스 레코드를 추가 해야 합니다.  
  
|입력|type|주소|  
|---------|--------|-----------|  
|federation @ no__t-0service @ no__t-1name|호스트 \(A @ no__t-1|AD FS 서버 팜 앞에 구성 된 AD FS 서버의 IP 주소 또는 부하 분산 장치의 IP 주소|  
|enterpriseregistration|별칭 \(CNAME @ no__t-1|페더레이션 @ no__t-0server\_name.contoso.com|  
  
다음 절차에 따라 페더레이션 서버 및 장치 등록 서비스에 대 한 호스트 \(A @ no__t-1 및 별칭 \(CNAME @ no__t-3 리소스 레코드를 회사 DNS에 추가할 수 있습니다.  
  
이 절차를 완료 하려면 최소한 **Administrators**그룹의 구성원 이거나 이와 동등한 자격이 필요 합니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
#### <a name="to-add-a-host-a-and-alias-cname-resource-records-to-dns-for-your-federation-server"></a>@No__t-0A @ no__t-1 및 별칭 \(CNAME @ no__t-3 리소스 레코드를 추가 하려면 페더레이션 서버에 대 한 DNS에  
  
1.  도메인 컨트롤러의 서버 관리자에 있는 **도구** 메뉴에서 **dns** 를 클릭 하 여 dns snap @ no__t-2를 엽니다.  
  
2.  콘솔 트리에서 **도메인 @ no__t-1controller @ no__t-2name** 노드를 확장 하 고 **전방 조회 영역**을 확장 한 다음 **도메인 @ no__t-6Name**을 클릭 하 고 **새 호스트 \(A 또는 AAAA @ no__t-9**를 클릭 합니다.  
  
3.  **이름** 상자에 AD FS 팜에 사용할 이름을 입력 합니다.  
  
4.  **IP 주소** 상자에 페더레이션 서버의 IP 주소를 입력합니다. **호스트 추가**를 클릭합니다.  
  
5.  Right @ no__t-0 **도메인 @ no__t-2name** 노드를 클릭 한 다음 **새 별칭 \(cname @ no__t-5**를 클릭 합니다.  
  
6.  **새 리소스 레코드** 대화 상자의 **별칭 이름** 상자에 **enterpriseregistration**을 입력합니다.  
  
7.  정규화 된 도메인 이름 \(FQDN @ no__t-1 (대상 호스트) 상자에 **federation @ no__t-3service @ no__t-4farm @ no__t-5name. domain @ no__t-6name .com**을 입력 한 다음 **확인**을 클릭 합니다.  
  
    > [!IMPORTANT]  
    > 실제 배포에서는 회사에 여러 사용자 계정 이름 \(UPN @ no__t-1 접미사가 있는 경우 DNS의 각 UPN 접미사에 대해 여러 CNAME 레코드를 만들어야 합니다.  
  
## <a name="see-also"></a>관련 항목 

[AD FS 배포](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS 배포 가이드](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[페더레이션 서버 팜 배포](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  

