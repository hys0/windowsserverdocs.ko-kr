---
ms.assetid: aca4a4fa-b12c-4eed-a499-f9aedb7d2fd6
title: 페더레이션된 서비스와 DRS에 대해 회사 DNS 구성
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: cd8febf9eff300b1a83d22828874b4a577b8af36
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192322"
---
# <a name="configure-corporate-dns-for-the-federation-service-and-drs"></a>페더레이션된 서비스와 DRS에 대해 회사 DNS 구성
  
## <a name="step-6-add-a-host-a-and-alias-cname-resource-record-to-corporate-dns-for-the-federation-service-and-drs"></a>6단계: 호스트 추가 \(A\) 및 별칭 \(CNAME\) 페더레이션 서비스와 DRS에 대해 회사 DNS에 리소스 레코드  
회사 도메인 이름 시스템에 다음 리소스 레코드를 추가 해야 합니다 \(DNS\) 에 페더레이션 서비스와 이전 단계에서 구성한 Device Registration Service에 대 한 합니다.  
  
|입력|형식|주소|  
|---------|--------|-----------|  
|federation\_service\_name|호스트 \(는\)|AD FS 서버 또는 AD FS 서버 팜에 앞에 구성 된 부하 분산 장치의 IP 주소는 IP 주소|  
|enterpriseregistration|별칭 \(CNAME\)|federation\_server\_name.contoso.com|  
  
다음 절차를 사용 하 여 호스트를 추가 하려면 \(A\) 및 별칭 \(CNAME\) 페더레이션 서버에 대해 회사 DNS 및 Device Registration Service에 대 한 리소스 레코드입니다.  
  
멤버 자격이 **관리자**, 또는 이와 동등한이 절차를 완료 하려면 최소한 합니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
#### <a name="to-add-a-host-a-and-alias-cname-resource-records-to-dns-for-your-federation-server"></a>호스트를 추가 하려면 \(A\) 및 별칭 \(CNAME\) 페더레이션 서버에 대 한 dns 리소스 레코드  
  
1.  하면 도메인 컨트롤러에서 서버 관리자에서에 **도구** 메뉴에서 클릭 **DNS** DNS 스냅인을 열려면\-에서 합니다.  
  
2.  콘솔 트리에서 확장 합니다 **도메인\_컨트롤러\_이름** 노드를 확장 하 고 **정방향 조회 영역**, 오른쪽\-클릭 **도메인\_이름을**를 클릭 하 고 **새 호스트 \(A 또는 AAAA\)** 합니다.  
  
3.  에 **이름을** 상자에 AD FS 팜에 사용할 이름을 입력 합니다.  
  
4.  **IP 주소** 상자에 페더레이션 서버의 IP 주소를 입력합니다. **호스트 추가**를 클릭합니다.  
  
5.  오른쪽\-를 클릭 합니다 **도메인\_이름** 노드를 차례로 클릭 한 다음 **새 별칭 \(CNAME\)** 합니다.  
  
6.  **새 리소스 레코드** 대화 상자의 **별칭 이름** 상자에 **enterpriseregistration**을 입력합니다.  
  
7.  정규화 된 도메인 이름에 \(FQDN\) 대상 호스트 상자의 형식의 **페더레이션\_service\_팜\_name.domain\_name.com**, 고 클릭 **확인**합니다.  
  
    > [!IMPORTANT]  
    > 실제 배포에서는 회사에 여러 사용자 계정 이름 \(UPN\) 접미사를 DNS에 해당 UPN 접미사 마다 여러 CNAME 레코드를 만들어야 합니다.  
  
## <a name="see-also"></a>관련 항목 

[AD FS 배포](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS 배포 가이드](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[페더레이션 서버 팜 배포](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  

