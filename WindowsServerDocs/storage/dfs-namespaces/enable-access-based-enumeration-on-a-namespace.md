---
title: 네임스페이스에 액세스 기반 열거 사용
description: 이 문서에서는 네임 스페이스에 대 한 액세스 기반 열거를 사용 하도록 설정 하는 방법을 설명 합니다.
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 7f011bc12c26567ed3a0e912dca3c3a8de9bfff9
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85474930"
---
# <a name="enable-access-based-enumeration-on-a-namespace"></a>네임 스페이스에 대 한 액세스 기반 열거 사용

> 적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

액세스 기반 열거는 사용자에 게 액세스 권한이 없는 파일 및 폴더를 숨깁니다. 기본적으로이 기능은 DFS 네임 스페이스에 대해 사용 하도록 설정 되어 있지 않습니다. Dfs 관리를 사용 하 여 DFS 폴더의 액세스 기반 열거를 사용 하도록 설정할 수 있습니다. 폴더 대상의 파일 및 폴더에 대 한 액세스 기반 열거를 제어 하려면 공유 및 저장소 관리를 사용 하 여 각 공유 폴더에 대 한 액세스 기반 열거를 사용 하도록 설정 해야 합니다.

네임 스페이스에 대 한 액세스 기반 열거를 사용 하도록 설정 하려면 모든 네임 스페이스 서버에서 Windows Server 2008 이상 버전을 실행 해야 합니다. 또한 도메인 기반 네임 스페이스는 Windows Server 2008 모드를 사용 해야 합니다. Windows Server 2008 모드의 요구 사항에 대 한 자세한 내용은 [네임 스페이스 유형 선택](choose-a-namespace-type.md)을 참조 하세요.

일부 환경에서는 액세스 기반 열거를 사용 하도록 설정 하면 서버에서 CPU 사용률이 높아질 수 있으며 사용자에 대 한 응답 시간이 느려질 수 있습니다.

> [!NOTE]
> 기존 도메인 기반 네임 스페이스가 있는 상태에서 도메인 기능 수준을 Windows Server 2008로 업그레이드 하는 경우 DFS 관리를 통해 이러한 네임 스페이스에 대 한 액세스 기반 열거를 사용 하도록 설정할 수 있습니다. 그러나 네임 스페이스를 Windows Server 2008 모드로 마이그레이션하는 경우를 제외 하 고는 그룹 또는 사용자의 폴더를 숨기도록 사용 권한을 편집할 수 없습니다. 자세한 내용은 [Windows Server 2008 모드로 도메인 기반 네임 스페이스 마이그레이션](migrate-a-domain-based-namespace-to-windows-server-2008-mode.md)을 참조 하세요.


DFS 네임 스페이스에서 액세스 기반 열거를 사용 하려면 다음 단계를 수행 해야 합니다.

-   네임 스페이스에 대 한 액세스 기반 열거 사용
-   개별 DFS 폴더를 볼 수 있는 사용자 및 그룹 제어


> [!WARNING]
> 액세스 기반 열거를 사용 하면 사용자가 이미 DFS 경로를 알고 있는 경우 폴더 대상에 대 한 조회를 가져올 수 있습니다. 공유 권한 또는 폴더 대상 (공유 폴더) 자체의 NTFS 파일 시스템 권한만 있으면 사용자가 폴더 대상에 액세스 하지 못할 수 있습니다. Dfs 폴더 권한은 dfs 폴더를 표시 하거나 숨기는 데 사용 되며 액세스를 제어 하는 것이 아니라 DFS 폴더 수준에서의 유일한 관련 사용 권한에 대 한 읽기 권한을 부여 하는 데 사용 됩니다. 자세한 내용은 [액세스 기반 열거와 함께 상속 된 권한 사용](https://technet.microsoft.com/library/dd834874(v=ws.11).aspx) 을 참조 하세요.

<br />
Windows 인터페이스를 사용 하거나 명령줄을 사용 하 여 네임 스페이스에 대 한 액세스 기반 열거를 사용 하도록 설정할 수 있습니다.

## <a name="to-enable-access-based-enumeration-by-using-the-windows-interface"></a>Windows 인터페이스를 사용 하 여 액세스 기반 열거를 사용 하도록 설정 하려면

1.  콘솔 트리의 **네임 스페이스** 노드에서 적절 한 네임 스페이스를 마우스 오른쪽 단추로 클릭 한 다음 **속성** 을 클릭 합니다.

2.  **고급** 탭을 클릭 하 고 **이 네임 스페이스에 대 한 액세스 기반 열거 사용** 확인란을 선택 합니다.

## <a name="to-enable-access-based-enumeration-by-using-a-command-line"></a>명령줄을 사용 하 여 액세스 기반 열거를 사용 하도록 설정 하려면

1.  **분산 파일 시스템** 역할 서비스 또는 **분산 파일 시스템 도구** 기능이 설치 된 서버에서 명령 프롬프트 창을 엽니다.

2.  다음 명령을 입력 합니다. 여기서 *네임 스페이스 \_ 루트>* 는 네임 스페이스의 루트<합니다.

    ```
    dfsutil property abe enable \\ <namespace_root>
    ```

> [!TIP]
> Windows PowerShell을 사용 하 여 네임 스페이스에 대 한 액세스 기반 열거를 관리 하려면 [DfsnRoot](https://technet.microsoft.com/library/jj884281.aspx), [DfsnAccess](https://technet.microsoft.com/library/jj884272.aspx)및 [DfsnAccess](https://technet.microsoft.com/library/jj884273.aspx) cmdlet을 사용 합니다. DFSN Windows PowerShell 모듈은 Windows Server 2012에서 도입 되었습니다.

Windows 인터페이스를 사용 하거나 명령줄을 사용 하 여 개별 DFS 폴더를 볼 수 있는 사용자 및 그룹을 제어할 수 있습니다.

## <a name="to-control-folder-visibility-by-using-the-windows-interface"></a>Windows 인터페이스를 사용 하 여 폴더 표시 유형을 제어 하려면

1.  콘솔 트리의 **네임 스페이스** 노드에서 표시 유형을 제어 하려는 대상이 있는 폴더를 찾아 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 클릭 합니다.

2.  **고급** 탭을 클릭합니다.

3.  **DFS 폴더에 대 한 명시적 보기 권한 설정** 을 클릭 한 다음 **보기 권한을 구성**합니다.

4.  **추가** 또는 **제거**를 클릭 하 여 그룹 또는 사용자를 추가 하거나 제거 합니다.

5.  사용자가 DFS 폴더를 볼 수 있도록 허용 하려면 그룹 또는 사용자를 선택한 다음 **허용** 확인란을 선택 합니다.

    그룹 또는 사용자에서 폴더를 숨기려면 그룹 또는 사용자를 선택한 다음 **거부** 확인란을 선택 합니다.

## <a name="to-control-folder-visibility-by-using-a-command-line"></a>명령줄을 사용 하 여 폴더 표시 유형을 제어 하려면

1. **분산 파일 시스템** 역할 서비스 또는 **분산 파일 시스템 도구** 기능이 설치 된 서버에서 명령 프롬프트 창을 엽니다.

2. 다음 명령을 입력 합니다. 여기서 * &lt; DFSPath &gt; * 은 DFS 폴더 (링크)의 경로이 고 *<, 도메인 \\ 계정>* 는 그룹 또는 사용자 계정의 이름이 고, *(...)* 는 추가 Access Control 항목 (ace)으로 바뀝니다.

   ```
   dfsutil property sd grant <DFSPath> DOMAIN\Account:R (...) Protect Replace
   ```

   예를 들어, 도메인 관리자 및 CONTOSO \\ 담당자 그룹이 office\public\training 폴더에 대 한 읽기 (R) 액세스를 허용 하는 사용 권한으로 기존 사용 권한을 바꾸려면 \\ 다음 명령을 입력 합니다.

   ```
   dfsutil property sd grant \\contoso.office\public\training "CONTOSO\Domain Admins":R CONTOSO\Trainers:R Protect Replace
   ```

3. 명령 프롬프트에서 추가 작업을 수행 하려면 다음 명령을 사용 합니다.


| 명령 | 설명 |
|---|---|
|[Dfsutil 속성 sd 거부](https://msdn.microsoft.com/library/dd759150(v=ws.11).aspx)|그룹이 나 사용자에 게 폴더를 볼 수 있는 권한을 거부 합니다.|
|[Dfsutil 속성 sd 다시 설정](https://msdn.microsoft.com/library/dd759150(v=ws.11).aspx) |폴더에서 모든 사용 권한을 제거 합니다.|
|[Dfsutil 속성 sd 취소](https://msdn.microsoft.com/library/dd759150(v=ws.11).aspx)| 폴더에서 그룹 또는 사용자 ACE를 제거 합니다. |

## <a name="additional-references"></a>추가 참조

-   [DFS 네임스페이스 만들기](create-a-dfs-namespace.md)
-   [DFS 네임스페이스에 대한 관리 권한 위임](delegate-management-permissions-for-dfs-namespaces.md)
-   [DFS 설치](https://technet.microsoft.com/library/cc731089(v=ws.11).aspx)
-   [액세스 기반 열거와 함께 상속 된 권한 사용](using-inherited-permissions-with-access-based-enumeration.md)