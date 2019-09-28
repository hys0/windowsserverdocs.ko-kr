---
ms.assetid: 30657638-5709-48c5-87aa-98f688e07b4c
title: 검사 목록-웹 SSO 디자인 구현
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 8488e0c9195930374aacd959e72d0eff34142ca7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408469"
---
# <a name="checklist-implementing-a-web-sso-design"></a>검사 목록: 웹 SSO 디자인 구현

이 상위 검사 목록에는 웹 단일 @ @no__t no__t에 대 한 중요 한 개념에 대 한 참조 링크 (no__t)에 대 한 참조 링크 (Active Directory Federation Services \(AD FS @ no__t-6의 경우) 또한 이 디자인을 구현하는 데 필요한 작업을 완료하는 데 도움이 되는 하위 검사 목록의 링크가 포함되어 있습니다.  
  
> [!NOTE]  
> 이 검사 목록의 작업을 순서대로 완료하세요. 참조 링크가 개념 항목 또는 하위 검사 목록에 연결된 경우 해당 개념 항목을 검토하거나 하위 검사 목록의 작업을 완료한 후 이 항목으로 돌아와 이 검사 목록의 나머지 작업을 계속 진행해야 합니다.  
  
![web sso @ no__t-1 검사 목록: 웹 SSO 디자인 구현**  
  
||태스크|참조|  
|-|--------|-------------|  
|![웹 sso](media/icon_checkboxo.gif)|웹 SSO 디자인에 대 한 중요 한 개념을 검토 하 고이 디자인을 조직의 요구에 맞게 사용자 지정 하는 데 사용할 수 있는 AD FS 배포 목표를 결정 합니다. **참고:**|![web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[웹 Sso 디자인](https://technet.microsoft.com/library/dd807033.aspx)<br /><br />![web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 배포 목표 식별](https://technet.microsoft.com/library/dd807053.aspx)|  
|![웹 sso](media/icon_checkboxo.gif)|하드웨어, 소프트웨어, 인증서, 도메인 이름 시스템 검토 \(DNS\), 특성 저장소 및 조직에서 AD FS를 배포 하기 위한 클라이언트 요구 사항입니다.|![web sso @ no__t-1Appendix A: AD FS 요구 사항 검토](https://technet.microsoft.com/library/ff678034.aspx)|  
|![웹 sso](media/icon_checkboxo.gif)|디자인 계획에 따라 회사 네트워크 또는 경계 네트워크에 있는 하나 이상의 페더레이션 서버를 설치 합니다. **참고:** 웹 SSO 디자인을 제대로 작동 하려면 페더레이션 서버가 하나만 필요 합니다. 단일 페더레이션 서버는 클레임 공급자 역할과 신뢰 당사자 역할에서 작동합니다.|![web sso @ no__t-1 검사 목록: 페더레이션 서버 설정](Checklist--Setting-Up-a-Federation-Server.md)|  
|![웹 sso](media/icon_checkboxo.gif)|@no__t 선택적 @ no__t-1은 조직에 경계 네트워크에 페더레이션 서버 프록시가 필요한 지 여부를 결정 합니다.|![web sso @ no__t-1 검사 목록: 페더레이션 서버 프록시 설정](Checklist--Setting-Up-a-Federation-Server-Proxy.md)|  
|![웹 sso](media/icon_checkboxo.gif)|웹 SSO 디자인 계획 및 이를 사용하려는 방법에 따라 적절한 특성 저장소, 신뢰 당사자 트러스트, 클레임 및 클레임 규칙을 페더레이션 서비스에 추가합니다.|![web sso @ no__t-1 검사 목록: 계정 파트너 조직 구성 @ no__t-0|  
|![웹 sso](media/icon_checkboxo.gif)|리소스 파트너 조직의 관리자 인 경우 클레임 @ no__t-0enable 및 WIF SDK를 사용 하 여 웹 브라우저 응용 프로그램, 웹 서비스 응용 프로그램 또는 Microsoft® Office SharePoint® Server 응용 프로그램을 사용 하도록 설정 합니다. **참고:**|![web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Identity Foundation](https://go.microsoft.com/fwlink/?LinkId=122266)<br /><br />![web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Identity FOUNDATION SDK](https://go.microsoft.com/fwlink/?LinkId=122266)| 
