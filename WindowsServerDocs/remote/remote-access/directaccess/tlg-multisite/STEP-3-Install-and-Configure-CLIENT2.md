---
title: 3 단계 CLIENT2 설치 및 구성
description: 이 항목은 테스트 랩 가이드-Windows Server 2016에 대 한 DirectAccess 멀티 사이트 배포 시연의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f009fdd1-94e6-4ccb-8c6e-609a5394db53
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4b2d8cb1538de35a97ae83888d26abd7ad7bc8b3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71388322"
---
# <a name="step-3-install-and-configure-client2"></a>3 단계 CLIENT2 설치 및 구성

>적용 대상: Windows Server(반기 채널), Windows Server 2016

CLIENT2는 Windows Server 2016 서버에서 실행 되는 원격 액세스의 이전 버전과의 호환성을 보여 주는 데 사용 되는 Windows 7 @ no__t 컴퓨터입니다.  
  
1. CLIENT2에 운영 체제를 설치 합니다. CLIENT2에 Windows @ no__t-0 7 Enterprise 또는 Windows @ no__t-1 7 Ultimate를 설치 합니다.  
  
2. CLIENT2를 CORP 도메인에 가입 시킵니다. CLIENT2을 corp.contoso.com 도메인에 가입 시킵니다.  
  
## <a name="to-install-the-operating-system-on-client2"></a>CLIENT2에 운영 체제를 설치 하려면  
  
1.  Windows 7 설치를 시작 합니다.  
  
2.  사용자 이름을 입력 하 라는 메시지가 표시 되 면 **User1**을 입력 합니다. 컴퓨터 이름을 입력 하 라는 메시지가 표시 되 면 **CLIENT2**를 입력 합니다.  
  
3.  암호를 입력 하 라는 메시지가 표시 되 면 강력한 암호를 두 번 입력 합니다.  
  
4.  보호 설정을 입력 하 라는 메시지가 표시 되 면 **권장 설정 사용**을 클릭 합니다.  
  
5.  컴퓨터의 현재 위치를 묻는 메시지가 표시 되 면 **회사 네트워크**를 클릭 합니다.  
  
6.  인터넷에 연결 된 네트워크에 CLIENT2을 연결 하 고 Windows 업데이트를 실행 하 여 Windows 7 용 최신 업데이트를 설치한 다음 인터넷 연결을 끊습니다.  
  
7.  CLIENT2을 Corpnet 서브넷에 연결 합니다.  
  
## <a name="user-account-control"></a>사용자 계정 컨트롤  
Windows 7 운영 체제를 구성 하는 경우 일부 작업의 경우 UAC ( **사용자 계정 컨트롤** ) 대화 상자에서 **계속** 을 클릭 해야 합니다. 몇 가지 구성 작업을 수행 하려면 UAC 승인이 필요 합니다. 메시지가 표시 되 면 항상 **계속** 을 클릭 하 여 이러한 변경 내용을 승인 합니다.  
  
## <a name="to-join-client2-to-the-corp-domain"></a>CLIENT2를 CORP 도메인에 가입 시키려면  
  
1.  **시작**을 클릭하고 **컴퓨터**를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
2.  **시스템** 페이지의 **컴퓨터 이름, 도메인 및 작업 그룹 설정** 영역에서 **설정 변경**을 클릭 합니다.  
  
3.  **시스템 속성** 대화 상자의 **컴퓨터 이름** 탭에서 **변경**을 클릭합니다.  
  
4.  **컴퓨터 이름/도메인 변경** 대화 상자에서 **도메인**을 클릭 하 고 **Corp.contoso.com**를 입력 한 다음 **확인**을 클릭 합니다.  
  
5.  사용자 이름 및 암호를 입력 하 라는 메시지가 표시 되 면 User1 도메인 계정의 사용자 이름 및 암호를 입력 한 다음 **확인**을 클릭 합니다.  
  
6.  corp.contoso.com 도메인을 시작한다는 내용의 대화 상자가 표시되면 **확인**을 클릭합니다.  
  
7.  컴퓨터를 다시 시작 하 라는 대화 상자가 표시 되 면 **확인**을 클릭 합니다.  
  
8.  **시스템 속성** 대화 상자에서 **닫기**를 클릭 하 고 컴퓨터를 다시 시작 하 라는 대화 상자가 표시 되 면 **지금 다시 시작**을 클릭 합니다.  
  
9. 컴퓨터를 다시 시작한 후 Corp\user1 계정로 로그온 합니다.
