---
title: Active Directory 관리 센터에서 다른 도메인 관리
ms.prod: windows-server
description: Windows Server 보안
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.assetid: 166351c3-4076-48be-aa8f-797adf1e9d68
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 71edf6bb38cc665fe5c780ce986d0c0b8807d6ab
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386933"
---
# <a name="manage-different-domains-in-active-directory-administrative-center"></a>Active Directory 관리 센터에서 다른 도메인 관리

>적용 대상: Windows Server(반기 채널), Windows Server 2016

  Active Directory 관리를 열면 해당 컴퓨터에서 현재 로그온 되어 있는 도메인이 로컬 도메인\) \(왼쪽 창 \(Active Directory 관리 센터 탐색 창에 표시 됩니다.\) 현재 로그온 자격 증명 집합의 권한에 따라이 로컬 도메인의 Active Directory 개체를 보거나 관리할 수 있습니다.

 동일한 로그온 자격 증명 집합 및 동일한 Active Directory 관리 센터 인스턴스를 사용 하 여 동일한 포리스트의 다른 도메인에 있는 Active Directory 개체를 확인 하거나 관리 하거나 로컬와의 트러스트 관계가 설정 된 다른 포리스트의 도메인을 볼 수도 있습니다. 도메인. \-단방향 트러스트와 두 개의\-단방향 트러스트가 지원 됩니다.

> [!NOTE]
>  도메인 a의 사용자가 도메인 B의 리소스에 액세스할 수 있지만 도메인 B의 사용자가 도메인 A의 리소스에 액세스할 수 있는 도메인 a와 도메인 B 간에\-단방향 트러스트 관계가 있는 경우 도메인 B의 사용자는 도메인 A의 리소스에 액세스할 수 없으며, 도메인 A가 로컬 도메인에 있는 컴퓨터에서 Active Directory 관리 센터를 실행 하는 경우 현재 로그온 자격 증명 집합과 동일한 Active Directory 관리 센터 인스턴스를 사용 하 여 도메인 그러나 도메인 B가 로컬 도메인에 있는 컴퓨터에서 Active Directory 관리 센터를 실행 하는 경우 동일한 Active Directory 관리 센터 인스턴스에서 동일한 자격 증명 집합을 사용 하 여 도메인 A에 연결할 수 없습니다.

 이 절차를 완료하는 데 필요한 최소 그룹 구성원 자격은 없습니다.

### <a name="windows-server-2012-to-manage-a-foreign-domain-in-the-selected-instance-of-active-directory-administrative-center-using-the-current-set-of-logon-credentials"></a>Windows Server 2012: 현재 로그온 자격 증명 집합을 사용 하 여 Active Directory 관리 센터의 선택 된 인스턴스에서 외부 도메인을 관리 하려면

1.  Active Directory 관리 센터를 열려면 **서버 관리자**에서 **도구**를 클릭 한 다음 **Active Directory 관리 센터**을 클릭 합니다.

    > [!NOTE]
    >  **시작**을 클릭 한 다음 **dsac .exe**를 입력 하 여 Active Directory 관리 센터를 열 수도 있습니다.

2.  **탐색 노드 추가**를 열려면 다음 그림과 같이 **관리**를 클릭 하 고 **탐색 노드 추가** 를 클릭 합니다.

     ![\* * 탐색 노드 추가 * * UI를 보여 주는 스크린샷](media/ADDS_ADACAddNavNode.gif)

3.  **탐색 노드 추가**에서 다음 그림에 표시 된 것 처럼 **다른 도메인에 연결** 을 클릭 합니다.

     ![\* * 탐색 노드 추가 * * UI를 보여 주는 스크린샷](media/ADDS_ADACConnectToDomain.gif)

4.  **연결 대상**에 \(관리 하려는 외부 도메인의 이름을 입력 하 고 예를 들어 **contoso.com**\)을 입력 한 다음 **확인**을 클릭 합니다.

5.  외래 도메인에 성공적으로 연결 되 면 **탐색 노드 추가** 창에서 열을 찾아 Active Directory 관리 센터 탐색 창에 추가할 컨테이너를 선택 하 고 **확인**을 클릭 합니다.

### <a name="windows-server-2008-r2-to-manage-a-foreign-domain-in-the-selected-instance-of-active-directory-administrative-center-using-the-current-set-of-logon-credentials"></a>Windows Server 2008 R2: 현재 로그온 자격 증명 집합을 사용 하 여 Active Directory 관리 센터의 선택 된 인스턴스에서 외부 도메인을 관리 하려면

1. Active Directory 관리 센터를 열려면 **시작**, **관리 도구**, **Active Directory 관리 센터**를 차례로 클릭 합니다.

   > [!NOTE]
   >  **시작**을 클릭 하 고 **실행**을 클릭 한 다음 **dsac .exe**를 입력 하 여 Active Directory 관리 센터를 열 수도 있습니다.

2. **탐색 노드 추가**를 열려면 Active Directory 관리 센터 창의 맨 위에 있는 다음 그림과 같이 **탐색 노드 추가** 를 클릭 합니다.

    ![\* * 탐색 노드 추가 * * UI를 보여 주는 스크린샷](media/click_add_nav_nodes.gif)

   > [!NOTE]
   >  **탐색 노드 추가** 를 열려면 Active Directory 관리 센터 탐색 창에서 빈 공간을 마우스 오른쪽 단추로 클릭\-다음 **탐색 노드 추가**를 클릭 합니다.

3. **탐색 노드 추가**에서 다음 그림에 표시 된 것 처럼 **다른 도메인에 연결** 을 클릭 합니다.

    ![\* * 탐색 노드 추가 * * * * 다른 도메인에 연결 * * UI를 보여 주는 스크린샷](media/add_nav_nodes.gif)

4. **연결 대상**에 \(관리 하려는 외부 도메인의 이름을 입력 하 고 예를 들어 **contoso.com**\)을 입력 한 다음 **확인**을 클릭 합니다.

5. 외래 도메인에 성공적으로 연결 되 면 **탐색 노드 추가** 창에서 열을 찾아 Active Directory 관리 센터 탐색 창에 추가할 컨테이너를 선택 하 고 **확인**을 클릭 합니다.

   Active Directory 관리 센터 탐색 창을 사용자 지정 하는 방법에 대 한 자세한 내용은 [Active Directory 관리 센터 탐색 창 사용자 지정](customize-the-active-directory-administrative-center-navigation-pane.md)을 참조 하세요.

   현재 로그온 자격 증명 집합과는 다른 로그온 자격 증명 집합을 사용 하 여 Active Directory 관리 센터를 열 수도 있습니다. 일반 사용자 자격 증명을 사용 하 여 Active Directory 관리 센터를 실행 하는 컴퓨터에 로그온 했지만이 컴퓨터의 Active Directory 관리 센터를 사용 하 여를 관리 하려면 다음 절차의 명령이 유용할 수 있습니다. 관리자 인 로컬 도메인입니다. 이 명령은 Active Directory 관리 센터를 사용 하 여 현재 로그온 자격 증명 집합과 다른 자격 증명 집합을 사용 하 여 로컬 도메인과 다른 외부 도메인을 원격으로 관리 하려는 경우에도 유용할 수 있습니다. \( 그러나 외부 도메인에는 로컬 도메인과의 트러스트가 설정 되어 있어야 합니다.\)

   이 절차를 완료하는 데 필요한 최소 그룹 구성원 자격은 없습니다.

### <a name="to-manage-a-domain-using-logon-credentials-that-are-different-from-the-current-set-of-logon-credentials"></a>현재 로그온 자격 증명 집합과는 다른 로그온 자격 증명을 사용하여 도메인을 관리하려면

1.  Active Directory 관리 센터를 열려면 명령 프롬프트에서 다음 명령을 입력 한 후 ENTER 키를 누릅니다.

     `runas /user:<domain\user> dsac`

     여기서 `<domain\user>`은 Active Directory 관리 센터 열려는 자격 증명 집합이 고 `dsac` Active Directory 관리 센터 실행 파일 이름 \(Dsac .exe\)입니다.

     예를 들어 다음 명령을 입력한 후 Enter 키를 누릅니다.

     `runas /user:contoso\administrator dsac`

2.  Active Directory 관리 센터 열려 있으면 탐색 창을 탐색 하 여 Active Directory 도메인을 보거나 관리 합니다.

  

