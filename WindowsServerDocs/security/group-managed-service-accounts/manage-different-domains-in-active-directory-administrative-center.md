---
title: "관리 센터 Active Directory에에서 다른 도메인 관리"
ms.prod: windows-server-threshold
description: "Windows Server 보안"
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
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="manage-different-domains-in-active-directory-administrative-center"></a>관리 센터 Active Directory에에서 다른 도메인 관리

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

  When you open Active Directory Administrative, the domain that you are currently logged on to on this computer \(the local domain\) appears in the Active Directory Administrative Center navigation pane \(the left pane\). Depending on the rights of your current set of logon credentials, you can view or manage the Active Directory objects in this local domain.

 You can also use the same set of logon credentials and the same instance of Active Directory Administrative Center to view or manage Active Directory objects in any other domain in the same forest, or a domain in another forest that has an established trust with the local domain. One\ 방향 신뢰 및 two\ 방향 신뢰 지원 됩니다.

> [!NOTE]
>  If there is a one\-way trust between Domain A and Domain B through which users in Domain A can access resources in Domain B but users in Domain B cannot access resources in Domain A, if you are running Active Directory Administrative Center on the computer where Domain A is your local domain, you can connect to Domain B with the current set of logon credentials and in the same instance of Active Directory Administrative Center. But if you are running Active Directory Administrative Center on the computer where Domain B is your local domain, you cannot connect to Domain A with the same set of credentials in the same instance of the Active Directory Administrative Center.

 이 절차를 수행 하는 데 필요한 없는 최소 그룹 구성원이 있습니다.

### <a name="windows-server-2012-to-manage-a-foreign-domain-in-the-selected-instance-of-active-directory-administrative-center-using-the-current-set-of-logon-credentials"></a>Windows Server 2012: To manage a foreign domain in the selected instance of Active Directory Administrative Center using the current set of logon credentials

1.  To open Active Directory Administrative Center, in **Server Manager**, click **Tools**, and then click **Active Directory Administrative Center**.

    > [!NOTE]
    >  Another way to open Active Directory Administrative Center is to click **Start**, and then type **dsac.exe**.

2.  열려는 **탐색 노드 추가**, 클릭 **관리**, 클릭 한 다음 **탐색 노드 추가** 다음과 같이 합니다.

     ![보여 주는 스크린샷 * * 탐색 노드 * * UI를 추가](media/ADDS_ADACAddNavNode.gif)

3.  **탐색 노드 추가**, 클릭 **다른 도메인에 연결** 다음과 같이 합니다.

     ![보여 주는 스크린샷 * * 탐색 노드 * * UI를 추가](media/ADDS_ADACConnectToDomain.gif)

4.  **연결할**, 이름을 입력 하 고 관리 하려면 외부 도메인의 \ (예를 들어, **contoso.com**\)을 차례로 클릭 하 고 **확인**합니다.

5.  When you are successfully connected to the foreign domain, browse through the columns in the **Add Navigation Nodes** window, select the container or containers to add to your Active Directory Administrative Center navigation pane, and then click **OK**.

### <a name="windows-server-2008-r2-to-manage-a-foreign-domain-in-the-selected-instance-of-active-directory-administrative-center-using-the-current-set-of-logon-credentials"></a>Windows Server 2008 R2: To manage a foreign domain in the selected instance of Active Directory Administrative Center using the current set of logon credentials

1.  To open Active Directory Administrative Center, click **Start**, click **Administrative Tools**, and then click **Active Directory Administrative Center**.

    > [!NOTE]
    >  Another way to open Active Directory Administrative Center is to click **Start**, click **Run**, and then type **dsac.exe**.

2.  To open **Add Navigation Nodes**, near the top of the Active Directory Administrative Center window, click **Add Navigation Nodes** as shown in the following illustration.

     ![보여 주는 스크린샷 * * 탐색 노드 * * UI를 추가](media/click_add_nav_nodes.gif)

    > [!NOTE]
    >  Another way to open **Add Navigation Nodes** is to right\-click anywhere in the empty space in the Active Directory Administrative Center navigation pane, and then click **Add Navigation Nodes**.

3.  **탐색 노드 추가**, 클릭 **다른 도메인에 연결** 다음과 같이 합니다.

     ![보여 주는 스크린샷 * * 추가 탐색 노드 * * * * 다른 도메인 * * UI에 연결](media/add_nav_nodes.gif)

4.  **연결할**, 이름을 입력 하 고 관리 하려면 외부 도메인의 \ (예를 들어, **contoso.com**\)을 차례로 클릭 하 고 **확인**합니다.

5.  When you are successfully connected to the foreign domain, browse through the columns in the **Add Navigation Nodes** window, select the container or containers to add to your Active Directory Administrative Center navigation pane, and then click **OK**.

 For more information about customizing the Active Directory Administrative Center navigation pane, see [Customize the Active Directory Administrative Center Navigation Pane](customize-the-active-directory-administrative-center-navigation-pane.md).

 You can also open Active Directory Administrative Center by using a set of logon credentials that is different from your current set of logon credentials. The command in the following procedure can be useful if you are logged on to the computer that is running Active Directory Administrative Center with normal user credentials, but you want to use Active Directory Administrative Center on this computer to manage your local domain as an administrator. \(This command can also be useful if you want to use Active Directory Administrative Center to remotely manage a foreign domain that is different from your local domain with a set of credentials that is different from your current set of logon credentials. 그러나 외부 도메인 기다렸다가으로 설정 된는 신뢰할 수 있어야 합니다. \)

 이 절차를 수행 하는 데 필요한 없는 최소 그룹 구성원이 있습니다.

### <a name="to-manage-a-domain-using-logon-credentials-that-are-different-from-the-current-set-of-logon-credentials"></a>도메인 로그온 자격 증명은 현재 세트 다른 로그온 자격 증명을 사용 하 여을 관리 하려면

1.  To open Active Directory Administrative Center, at a command prompt, type the following command, and then press ENTER:

     `runas /user:<domain\user> dsac`

     Where `<domain\user>` is the set of credentials that you want to open Active Directory Administrative Center with and `dsac` is the Active Directory Administrative Center executable file name \(Dsac.exe\).

     예를 들어 다음 명령을 입력 한 다음 ENTER 키를 누릅니다.

     `runas /user:contoso\administrator dsac`

2.  When Active Directory Administrative Center is open, browse through the navigation pane to view or manage your Active Directory domain.

  

