---
title: Active Directory 도메인에서 NPS 등록
description: 네트워크 정책 서버 NPS 기본 도메인 또는 다른 도메인의 Windows Server 2016에서 실행 하는 서버를 등록 하려면이 항목에서는 사용할 수 있습니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 2de954fd-a7d8-4cc6-85b1-b0c3c06f788f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4a289ec519e5107576becf2905cd881cf9def190
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877654"
---
# <a name="register-an-nps-in-an-active-directory-domain"></a>Active Directory 도메인에서 NPS 등록

>적용 대상: Windows Server (반기 채널), Windows Server 2016

네트워크 정책 서버 NPS 기본 도메인 또는 다른 도메인의 Windows Server 2016에서 실행 하는 서버를 등록 하려면이 항목에서는 사용할 수 있습니다.

## <a name="register-an-nps-in-its-default-domain"></a>기본 도메인에서 NPS 등록

NPS 서버는 도메인 구성원 인 도메인에 등록 하려면이 절차를 사용할 수 있습니다. 

권한 부여 프로세스 동안 사용자 계정 전화 접속 속성을 읽을 수 있는 권한을 갖도록 NPSs Active Directory에 등록 되어야 합니다. 서버를 추가 하는 NPS를 등록 합니다 **RAS and IAS Servers** Active Directory의 그룹입니다.

이 절차를 수행하려면 최소한 **Administrators** 그룹의 구성원이거나 이와 동등한 자격이 필요합니다.

### <a name="to-register-an-nps-in-its-default-domain"></a>기본 도메인에서 NPS를 등록 하려면


1. NPS를 서버 관리자에서 클릭 **도구**를 클릭 하 고 **네트워크 정책 서버**합니다. 네트워크 정책 서버 콘솔이 열립니다.

2. 마우스 오른쪽 단추로 클릭 **NPS (로컬)** 를 클릭 하 고 **Active Directory에 서버 등록**합니다. **네트워크 정책 서버** 대화 상자가 열립니다.

3. **네트워크 정책 서버**, 클릭 **확인**, 를 클릭 하 고 **확인** 다시 합니다.

## <a name="register-an-nps-in-another-domain"></a>다른 도메인에는 NPS를 등록 합니다.

Active Directory의 사용자 계정 전화 접속 속성을 읽을 수 있는 권한을 가진 NPS를 제공 하려면 NPS는 계정이 있는 도메인에 등록 되어야 합니다.

NPS는 도메인 구성원이 아닙니다를 도메인에는 NPS를 등록 하려면이 절차를 사용할 수 있습니다.

이 절차를 수행하려면 최소한 **Administrators** 그룹의 구성원이거나 이와 동등한 자격이 필요합니다.

### <a name="to-register-an-nps-in-another-domain"></a>다른 도메인에는 NPS를 등록 하려면

1. 도메인 컨트롤러에서 서버 관리자에서 클릭 **도구**를 클릭 하 고 **Active Directory Users and Computers**합니다. Active Directory 사용자 및 컴퓨터 콘솔을 엽니다.

2. 콘솔 트리에서 사용자 계정 정보를 읽지 NPS를 만들려는 도메인으로 이동 하 고 클릭 합니다 **사용자** 폴더입니다. 

3. 세부 정보 창에서 마우스 오른쪽 단추로 클릭 **RAS and IAS Servers**를 클릭 하 고 **속성**합니다. 합니다 **RAS 및 IAS 서버 속성** 대화 상자가 열립니다.

4. 에 **RAS 및 IAS 서버 속성** 대화 상자에서 클릭 합니다 **멤버** 탭에서 각 도메인에 등록 하 고 클릭 하려는 NPSs 추가 **확인**합니다.


### <a name="to-register-an-nps-in-another-domain-by-using-netsh-commands-for-nps"></a>NPS 용 Netsh 명령을 사용 하 여 다른 도메인에는 NPS를 등록 하려면

1. 명령 프롬프트 또는 windows PowerShell 엽니다. 

2. 명령 프롬프트에서 다음을 입력: **netsh nps 추가 registeredserver** &nbsp; *도메인* &nbsp; *server*, 한 다음 ENTER를 누릅니다.

>[!NOTE]
>이전 명령에서 *도메인* NPS를 등록 하려는 도메인의 DNS 도메인 이름 및 *server* NPS 컴퓨터의 이름입니다.

