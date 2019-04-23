---
ms.assetid: 2e748187-6a10-4bb0-aed5-34f886a250d2
title: Fsutil
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 08/21/2018
ms.openlocfilehash: df8d25b01b67010734deb8dd7e42f3233e6011fe
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59866814"
---
# <a name="fsutil"></a>Fsutil

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7

파일 할당 테이블 (FAT) 및 NTFS 파일 시스템 재분석 관리와 같은 요소, 스파스 파일 관리 또는 볼륨을 분리 하 여 관련 작업을 수행 합니다. 매개 변수 없이 사용 하는 경우 **Fsutil** 지원 되는 하위 명령 목록이 표시 됩니다. 

> [!Note] 
> Fsutil을 사용 하는 관리자 또는 Administrators 그룹의 구성원으로 로그온 해야 합니다. Fsutil 명령어 매우 강력 하 고 Windows 운영 체제에 잘 알고 있는 고급 사용자에 의해서만 사용 해야 합니다.
>
>실행 하기 전에 Linux 용 Windows 하위 시스템을 사용 하도록 설정 해야 **Fsutil**합니다. 이 선택적 기능을 사용 하도록 설정 하려면 PowerShell에서 관리자 권한으로 다음 명령을 실행 합니다.
>
>```
> Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
>```
> 설치한 후 컴퓨터를 다시 시작 하 라는 메시지가 표시 됩니다. 컴퓨터를 다시 시작한 후에 실행할 수 있습니다 **Fsutil** 관리자 권한으로 합니다.

## <a name="parameters"></a>매개 변수

|하위 명령 |설명|
|---|---|
|[Fsutil 8dot3name](fsutil-8dot3name.md) | 쿼리 또는 예를 들어 시스템에서 약식 이름 동작에 대 한 설정 변경, 8.3 문자 길이 파일 이름을 생성 합니다. 디렉터리 내의 모든 파일의 짧은 이름 제거 디렉터리를 검색 하 고 짧은 이름 디렉터리의 파일에서 제거 된 경우 영향을 받을 수 있는 레지스트리 키를 식별 합니다.|
|[fsutil 동작](fsutil-behavior.md) |쿼리 또는 볼륨 동작을 설정 합니다.|
|[fsutil 커밋되지 않은 데이터](fsutil-dirty.md)| 볼륨의 더티 비트 설정 된 볼륨의 더티 비트를 설정 하는지 여부를 쿼리 합니다. 볼륨의 더티 비트가 설정 됩니다, **않은** 자동으로 오류에 대 한 볼륨을 다음에 컴퓨터를 다시 확인 합니다.|
|[fsutil 파일](fsutil-file.md)|(디스크 할당량 사용) 하는 경우 사용자 이름으로 파일을 찾거나, 파일에 할당 된 범위를 쿼리, 파일의 짧은 이름을 설정, 파일의 유효한 데이터 길이 설정, 파일에 대 한 제로 값을 설정, 지정된 된 크기의 새 파일을 만듭니다, 그리고 이름을 지정 하는 경우 파일 ID를 찾습니다. 에 지정 된 파일 ID에 대 한 파일 링크 이름을 찾습니다 또는|
|[fsutil fsinfo](fsutil-fsinfo.md)|모든 드라이브를 나열 하 고 드라이브 종류, 볼륨 정보, NTFS 관련 볼륨 정보 또는 파일 시스템 통계를 쿼리 합니다.|
|[fsutil hardlink](fsutil-hardlink.md)|파일에 대 한 하드 링크를 나열 하거나 하드 링크 (파일에 대 한 디렉터리 항목)를 만듭니다. 모든 파일을 하나 이상의 하드 링크 간주할 수 있습니다. NTFS 볼륨에 단일 파일 많은 디렉터리에 (또는 다른 이름의 같은 디렉터리에도) 표시 될 수 있도록 각 파일 여러 하드 링크가 있을 수 있습니다. 동일한 파일을 참조 하는 모든 링크가 하므로 프로그램 링크 연 파일을 수정 합니다. 에 대 한 모든 링크를 삭제 한 후에 파일을 파일 시스템에서 삭제 됩니다. 하드 링크를 만든 후 프로그램에서 다른 파일 이름 처럼 사용할 수 있습니다.|
|[Fsutil objectid](fsutil-objectid.md)|파일 및 디렉터리와 같은 개체를 추적 하는 Windows 운영 체제에서 사용 되는 개체 식별자를 관리 합니다.|
|[fsutil 할당량](fsutil-quota.md)|네트워크 기반 저장소 보다 자세하게 제어할 수 있도록 NTFS 볼륨의 디스크 할당량을 관리 합니다. 디스크 할당량은 볼륨 단위로에 구현 되며 두 가지 하드 및 소프트-저장소 제한을 모두 사용자별으로 구현 합니다.|
|[fsutil 복구](fsutil-repair.md)|쿼리 또는 볼륨의 자동 복구 상태를 설정 합니다. 요구 하지 않고 온라인 NTFS 파일 시스템의 손상을 해결 하려고 NTFS를 자체 치유 **Chkdsk.exe** 실행 되도록 합니다. 디스크 확인을 시작 및 복구 완료 되기를 기다리는 포함 되어 있습니다.|
|[fsutil reparsepoint](fsutil-reparsepoint.md)|쿼리 또는 삭제 재분석 지점 (NTFS 파일 시스템 개체 정의할 수 있는 특성을 사용자 제어 데이터를 포함 하는). 재분석 지점은 입/출력 (I/O) 하위 시스템의 기능을 확장 하는 데 사용 됩니다. 디렉터리 연결 지점과 볼륨 탑재 지점에 사용 됩니다. 특정 파일에 해당 드라이버에 특별 한 것으로 표시 하 여 파일 시스템 필터 드라이버 사용 되기도 합니다.|
|[fsutil 리소스](fsutil-resource.md)|보조 트랜잭션 리소스 관리자를 만들고, 시작 또는 트랜잭션 리소스 관리자를 중지, 트랜잭션 리소스 관리자에 대 한 정보를 표시 또는 해당 동작을 수정 합니다.|
|[fsutil 스파스](fsutil-sparse.md)|스파스 파일을 관리 합니다. 스파스 파일은 하나 이상의 영역에 할당 되지 않은 데이터를 포함 하는 파일입니다. 프로그램 0 값을 포함 하 여 바이트를 포함 하는 것이 할당 되지 않은 지역이 표시 됩니다. 그러나 디스크 공간이 없으면이 0을 나타내는 데 사용 됩니다. 모든 의미 있는 또는 0이 아닌 데이터는 할당 되지만 모든 의미 없는 데이터 (0으로 구성 된 데이터의 큰 문자열) 할당 되지 않습니다. 스파스 파일을 읽을 때 할당 된 데이터는 저장 하 고 할당 되지 않은 데이터는 기본적으로 c2 보안 요구 사항에 따라 0으로 반환 됩니다. 할당을 취소할 수에서 아무 곳 이나 파일에서 데이터를 허용 하는 스파스 파일을 지원 합니다.|
|[Fsutil 계층화](fsutil-tiering.md)|설정 및 플래그를 사용 하지 않도록 설정 하 고 계층 목록 같은 저장소 계층 함수를 관리할 수 있습니다.|
|[fsutil 트랜잭션](fsutil-transaction.md)|지정된 된 트랜잭션을 커밋합니다, 그리고 지정된 된 트랜잭션을 롤백합니다 또는 트랜잭션에 대 한 정보가 표시 됩니다.|
|[fsutil usn](fsutil-usn.md)|볼륨의 파일에 대 한 모든 변경 내용 영구적 로그를 제공 하는 업데이트 시퀀스 번호 (USN) 변경 저널을 관리 합니다.|
|[fsutil 볼륨](fsutil-volume.md)|볼륨을 관리합니다. 볼륨을 쿼리 하는 디스크에서 사용 가능한 공간을 분리 하거나 지정된 된 클러스터를 사용 하는 파일을 찾습니다.|
|[fsutil wim](fsutil-wim.md)|검색 하 고 WIM 기반의 파일 관리 함수를 제공 합니다.|

## <a name="see-also"></a>참조
[명령줄 구문 키](Command-Line-Syntax-Key.md)