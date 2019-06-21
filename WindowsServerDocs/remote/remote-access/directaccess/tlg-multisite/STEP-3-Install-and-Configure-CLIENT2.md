---
title: 3 설치 단계 및 CLIENT2를 구성 합니다.
description: 이 항목에서는 테스트 랩 가이드의 일부인-DirectAccess 멀티 사이트 배포에 대 한 Windows Server 2016를 보여 줍니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f009fdd1-94e6-4ccb-8c6e-609a5394db53
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 2c7ff4953fd4369340f55f40f93cfc01d4240b26
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67281463"
---
# <a name="step-3-install-and-configure-client2"></a>3 설치 단계 및 CLIENT2를 구성 합니다.

>적용 대상: Windows Server (반기 채널), Windows Server 2016

CLIENT2는 Windows 7&reg; 보여 주기 위해 사용 되는 컴퓨터는 이전 버전과 호환성을 Windows Server 2016 서버에서 실행 되는 원격 액세스 합니다.  
  
1. CLIENT2에서 운영 체제를 설치 합니다. Windows 설치&reg; 7 Enterprise 또는 Windows&reg; CLIENT2에서 7 Ultimate입니다.  
  
2. CLIENT2 CORP 도메인에 가입 합니다. CLIENT2 corp.contoso.com 도메인에 조인 합니다.  
  
## <a name="to-install-the-operating-system-on-client2"></a>CLIENT2에서 운영 체제를 설치 하려면  
  
1.  Windows 7의 설치를 시작 합니다.  
  
2.  사용자 이름을 묻는 메시지가 나타나면 입력 **User1**합니다. 컴퓨터 이름을 묻는 메시지가 나타나면 입력 **CLIENT2**합니다.  
  
3.  암호를 묻는 메시지가 나타나면 강력한 암호를 두 번 입력 합니다.  
  
4.  보호 설정에 대 한 메시지가 표시 되 면 **권장 설정 사용**합니다.  
  
5.  컴퓨터의 현재 위치에 대 한 메시지가 표시 되 면 **회사 네트워크**합니다.  
  
6.  CLIENT2를 인터넷에 연결 하는 네트워크에 연결 하 고 Windows 7에 대 한 최신 업데이트를 설치 하 고 인터넷에서 연결을 해제 하려면 Windows Update를 실행 합니다.  
  
7.  CLIENT2 Corpnet 서브넷에 연결 합니다.  
  
## <a name="user-account-control"></a>사용자 계정 컨트롤  
클릭 해야 Windows 7 운영 체제를 구성한 경우 **계속** 에 **사용자 계정 컨트롤** 일부 작업에 대 한 대화 상자 (UAC). 다양 한 구성 작업에는 UAC 승인이 필요합니다. 메시지가 표시 되는 경우 항상 클릭 **계속** 이러한 변경 권한을 부여 합니다.  
  
## <a name="to-join-client2-to-the-corp-domain"></a>CLIENT2 CORP 도메인에 가입  
  
1.  **시작**을 클릭하고 **컴퓨터**를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
2.  에 **시스템** 페이지를 **컴퓨터 이름, 도메인 및 작업 그룹 설정** 영역에서 클릭 **설정을 변경할**합니다.  
  
3.  **시스템 속성** 대화 상자의 **컴퓨터 이름** 탭에서 **변경**을 클릭합니다.  
  
4.  에 **컴퓨터 이름/도메인 변경** 대화 상자, 클릭 **도메인**, 형식 **corp.contoso.com**를 클릭 하 고 **확인**합니다.  
  
5.  사용자 이름과 암호를 묻는 메시지가 나타나면 사용자 이름 및 User1 도메인 계정의 암호를 입력 한 다음 클릭 **확인**합니다.  
  
6.  corp.contoso.com 도메인을 시작한다는 내용의 대화 상자가 표시되면 **확인**을 클릭합니다.  
  
7.  컴퓨터를 다시 시작을 클릭 하 라는 대화 상자를 표시 되 면 **확인**합니다.  
  
8.  에 **시스템 속성** 대화 상자, 클릭 **닫기**, 및 컴퓨터를 다시 시작을 클릭 하 라는 대화 상자가 표시 되 면 **지금 다시 시작**합니다.  
  
9. 컴퓨터 다시 시작 되 면 CORP\User1로 로그온 합니다.
