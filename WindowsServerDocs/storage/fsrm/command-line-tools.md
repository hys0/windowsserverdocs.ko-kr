---
title: 파일 서버 리소스 관리자 명령줄 도구
description: 이 문서에서는 Windows Server 2016 명령줄 도구에 대해 설명합니다.
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 9b31c133b0ee4382b5b9aeded9b3852c7230d2d8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858444"
---
# <a name="file-server-resource-manager-command-line-tools"></a>파일 서버 리소스 관리자 명령줄 도구

> 적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

파일 서버 리소스 관리자는 [FileServerResourceManager](https://technet.microsoft.com/itpro/powershell/windows/fileserverresourcemanager/fileserverresourcemanager) PowerShell cmdlet과 다음 명령줄 도구를 설치합니다.

-   **Dirquota.exe**. 할당량, 할당량 자동 적용, 할당량 템플릿을 만들고 관리하는 데 사용됩니다.
-   **Filescrn.exe**. 파일 차단, 파일 차단 템플릿, 파일 차단 예외 및 파일 그룹을 만들고 관리하는 데 사용됩니다.
-   **Storrept.exe**. 보고서 매개 변수를 구성하고 주문형 저장소 보고서를 생성하는 데 사용됩니다. 또한 **schtasks.exe**를 사용하여 예약할 수 있는 보고서 작업을 만드는 데 사용됩니다.

이러한 도구를 사용하여 로컬 컴퓨터 또는 원격 컴퓨터의 저장소 리소스를 관리할 수 있습니다. 이러한 명령줄 도구에 대한 자세한 내용은 다음 자료를 참조하세요.

-   **Dirquota**: <https://go.microsoft.com/fwlink/?LinkId=92741>
-   **Filescrn**: <https://go.microsoft.com/fwlink/?LinkId=92742>
-   **Storrept**: <https://go.microsoft.com/fwlink/?LinkId=92743>


> [!Note]
> 명령에 대한 명령 구문 및 사용 가능한 매개 변수를 보려면 <strong>/?</strong> 필요합니다.


## <a name="remote-management-using-the-command-line-tools"></a>명령줄 도구를 사용한 원격 관리

각 도구에는 파일 서버 리소스 관리자 MMC 스냅인에서 사용할 수 있는 작업과 유사한 작업을 수행하는 몇 가지 옵션이 있습니다. 로컬 컴퓨터가 아닌 원격 컴퓨터에서 명령을 수행하려면 **/remote**:*ComputerName* 매개 변수를 사용합니다.

예를 들어, **Dirquota.exe**에는 할당량 템플릿 설정을 XML 파일에 쓰기 위한 **template export** 매개 변수와 XML 파일에서 템플릿 설정을 가져오기 위한 **template import** 매개 변수가 포함되어 있습니다. **/remote**:*ComputerName* 매개 변수를 **Dirquota.exe template import** 명령에 추가하면 로컬 컴퓨터의 XML 파일에서 원격 컴퓨터로 템플릿을 가져옵니다.

> [!Note]
> 원격 컴퓨터에 템플릿 내보내기(또는 가져오기)를 수행하기 위해 **/remote**:<em>ComputerName</em> 매개 변수를 사용하여 명령줄 도구를 실행하면, 템플릿이 로컬 컴퓨터의 XML 파일에 작성되거나 XML 파일에서 복사됩니다.

<br />

## <a name="additional-considerations"></a>추가 고려 사항 

명령줄 도구를 사용하여 원격 리소스를 관리하려면:

-   로컬 컴퓨터 및 원격 컴퓨터에서 **Administrators** 그룹의 구성원인 도메인 계정으로 로그온해야 합니다.
-   권한이 상승된 명령 프롬프트 창에서 명령줄 도구를 실행해야 합니다. 관리자 권한 명령 프롬프트 창을 열려면 **시작**, **모든 프로그램**, **보조프로그램**을 차례로 클릭하고 **명령 프롬프트**를 마우스 오른쪽 단추로 클릭한 다음 **관리자 권한으로 실행**을 클릭합니다.
-   원격 컴퓨터는 Windows Server를 실행 중이어야 하며 파일 서버 리소스 관리자가 설치되어 있어야 합니다.
-   원격 컴퓨터에서 **원격 파일 서버 리소스 관리자 관리** 예외를 사용하도록 설정되어 있어야 합니다. 이 예외는 제어판의 Windows 방화벽을 통해 사용하도록 설정합니다.


## <a name="see-also"></a>참조

-   [원격 저장소 리소스 관리](managing-remote-storage-resources.md)