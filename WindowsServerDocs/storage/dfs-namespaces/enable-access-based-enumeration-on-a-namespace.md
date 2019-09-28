---
title: 네임스페이스에 액세스 기반 열거 사용
description: 이 문서에서는 네임스페이스에 액세스 기반 열거를 사용하는 방법을 설명합니다.
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 246df5b13a1dbea614886ab7fe445dd448ae1763
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402176"
---
# <a name="enable-access-based-enumeration-on-a-namespace"></a>네임스페이스에 액세스 기반 열거 사용

> 적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

액세스 기반 열거는 사용자가 액세스 권한이 없는 파일과 폴더를 숨깁니다. 기본적으로 이 기능은 DFS 네임스페이스에 사용할 수 없습니다. DFS 관리를 사용하여 DFS 폴더의 액세스 기반 열거를 사용하도록 설정할 수 있습니다. 폴더 대상에서 파일과 폴더의 액세스 기반 열거를 제거하려면 공유 및 저장소 관리를 사용하여 각 공유 폴더에 액세스 기반 열거를 사용하도록 설정해야 합니다.

네임 스페이스에 대 한 액세스 기반 열거를 사용 하도록 설정 하려면 모든 네임 스페이스 서버에서 Windows Server 2008 이상 버전을 실행 해야 합니다. 또한 도메인 기반 네임 스페이스는 Windows Server 2008 모드를 사용 해야 합니다. Windows Server 2008 모드의 요구 사항에 대 한 자세한 내용은 [네임 스페이스 유형 선택](choose-a-namespace-type.md)을 참조 하세요.

일부 환경에서 액세스 기반 열거를 사용하면 서버 쪽의 CPU 사용률이 높아지고 사용자에 대한 응답 시간이 느려질 수 있습니다.

> [!NOTE]
> 기존 도메인 기반 네임 스페이스가 있는 상태에서 도메인 기능 수준을 Windows Server 2008로 업그레이드 하는 경우 DFS 관리를 통해 이러한 네임 스페이스에 대 한 액세스 기반 열거를 사용 하도록 설정할 수 있습니다. 그러나 네임 스페이스를 Windows Server 2008 모드로 마이그레이션하는 경우를 제외 하 고는 그룹 또는 사용자의 폴더를 숨기도록 사용 권한을 편집할 수 없습니다. 자세한 내용은 [Windows Server 2008 모드로 도메인 기반 네임스페이스 마이그레이션](migrate-a-domain-based-namespace-to-windows-server-2008-mode.md)을 참조하세요.


DFS 네임스페이스에 액세스 기반 열거를 사용하려면 다음 단계를 수행해야 합니다.

-   네임스페이스에 액세스 기반 열거 사용
-   개별 DFS 폴더를 볼 수 있는 사용자와 그룹 제어


> [!WARNING]
> 사용자가 DFS 경로를 이미 알고 있는 경우 액세스 기반 열거는 사용자가 폴더 대상에 조회하지 못하게 합니다. 폴더 대상(공유 폴더) 자체의 공유 사용 권한이나 NTFS 파일 시스템 사용 권한은 사용자가 폴더 대상에 액세스하지 못하게 할 수 있습니다. DFS 폴더 사용 권한은 DFS 폴더를 표시하거나 숨기는 데만 사용되고 액세스를 제어하는 데 사용되지 않습니다. 따라서 읽기 권한이 DFS 폴더 수준의 유일한 관련 사용 권한이 됩니다. 자세한 내용은 [액세스 기반 열거와 함께 상속된 사용 권한 사용](https://technet.microsoft.com/library/dd834874(v=ws.11).aspx)을 참조하세요.

<br />
Windows 인터페이스나 명령줄을 사용하여 네임스페이스에 액세스 기반 열거를 사용할 수 있습니다.

## <a name="to-enable-access-based-enumeration-by-using-the-windows-interface"></a>Windows 인터페이스를 사용하여 액세스 기반 열거를 사용하려면

1.  콘솔 트리의 **네임스페이스** 노드에서 적절한 네임스페이스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.

2.  **고급** 탭을 클릭하고 **이 네임스페이스에 액세스 기반 열거 사용** 확인란을 선택합니다.

## <a name="to-enable-access-based-enumeration-by-using-a-command-line"></a>명령줄을 사용하여 액세스 기반 열거를 사용하려면

1.  **분산 파일 시스템** 역할 서비스나 **분산 파일 시스템 도구** 기능이 설치된 서버에서 명령 프롬프트 창을 엽니다.

2.  다음 명령을 입력 합니다. 여기서 *< namespace @ no__t-1root >* 는 네임 스페이스의 루트입니다.

    ```  
    dfsutil property abe enable \\ <namespace_root>
    ```

> [!TIP]
> Windows PowerShell을 사용하여 네임스페이스에 액세스 기반 열거를 관리하려면 [Set-DfsnRoot](https://technet.microsoft.com/library/jj884281.aspx), [Grant-DfsnAccess](https://technet.microsoft.com/library/jj884272.aspx) 및 [Revoke-DfsnAccess](https://technet.microsoft.com/library/jj884273.aspx) cmdlet을 사용합니다. DFSN Windows PowerShell 모듈은 Windows Server 2012에서 도입되었습니다.

Windows 인터페이스나 명령줄을 사용하여 개별 DFS 폴더를 볼 수 있는 사용자와 그룹을 제어할 수 있습니다.

## <a name="to-control-folder-visibility-by-using-the-windows-interface"></a>Windows 인터페이스를 사용하여 폴더 표시 여부를 제어하려면

1.  콘솔 트리의 **네임스페이스** 노드 아래에서 표시 여부를 제어할 대상을 가진 폴더를 찾아서 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.

2.  **고급** 탭을 클릭합니다.

3.  **DFS 폴더에 대한 명시적 보기 권한 설정**과 **보기 권한 구성**을 차례로 클릭합니다.

4.  **추가** 또는 **제거**를 클릭하여 그룹이나 사용자를 추가하거나 제거합니다.

5.  사용자가 DFS 폴더를 볼 수 있게 하려면 그룹이나 사용자를 선택하고 **허용** 확인란을 선택합니다.

    그룹이나 사용자로부터 폴더를 숨기려면 그룹이나 사용자를 선택하고 **거부** 확인란을 선택합니다.

## <a name="to-control-folder-visibility-by-using-a-command-line"></a>명령줄을 사용하여 폴더 표시 여부를 제어하려면

1. **분산 파일 시스템** 역할 서비스나 **분산 파일 시스템 도구** 기능이 설치된 서버에서 명령 프롬프트 창을 엽니다.

2. 다음 명령을 입력 합니다. *@no__t 여기서 1DFSPath @ no__t* 은 DFS 폴더 (링크)의 경로이 고 *< DOMAIN @ no__t-4account >* 는 그룹 또는 사용자 계정의 이름입니다 *. (...)* 는 추가 Access Control 항목 (...)으로 대체 됩니다. Ace):

   ```
   dfsutil property sd grant <DFSPath> DOMAIN\Account:R (...) Protect Replace
   ```

   예를 들어, 도메인 관리자 및 CONTOSO @ no__t-0Trainers 그룹이 @no__t-office\public\training 폴더에 대 한 액세스를 허용 하는 권한으로 기존 사용 권한을 바꾸려면 다음 명령을 입력 합니다.

   ```
   dfsutil property sd grant \\contoso.office\public\training "CONTOSO\Domain Admins":R CONTOSO\Trainers:R Protect Replace 
   ```

3. 명령 프롬프트에서 추가 작업을 수행하려면 다음 명령을 사용합니다.


| 명령 | 설명 |
|---|---|
|[Dfsutil 속성 sd 거부](https://msdn.microsoft.com/library/dd759150(v=ws.11).aspx)|그룹이나 사용자에게 폴더를 볼 수 있는 권한을 주지 않습니다.|
|[Dfsutil 속성 sd 다시 설정](https://msdn.microsoft.com/library/dd759150(v=ws.11).aspx) |폴더에서 모든 사용 권한을 제거합니다.|
|[Dfsutil 속성 sd 취소](https://msdn.microsoft.com/library/dd759150(v=ws.11).aspx)| 폴더에서 그룹 또는 사용자 ACE를 제거합니다. |

## <a name="see-also"></a>참조

-   [DFS 네임스페이스 만들기](create-a-dfs-namespace.md)
-   [DFS 네임스페이스에 대한 관리 권한 위임](delegate-management-permissions-for-dfs-namespaces.md)
-   [DFS 설치](https://technet.microsoft.com/library/cc731089(v=ws.11).aspx)
-   [액세스 기반 열거와 함께 상속 된 권한 사용](using-inherited-permissions-with-access-based-enumeration.md)