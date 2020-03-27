---
title: 호스트 캐시 서버에서 콘텐츠 사전 해싱 및 사전 로딩(선택 사항)
description: 이 항목은 분산 및 호스트 캐시 모드에서 BranchCache를 배포 하 여 지점의 WAN 대역폭 사용량을 최적화 하는 방법을 보여 주는 Windows Server 2016 용 BranchCache 배포 가이드의 일부입니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 5a09d9f1-1049-447f-a9bf-74adf779af27
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 7fe43b3a7c8dc7906e678a219b67ed096aa951d4
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80319124"
---
# <a name="prehashing-and-preloading-content-on-hosted-cache-servers-optional"></a>호스트 캐시 서버에서 콘텐츠 사전 해싱 및 사전 로딩(선택 사항)

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 절차를 사용 하 여 BranchCache 사용 웹 및 파일 서버에 대 한 콘텐츠 정보 (해시 라고도 함)를 강제로 만들 수 있습니다. 또한 파일 및 웹 서버의 데이터를 원격 호스트 캐시 서버로 전송할 수 있는 패키지로 수집할 수 있습니다.  그러면 원격 호스트 캐시 서버에서 콘텐츠를 미리 로드 하 여 첫 번째 클라이언트 액세스에 데이터를 사용할 수 있게 됩니다.  
  
멤버 여야 **관리자**, 하거나이 절차를 수행 하려면 해당 합니다.  
  
### <a name="to-prehash-content-and-preload-the-content-on-hosted-cache-servers"></a>콘텐츠를 사전 해시 하 고 호스트 캐시 서버에서 콘텐츠를 미리 로드 하려면  
  
1.  미리 로드할 데이터가 포함 된 파일 또는 웹 서버에 로그온 하 고 하나 이상의 원격 호스트 캐시 서버에서 로드 하려는 폴더와 파일을 식별 합니다.  
  
2.  관리자 권한으로 Windows PowerShell을 실행 합니다. 각 폴더와 파일에 대해 `Publish-BCFileContent` 명령 또는 `Publish-BCWebContent` 명령 (콘텐츠 서버 유형에 따라)을 실행 하 여 해시 생성을 트리거하고 데이터 패키지에 데이터를 추가 합니다.  
  
3.  데이터 패키지에 모든 데이터를 추가한 후에는 `Export-BCCachePackage` 명령을 사용 하 여 데이터 패키지 파일을 생성 하 여 데이터를 내보냅니다.  
  
4.  원하는 파일 전송 기술을 사용 하 여 원격 호스트 캐시 서버로 데이터 패키지 파일을 이동 합니다.  FTP, SMB, HTTP, DVD 및 휴대용 하드 디스크는 모두 유효한 전송입니다.  
  
5.  `Import-BCCachePackage` 명령을 사용 하 여 원격 호스트 캐시 서버에서 데이터 패키지 파일을 가져옵니다.  
  

