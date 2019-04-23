---
title: Active Directory 관리 센터에서 다른 도메인 관리
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 5f253bd4952d8a347e97eafdb38d86fa98024b8d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839944"
---
# <a name="manage-different-domains-in-active-directory-administrative-center"></a>Active Directory 관리 센터에서 다른 도메인 관리

>적용 대상: Windows Server (반기 채널), Windows Server 2016

  여는 경우 Active Directory 관리, 현재 로그온에이 컴퓨터는 도메인 \(로컬 도메인\) Active Directory 관리 센터 탐색 창에 나타납니다 \(왼쪽된창\). 로그온 자격 증명의 현재 집합의 권한에 따라 볼 수도 있고이 로컬 도메인의 Active Directory 개체를 관리할 수 있습니다.

 보거나 동일한 포리스트의 다른 도메인 또는 로컬 트러스트 관계에 있는 다른 포리스트에 있는 도메인의 Active Directory 개체를 관리 하려면 Active Directory 관리 센터의 동일한 인스턴스와 로그온 자격 증명의 동일한 집합을 사용할 수도 있습니다. 도메인입니다. 둘\-양방향 트러스트 및 두 개의\-양방향 트러스트 지원 됩니다.

> [!NOTE]
>  있는 경우\-도메인 A와 도메인 B는 도메인 A의 사용자가 도메인 B의 리소스에 액세스할 수 있지만 도메인 B의 사용자가 컴퓨터에서 Active Directory 관리 센터를 실행 하는 경우 도메인 A의 리소스에에서 액세스할 수 없습니다 간에 양방향 트러스트 도메인 A가 로컬 도메인에 현재 로그온 자격 증명 및 Active Directory 관리 센터 인스턴스에서 동일한 집합을 사용 하 여 도메인 B에 연결할 수 있습니다. 하지만 실행 하는 경우 Active Directory 관리 센터 컴퓨터의 도메인 B가 로컬 도메인, 도메인 A는 동일한 Active Directory 관리 센터 인스턴스에서 동일한 자격 증명 집합을 사용 하 여을 연결할 수 없습니다.

 이 절차를 완료하는 데 필요한 최소 그룹 구성원 자격은 없습니다.

### <a name="windows-server-2012-to-manage-a-foreign-domain-in-the-selected-instance-of-active-directory-administrative-center-using-the-current-set-of-logon-credentials"></a>Windows Server 2012: 현재 로그온 자격 증명을 사용 하 여 Active Directory 관리 센터의 선택한 인스턴스에서 외부 도메인을 관리 하려면

1.  Active Directory 관리 센터를 열려면 **서버 관리자**, 클릭 **도구**를 클릭 하 고 **Active Directory 관리 센터**합니다.

    > [!NOTE]
    >  Active Directory 관리 센터를 열 수를 클릭 하는 것 **시작**를 차례로 **dsac.exe**합니다.

2.  열려는 **탐색 노드 추가**, 클릭 **관리**, 클릭 **탐색 노드 추가** 다음 그림과에서 같이 합니다.

     ![보여 주는 스크린샷 * * 추가 탐색 노드 * * UI](media/ADDS_ADACAddNavNode.gif)

3.  **탐색 노드 추가**, 클릭 **다른 도메인에 연결** 다음 그림과에서 같이 합니다.

     ![보여 주는 스크린샷 * * 추가 탐색 노드 * * UI](media/ADDS_ADACConnectToDomain.gif)

4.  **연결할**, 관리 하려는 외부 도메인의 이름을 입력 \(예를 들어 **contoso.com**\)를 클릭 하 고 **확인**합니다.

5.  열을 탐색 하는 외부 도메인에 연결 하는 경우는 **탐색 노드 추가** 창에 Active Directory 관리 센터 탐색 창에 추가할 컨테이너를 선택 하 고 누른 **확인**합니다.

### <a name="windows-server-2008-r2-to-manage-a-foreign-domain-in-the-selected-instance-of-active-directory-administrative-center-using-the-current-set-of-logon-credentials"></a>Windows Server 2008 R2: 현재 로그온 자격 증명을 사용 하 여 Active Directory 관리 센터의 선택한 인스턴스에서 외부 도메인을 관리 하려면

1.  Active Directory 관리 센터를 열려면 **시작**, 클릭 **관리 도구**를 클릭 하 고 **Active Directory 관리 센터**합니다.

    > [!NOTE]
    >  Active Directory 관리 센터를 열 수를 클릭 하는 것 **시작**, 클릭 **실행**, 차례로 **dsac.exe**합니다.

2.  열려는 **탐색 노드 추가**, Active Directory 관리 센터 창의 위쪽에 클릭 **탐색 노드 추가** 다음 그림과에서 같이 합니다.

     ![보여 주는 스크린샷 * * 추가 탐색 노드 * * UI](media/click_add_nav_nodes.gif)

    > [!NOTE]
    >  또 다른 방법은 엽니다 **탐색 노드 추가** 오른쪽에\-Active Directory 관리 센터 탐색 창에서 빈 공간에서 아무 곳 이나 클릭 한 다음 클릭 **탐색 노드 추가**.

3.  **탐색 노드 추가**, 클릭 **다른 도메인에 연결** 다음 그림과에서 같이 합니다.

     ![보여 주는 스크린샷 * * 추가 탐색 노드 * * * * 다른 도메인 * * UI에 연결](media/add_nav_nodes.gif)

4.  **연결할**, 관리 하려는 외부 도메인의 이름을 입력 \(예를 들어 **contoso.com**\)를 클릭 하 고 **확인**합니다.

5.  열을 탐색 하는 외부 도메인에 연결 하는 경우는 **탐색 노드 추가** 창에 Active Directory 관리 센터 탐색 창에 추가할 컨테이너를 선택 하 고 누른 **확인**합니다.

 Active Directory 관리 센터 탐색 창 사용자 지정 하는 방법에 대 한 자세한 내용은 참조 하세요. [Active Directory 관리 센터 탐색 창 사용자 지정](customize-the-active-directory-administrative-center-navigation-pane.md)합니다.

 또한 로그온 자격 증명 집합을 다른 로그온 자격 증명의 현재 집합을 사용 하 여 Active Directory 관리 센터를 열 수 있습니다. 다음 절차의 명령은 정상적인 사용자 자격 증명을 사용 하 여 Active Directory 관리 센터를 실행 하는 컴퓨터에 로그온 하는 경우 유용할 수 있습니다 하지만이 컴퓨터에 Active Directory 관리 센터를 사용 하 여 관리 하려는 사용자 관리자 권한으로 로컬 도메인입니다. \(이 명령은 Active Directory 관리 센터를 사용 하 여 자격 증명 집합을 다른 로그온 자격 증명의 현재 집합을 사용 하 여 로컬 도메인에서 다른 외부 도메인을 원격으로 관리 하려는 경우에 유용할 수도 있습니다. 그러나 외부 도메인에 로컬 도메인과 트러스트 관계가 설정된 있어야 합니다.\)

 이 절차를 완료하는 데 필요한 최소 그룹 구성원 자격은 없습니다.

### <a name="to-manage-a-domain-using-logon-credentials-that-are-different-from-the-current-set-of-logon-credentials"></a>현재 로그온 자격 증명 집합과는 다른 로그온 자격 증명을 사용하여 도메인을 관리하려면

1.  Active Directory 관리 센터를 명령 프롬프트를 열려면 다음 명령을 입력 하 고 enter 키를 누릅니다.

     `runas /user:<domain\user> dsac`

     여기서 `<domain\user>` 는 Active Directory 관리 센터를 열려고 하는 자격 증명 집합이 며 및 `dsac` 실행 파일 이름은 Active Directory 관리 센터 \(Dsac.exe\)합니다.

     예를 들어 다음 명령을 입력한 후 Enter 키를 누릅니다.

     `runas /user:contoso\administrator dsac`

2.  Active Directory 관리 센터 열려 있는 보거나 Active Directory 도메인을 관리 하려면 탐색 창 탐색 합니다.

  

