---
ms.assetid: 4d002764-58b4-4137-9c86-1e55b02e07ce
title: "파트너 조직 구성"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 5494f3bd8d012bf1ecc240439ff880d1bb52c280
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="configuring-partner-organizations"></a>파트너 조직 구성

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

새 파트너 조직을 Active Directory Federation Services \(AD FS\)를 배포 하려면 중 하나에서 작업을 완료 [검사: 리소스 파트너 조직 구성](Checklist--Configuring-the-Resource-Partner-Organization.md) 또는 [검사: 계정 파트너 조직 구성](Checklist--Configuring-the-Account-Partner-Organization.md)ADFS 디자인에 따라 합니다.  
  
> [!NOTE]  
> 이러한 검사를 사용 하면 좋습니다 먼저 계정 파트너 또는 계획에 대 한 지침 리소스 파트너에 대 한 언급을 읽고는 [Windows Server 2012에서 광고 FS 디자인 가이드](https://technet.microsoft.com/library/dd807036.aspx) 계속 하는 방법에 대해 새로운 파트너 조직을 설정 하기 전에 합니다. 이런 방법으로 검사를 수행 계정 파트너 또는 리소스 파트너 조직에 대 한 전체 ADFS 디자인 및 배포 이야기를 더 잘 이해를 제공 하는 데 도움이 됩니다.  
  
## <a name="about-account-partner-organizations"></a>파트너 조직 계정 정보  
계정 파트너 AD 특성 FS – 지원 되는 스토어에서 사용자 계정 물리적으로 저장 하는 federation 신뢰 관계에는 조직입니다. 계정 파트너는 수집 하 고 사용자의 자격 증명, 클레임 해당 사용자에 대 한 구성 인증과 보안 토큰으로 클레임 패키징 담당 합니다. 이 토큰 연합 신뢰 리소스 파트너 조직에 있는 Web\ 기반 리소스에 액세스할 수 있도록를 통해 제공할 수 있습니다.  
  
즉, 계정 파트너 account\ 측 federation 서버 해당 사용자에 대 한 보안 토큰 문제 조직을 나타냅니다. 계정 파트너 조직에서 federation 서버 인증 하는 로컬 사용자 하 고 승인 결정을 내리는 보안 토큰 리소스 파트너 사용을 만듭니다.  
  
특성 스토어와 관련 하 여 Adfs의 계정을 파트너는 다른 숲 속에 있는 리소스에 액세스 해야 하는 계정이 단일 Active Directory 숲 개념 같습니다. 이 숲 속의 계정 외부 신뢰 또는 숲 두 숲 사이 관계가 및 액세스 하 려는 사용자가 있는 리소스 허가가 사용 권한으로 설정한 신뢰 하는 경우에 리소스 숲 속의 리소스에 액세스할 수 있습니다.  
  
## <a name="about-resource-partner-organizations"></a>파트너 조직 리소스에 대 한  
리소스 파트너는 웹 서버는 어디에 ADFS 배포 조직 합니다. 사용자가 인증 계정 파트너가 신뢰 하는 자원 파트너 합니다. 따라서 리소스 파트너 승인 결정을 내릴 수의 사용자 계정 파트너에 게 제공 하는 보안 토큰에 패키지 클레임을 사용 합니다.  
  
즉, 리소스 파트너 resource\ 측 federation 서버에 의해 보호 하는 웹 서버를 조직을 나와 있습니다. 리소스 파트너에서 federation 서버 리소스 파트너의 웹 서버에 대 한 권한 결정 하는 계정 파트너가 생성 되는 보안 토큰을 사용 합니다.  
  
ADFS 리소스 웹 서버 리소스 파트너 조직에서 하거나 Windows 신원을 파운데이션 \(WIF\) 있어야으로 작동 하는 데 설치 하거나 설치한 Active Directory Federation Services \(AD FS\) 1.x Claims\ 인식 웹 에이전트 역할 서비스. ADFS 리소스로 작동 하는 웹 서버 browser\ 기반 시작 Web\ 또는 Web\ service\ 기반 응용 프로그램을 호스트할 수 있습니다.  
