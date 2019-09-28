---
ms.assetid: bbb5b68f-00ad-4715-8176-0c2769b706c4
title: Windows Server 2012 R2 AD FS 배포 가이드
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: e5507cd567114d17c6500655ee210b70bd9ea1ec
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408415"
---
# <a name="deploying-a-federation-server-farm"></a>페더레이션 서버 팜 배포


페더레이션 서버 팜을 배포하려면 이 검사 목록의 작업을 순서대로 완료합니다. 참조 링크를 클릭하면 개념이 설명된 항목으로 이동하며 이 내용을 읽은 후 이 검사 목록으로 돌아와서 검사 목록의 나머지 작업을 계속할 수 있습니다.  
  
![ 페더레이션된 서버 팜 배포 @ no__t-1 검사 목록: 페더레이션 서버 팜 배포 @ no__t-0  
  
||태스크|참조|  
|-|--------|-------------|  
|![페더레이션된 서버 팜 배포](media/icon_checkboxo.gif)|Active Directory Federation Services \(AD FS @ no__t-1을 배포 하기 위해 준비할 때 중요 한 개념 및 고려 사항을 검토 합니다. **참고:**|![ Windows Server 2012 r 2에서 페더레이션 서버 팜 배포](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 디자인 가이드](../../ad-fs/design/AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)<br /><br />![deploying 서버 팜 배포](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[주요 AD FS 개념 이해](../../ad-fs/technical-reference/Understanding-Key-AD-FS-Concepts.md)|  
||AD FS 구성 저장소에 Microsoft SQL Server를 사용하려는 경우 SQL Server의 기능 인스턴스를 배포해야 합니다.|[SQL Server](https://technet.microsoft.com/sqlserver) **경고:** Windows Server 2012 R2에서 AD FS 팜을 만들고 SQL Server를 사용하여 구성 데이터를 저장하려면 SQL Server 2008 이상(SQL Server 2012 포함)을 사용하면 됩니다.|  
|![페더레이션된 서버 팜 배포](media/icon_checkboxo.gif)|Active Directory 도메인에 컴퓨터를 가입시킵니다.|![ 페더레이션 서버 팜 배포](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[컴퓨터를 도메인에 가입](Join-a-Computer-to-a-Domain.md)|  
|![페더레이션된 서버 팜 배포](media/icon_checkboxo.gif)|등록 한 Secure Socket Layer \(SSL\) AD FS에 대 한 인증서입니다.|![](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[AD FS에 대 한 SSL 인증서를 등록 하는](Enroll-an-SSL-Certificate-for-AD-FS.md) 페더레이션된 서버 팜 배포|  
|![페더레이션된 서버 팜 배포](media/icon_checkboxo.gif)|AD FS 역할 서비스를 설치합니다.|![ 페더레이션된 서버 팜을 배포](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[AD FS 역할 서비스를 설치 합니다](Install-the-AD-FS-Role-Service.md) .|  
|![페더레이션된 서버 팜 배포](media/icon_checkboxo.gif)|페더레이션 서버를 구성합니다.|![ 페더레이션 서버 팜 배포](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[페더레이션 서버 구성](Configure-a-Federation-Server.md)|  
|![페더레이션된 서버 팜 배포](media/icon_checkboxo.gif)|선택적 단계: 장치 등록 서비스 \(DRS @ no__t-1을 사용 하 여 페더레이션 서버를 구성 합니다.|![ 페더레이션된 서버 팜 배포](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[장치 등록 서비스를 사용 하 여 페더레이션 서버 구성](Configure-a-federation-server-with-Device-Registration-Service.md)|  
|![페더레이션된 서버 팜 배포](media/icon_checkboxo.gif)|호스트 추가 \(A\) 및 별칭을 \(CNAME\) 회사 도메인 이름 시스템에 리소스 레코드 \(DNS\) 페더레이션 서비스와 DRS에 대 한 합니다.|![ 페더레이션된 서버 팜 배포](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[페더레이션 서비스 및 DRS에 대해 회사 DNS 구성](Configure-Corporate-DNS-for-the-Federation-Service-and-DRS.md)|  
|![페더레이션된 서버 팜 배포](media/icon_checkboxo.gif)|페더레이션 서버가 작동하는지 확인합니다.|![ 페더레이션 서버 팜 배포](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[페더레이션 서버가 작동 하는지 확인](Verify-That-a-Federation-Server-Is-Operational.md)|  
  

## <a name="see-also"></a>관련 항목  
[AD FS 배포](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS 배포 가이드](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
  

