---
title: 파일 서버 리소스 관리자 명령줄 도구
description: 이 문서에서는 Windows Server 2016 명령줄 도구에 대해 설명 합니다.
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 2acce64aa14d60503a5b443b831a03338c204be2
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85472819"
---
# <a name="file-server-resource-manager-command-line-tools"></a>파일 서버 리소스 관리자 명령줄 도구

> 적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

파일 서버 리소스 관리자는 [FileServerResourceManager](https://technet.microsoft.com/itpro/powershell/windows/fileserverresourcemanager/fileserverresourcemanager) PowerShell cmdlet 및 다음 명령줄 도구를 설치 합니다.

-   **Dirquota.exe**. 할당량 만들기 및 관리, 할당량 자동 적용 및 할당량 템플릿
-   **Filescrn.exe**. 를 사용 하 여 파일 화면, 파일 화면 템플릿, 파일 화면 예외 및 파일 그룹을 만들고 관리할 수 있습니다.
-   **Storrept.exe**. 를 사용 하 여 보고서 매개 변수를 구성 하 고 요청 시 저장소 보고서를 생성 합니다. 또한를 사용 하 여 보고서 작업을 만들 수 있습니다 .이 작업은 **schtasks.exe**를 사용 하 여 예약할 수 있습니다.

이러한 도구를 사용 하 여 로컬 컴퓨터 또는 원격 컴퓨터에서 저장소 리소스를 관리할 수 있습니다. 이러한 명령줄 도구에 대 한 자세한 내용은 다음 참조를 참조 하세요.

-   **Dirquota**:<https://go.microsoft.com/fwlink/?LinkId=92741>
-   **Filescrn**:<https://go.microsoft.com/fwlink/?LinkId=92742>
-   **Storrept**:<https://go.microsoft.com/fwlink/?LinkId=92743>


> [!Note]
> 명령 구문 및 명령에 사용할 수 있는 매개 변수를 보려면 <strong>/?</strong> 를 사용 하 여 명령을 실행 합니다. 필요합니다.


## <a name="remote-management-using-the-command-line-tools"></a>명령줄 도구를 사용한 원격 관리

각 도구에는 파일 서버 리소스 관리자 MMC 스냅인에서 사용할 수 있는 것과 유사한 작업을 수행 하기 위한 몇 가지 옵션이 있습니다. 명령이 로컬 컴퓨터 대신 원격 컴퓨터에서 작업을 수행 하도록 하려면 **/remote**:*ComputerName* 매개 변수를 사용 합니다.

예를 들어**Dirquota.exe** 에는 xml 파일에 할당량 템플릿 설정을 쓰기 위한 **템플릿 내보내기** 매개 변수 및 xml 파일에서 템플릿 설정을 가져올 **템플릿 가져오기** 매개 변수가 포함 되어 있습니다. **Dirquota.exe template 가져오기** 명령에 **/remote**:*ComputerName* 매개 변수를 추가 하면 로컬 컴퓨터의 XML 파일에서 원격 컴퓨터로 템플릿을 가져옵니다.

> [!Note]
> **/Remote**:<em>ComputerName</em> 매개 변수를 사용 하 여 명령줄 도구를 실행 하 여 원격 컴퓨터에서 템플릿 내보내기 (또는 가져오기)를 수행 하는 경우 템플릿은 로컬 컴퓨터의 XML 파일에 기록 (또는 복사) 됩니다.

<br />

## <a name="additional-considerations"></a>기타 고려 사항

명령줄 도구를 사용 하 여 원격 리소스를 관리 하려면:

-   로컬 컴퓨터와 원격 컴퓨터에서 **Administrators** 그룹의 구성원 인 도메인 계정을 사용 하 여 로그온 해야 합니다.
-   관리자 권한 명령 프롬프트 창에서 명령줄 도구를 실행 해야 합니다. 관리자 권한 명령 프롬프트 창을 열려면 **시작**, **모든 프로그램**, **보조프로그램**을 차례로 클릭하고 **명령 프롬프트**를 마우스 오른쪽 단추로 클릭한 다음 **관리자 권한으로 실행**을 클릭합니다.
-   원격 컴퓨터에서 Windows Server를 실행 하 고 있어야 하며 파일 서버 리소스 관리자를 설치 해야 합니다.
-   원격 컴퓨터에서 **원격 파일 서버 리소스 관리자 관리** 예외를 사용 하도록 설정 해야 합니다. 제어판에서 Windows 방화벽을 사용 하 여이 예외를 사용 하도록 설정 합니다.


## <a name="additional-references"></a>추가 참조

-   [원격 스토리지 리소스 관리](managing-remote-storage-resources.md)