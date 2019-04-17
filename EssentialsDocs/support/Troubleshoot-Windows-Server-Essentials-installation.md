---
title: "Windows Server Essentials 설치 문제 해결"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ecf19216-7aac-4aca-839a-342ac28f5329
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 293b392203269a65efffcefb3744bedc659f71c9
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="troubleshoot-windows-server-essentials-installation"></a>Windows Server Essentials 설치 문제 해결

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

이 항목에서는 Windows Server Essentials를 설치할 때 발생 하는 문제를 해결 합니다. 지침은은 다음과 같은 지역에서 제공 됩니다.  
  

-   [일반 문제 해결](Troubleshoot-Windows-Server-Essentials-installation.md#BKMK_GeneralTroubleshootingSteps)  
  
-   [드라이버 문제 해결](Troubleshoot-Windows-Server-Essentials-installation.md#BKMK_TroubleshootDrivers)  

-   [일반 문제 해결](Troubleshoot-Windows-Server-Essentials-installation.md#BKMK_GeneralTroubleshootingSteps)  
  
-   [드라이버 문제 해결](Troubleshoot-Windows-Server-Essentials-installation.md#BKMK_TroubleshootDrivers)  

  
> [!NOTE]
>  Windows Server Essentials 커뮤니티에서 가장 최근 문제 해결 정보에 대 한 것이 좋습니다 방문 하 여 [Windows Server Essentials 포럼](https://social.technet.microsoft.com/Forums/winserveressentials/threads)합니다. Windows Server Essentials 포럼에 대 한 도움말을 검색 하거나 질문 하기에 좋은 장소입니다.  
  
##  <a name="BKMK_GeneralTroubleshootingSteps"></a>일반 문제 해결  
 Windows Server Essentials의 설치가 실패 하는 경우 오류가 발생 하는 문제를 확인 하려면 다음이 단계를 수행 합니다.  
  
> [!IMPORTANT]
>  것는 시작 하지 않으면 수동으로 서버 Windows Server Essentials를 설치 하는 동안 중요 합니다. 서버 자동으로 몇 번 다시 시작 하는 동안 설정 및 초기 구성 합니다. 본 수동으로 전에 서버 다시 시작 하는 경우는 **서버 설치를 완료** 설치를 중단 한 실패 원인이 수 있다는 메시지가 표시 됩니다.  
  
#### <a name="to-identify-issues-in-a-failed-installation-of-windows-server-essentials"></a>Windows Server Essentials 설치에 실패의 문제를 식별  
  
1.  서버 하드웨어 최소 요구 사항을 충족 하는지 확인 합니다. 하드웨어 요구 사항에 대 한 내용은 [Windows Server Essentials의 시스템 요구 사항에 대 한](../get-started/system-requirements.md)합니다.  
  
2.  Windows Server Essentials 설치 DVD MSDN에서 제공한 경우 SHA1 sum 확인 하 여 DVD 올바른지 확인 합니다. 자세한 내용은 참조 [가용성 및 파일 검사 무결성 검증 유틸리티 설명](https://go.microsoft.com/fwlink/?LinkId=220495) (https://go.microsoft.com/fwlink/?LinkId=220495).  
  
3.  네트워크 케이블 여 서버에 네트워크 어댑터 라우터에 연결 되어 있는지 확인 합니다.  
  
4.  서버에 둘 이상의 네트워크 어댑터가 있는 경우 해당 하나만 네트워크 어댑터를 사용할 수를 확인 합니다.  
  
    > [!IMPORTANT]
    >  네트워크 케이블을 분리 하거나 Windows Server Essentials를 설치 하는 동안 라우터를 다시 시작 하지 않습니다.  
  
5.  "서버 설치 및 배포" 검토 [Windows Server Essentials 릴리스 설명서](../get-started/release-notes.md)  
  
6.  오류 메시지가 나타나는 경우 설치 하는 동안 서버 설정 서버를 공장 기본 설정으로 복원 하려면 서버 복구 DVD와 하드웨어 제조업체에서 제공 하 고 지침을 사용 하는 동안 오류가 발생 합니다.  
  
##  <a name="BKMK_TroubleshootDrivers"></a>드라이버 문제 해결  
 Windows Server Essentials를 설치 하는 가장 일반적인 문제는 드라이버를 수동으로 설치 해야 하는 storage 컨트롤러입니다. Windows에는 여러 스토리지 컨트롤러용 드라이버가 하지만 특정 하드웨어에 대 한 드라이버를 포함 하지 될 수 있습니다.  
  
 또한 특정 하드웨어에 대 한 네트워크 카드 드라이버를 수동으로 설치 해야 할 수 있습니다.  
  
###  <a name="BKMK_StorageDrivers"></a>저장 컨트롤러 드라이버를 추가  
 하드웨어 요구 Windows Server Essentials와 함께 제공 된 저장소 드라이버를 설치를 완료 하려면 다음 정보를 사용 합니다.  
  
 설치 하는 동안 다음과 같은 메시지가 나타나면 저장소 컨트롤러의 드라이버를 수동으로 추가 해야 합니다.  
  
 **Windows Server 설치 오류**  
  
 Windows Server Essentials 호스트할 수 하드 디스크 드라이브를 찾을 수 없습니다. 저장소 추가 드라이버를 로드 하 시겠습니까?  
  
 다음 절차를 사용 하 여 저장소 컨트롤러 드라이버를 설치 해야 합니다.  
  
##### <a name="to-manually-install-a-storage-controller-driver"></a>저장소 컨트롤러 드라이버를 수동으로 설치 하려면  
  
1.  저장소 컨트롤러 드라이버를 제공 합니다. 하드웨어 제조업체에서 제공 됩니다 있으며 제조업체의 웹 사이트에서 사용할 수 있는 수 있습니다.  
  
2.  플로피 디스크에 드라이버를 라는 폴더 만들기 또는 USB 플래시 드라이브를 하 고 드라이버 폴더에 복사 합니다.  
  
3.  플로피 드라이브 또는 USB 플래시 드라이브의 드라이버를 컴퓨터에 연결  
  
4.  Windows Server Essentials DVD에서 컴퓨터를 부팅 합니다.  
  
     모든 저장소 컨트롤러 드라이버 누락 된 경우 Windows Server Essentials 설치 오류 대화 상자가 표시 됩니다.  
  
5.  Windows Server Essentials 설치 오류 대화 상자에서 클릭 **예** 추가 저장소 드라이버를 로드 합니다.  
  
6.  에 **드라이버의 inf 파일을 선택 하십시오** 라는, 플로피 디스크 또는 USB 플래시 드라이브에 드라이버 폴더에서.inf 파일을 찾아, 파일, 파일 이름을 마우스 오른쪽 단추로 클릭 선택한 클릭 한 다음 **열기**합니다. 드라이버를 로드 합니다.  
  
    > [!NOTE]
    >  파일을 로드할 시도 하기 전에 파일 이름 확장명 (.inf) 소문자로 인지 확인 합니다. 이 작업은 대/소문자를 구분 하 고 드라이버 파일이 파일 이름 확장명 대문자에 로드 되지 않습니다.  
  
7.  프롬프트에 클릭 **예** 설정의 텍스트 모드 단계 저장소 드라이버를 사용할 수 있도록 해야 합니다.  
  
 이제 설정 일반적으로 계속 합니다.  
  
###  <a name="BKMK_AddingNICdrivers"></a>네트워크 어댑터 드라이버를 추가  
 컴퓨터에 네트워크 어댑터는 Windows Server Essentials에서 지원 되지 않는 경우 서버는 없을 네트워크 연결 설치가 완료 된 후 컴퓨터를 서버에 연결할 수 없습니다.  
  
 Windows Server Essentials 설치 끝 네트워크 어댑터 드라이버를 자동으로 설치 되지 않은 경우 알 수 있습니다. 사용할 수 있습니다 **네트워크 연결** 제어판 누락 된 네트워크 어댑터 드라이버를 확인 합니다. 서버에 네트워크 어댑터와 관련 된 네트워크 연결을 표시 되지 않으면 드라이버를 설치 해야 합니다.  
  
 컴퓨터에서 지원 되는 모든 네트워크 어댑터 드라이버를 없는 경우 올바른 네트워크 어댑터 드라이버를 수동으로 설치 하 고 다음 서버를 다시 시작 해야 합니다. 다음 절차를 사용 합니다.  
  
##### <a name="to-install-a-network-adapter-driver"></a>네트워크 어댑터 드라이버를 설치 하려면  
  
1.  네트워크 어댑터의 제조업체가에서 누락 된 드라이버를 가져옵니다.  
  
2.  드라이버를 설치 하려면 제조업체의 설치 지침을 따릅니다.  
  
3.  컴퓨터를 다시 시작 합니다.  
  
    > [!IMPORTANT]
    >  서버를 누락 된 네트워크 어댑터 드라이버를 설치한 후에 다시 시작 하지 않으면 클라이언트 컴퓨터에 Windows Server Essentials 커넥터 소프트웨어의 설치 실패할 수 있습니다.
