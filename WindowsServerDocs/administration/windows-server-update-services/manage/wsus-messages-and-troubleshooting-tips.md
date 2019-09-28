---
title: WSUS 메시지 및 문제 해결 팁
description: WSUS (Windows Server Update Service) 항목-WSUS 메시지를 사용 하 여 문제 해결
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-wsus
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9f6317f7-bfe0-42d9-87ce-d8f038c728ca
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1e432a962662995cf570b28d0b9496594f3e10e6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71369862"
---
# <a name="wsus-messages-and-troubleshooting-tips"></a>WSUS 메시지 및 문제 해결 팁

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에는 다음과 같은 WSUS 메시지에 대 한 정보가 포함 되어 있습니다.

-   "컴퓨터가 상태를 보고 하지 않았습니다."

-   "메시지 ID 6703-WSUS 동기화 실패"

-   "오류 0x80070643: 설치 하는 동안 심각한 오류가 발생 했습니다. "

-   "일부 서비스가 실행 되 고 있지 않습니다. 다음 서비스 [...]를 확인 합니다.

## <a name="computer-has-not-reported-status"></a>컴퓨터가 상태를 보고 하지 않음
이 메시지는 wsus 클라이언트 컴퓨터가 현재 업데이트 상태를 나타내기 위해 WSUS 서버에 정보를 보내지 않는 경우 WSUS 콘솔에 생성 됩니다. 이 문제는 일반적으로 WSUS 클라이언트 컴퓨터는 WSUS 서버에 의해 발생 합니다.

가장 일반적인 원인은 다음과 같습니다.

-   네트워크 연결을 손실 했습니다.
    -   네트워크 케이블이 연결 되어 있지 않습니다.
    -   중간 네트워크 케이블에 오류가 발생 했습니다.
    -   컴퓨터에 잘못 된 네트워크 어댑터가 있습니다.
    -   컴퓨터가 연결 되는 네트워크 포트를 사용할 수 없습니다.
    -   무선 어댑터가에 연결 하 고 회사 무선 액세스 지점에 연결할 수 없습니다.
-   컴퓨터가 꺼져 있습니다. (종료 되었거나 절전 모드 또는 최대 절전 모드에 있습니다.)

## <a name="message-id-6703---wsus-synchronization-failed"></a>메시지 ID 6703-WSUS 동기화 실패
> 메시지: HTTP 상태 503로 인해 요청이 실패 했습니다. 서비스를 사용할 수 없습니다.
> 
> 출처: Microsoft.UpdateServices.Administration.AdminProxy.createUpdateServer.

WSUS 서버의 업데이트 서비스를 열려고 시도 하면 다음과 같은 오류가 나타납니다.

> 오류: 연결 오류
> 
> WSUS 서버에 연결 하는 동안 오류가 발생 합니다. 이 오류는 여러 가지 이유로 발생할 수 있습니다. 문제가 지속 되 면 네트워크 관리자에 게 문의 하십시오. 서버에 다시 연결 하려면 서버 다시 설정 노드를 클릭 합니다.

위의 외에도 WSUS 관리 웹 사이트 (예: `http://CM12CAS:8530`)의 URL에 액세스 하려고 하면 다음 오류가 발생 합니다.

> HTTP 오류 503 합니다. 서비스를 사용할 수 없습니다.

이 상황에서 가장 일반적인 원인은 IIS에서 WsusPool 응용 프로그램 풀 중지 된 상태입니다.

또한 애플리케이션 풀의 프라이빗 메모리 제한(KB)은 기본값인 1843200K로 설정될 수 있습니다. 이 문제가 발생하면 프라이빗 메모리 제한을 4GB(4000000KB)로 늘리고 애플리케이션 풀을 다시 시작합니다. 개인 메모리 제한을 늘리려면 WsusPool 응용 프로그램 풀을 선택 하 고 응용 프로그램 풀 편집에서 고급 설정을 클릭 합니다. 그런 다음, 프라이빗 메모리 제한을 4GB(4000000 KB)로 설정합니다. 응용 프로그램 풀이 다시 시작 후 SMS_WSUS_SYNC_MANAGER 구성 요소 상태, wcm.log 및 실패에 대 한 wsyncmgr.log를 모니터링 합니다. 환경에 따라 프라이빗 메모리 제한을 8GB(8000000 KB) 이상으로 늘려야 할 수 있습니다.

자세한 내용은 다음을 참조 하세요. [HTTP 503 오류로 인해 ConfigMgr 2012의 WSUS 동기화가 실패 함](http://blogs.technet.com/b/sus/archive/2015/03/23/configmgr-2012-support-tip-wsus-sync-fails-with-http-503-errors.aspx)

## <a name="error-0x80070643-fatal-error-during-installation"></a>오류 0x80070643: 설치 하는 동안 심각한 오류가 발생 했습니다.
WSUS 설치 프로그램은 Microsoft SQL Server를 사용 하 여 설치를 수행 합니다. 이 문제는 WSUS 설치 프로그램을 실행 하는 사용자에 게 SQL Server에서 시스템 관리자 권한이 없기 때문에 발생 합니다.

이 문제를 해결 하려면 SQL Server에서 사용자 계정 또는 그룹 계정에 시스템 관리자 권한을 부여 하 고 WSUS 설치 프로그램을 다시 실행 하십시오.

## <a name="some-services-are-not-running-check-the-following-services"></a>일부 서비스는 실행 되지 않는 경우 다음 서비스를 확인 합니다.

- **Selfupdate** Selfupdate 서비스 문제 해결에 대 한 자세한 내용은 [자동 업데이트를 업데이트 해야](https://technet.microsoft.com/library/cc708554(v=ws.10).aspx) 합니다.

- **WSSUService.exe:** 이 서비스는 동기화를 용이 하 게 합니다. 동기화에 문제가 있는 경우 **시작**을 클릭 하 고 **관리 도구**를 가리킨 **다음 서비스를 클릭 하**고 서비스 목록에서 **Windows Server Update Service** 를 찾아 WSUSService에 액세스 합니다. 다음을 수행합니다.
    
    -   이 서비스가 실행 되 고 있는지 확인 합니다. 클릭 **시작** 중지 된 경우 또는 **다시 시작** 서비스를 새로 고칠 수 있습니다.
    
    -   이벤트 뷰어를 사용 하 여 확인할는 **응용 프로그램**, **보안**y, 및 **시스템** 이벤트 로그는 이벤트가 문제를 나타낼 수 있는지 확인 합니다.
    
    -   문제를 나타내는 이벤트가 있는지 확인 하기 위해 SoftwareDistribution.log를 확인할 수 있습니다.

- **웹 servicesSQL 서비스:** 웹 서비스는 IIS에서 호스팅됩니다. 실행 되지 않는 경우에 IIS (또는 실행 시작)가 있는지 확인 합니다. 입력 하 여 웹 서비스를 다시 설정 해도 **iisreset** 명령 프롬프트입니다.

- **SQL Service:** Selfupdate 서비스를 제외한 모든 서비스에는 SQL 서비스가 실행 중 이어야 합니다. SQL 연결 문제를 결과 로그 파일의 경우 먼저 SQL 서비스를 확인 합니다. SQL 서비스에 액세스 하려면 **시작**, 가리킨 **관리 도구**, 클릭 **서비스**, 를 찾은 후 다음 중 하나에 대 한 합니다.
    
  - **MSSQLSERver** (WMSDE 또는 MSDE를 사용 하는 경우 또는 SQL Server를 사용 하며 인스턴스 이름에 기본 인스턴스 이름을 사용 하는 경우)
    
  - **MSSQL$ WSUS** (하는 경우를 사용 중인 SQL Server 데이터베이스에는 명명 된 데이터베이스 인스턴스 "WSUS")
    
    서비스를 마우스 오른쪽 단추로 클릭 하 고 클릭 한 다음 **시작** 서비스를 실행 하지 않는 경우 또는 **다시 시작** 실행 되는 경우에 서비스를 새로 고칠 수 있습니다.
