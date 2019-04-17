---
ms.assetid: bbb5b68f-00ad-4715-8176-0c2769b706c4
title: "지침에 따라 Windows Server 2012 r 2 광고 FS 배포"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 05f1ea6830237813e6fd2bd6a172f467e8d81065
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="deploying-a-federation-server-farm"></a>Federation 서버 농장 배포

>적용 대상: Windows Server 2016, Windows Server 2012 r 2

Federation 서버 농장 배포를 위해이 검사 순서로 나열의 작업을 완료 합니다. 이 검사에서 나머지 작업 진행할 수 있도록 개념 항목을 검토 한 후이 검사에 한 참조 링크 개념 항목으로 이동 때 돌아갑니다.  
  
![연결 된 팜 배포](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**검사: Federation 서버 농장 배포**  
  
||작업|참조|  
|-|--------|-------------|  
|![연결 된 팜 배포](media/icon_checkboxo.gif)|중요 한 개념 및 사항을 준비 Active Directory Federation Services \(AD FS\) 배포 하는 동안 검토 합니다. **참고:**|![연결 된 팜 배포](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[광고 FS 디자인 가이드 Windows Server 2012 r 2](../../ad-fs/design/AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)<br /><br />![연결 된 팜 배포](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[이해 키 광고 FS 개념](../../ad-fs/technical-reference/Understanding-Key-AD-FS-Concepts.md)|  
||Microsoft SQL Server ADFS 구성 스토어에 대 한 사용 하려는 경우 배포 하는 기능 SQL Server 인스턴스를 확인 합니다.|[SQL Server ](https://technet.microsoft.com/sqlserver)**경고:** Windows Server 2012 R2, ADFS 농장을 만들고 사용 SQL Server 구성 데이터를 저장 하려는 경우 사용할 수 있습니다 SQL Server 2008 및 SQL Server 2012를 포함 하 여 최신 버전입니다.|  
|![연결 된 팜 배포](media/icon_checkboxo.gif)|컴퓨터 Active Directory 도메인에 가입입니다.|![연결 된 팜 배포](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[컴퓨터 도메인에 가입](Join-a-Computer-to-a-Domain.md)|  
|![연결 된 팜 배포](media/icon_checkboxo.gif)|Adfs Secure Socket 계층 \(SSL\) 인증서를 등록 합니다.|![연결 된 팜 배포](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[SSL 인증서 adfs 등록](Enroll-an-SSL-Certificate-for-AD-FS.md)|  
|![연결 된 팜 배포](media/icon_checkboxo.gif)|ADFS 역할 서비스를 설치 합니다.|![연결 된 팜 배포](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[ADFS 역할 서비스 설치](Install-the-AD-FS-Role-Service.md)|  
|![연결 된 팜 배포](media/icon_checkboxo.gif)|Federation 서버를 구성 합니다.|![연결 된 팜 배포](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[Federation 서버 구성](Configure-a-Federation-Server.md)|  
|![연결 된 팜 배포](media/icon_checkboxo.gif)|단계: 장치 등록 서비스 \(DRS\) 사용 federation 서버를 구성 합니다.|![연결 된 팜 배포](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[federation 서버 등록 서비스 디바이스를 구성](Configure-a-federation-server-with-Device-Registration-Service.md)|  
|![연결 된 팜 배포](media/icon_checkboxo.gif)|호스트 \(A\) 및 별칭 \(CNAME\) 리소스 레코드 federation 서비스에 대 한 회사 Domain Name System \(DNS\) 및 DRS를 추가 합니다.|![연결 된 팜 배포](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Federation 서비스 및 DRS 회사 DNS 구성](Configure-Corporate-DNS-for-the-Federation-Service-and-DRS.md)|  
|![연결 된 팜 배포](media/icon_checkboxo.gif)|Federation 서버 작동 중인지 확인 합니다.|![연결 된 팜 배포](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[되어 있는지 확인 한 Federation 서버는 운영](Verify-That-a-Federation-Server-Is-Operational.md)|  
  

## <a name="see-also"></a>참조 하십시오  
[AD FS 배포](../../ad-fs/AD-FS-Deployment.md)  

[지침에 따라 Windows Server 2012 r 2 광고 FS 배포](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
  

