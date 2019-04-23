---
title: 호스트 캐시 서버에서 콘텐츠 사전 해싱 및 사전 로딩(선택 사항)
description: 이 항목은 BranchCache 배포 가이드에 대 한 Windows Server 2016, 지사에 WAN 대역폭 사용량을 최적화 하기 위해 분산 및 호스트 캐시 모드로 BranchCache를 배포 하는 방법에 설명 하는 부분입니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 5a09d9f1-1049-447f-a9bf-74adf779af27
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b421132a44240520e3e3ba294623584c36b18ab4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867004"
---
# <a name="prehashing-and-preloading-content-on-hosted-cache-servers-optional"></a>호스트 캐시 서버에서 콘텐츠 사전 해싱 및 사전 로딩(선택 사항)

>적용 대상: Windows Server (반기 채널), Windows Server 2016

BranchCache 사용 가능 웹 및 파일 서버에서 해시-라고도 하는 콘텐츠 정보-의 생성을 강제로이 절차를 사용할 수 있습니다. 원격 호스트 캐시 서버로 전송할 수 있는 패키지에 파일 및 웹 서버에서 데이터를 수집할 수 있습니다.  이 데이터는 첫 번째 클라이언트 액세스를 사용할 수 있도록 원격 호스트 캐시 서버에서 콘텐츠를 미리 로드 하는 기능을 사용 하 여 제공 합니다.  
  
멤버 여야 **관리자**, 하거나이 절차를 수행 하려면 해당 합니다.  
  
### <a name="to-prehash-content-and-preload-the-content-on-hosted-cache-servers"></a>콘텐츠를 prehash 및 호스트 캐시 서버에서 콘텐츠를 미리 로드 하려면  
  
1.  파일 또는, 미리 로드 하려는 데이터를 포함 하는 웹 서버에 로그온 하 고 하나 이상의 원격 호스트 캐시 서버에 로드 하려는 파일과 폴더를 식별 합니다.  
  
2.  관리자 권한으로 Windows PowerShell을 실행 합니다. 각 폴더 및 파일에 대 한 중 하나를 실행 합니다 `Publish-BCFileContent` 명령 또는 `Publish-BCWebContent` 해시 생성을 트리거할 수 및 데이터 패키지에 데이터를 추가할 콘텐츠 서버 유형에 따라 명령을 사용 합니다.  
  
3.  모든 데이터에 데이터 패키지에 추가 된 후 사용 하 여 내보내기는 `Export-BCCachePackage` 데이터 패키지 파일을 생성 하는 명령입니다.  
  
4.  파일 전송 기술 여러분이 사용 하 여 원격 호스트 캐시 서버에 데이터 패키지 파일을 이동 합니다.  FTP, SMB, HTTP, DVD 및 이식 가능한 하드 디스크는 실행 가능한 모든 전송 합니다.  
  
5.  사용 하 여 원격 호스트 캐시 서버에서 데이터 패키지 파일을 가져오려면는 `Import-BCCachePackage` 명령입니다.  
  

