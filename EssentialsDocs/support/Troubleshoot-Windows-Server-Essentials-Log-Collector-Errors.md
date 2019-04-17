---
title: "Windows Server Essentials 로그 수집기 오류 문제 해결"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fa2e1685-31c0-4d4f-a10a-6c8885dfc493
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: e92236c8e5d956b50f657ebcbe1a942b5841fded
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="troubleshoot-windows-server-essentials-log-collector-errors"></a>Windows Server Essentials 로그 수집기 오류 문제 해결

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

로그 수집기를 실행 하면 다음과 같은 오류 중 하나가 발생할 수 있습니다. 문제를 해결 하려면 관련된 오류에 대 한 제공 되는 지침을 따릅니다.  
  
> [!NOTE]
>  이 문서에서 서버를 이외의 네트워크의 컴퓨터 네트워크 컴퓨터 라고?  
  
###  <a name="BKMK_TheDestinationFolderIsNotValid"></a>대상 폴더 잘못 되었습니다.  
 **원인:** 로그 파일을 복사 하려는 폴더 존재 하지 않거나에서 파일을 저장할 충분 한 공간이 없는 수 있습니다.  
  
 **해결 방법:** 선택한 폴더 있는지, 그리고 파일에 대 한 드라이브에 사용할 수 있는 충분 한 여유 공간이 있는지 확인 합니다. 또한 남아 있는 기가 드라이브에 충분 한 여유 공간이 있는지 확인 해야 합니다.  
  
###  <a name="BKMK_ANetworkErrorHasOccurred"></a>네트워크 오류가 발생 했습니다.  
 **원인:** 네트워크 컴퓨터 또는 서버에 네트워크와 관련 된 문제일 수 있습니다.  
  
 **해결 방법:** 모든 컴퓨터 및 네트워크에 연결 된 디바이스가 켜져 있고 네트워크에 연결 되어 있는지 확인 합니다. 이 문제를 해결할 수 없는 경우 지원에 대 한 네트워크를 유지 사람에 게 문의 합니다.  
  
###  <a name="BKMK_CannotCollectLogFiles"></a>컴퓨터에 대 한 로그 파일 수집할 수 없습니다.  
 **원인:** 컴퓨터 서버 마법사 컴퓨터 연결을 사용 하 여 서버에 연결 되지 않은 때문에 로그 컬렉터 컴퓨터에 설치 되지 않을 수 있습니다.  
  
 **해결 방법:** 서버에 연결에 대 한 문제를 해결 하는 방법에 대 한 정보를 참조 하세요. [컴퓨터 서버에 연결 문제 해결](https://go.microsoft.com/fwlink/p/?LinkID=241492)있나요? (https://go.microsoft.com/fwlink/p/?LinkID=241492) Microsoft 웹 사이트에서 합니다.  
  
 컴퓨터의 서버에 연결할 수 없는 경우 다음 복사할 수 있습니다 로그 파일 수동으로 USB 플래시 드라이브를 다음과 같습니다.  
  
-   Windows 7, Windows 8 또는 Windows Server 다중을 실행 하는 클라이언트 컴퓨터에 복사할 수는 **로그** 폴더에 있는 **%sysdir%\programdata\Microsoft\Windows 서버**합니다.  
  
###  <a name="BKMK_YouDoNotHavePermission"></a>파일을 저장할 로그 폴더에 권한이  
 **원인:** 선택한 로그 파일을 저장할 폴더를 쓰기 권한이 없는 수 있습니다.  
  
 **해결 방법:** 기본 경로 로그 파일을 저장할를 사용 하는 경우, 공유 폴더에 대 한 쓰기 권한이 있는지 확인 **\\\ < ServerName\ > \Logs**합니다. 네트워크 컴퓨터에서 로그를 저장 하는 경우 로그 파일을 저장 하기 위한 선택한 폴더에 대 한 쓰기 권한이 있는지 확인 합니다.  
  
###  <a name="BKMK_TheComputerIsNotConfiguredProperly"></a>로그 파일을 수집 하는 컴퓨터 올바르게 구성 되지 않았습니다.  
 **원인:** 컴퓨터에 대 한 로그 수집기 올바르게 구성 되지 않았습니다.  
  
 **해결 방법:** 로그 수집기를 다시 설치 합니다. 참조 [로그 수집기 다시 설치](Install-the-Windows-Server-Essentials-Log-Collector.md#BKMK_Reinstall)합니다.  
  
###  <a name="BKMK_AnUnknownErrorOccurred"></a>오류가 발생 했습니다.  
 **원인:** 알 수 있습니다.  
  
 **해결 방법 1:** 로그 수집기 다시 실행 합니다. 오류가 발생 다시 연결 문제가 없는지 확인 합니다. 로그 수집기를 다시 설치할 수도 있습니다. 참조 [로그 수집기 다시 설치](Install-the-Windows-Server-Essentials-Log-Collector.md#BKMK_Reinstall)합니다. 이 문제를 해결할 수 없는 경우 지원에 대 한 네트워크를 유지 사람에 게 문의 합니다.  
  
 **해결 방법 2:** 먼저 로그 파일이 저장 된 폴더를 엽니다. 컴퓨터 이름으로 zip 파일 이미 생성,이 오류를 무시 하 고 로그 파일을 대신 사용 합니다. 생성 로그 파일이 없는 경우 다시 로그 수집기 실행 합니다. 오류가 발생 다시 연결 문제가 없는지 확인 합니다. 로그 수집기를 다시 설치할 수도 있습니다. 참조 [로그 수집기 다시 설치](Install-the-Windows-Server-Essentials-Log-Collector.md#BKMK_Reinstall)합니다. 이 문제를 해결할 수 없는 경우 지원에 대 한 네트워크를 유지 사람에 게 문의 합니다.