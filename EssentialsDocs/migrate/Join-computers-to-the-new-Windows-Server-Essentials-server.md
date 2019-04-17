---
title: "새로운 Windows Server Essentials 서버 1 컴퓨터 가입"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cdfa9504-9881-4265-b308-c7ee8721bfaa
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 1a67cda9e4b04e8d861232b48f45915fb2b460d1
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="join-computers-to-the-new-windows-server-essentials-server1"></a>새로운 Windows Server Essentials 서버 1 컴퓨터 가입

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

##  <a name="BKMK_JoinComputers"></a>   
 마이그레이션 프로세스의 다음 단계 클라이언트 컴퓨터 새로운 Windows Server Essentials 네트워크에 가입 하 고 그룹 정책 설정을 업데이트 하는 것입니다.  
  
> [!NOTE]
>  클라이언트 컴퓨터가 이미 소스 서버에 가입, 컴퓨터 대상 서버에 연결 하기 전에 먼저 가지의 커넥터 소프트웨어를 제거 해야 합니다.  
  
 컴퓨터에 연결 하는 클라이언트는 서버는 과정은 도메인에 가입 하거나 도메인 가입 된 컴퓨터에 대 한 동일 합니다.  
  
-   찾아보기 **http://***목적지 이름***연결 /** 이것은 새 컴퓨터 하는 경우 Windows Server Connector 소프트웨어를 설치 하 고 있습니다.  
  
> [!NOTE]
>  Windows Server Connector 소프트웨어는 Windows XP 또는 Windows Vista를 실행 하는 컴퓨터를 지원 하지 않습니다. 도메인에 가입한 이미 Windows XP 또는 Windows Vista를 실행 하는 컴퓨터를 사용 하는 경우이 단계를 건너뛸 수 있습니다.  
  
### <a name="ensure-that-group-policy-has-updated"></a>그룹 정책은 업데이트 확인  
  
> [!NOTE]
>  이 단계 이며 기능도 못하는 것은 사용자 지정 그룹 정책 설정 폴더 리디렉션을 등으로 원본 서버 구성 된 경우 필요 합니다.  
  
 원본 서버와 대상 서버는 여전히 온라인, 그룹 정책 설정 클라이언트 컴퓨터에 복제 대상 서버에서 확인 해야 합니다. 각 클라이언트 컴퓨터에서 다음 단계를 수행 합니다.  
  
1.  명령 프롬프트 창을 엽니다.  
  
2.  명령 프롬프트에 입력 **GPRESULT /R**, ENTER 키를 누릅니다.  
  
3.  결과에서 그룹 정책을 적용 된 섹션에 대 한 출력 검토:와 같은 대상 서버가 나열 되어 있는지 확인 하 고 **DestinationSrv.Domain.local**합니다. 예를 들어:  
  
    ```  
    USER SETTINGS  
    --------------  
        CN=User,OU=Users,DC=DOMAIN,DC=Local  
        Last time Group Policy was applied: 1/24/2011 at 1:26:27 PM  
        Group Policy was applied from:      DestinationSrv.Domain.local  
        Group Policy slow link threshold:   500 kbps  
        Domain Name:                        Domain  
        Domain Type:                        Windows 2011  
  
    ```  
  
4.  대상 서버 나열 되지 않은 명령 프롬프트에 입력 **gpupdate /force**, enter를 새로 고침 그룹 정책 설정 하 고 있습니다. 그런 다음 다시 이전 절차를 수행 합니다.  
  
5.  대상 서버 표시 되지 않는 경우에 특정 클라이언트가 컴퓨터에 적용 오류나 그룹 정책 설정에 오류가 수도 있습니다. 대상 서버 표시 되지 않으면 다음 단계를 수행 합니다.  
  
    1.  클릭 **시작**, 클릭 **실행**, 입력 **rsop.msc** (설정 정책 결과), ENTER 키를 누릅니다.  
  
    2.  노드를 받을 때까지에 x 트리를 확장 합니다.  
  
    3.  노드를 마우스 오른쪽 단추로 클릭 한 **보기 오류** 이유에 대 한 정보에 대 한 그룹 정책 설정을 나열 된 컴퓨터에 실패 합니다.
