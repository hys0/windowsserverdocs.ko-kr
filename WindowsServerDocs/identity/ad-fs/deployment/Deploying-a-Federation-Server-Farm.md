---
ms.assetid: bbb5b68f-00ad-4715-8176-0c2769b706c4
title: Windows Server 2012 R2 AD FS 배포 가이드
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: c0f8dca425f644952c36a289ec72651f6383e846
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192190"
---
# <a name="deploying-a-federation-server-farm"></a>페더레이션 서버 팜 배포


페더레이션 서버 팜을 배포하려면 이 검사 목록의 작업을 순서대로 완료합니다. 참조 링크를 클릭하면 개념이 설명된 항목으로 이동하며 이 내용을 읽은 후 이 검사 목록으로 돌아와서 검사 목록의 나머지 작업을 계속할 수 있습니다.  
  
![페더레이션된 서버 팜 배포](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**검사 목록: 페더레이션 서버 팜 배포**  
  
||태스크|참조|  
|-|--------|-------------|  
|![페더레이션된 서버 팜 배포](media/icon_checkboxo.gif)|Active Directory Federation Services 배포를 준비할 때 중요 한 개념 및 고려 사항을 검토 \(AD FS\)합니다. **참고:**|![페더레이션된 서버 팜 배포](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Server 2012 R2에서 AD FS 디자인 가이드](../../ad-fs/design/AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)<br /><br />![페더레이션된 서버 팜 배포](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 개념 이해 키](../../ad-fs/technical-reference/Understanding-Key-AD-FS-Concepts.md)|  
||AD FS 구성 저장소에 Microsoft SQL Server를 사용하려는 경우 SQL Server의 기능 인스턴스를 배포해야 합니다.|[SQL Server](https://technet.microsoft.com/sqlserver) **Warning:** Windows Server 2012 R2에서 AD FS 팜을 만들고 SQL Server를 사용하여 구성 데이터를 저장하려면 SQL Server 2008 이상(SQL Server 2012 포함)을 사용하면 됩니다.|  
|![페더레이션된 서버 팜 배포](media/icon_checkboxo.gif)|Active Directory 도메인에 컴퓨터를 가입시킵니다.|![페더레이션된 서버 팜 배포](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[컴퓨터를 도메인에 가입](Join-a-Computer-to-a-Domain.md)|  
|![페더레이션된 서버 팜 배포](media/icon_checkboxo.gif)|등록 한 Secure Socket Layer \(SSL\) AD FS에 대 한 인증서입니다.|![페더레이션된 서버 팜 배포](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[AD FS에 대 한 SSL 인증서를 등록 합니다.](Enroll-an-SSL-Certificate-for-AD-FS.md)|  
|![페더레이션된 서버 팜 배포](media/icon_checkboxo.gif)|AD FS 역할 서비스를 설치합니다.|![페더레이션된 서버 팜 배포](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[AD FS 역할 서비스 설치](Install-the-AD-FS-Role-Service.md)|  
|![페더레이션된 서버 팜 배포](media/icon_checkboxo.gif)|페더레이션 서버를 구성합니다.|![페더레이션된 서버 팜 배포](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[페더레이션 서버 구성](Configure-a-Federation-Server.md)|  
|![페더레이션된 서버 팜 배포](media/icon_checkboxo.gif)|선택적 단계: Device Registration Service를 사용 하 여 페더레이션 서버 구성 \(DRS\)합니다.|![페더레이션된 서버 팜 배포](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Device Registration Service를 사용 하 여 페더레이션 서버 구성](Configure-a-federation-server-with-Device-Registration-Service.md)|  
|![페더레이션된 서버 팜 배포](media/icon_checkboxo.gif)|호스트 추가 \(A\) 및 별칭을 \(CNAME\) 회사 도메인 이름 시스템에 리소스 레코드 \(DNS\) 페더레이션 서비스와 DRS에 대 한 합니다.|![페더레이션된 서버 팜 배포](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[페더레이션 서비스와 DRS에 대해 회사 DNS 구성](Configure-Corporate-DNS-for-the-Federation-Service-and-DRS.md)|  
|![페더레이션된 서버 팜 배포](media/icon_checkboxo.gif)|페더레이션 서버가 작동하는지 확인합니다.|![페더레이션된 서버 팜 배포](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[확인 하는 페더레이션 서버 작동](Verify-That-a-Federation-Server-Is-Operational.md)|  
  

## <a name="see-also"></a>관련 항목  
[AD FS 배포](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS 배포 가이드](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
  

