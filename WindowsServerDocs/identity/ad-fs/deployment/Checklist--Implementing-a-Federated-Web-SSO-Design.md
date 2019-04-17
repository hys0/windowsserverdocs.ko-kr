---
ms.assetid: 6b49cde3-d2cb-4ece-b9b7-dc600e037495
title: "연결 된 웹 SSO 디자인을 구현 목록"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 1122ee3814f656a7229dc2946d7441d525de5ae2
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="checklist-implementing-a-federated-web-sso-design"></a>연합된 웹 SSO 디자인을 구현 검사:

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 부모 검사 \(AD FS\) Active Directory Federation Services에 대 한 웹 Single\-Sign\-On 연방 \(SSO\) 디자인에 대 한 중요 한 개념 cross\ 참조 링크가 포함 되어 있습니다. 또한이 디자인을 구현 하는 데 필요한 작업을 수행할 수 있도록 검사 목록이 하위 링크가 포함 되어 있습니다.  
  
> [!NOTE]  
> 주문에서이 검사의 작업을 완료 합니다. 참조 링크를 이용 하면 개념 항목을 나 하위 검사 때 개념 항목을 검토 하거나이 검사에서 나머지 작업 진행할 수 있도록 하위 검사 목록에서 작업을 완료 한 후이 항목으로 돌아갑니다.  
  
![웹 sso 연방](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**검사: 웹 SSO 연방 디자인을 구현 합니다.**  
  
||작업|참조|  
|-|--------|-------------|  
|![연결 된 웹 sso](media/icon_checkboxo.gif)|중요 한 웹 SSO 연방 디자인 개념을 검토 하 고 사용자 지정이 디자인 조직에서 요구 하는 데 사용할 수 있는 ADFS 배포 목표를 결정 합니다.|![웹 sso 연방](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[웹 연방 SSO 디자인](https://technet.microsoft.com/library/dd807050.aspx)<br /><br />![웹 sso 연방](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 배포 목표에 확인](https://technet.microsoft.com/library/dd807053.aspx)<br /><br />![웹 sso 연방](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[배포를 계획](https://technet.microsoft.com/library/dd807083.aspx)|  
|![연결 된 웹 sso](media/icon_checkboxo.gif)|하드웨어, 소프트웨어, 인증서, Domain Name System \(DNS\), 특성 저장소 및 ADFS 조직에서 배포 하기 위한 클라이언트 요구 검토 합니다.|![웹 sso 연방](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[부록 a: 검토 광고 FS 요구 사항](https://technet.microsoft.com/library/ff678034.aspx)|  
|![연결 된 웹 sso](media/icon_checkboxo.gif)|ADFS 모두 파트너 조직에서 배포 하기 전에 규칙과 특성 스토어 ADFS 구성 데이터베이스 주장, 청구에 대 한 중요 한 개념 검토 합니다.|![웹 sso 연방](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[이해 키 광고 FS 개념](../../ad-fs/technical-reference/Understanding-Key-AD-FS-Concepts.md)|  
|![연결 된 웹 sso](media/icon_checkboxo.gif)|디자인 요금제에 따라 모든 파트너 조직에서 하나 이상의 federation 서버를 설치 합니다. **참고:** 계정 파트너 조직에서 하나 이상의 federation 서버 및 리소스 파트너 조직에서 하나 이상의 federation 서버 필요 웹 SSO 연방 디자인에 대 한 합니다.|![웹 sso 연방](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[검사: Federation 서버 설정](Checklist--Setting-Up-a-Federation-Server.md)|  
|![연결 된 웹 sso](media/icon_checkboxo.gif)|확인 \(Optional\) 여부 조직에는 federation 서버 프록시 필요 합니다. 디자인 요금제에 대 한 프록시 전화 하는 경우 각 파트너 조직에서 하나 이상의 federation 서버 프록시 설치할 수 있습니다.|![웹 sso 연방](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[검사: Federation 서버 프록시를를 크게 설정](Checklist--Setting-Up-a-Federation-Server-Proxy.md)|  
|![연결 된 웹 sso](media/icon_checkboxo.gif)|디자인 요금제에 따라 인증서를 공유, 클라이언트를 구성 하 고 federation 신뢰를 통해 통신할 수 있도록 두 파트너 조직에서 보안 관계를 구성 합니다.|![웹 sso 연방](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[검사: 계정 파트너 조직 구성](Checklist--Configuring-the-Account-Partner-Organization.md)<br /><br />![웹 sso 연방](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[검사: 리소스 파트너 조직의 구성](Checklist--Configuring-the-Resource-Partner-Organization.md)|  
|![연결 된 웹 sso](media/icon_checkboxo.gif)|리소스 파트너 조직에서 관리자 인 경우 claims\ 사용 웹 브라우저 응용 프로그램, 웹 서비스 응용 프로그램 또는 군 및 군 SDK를 사용 하 여 Microsoft Office SharePoint® 서버® 응용 프로그램입니다.|![웹 sso 연방](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows 신원을 파운데이션](https://go.microsoft.com/fwlink/?LinkId=122266)<br /><br />![웹 sso 연방](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows 신원을 Foundation SDK](https://go.microsoft.com/fwlink/?LinkId=122266)|  
