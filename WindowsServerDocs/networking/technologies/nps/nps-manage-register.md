---
title: Active Directory 도메인에서 NPS 등록
description: 이 항목을 사용 하 여 NPS 기본 도메인 또는 다른 도메인의 Windows Server 2016에서 네트워크 정책 서버를 실행 하는 서버를 등록할 수 있습니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 2de954fd-a7d8-4cc6-85b1-b0c3c06f788f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 6b72624f5817d2da5d2fb4e8622883e1ef4559cb
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71396179"
---
# <a name="register-an-nps-in-an-active-directory-domain"></a>Active Directory 도메인에서 NPS 등록

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목을 사용 하 여 NPS 기본 도메인 또는 다른 도메인의 Windows Server 2016에서 네트워크 정책 서버를 실행 하는 서버를 등록할 수 있습니다.

## <a name="register-an-nps-in-its-default-domain"></a>기본 도메인에 NPS 등록

이 절차를 사용 하 여 서버가 도메인 구성원 인 도메인에 NPS를 등록할 수 있습니다. 

NPSs는 권한 부여 프로세스 동안 사용자 계정의 전화 접속 속성을 읽을 수 있는 권한을 갖도록 Active Directory에 등록 되어야 합니다. NPS를 등록 하면 서버가 Active Directory의 **RAS 및 IAS 서버** 그룹에 추가 됩니다.

이 절차를 수행하려면 최소한 **Administrators** 그룹의 구성원이거나 이와 동등한 자격이 필요합니다.

### <a name="to-register-an-nps-in-its-default-domain"></a>기본 도메인에 NPS를 등록 하려면


1. NPS의 서버 관리자에서 **도구**를 클릭 한 다음 **네트워크 정책 서버**를 클릭 합니다. 네트워크 정책 서버 콘솔이 열립니다.

2. **NPS (로컬)** 를 마우스 오른쪽 단추로 클릭 한 다음 **Active Directory에 서버 등록**을 클릭 합니다. **네트워크 정책 서버** 대화 상자가 열립니다.

3. **네트워크 정책 서버**, 클릭 **확인**, 를 클릭 하 고 **확인** 다시 합니다.

## <a name="register-an-nps-in-another-domain"></a>다른 도메인에 NPS 등록

Active Directory에서 사용자 계정의 전화 접속 속성을 읽을 수 있는 권한을 NPS에 제공 하려면 계정이 상주 하는 도메인에 NPS를 등록 해야 합니다.

이 절차를 사용 하 여 nps가 도메인 구성원이 아닌 도메인에 NPS를 등록할 수 있습니다.

이 절차를 수행하려면 최소한 **Administrators** 그룹의 구성원이거나 이와 동등한 자격이 필요합니다.

### <a name="to-register-an-nps-in-another-domain"></a>다른 도메인에 NPS를 등록 하려면

1. 도메인 컨트롤러의 서버 관리자에서 **도구**를 클릭 한 다음 **사용자 및 컴퓨터 Active Directory**를 클릭 합니다. Active Directory 사용자 및 컴퓨터 콘솔을 엽니다.

2. 콘솔 트리에서 NPS가 사용자 계정 정보를 읽을 도메인으로 이동한 다음 **사용자** 폴더를 클릭 합니다. 

3. 세부 정보 창에서 **RAS 및 IAS 서버**를 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 클릭 합니다. **RAS 및 IAS 서버 속성** 대화 상자가 열립니다.

4. **RAS 및 IAS 서버 속성** 대화 상자에서 **구성원** 탭을 클릭 하 고 도메인에 등록 하려는 각 Npss를 추가한 다음 **확인**을 클릭 합니다.


### <a name="to-register-an-nps-in-another-domain-by-using-netsh-commands-for-nps"></a>NPS 용 Netsh 명령을 사용 하 여 다른 도메인에 NPS를 등록 하려면

1. 명령 프롬프트 또는 windows PowerShell을 엽니다. 

2. 명령 프롬프트에서 다음을 입력 합니다. **netsh nps add registeredserver** &nbsp;*도메인* &nbsp;*서버*를 입력 한 다음 enter 키를 누릅니다.

>[!NOTE]
>위의 명령에서 *domain* 은 nps를 등록할 도메인의 DNS 도메인 이름이 고, *server* 는 nps 컴퓨터의 이름입니다.

