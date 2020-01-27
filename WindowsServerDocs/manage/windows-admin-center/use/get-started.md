---
title: Windows Admin Center 시작하기
description: Windows Admin Center 시작하기
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.localizationpriority: medium
ms.prod: windows-server
ms.date: 02/15/2019
ms.openlocfilehash: fc8e6ffa39320cfc73bf3f5bd0a5bc765ded24b4
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/14/2020
ms.locfileid: "75950522"
---
# <a name="get-started-with-windows-admin-center"></a>Windows 관리 센터 시작

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

> [!Tip]
> Windows Admin Center를 처음 사용하시나요?
> [Windows Admin Center에 대해 자세히 알아보거나](../overview.md)[지금 다운로드](https://aka.ms/windowsadmincenter)하세요.

## <a name="windows-admin-center-installed-on-windows-10"></a>Windows 10에 설치 된 windows 관리 센터

> [!IMPORTANT]
> Windows 10에서 Windows 관리 센터를 사용 하려면 로컬 관리자 그룹의 구성원 이어야 합니다.

### <a name="selecting-a-client-certificate"></a>클라이언트 인증서 선택

Windows 10에서 windows 관리 센터를 처음 열 때 *Windows 관리 센터 클라이언트* 인증서를 선택 해야 합니다. 그렇지 않으면 "이 페이지로 이동할 수 없습니다." 라는 HTTP 403 오류가 발생 합니다.

Microsoft Edge에서이 대화 상자가 표시 되 면 다음을 수행 합니다.
 
1. **추가 선택 항목** 을 클릭 합니다.

    ![](../media/launch-cert-1.png)

2. **Windows 관리 센터 클라이언트** 라는 레이블이 지정 된 인증서를 선택 하 고 **확인을** 클릭 합니다.

    ![](../media/launch-cert-2.png)

3. **항상 액세스 허용** 이 선택 되어 있는지 확인 하 고 **허용** 을 클릭 합니다.

    ![](../media/launch-cert-3.png)

## <a name="connecting-to-managed-nodes-and-clusters"></a>관리 되는 노드 및 클러스터에 연결

Windows 관리 센터 설치를 완료 한 후에는 기본 개요 페이지에서 관리할 서버 또는 클러스터를 추가할 수 있습니다.

 **단일 서버 또는 클러스터를 관리 노드로 추가**

1. **모든 연결**에서 **+ 추가** 를 클릭 합니다.

   ![](../media/launch/addserver0.png)

2. 서버, 클러스터, Windows PC 또는 Azure VM을 추가 하도록 선택 합니다.
    
   ![](../media/launch/ChooseConnectionType.png)

3. 관리할 서버 또는 클러스터의 이름을 입력 하 고 **제출**을 클릭 합니다. 서버 또는 클러스터가 개요 페이지의 연결 목록에 추가 됩니다.

   ![](../media/launch/addserver2.png)

   **--또는--**

**여러 서버 대량 가져오기**

 1. **서버 연결 추가** 페이지에서 **서버 가져오기** 탭을 선택 합니다.

    ![](../media/launch/import-servers.png)

 2. **찾아보기** 를 클릭 하 고 추가 하려는 서버에 대 한 쉼표 또는 쉼표로 구분 된 새 줄을 포함 하는 텍스트 파일을 선택 합니다.

> [!Note]
> [PowerShell을 사용](#use-powershell-to-import-or-export-your-connections-with-tags) 하 여 연결을 내보내 만든 .csv 파일에는 서버 이름 이외에 추가 정보가 포함 되어 있으며이 가져오기 방법과 호환 되지 않습니다.

  **--또는--**

**Active Directory 검색 하 여 서버 추가**

 1. **서버 연결 추가** 페이지에서 **검색 Active Directory** 탭을 선택 합니다.

    ![](../media/launch/search-ad.png)

 2. 검색 조건을 입력 하 고 **검색**을 클릭 합니다. 와일드 카드 (*)를 사용할 수 있습니다.

 3. 검색이 완료 되 면 하나 이상의 결과를 선택 하 고 필요에 따라 태그를 추가 하 고 **추가**를 클릭 합니다.

## <a name="authenticate-with-the-managed-node"></a>관리 노드를 사용 하 여 인증 ##

Windows 관리 센터는 관리 되는 노드로 인증 하기 위한 여러 메커니즘을 지원 합니다. Single sign-on이 기본값입니다.

**Single Sign-on**

현재 Windows 자격 증명을 사용 하 여 관리 되는 노드에 인증할 수 있습니다. 이는 기본값 이며, Windows 관리 센터에서 서버를 추가할 때 로그온을 시도 합니다. 

**Windows Server에 서비스로 배포된 경우의 Single Sign-On**

Windows Server에 Windows 관리 센터를 설치한 경우 Single Sign-On 하려면 추가 구성이 필요 합니다.  [위임할 환경 구성](../configure/user-access-control.md)

**--또는--**

**다음 *으로 관리* 를 사용 하 여 자격 증명 지정**

**모든 연결**아래의 목록에서 서버를 선택 하 고 다음 **으로 관리** 를 선택 하 여 관리 되는 노드에 인증 하는 데 사용할 자격 증명을 지정 합니다.

![](../media/launch-use-6.png)

Windows 관리 센터에서 windows Server의 서비스 모드로 실행 중이지만 Kerberos 위임이 구성 되지 않은 경우 Windows 자격 증명을 다시 입력 해야 합니다.

![](../media/launch-use-7.png)

모든 연결에 자격 증명을 적용할 수 있습니다. 그러면 해당 특정 브라우저 세션에 대 한 자격 증명을 캐시 합니다. 브라우저를 다시 로드 하는 경우 **관리** 자격 증명을 다시 입력 해야 합니다.

**로컬 관리자 암호 솔루션 (LAPS)**

환경에서 [LAPS](https://technet.microsoft.com/mt227395.aspx)를 사용 하 고 WINDOWS 10 PC에 Windows 관리 센터를 설치한 경우 LAPS 자격 증명을 사용 하 여 관리 되는 노드로 인증할 수 있습니다. **이 시나리오를 사용 하는 경우** [피드백을 제공 해 주세요 ](https://aka.ms/WACFeedback).

## <a name="using-tags-to-organize-your-connections"></a>태그를 사용 하 여 연결 구성

태그를 사용 하 여 연결 목록에서 관련 서버를 식별 하 고 필터링 할 수 있습니다.  이렇게 하면 연결 목록에서 서버의 하위 집합을 볼 수 있습니다.  많은 연결이 있는 경우 특히 유용 합니다.

### <a name="edit-tags"></a>태그 편집

* 모든 연결 목록에서 서버 또는 여러 서버를 선택 합니다.
* **모든 연결**에서 **태그 편집** 을 클릭 합니다.

![](../media/launch/tags-5.png)

**연결 태그 편집** 창을 사용 하 여 선택한 연결에서 태그를 수정, 추가 또는 제거할 수 있습니다.

* 선택한 연결에 새 태그를 추가 하려면 **태그 추가** 를 선택 하 고 사용할 태그 이름을 입력 합니다.

* 선택한 연결에 기존 태그 이름을 표시 하려면 적용 하려는 태그 이름 옆의 확인란을 선택 합니다.

* 선택한 모든 연결에서 태그를 제거 하려면 제거할 태그 옆에 있는 확인란의 선택을 취소 합니다.

* 선택한 연결의 하위 집합에 태그를 적용 하는 경우에는 확인란이 중간 상태로 표시 됩니다. 확인란을 클릭 하 여 선택한 모든 연결에 태그를 적용 하 고 적용 하거나 다시 클릭 하 여 선택을 취소 하 고 선택한 모든 연결에서 태그를 제거할 수 있습니다.

![](../media/launch/tags-6.png)

### <a name="filter-connections-by-tag"></a>태그별로 연결 필터링

하나 이상의 서버 연결에 태그를 추가한 후에는 연결 목록에서 태그를 보고 태그를 기준으로 연결 목록을 필터링 할 수 있습니다.

* 태그를 기준으로 필터링 하려면 검색 상자 옆에 있는 필터 아이콘을 선택 합니다.
![](../media/launch/tags-7.png)
* "Or", "and" 또는 "not"을 선택 하 여 선택한 태그의 필터 동작을 수정할 수 있습니다.
![](../media/launch/tags-8.png)

## <a name="use-powershell-to-import-or-export-your-connections-with-tags"></a>PowerShell을 사용하여 연결 가져오기 또는 내보내기(tags 사용)

[!INCLUDE [ps-connections](../includes/ps-connections.md)]

## <a name="view-powershell-scripts-used-in-windows-admin-center"></a>Windows 관리 센터에서 사용 되는 PowerShell 스크립트 보기

서버, 클러스터 또는 PC에 연결 하면 Windows 관리 센터에서 사용할 수 있는 UI 작업을 수행 하는 PowerShell 스크립트를 살펴볼 수 있습니다. 도구 내에서 위쪽 응용 프로그램 표시줄의 PowerShell 아이콘을 클릭 합니다. 드롭다운 목록에서 원하는 명령을 선택 하 여 해당 PowerShell 스크립트로 이동 합니다.

![](../media/launch/showscript.png)
