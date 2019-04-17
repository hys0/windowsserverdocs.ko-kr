---
title: "서버에 WinSAT 점수 설정"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 911dc494-0f8f-4723-93d6-2106f914b906
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 77866acccac13ac48da8779700c8654f2c7f3277
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="set-the-winsat-score-on-the-server"></a>서버에 WinSAT 점수 설정

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

WinSAT CPU 점수는 비디오 스트리밍 해상도 최적화 하기 위해 Windows Server Essentials 운영 체제를 실행 하는 서버에 대 한 설정 해야 합니다. 만들고.xml WinSAT 점수 정보가 포함 된 파일을 설치 하 여이 작업을 수행 합니다.  
  
## <a name="obtain-the-winsat-cpu-score"></a>WinSAT CPU 점수 받기  
 프로그램 WinServerSAT.exe WinSAT CPU 점수를 검색 하 고 운영 체제 읽고 WinServerSAT.xml 파일에 해당 정보를 저장 하는 라고 OPK 제공 됩니다.  
  
#### <a name="to-obtain-the-winsat-cpu-score"></a>WinSAT CPU 점수 얻는  
  
1.  Resources\WinServerSAT\\ * ADK 미디어에서 컴퓨터에 복사 참조 합니다.  
  
2.  참조 컴퓨터에서 관리자 권한 명령 프롬프트 창을 엽니다.  
  
3.  %ProgramFiles%\Windows Server\Bin\OEM 폴더가 없는 경우 다음 명령을 입력 하 고 Enter 키를 누릅니다.  
  
     **Mkdir "%ProgramFiles%\Windows Server\Bin\OEM"**  
  
4.  다음 명령을 입력 하 고 Enter 키를 누릅니다.  
  
     **WinServerSAT.exe "%ProgramFiles%\Windows Server\Bin\OEM\WinServerSAT.xml"**  
  
 만든 WinServerSAT.xml 파일의 XML 콘텐츠는 다음과 같습니다.  
  
```  
  
<?xml version="1.0" encoding="UTF-16"?>  
<WinSAT>  
   <CpuScore description="WinSAT CPU score">WinSAT_Score</CpuScore>  
</WinSAT>  
```  
  
 여기서 *WinSAT_Score* 서버에서 발견 값으로 대체 됩니다.  
  
> [!IMPORTANT]
>  사진 촬영 하기 전에 참조 컴퓨터에서 WinServerSAT.exe, winsat.prx, winsat.wmv WinSATEncode.wmv 파일 제거 해야 합니다.
