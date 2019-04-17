---
title: NPS 서버 Active Directory 도메인 프로그램 등록
description: Windows Server 2016 NPS 서버 기본 도메인 또는 다른 도메인 네트워크 정책 서버를 실행 하는 서버에 등록할 수이 항목을 사용할 수 있습니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 2de954fd-a7d8-4cc6-85b1-b0c3c06f788f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7ba18f6c994e8b15da3a07a3e37550d5dbff24af
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="register-an-nps-server-in-an-active-directory-domain"></a>NPS 서버 Active Directory 도메인 프로그램 등록

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

Windows Server 2016 NPS 서버 기본 도메인 또는 다른 도메인 네트워크 정책 서버를 실행 하는 서버에 등록할 수이 항목을 사용할 수 있습니다.

## <a name="register-an-nps-server-in-its-default-domain"></a>기본 도메인에 NPS 서버 등록

이 절차 NPS 서버 서버 도메인 구성원 되는 도메인의 등록에 사용할 수 있습니다. 

NPS 서버 인증 과정에서 사용자 계정의 전화 속성 읽을 수 있도록 Active Directory에 등록 해야 합니다. 서버를 추가 하는 NPS 서버 등록는 **RAS 및 서버 IAS** Active Directory에 그룹입니다.

회원 **관리자**, 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.

### <a name="to-register-an-nps-server-in-its-default-domain"></a>NPS 서버 기본 도메인에 등록 하려면


1. 서버 관리자에서 NPS 서버에서 클릭 **도구**을 차례로 클릭 하 고 **네트워크 정책 서버**합니다. 네트워크 정책 서버 console을 엽니다.

2. 마우스 오른쪽 단추로 클릭 **NPS (로컬)**을 차례로 클릭 하 고 **서버 Active Directory에 등록**합니다. **네트워크 정책 서버** 대화 상자를 엽니다.

3. **네트워크 정책 서버**, 클릭 **확인**을 차례로 클릭 하 고 **확인** 다시 합니다.

## <a name="register-an-nps-server-in-another-domain"></a>다른 도메인에 NPS 서버 등록

NPS 서버와의 사용자 계정 Active Directory 전화 접속 속성에 읽을 수 있는 권한을 제공, NPS 서버 계정의 위치 도메인에 등록 해야 합니다.

이 절차 NPS 서버 NPS 서버는 도메인 구성원이 아닙니다 도메인에 등록에 사용할 수 있습니다.

회원 **관리자**, 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.

### <a name="to-register-an-nps-server-in-another-domain"></a>NPS 서버 다른 도메인에 등록 하려면

1. 도메인 컨트롤러 서버 관리자에서 클릭 **도구**을 차례로 클릭 하 고 **Active Directory 사용자 및 컴퓨터**합니다. 콘솔 Active Directory 사용자 및 컴퓨터 엽니다.

2. 콘솔 트리에서 사용자 계정 정보를 읽는 NPS 서버 도메인으로 이동 하 고 클릭 한 다음는 **사용자** 폴더 합니다. 

3. 세부 정보 창에서 마우스 오른쪽 단추로 클릭 **RAS 및 서버 IAS**을 차례로 클릭 하 고 **속성**합니다. **RAS 및 서버 속성 IAS** 대화 상자를 엽니다.

4. 에 **RAS 및 서버 속성 IAS** 대화 상자를 클릭는 **회원** 탭, NPS 서버의 하는 도메인에 등록 하 고 클릭 한 다음 원하는 각 추가 **확인**합니다.


### <a name="to-register-an-nps-server-in-another-domain-by-using-netsh-commands-for-nps"></a>Netsh 명령을 NPS에 대 한 사용 하 여 NPS 서버 다른 도메인에 등록 하려면

1. Windows PowerShell 또는 명령 프롬프트를 엽니다. 

2. 명령 프롬프트에서 다음 명령을 입력: **netsh nps registeredserver 추가**&nbsp;*도메인*&nbsp;*서버*, ENTER 키를 누릅니다.

>[!NOTE]
>이전 명령에서 *도메인* NPS 서버 등록을 도메인 DNS 도메인 이름입니다 및 *서버* NPS 서버 컴퓨터의 이름입니다.

