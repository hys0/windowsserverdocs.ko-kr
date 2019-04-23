---
title: Windows Server Essentials 설치 문제 해결
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862024"
---
# <a name="troubleshoot-windows-server-essentials-installation"></a>Windows Server Essentials 설치 문제 해결

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

이 항목에서는 Windows Server Essentials를 설치 하는 경우 발생 하는 문제 해결 방법을 제공 합니다. 다음 영역에서 지침이 제공됩니다.  
  

-   [일반적인 문제 해결 단계](Troubleshoot-Windows-Server-Essentials-installation.md#BKMK_GeneralTroubleshootingSteps)  
  
-   [드라이버 문제 해결](Troubleshoot-Windows-Server-Essentials-installation.md#BKMK_TroubleshootDrivers)  

-   [일반적인 문제 해결 단계](Troubleshoot-Windows-Server-Essentials-installation.md#BKMK_GeneralTroubleshootingSteps)  
  
-   [드라이버 문제 해결](Troubleshoot-Windows-Server-Essentials-installation.md#BKMK_TroubleshootDrivers)  

  
> [!NOTE]
>  Windows Server Essentials 커뮤니티에서 최신 문제 해결 정보에 대 한 것이 좋습니다를 방문 하 여 [Windows Server Essentials 포럼](https://social.technet.microsoft.com/Forums/winserveressentials/threads)합니다. Windows Server Essentials 포럼은 도움말을 검색하거나 질문하기 좋은 곳입니다.  
  
##  <a name="BKMK_GeneralTroubleshootingSteps"></a> 일반적인 문제 해결 단계  
 Windows Server Essentials의 설치에 실패 하는 경우 오류를 발생 시킨 문제를 식별 하려면 다음이 단계를 수행 합니다.  
  
> [!IMPORTANT]
>  시작 하지 않으면 수동으로 서버에 Windows Server Essentials를 설치 하는 동안 중요 한 것입니다. 설정 및 초기 구성 중에 서버가 자동으로 여러 번 다시 시작됩니다. **서버 설치 성공** 메시지가 표시되기 전에 서버를 수동으로 다시 시작하면 설치가 중단되고 실패할 수 있습니다.  
  
#### <a name="to-identify-issues-in-a-failed-installation-of-windows-server-essentials"></a>Windows Server Essentials의 설치 실패의 문제를 식별 하려면  
  
1.  서버 하드웨어가 최소 요구 사항을 충족하는지 확인합니다. 하드웨어 요구 사항에 대 한 자세한 내용은 [Windows Server Essentials의 시스템 요구 사항에 대 한](../get-started/system-requirements.md)합니다.  
  
2.  MSDN에서 Windows Server Essentials 설치 DVD를 받은 경우 SHA1 합계를 확인 하 여 DVD가 유효한 지 확인 합니다. 자세한 내용은 [파일 체크섬 무결성 검증 도구 유틸리티의 가용성 및 설명](https://go.microsoft.com/fwlink/?LinkId=220495) (https://go.microsoft.com/fwlink/?LinkId=220495)합니다.  
  
3.  서버의 네트워크 어댑터가 네트워크 케이블을 통해 라우터에 연결되어 있는지 확인합니다.  
  
4.  서버에 둘 이상의 네트워크 어댑터가 있는 경우 하나의 네트워크 어댑터만 사용되는지 확인합니다.  
  
    > [!IMPORTANT]
    >  Windows Server Essentials를 설치 하는 동안 router를 다시 시작 하거나 네트워크 케이블을 분리 하지 마십시오.  
  
5.  "서버 설치 및 배포" 검토 [Release Documentation for Windows Server Essentials](../get-started/release-notes.md)  
  
6.  오류 메시지를 수신 하는 경우 설치 하는 동안 서버 설정 서버를 공장 기본 설정으로 복원 하려면 서버 복구 DVD 및 하드웨어의 제조업체에서 제공한 지침을 사용 하는 동안 오류가 발생 합니다.  
  
##  <a name="BKMK_TroubleshootDrivers"></a> 드라이버 문제 해결  
 Windows Server Essentials를 설치 하는 경우 가장 일반적인 문제는 저장소 컨트롤러 드라이버를 수동으로 설치 해야입니다. Windows에는 많은 저장소 컨트롤러용 드라이버가 포함되어 있지만 특정 하드웨어용 드라이버가 없을 수 있습니다.  
  
 특정 하드웨어용 네트워크 카드 드라이버를 수동으로 설치해야 할 수도 있습니다.  
  
###  <a name="BKMK_StorageDrivers"></a> 저장소 컨트롤러용 드라이버 추가  
 하드웨어와 Windows Server Essentials에 포함 되지 않은 저장소 드라이버가 필요한 경우 설치를 완료 하려면 다음 정보를 사용 합니다.  
  
 설치 중에 다음 메시지가 표시되는 경우 저장소 컨트롤러용 드라이버를 수동으로 추가해야 합니다.  
  
 **Windows Server 설치 오류**  
  
 Windows Server Essentials를 호스트할 수 있는 하드 디스크 드라이브를 찾을 수 없습니다. 추가 저장소 드라이버를 로드하시겠습니까?  
  
 다음 절차에 따라 저장소 컨트롤러 드라이버를 설치합니다.  
  
##### <a name="to-manually-install-a-storage-controller-driver"></a>저장소 컨트롤러 드라이버를 수동으로 설치하려면  
  
1.  저장소 컨트롤러용 드라이버를 찾습니다. 이러한 드라이버는 하드웨어 제조업체에서 제공되며, 제조업체 웹 사이트에서도 사용할 수 있습니다.  
  
2.  플로피 디스크 또는 USB 플래시 드라이브에 DRIVERS라는 폴더를 만든 다음 이 폴더에 드라이버를 복사합니다.  
  
3.  드라이버가 포함된 플로피 드라이브 또는 USB 플래시 드라이브를 컴퓨터에 연결합니다.  
  
4.  Windows Server Essentials DVD에서 컴퓨터를 부팅 합니다.  
  
     저장소 컨트롤러 드라이버가 없는 경우에 Windows Server Essentials 설치 오류 대화 상자가 표시 됩니다.  
  
5.  Windows Server Essentials 설치 오류 대화 상자에서 클릭 **예** 추가 저장소 드라이버를 로드 합니다.  
  
6.  **드라이버의 inf 파일을 선택하세요.** 프롬프트가 표시되면 플로피 디스크 또는 USB 플래시 드라이브의 DRIVERS 폴더에서 .inf 파일을 탐색하여 선택하고 파일 이름을 마우스 오른쪽 단추로 클릭한 다음 **열기**를 클릭합니다. 드라이버가 로드됩니다.  
  
    > [!NOTE]
    >  파일을 로드하기 전에 파일 이름 확장명(.inf)이 소문자인지 확인합니다. 이 작업은 대/소문자를 구분하며, 파일 이름 확장명에 대문자가 있으면 드라이버 파일이 로드되지 않습니다.  
  
7.  프롬프트가 표시되면 **예**를 클릭하여 설치 프로그램의 텍스트 모드 단계에서 저장소 드라이버를 사용할 수 있도록 합니다.  
  
 이제 설치가 정상적으로 계속됩니다.  
  
###  <a name="BKMK_AddingNICdrivers"></a> 네트워크 어댑터용 드라이버 추가  
 컴퓨터의 네트워크 어댑터를 Windows Server Essentials에서 지원 되지 않는 경우 설치가 완료 된 후 컴퓨터를 서버에 연결할 수 없습니다 서버가 네트워크에 연결이 되어 있지 됩니다.  
  
 Windows Server Essentials 설치가 끝날 때 네트워크 어댑터 드라이버를 자동으로 설치 되지 않은 경우를 알 수 있습니다. 제어판의 **네트워크 연결**을 사용하여 누락된 네트워크 어댑터 드라이버를 확인할 수도 있습니다. 서버의 네트워크 어댑터와 연결된 네트워크 연결이 표시되지 않는 경우 드라이버를 설치해야 합니다.  
  
 네트워크 어댑터에 대해 지원되는 드라이버가 컴퓨터에 없는 경우 올바른 네트워크 어댑터 드라이버를 수동으로 설치하고 서버를 다시 시작해야 합니다. 다음 절차를 사용합니다.  
  
##### <a name="to-install-a-network-adapter-driver"></a>네트워크 어댑터 드라이버를 설치하려면  
  
1.  네트워크 어댑터 제조업체에서 누락된 드라이버를 얻습니다.  
  
2.  제조업체의 설치 지침에 따라 드라이버를 설치합니다.  
  
3.  컴퓨터를 다시 시작합니다.  
  
    > [!IMPORTANT]
    >  누락 된 네트워크 어댑터 드라이버를 설치한 후 서버를 시작 하지 않으면 클라이언트 컴퓨터에서 Windows Server Essentials connector 소프트웨어 설치 실패할 수 있습니다.
