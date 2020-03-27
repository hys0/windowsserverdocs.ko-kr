---
title: Windows Server Essentials 로그 수집기 오류 문제 해결
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fa2e1685-31c0-4d4f-a10a-6c8885dfc493
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: a08826a979defa2b7c78b8257726eb35ed07d054
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80318624"
---
# <a name="troubleshoot-windows-server-essentials-log-collector-errors"></a>Windows Server Essentials 로그 수집기 오류 문제 해결

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

로그 수집기를 실행하면 다음 오류의 하나가 발생할 수 있습니다. 문제를 해결하려면 관련 오류에 대해 제공된 지침을 따릅니다.  
  
> [!NOTE]
> 이 문서에서는 서버가 아닌 네트워크의 컴퓨터를 네트워크 컴퓨터 라고 합니다.
  
###  <a name="the-destination-folder-is-not-valid"></a><a name="BKMK_TheDestinationFolderIsNotValid"></a>대상 폴더가 잘못 되었습니다.  
 **원인:** 로그 파일을 복사하려는 폴더가 존재하지 않거나 파일을 저장할 충분한 공간이 없을 수 있습니다.  
  
 **해결 방법:** 선택한 폴더가 존재하고 파일에 사용할 수 있는 충분한 여유 공간이 드라이브에 있는지 확인합니다. 또한 임시 폴더에 남아 있는 충분한 여유 공간이 드라이브에 있는지 확인해야 합니다.  
  
###  <a name="a-network-error-has-occurred"></a><a name="BKMK_ANetworkErrorHasOccurred"></a>네트워크 오류가 발생 했습니다.  
 **원인:** 네트워크 컴퓨터 또는 서버에 네트워크 관련 문제가 있을 수 있습니다.  
  
 **해결 방법:** 모든 컴퓨터와 네트워크로 연결된 장치의 전원이 켜져 있고 네트워크에 연결되어 있는지 확인합니다. 문제를 해결할 수 없으면 네트워크를 유지 관리하는 담당자에게 문의하세요.  
  
###  <a name="cannot-collect-log-files-for-the-computer"></a><a name="BKMK_CannotCollectLogFiles"></a>컴퓨터의 로그 파일을 수집할 수 없습니다.  
 **원인:** 컴퓨터가 서버에 컴퓨터 연결 마법사를 통해 서버에 연결되지 않았으므로 컴퓨터에 로그 수집기를 설치할 수 없습니다.  
  
 **해결 방법:** 서버 연결과 관련 된 문제를 해결 하는 방법에 대 한 자세한 내용은 [서버에 컴퓨터 연결 문제 해결](https://go.microsoft.com/fwlink/p/?LinkID=241492)을 참조 하세요.  
  
 그래도 서버에 컴퓨터를 연결할 수 없으면 다음과 같이 로그 파일을 USB 플래시 드라이브에 수동으로 복사할 수 있습니다.  
  
-   Windows 7, Windows 8 또는 Windows Multipoint Server를 실행하는 클라이언트 컴퓨터에서는 **%sysdir%\programdata\Microsoft\Windows Server** 에 있는 **Logs**폴더를 복사할 수 있습니다.  
  
###  <a name="you-do-not-have-permission-to-save-the-log-files-to-the-selected-folder"></a><a name="BKMK_YouDoNotHavePermission"></a>선택한 폴더에 로그 파일을 저장할 수 있는 권한이 없습니다.  
 **원인:** 로그 파일을 저장하도록 선택한 폴더에 대한 쓰기 권한이 없을 수 있습니다.  
  
 **해결 방법:** 로그 파일을 저장할 기본 경로를 사용 하는 경우 공유 폴더 **\\\\< ServerName\>\Logs**에 대 한 쓰기 권한이 있는지 확인 합니다. 네트워크 컴퓨터에서 로그를 저장하고 있으면 로그 파일을 저장하도록 선택한 폴더에 대한 쓰기 권한이 있는지 확인합니다.  
  
###  <a name="the-computer-is-not-configured-properly-to-collect-the-log-files"></a><a name="BKMK_TheComputerIsNotConfiguredProperly"></a>컴퓨터에서 로그 파일을 수집 하도록 제대로 구성 되어 있지 않습니다.  
 **원인:** 컴퓨터에서 로그 수집기가 제대로 구성되지 않았습니다.  
  
 **해결 방법:** 로그 수집기를 다시 설치합니다. [로그 수집기 다시 설치](Install-the-Windows-Server-Essentials-Log-Collector.md#BKMK_Reinstall)를 참조하세요.  
  
###  <a name="an-unknown-error-occurred"></a><a name="BKMK_AnUnknownErrorOccurred"></a>알 수 없는 오류가 발생 했습니다.  
 **원인:** 알 수 없습니다.  
  
 **해결 방법 1:** 로그 수집기를 다시 실행합니다. 오류가 다시 발생하면 연결 문제가 없는지 확인합니다. 로그 수집기를 다시 설치해 볼 수도 있습니다. [로그 수집기 다시 설치](Install-the-Windows-Server-Essentials-Log-Collector.md#BKMK_Reinstall)를 참조하세요. 문제를 해결할 수 없으면 네트워크를 유지 관리하는 담당자에게 문의하세요.  
  
 **해결 방법 2:** 먼저 로그 파일이 저장된 폴더를 열어 보세요. 컴퓨터 이름을 가진 zip 파일이 이미 생성되어 있으면 이 오류를 무시하고 로그 파일을 사용합니다. 생성된 로그 파일이 없으면 로그 수집기를 다시 실행합니다. 오류가 다시 발생하면 연결 문제가 없는지 확인합니다. 로그 수집기를 다시 설치해 볼 수도 있습니다. [로그 수집기 다시 설치](Install-the-Windows-Server-Essentials-Log-Collector.md#BKMK_Reinstall)를 참조하세요. 문제를 해결할 수 없으면 네트워크를 유지 관리하는 담당자에게 문의하세요.