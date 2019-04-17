---
title: Prehashing 및 미리 로드 서버의 콘텐츠를 호스트 캐시 (선택 사항)
description: 이 항목 대 한 Windows Server 2016을 지점에서 WAN 대역폭 사용을 최적화 하 분산 / 호스팅된 캐시 모드로 BranchCache 배포 하는 방법을 보여 주는 BranchCache 배포 가이드의 일부입니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 5a09d9f1-1049-447f-a9bf-74adf779af27
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c3d1ed62c6dca5b1de0ff560fde0a2e43ed0d080
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="prehashing-and-preloading-content-on-hosted-cache-servers-optional"></a>Prehashing 및 미리 로드 서버의 콘텐츠를 호스트 캐시 (선택 사항)

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 절차 BranchCache 활성화 파일 및 웹 서버에서 해시-라고도-콘텐츠 정보의 사용할 수 있습니다. 호스트 캐시 원격 서버에 전송 될 수 있는 패키지로 파일 및 웹 서버에 데이터를 수집할 수 있습니다.  이 데이터는 첫 번째 클라이언트 액세스할 수 있도록 원격 호스트 캐시 서버의 콘텐츠를 미리 로드 하는 기능이 제공 합니다.  
  
소속 있어야 **관리자**, 나이 절차를 수행 하는 것과 같습니다.  
  
### <a name="to-prehash-content-and-preload-the-content-on-hosted-cache-servers"></a>Prehash 콘텐츠를 호스트 캐시 서버에 콘텐츠를 미리 로드  
  
1.  파일 또는 미리 로드 하는 데이터를 포함 하는 웹 서버에에 로그인 하 고 하나 이상의 호스트 캐시 원격 서버에 로드 하고자 하는 파일과 폴더를 식별 합니다.  
  
2.  Windows PowerShell을 관리자 권한으로 실행 합니다. 각 폴더 및 파일을 실행 중 하나는 `Publish-BCFileContent`명령 또는 `Publish-BCWebContent`트리거하 해시 생성 하 고 데이터 데이터 패키지를 추가 하려면 콘텐츠 서버 유형에 따라 명령을 합니다.  
  
3.  후 데이터 패키지에 추가한 모든 데이터를 사용 하 여 내보낼는 `Export-BCCachePackage`명령 데이터 패키지 파일을 생성 합니다.  
  
4.  사용자가 선택한 파일 전송 기술 사용 하 여 호스팅된 캐시 원격 서버에 데이터 패키지 파일을 이동 합니다.  FTP, SMB, HTTP, DVD, 이동식 하드 디스크 모든 사용 가능한 전송 됩니다.  
  
5.  사용 하 여 호스팅된 캐시 원격 서버에 데이터 패키지 파일을 가져올는 `Import-BCCachePackage`명령을 합니다.  
  

