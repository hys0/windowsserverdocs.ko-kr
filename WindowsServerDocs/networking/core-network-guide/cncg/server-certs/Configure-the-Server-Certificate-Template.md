---
title: 서버 인증서 템플릿 구성
description: 이 항목은 서버 배포 인증서 802.1 X 유선 및 무선 배포 가이드의 일부
manager: brianlic
ms.topic: article
ms.assetid: 8ff610e2-43ca-407f-a828-06d9366e02f0
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 238579c945821d19e45dad7e623450d598830596
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886124"
---
# <a name="configure-the-server-certificate-template"></a>서버 인증서 템플릿 구성

>적용 대상: Windows Server (반기 채널), Windows Server 2016

Active Directory 인증서 템플릿을 구성 하려면이 절차를 사용할 수 있습니다&reg; 네트워크에서 서버에 등록 된 서버 인증서의 기반으로 인증서 서비스 (AD CS)에서 사용 합니다.  
  
이 템플릿을 구성 하는 동안 AD CS에서 서버 인증서를 자동으로 수신 해야 하는 Active Directory 그룹에 의해 서버를 지정할 수 있습니다.   
  
다음 절차는 다음과 같은 서버 유형의 모든 인증서를 발급 하도록 템플릿을 구성 하기 위한 지침에 포함 됩니다.  
  
- 구성원 인 RAS 게이트웨이 서버를 포함 하는 원격 액세스 서비스를 실행 하는 서버는 **RAS and IAS Servers** 그룹입니다.  
- 네트워크 정책 (NPS 서버) 서비스를 실행 하는 서버는의 멤버는 **RAS and IAS Servers** 그룹입니다.  
  
둘 다의 구성원은 **Enterprise Admins** 및 루트 도메인의 **Domain Admins** 그룹은이 절차를 완료 하려면 최소한 합니다.  
  
### <a name="to-configure-the-certificate-template"></a>인증서 템플릿을 구성 하려면  
  
1.  서버 관리자에서 c a 1에서 클릭 **도구**, 를 클릭 하 고 **인증 기관**합니다. 인증 기관 Microsoft Management Console (MMC)가 열립니다.  
  
2.  MMC에서 CA 이름을 두 번 클릭 마우스 오른쪽 단추로 클릭 **인증서 템플릿**, 를 클릭 하 고 **관리**합니다.  
  
3.  인증서 템플릿 콘솔이 열립니다. 인증서 템플릿의 모든 세부 정보 창에 표시 됩니다.  
  
4.  세부 정보 창에서 클릭 된 **RAS 및 IAS 서버** 템플릿.  
  
5.  클릭 된 **작업** 메뉴를 차례로 클릭 **중복 된 템플릿**합니다. 서식 파일 **속성** 대화 상자가 열립니다.  
  
6.  **보안** 탭을 클릭합니다.   
  
7.  에 **보안** 탭 **그룹 또는 사용자 이름**, 클릭 **RAS 및 IAS 서버**합니다.  
  
8.  **RAS 및 IAS 서버에 대 한 권한을**, 아래에서 **허용**, 되도록 **등록** 를 선택한 다음는 **자동 등록** 확인란 합니다. 클릭 **확인**, 인증서 템플릿 MMC를 닫습니다.  
  
9.  인증 기관 MMC에서 클릭 **인증서 템플릿**합니다. 에 **작업** 메뉴에서 **새로**, 를 클릭 하 고 **발급할 인증서 템플릿**합니다. **인증서 템플릿 사용** 대화 상자가 열립니다.  
  
10. **인증서 템플릿 사용**, 구성, 방금 인증서 템플릿의 이름을 클릭 하 고 클릭 한 다음 **확인**합니다. 예를 들어, 기본 인증서 템플릿 이름을 변경 하지 않은 경우 클릭 하 여 **복사본의 RAS 및 IAS 서버**, 를 클릭 하 고 **확인**합니다.  
  


