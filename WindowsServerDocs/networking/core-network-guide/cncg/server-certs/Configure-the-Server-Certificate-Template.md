---
title: 서버 인증서 템플릿을 구성합니다
description: 이 항목은 802.1 X 유선 및 무선 배포에 대 한 배포 서버 인증서 가이드
manager: brianlic
ms.topic: article
ms.assetid: 8ff610e2-43ca-407f-a828-06d9366e02f0
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e747fedd74dfc55c2c4df457d7f107b618423b8e
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="configure-the-server-certificate-template"></a>서버 인증서 템플릿을 구성합니다

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

Active Directory 인증서 템플릿을 구성 하려면이 절차를 사용할 수 있습니다&reg; 인증서 서비스 (AD CS) 기준으로 서버로 네트워크에 등록 서버의 인증서 사용 합니다.  
  
이 서식 파일을 구성 하는 동안 서버 인증서 AD CS에서 받을 자동으로 Active Directory 그룹별로 서버를 지정할 수 있습니다.   
  
아래 절차에 다음과 같은 서버 형식의 모든 문제 인증서를 템플릿을 구성 하기 위한 지침 포함 됩니다.  
  
- 원격 액세스 RAS 게이트웨이 서버의 회원를 포함 하 여 서비스를 실행 하는 서버는 **RAS 및 서버 IAS** 그룹입니다.  
- 네트워크 NPS 정책 서버 () 서비스를 실행 하는 서버의 회원은는 **RAS 및 서버 IAS** 그룹입니다.  
  
두 멤버십 **엔터프라이즈 관리자** 및 루트 도메인 **도메인 관리자** 그룹은이 절차를 수행 하는 데 필요한 최소 합니다.  
  
### <a name="to-configure-the-certificate-template"></a>인증서 템플릿을 구성 하려면  
  
1.  서버 관리자 CA1 클릭 **도구**을 차례로 클릭 하 고 **인증 기관**합니다. 인증 기관 Microsoft Management Console (MMC)을 엽니다.  
  
2.  캘리포니아 이름을 두 번 클릭 MMC를 마우스 오른쪽 단추로 클릭 **인증서 템플릿**을 차례로 클릭 하 고 **관리**합니다.  
  
3.  인증서 템플릿 console을 엽니다. 인증서 템플릿이 모든 세부 정보 창에 표시 됩니다.  
  
4.  세부 정보 창에서 클릭는 **RAS와 IAS 서버** 서식 합니다.  
  
5.  클릭 하 고 **알림** 메뉴를 클릭 한 다음 **템플릿 복제**합니다. 서식 **속성** 대화 상자를 엽니다.  
  
6.  클릭 하 고 **보안** 탭 합니다.   
  
7.  에 **보안** 탭에 **그룹 또는 사용자 이름**, 클릭 **RAS 및 IAS 서버**합니다.  
  
8.  **RAS 및 IAS 서버에 대 한 권한**, **허용**, 되도록 **등록** 를 선택 하 고 다음는 **자동** 확인란을 선택 합니다. 클릭 **확인**, 템플릿 MMC 인증서를 닫습니다.  
  
9.  인증 기관 MMC 클릭 **인증서 템플릿**합니다. 에 **작업** 메뉴에서 **새로**을 차례로 클릭 하 고 **인증서 템플릿을 문제에**합니다. **인증서 템플릿 사용** 대화 상자를 엽니다.  
  
10. **인증서 템플릿 사용**구성 방금 인증서 서식 파일의 이름을 클릭 한 다음 클릭, **확인**합니다. 예를 들어 기본 인증서 템플릿 이름을 변경 하지 않은 클릭 **RAS 복사 및 IAS 서버**, 클릭 한 다음 **확인**합니다.  
  


