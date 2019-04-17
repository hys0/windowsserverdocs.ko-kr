---
ms.assetid: 30657638-5709-48c5-87aa-98f688e07b4c
title: "웹 SSO 디자인을 구현 목록"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 265daf3acb9632aa92f85962abc44a6a9ea8dfed
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="checklist-implementing-a-web-sso-design"></a>웹 SSO 디자인을 구현 검사:

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 부모 검사에 웹에 대 한 Active Directory Federation Services \(AD FS\) Single\ Sign\-켜 짐 \(SSO\) 디자인에 대 한 중요 한 개념 cross\ 참조 링크가 포함 되어 있습니다. 또한이 디자인을 구현 하는 데 필요한 작업을 수행할 수 있도록 검사 목록이 하위 링크가 포함 되어 있습니다.  
  
> [!NOTE]  
> 주문에서이 검사의 작업을 완료 합니다. 참조 링크를 이용 하면 개념 항목을 나 하위 검사 때 개념 항목을 검토 하거나이 검사에서 나머지 작업 진행할 수 있도록 하위 검사 목록에서 작업을 완료 한 후이 항목으로 돌아갑니다.  
  
![웹 sso](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**검사: 웹 SSO 디자인을 구현 합니다.**  
  
||작업|참조|  
|-|--------|-------------|  
|![웹 sso](media/icon_checkboxo.gif)|중요 한 웹 SSO 디자인 개념을 검토 하 고 사용자 지정이 디자인 조직에서 요구 하는 데 사용할 수 있는 ADFS 배포 목표를 결정 합니다. **참고:**|![웹 sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[웹 SSO 디자인](https://technet.microsoft.com/library/dd807033.aspx)<br /><br />![웹 sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 배포 목표에 확인](https://technet.microsoft.com/library/dd807053.aspx)|  
|![웹 sso](media/icon_checkboxo.gif)|하드웨어, 소프트웨어, 인증서, Domain Name System \(DNS\), 특성 저장소 및 ADFS 조직에서 배포 하기 위한 클라이언트 요구 검토 합니다.|![웹 sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[부록 a: 검토 광고 FS 요구 사항](https://technet.microsoft.com/library/ff678034.aspx)|  
|![웹 sso](media/icon_checkboxo.gif)|디자인 요금제에 따라 주변 네트워크 또는 회사 네트워크에서 하나 이상의 federation 서버를 설치 합니다. **참고:** 웹 SSO 디자인 하나만 federation 서버 성공적으로 작동 하는 데 필요 합니다. 단일 federation 서버 클레임 공급자 역할 및 신뢰 파티 역할 둘 다에서 작동합니다.|![웹 sso](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[검사: Federation 서버 설정](Checklist--Setting-Up-a-Federation-Server.md)|  
|![웹 sso](media/icon_checkboxo.gif)|\(Optional\) 확인 조직에는 federation 서버 프록시 주변 네트워크에 필요한 여부.|![웹 sso](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[검사: Federation 서버 프록시를를 크게 설정](Checklist--Setting-Up-a-Federation-Server-Proxy.md)|  
|![웹 sso](media/icon_checkboxo.gif)|웹 SSO 디자인 요금제를 사용 하려는 방법에 따라 파티 신뢰, 청구, 의존 적절 한 특성 저장소를 추가 하 고 Federation 서비스에 규칙 주장.|![웹 sso](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[검사: 계정 파트너 조직 구성](Checklist--Configuring-the-Account-Partner-Organization.md)|  
|![웹 sso](media/icon_checkboxo.gif)|리소스 파트너 조직에서 관리자 인 경우 claims\ 사용 웹 브라우저 응용 프로그램, 웹 서비스 응용 프로그램 또는 군 및 군 SDK를 사용 하 여 Microsoft Office SharePoint® 서버® 응용 프로그램입니다. **참고:**|![웹 sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows 신원을 파운데이션](https://go.microsoft.com/fwlink/?LinkId=122266)<br /><br />![웹 sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows 신원을 Foundation SDK](https://go.microsoft.com/fwlink/?LinkId=122266)| 
