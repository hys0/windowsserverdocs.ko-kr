---
ms.assetid: 6b49cde3-d2cb-4ece-b9b7-dc600e037495
title: 검사 목록-페더레이션된 웹 SSO 디자인 구현
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 165471fd06031a68343a54d019357afee782d082
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359953"
---
# <a name="checklist-implementing-a-federated-web-sso-design"></a>검사 목록: 페더레이션된 웹 SSO 디자인 구현

이 상위 검사 목록에는\) Active Directory Federation Services \(AD FS에 대 한 \(SSO\)디자인에서 페더레이션된 웹 Single\-Sign\-에 대 한 중요 한 개념에 대 한 상호\-참조 링크가 포함 되어 있습니다. 또한 이 디자인을 구현하는 데 필요한 작업을 완료하는 데 도움이 되는 하위 검사 목록의 링크가 포함되어 있습니다.  
  
> [!NOTE]  
> 이 검사 목록의 작업을 순서대로 완료하세요. 참조 링크가 개념 항목 또는 하위 검사 목록에 연결된 경우 해당 개념 항목을 검토하거나 하위 검사 목록의 작업을 완료한 후 이 항목으로 돌아와 이 검사 목록의 나머지 작업을 계속 진행해야 합니다.  
  
![페더레이션된 웹 sso](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**검사 목록: 페더레이션된 웹 Sso 디자인 구현**  
  
||태스크|참고자료|  
|-|--------|-------------|  
|![페더레이션된 웹 sso](media/icon_checkboxo.gif)|페더레이션된 웹 SSO 디자인에 대 한 중요 한 개념을 검토 하 고이 디자인을 조직의 요구에 맞게 사용자 지정 하는 데 사용할 수 있는 AD FS 배포 목표를 결정 합니다.|![페더레이션된 웹 sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[페더레이션된 웹 Sso 디자인](https://technet.microsoft.com/library/dd807050.aspx)<br /><br />](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 배포 목표를 식별 하](https://technet.microsoft.com/library/dd807053.aspx) ![페더레이션된 웹 sso<br /><br />![페더레이션된 웹 sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[배포 계획](https://technet.microsoft.com/library/dd807083.aspx)|  
|![페더레이션된 웹 sso](media/icon_checkboxo.gif)|하드웨어, 소프트웨어, 인증서, 도메인 이름 시스템 검토 \(DNS\), 특성 저장소 및 조직에서 AD FS를 배포 하기 위한 클라이언트 요구 사항입니다.|![페더레이션된 웹 sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[부록 a: AD FS 요구 사항 검토](https://technet.microsoft.com/library/ff678034.aspx)|  
|![페더레이션된 웹 sso](media/icon_checkboxo.gif)|파트너 조직 모두에서 AD FS를 배포 하기 전에 규칙, 특성 저장소 및 AD FS 구성 데이터베이스를 클레임, 클레임에 대 한 중요 한 개념을 검토 합니다.|![페더레이션된 웹 sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[핵심 AD FS 개념 이해](../../ad-fs/technical-reference/Understanding-Key-AD-FS-Concepts.md)|  
|![페더레이션된 웹 sso](media/icon_checkboxo.gif)|디자인 계획에 따라 각 파트너 조직에 하나 이상의 페더레이션 서버를 설치 합니다. **참고:** 페더레이션된 웹 SSO 디자인 하면 계정 파트너 조직에서 하나 이상의 페더레이션 서버 및 리소스 파트너 조직에서 하나 이상의 페더레이션 서버입니다.|![페더레이션된 웹 sso](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[검사 목록: 페더레이션 서버 설정](Checklist--Setting-Up-a-Federation-Server.md)|  
|![페더레이션된 웹 sso](media/icon_checkboxo.gif)|선택\) \(조직에 페더레이션 서버 프록시가 필요한 지 여부를 결정할 수 있습니다. 디자인 계획에 대 한 프록시를 호출 하는 경우에 각 파트너 조직에서 하나 이상의 페더레이션 서버 프록시를 설치할 수 있습니다.|![페더레이션된 웹 sso](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[검사 목록: 페더레이션 서버 프록시 설정](Checklist--Setting-Up-a-Federation-Server-Proxy.md)|  
|![페더레이션된 웹 sso](media/icon_checkboxo.gif)|디자인 계획에 따라 두 파트너 조직이 페더레이션 트러스트를 통해 통신할 수 있도록 두 파트너 조직 모두에서 인증서를 공유하고, 클라이언트를 구성하며, 트러스트 관계를 구성합니다.|![페더레이션된 웹 sso](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[검사 목록: 계정 파트너 조직 구성](Checklist--Configuring-the-Account-Partner-Organization.md)<br /><br />![페더레이션된 웹 sso](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[검사 목록: 리소스 파트너 조직 구성](Checklist--Configuring-the-Resource-Partner-Organization.md)|  
|![페더레이션된 웹 sso](media/icon_checkboxo.gif)|리소스 파트너 조직의 관리자 인 경우 WIF 및 WIF SDK를 사용 하 여 웹 브라우저 응용 프로그램, 웹 서비스 응용 프로그램 또는 Microsoft® Office SharePoint® 서버 응용 프로그램을 사용 하도록 클레임\-합니다.|![페더레이션된 웹 sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Identity Foundation](https://go.microsoft.com/fwlink/?LinkId=122266)<br /><br />![페더레이션된 웹 sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Identity FOUNDATION SDK](https://go.microsoft.com/fwlink/?LinkId=122266)|  
