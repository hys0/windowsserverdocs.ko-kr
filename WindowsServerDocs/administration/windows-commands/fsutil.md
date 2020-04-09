---
ms.assetid: 2e748187-6a10-4bb0-aed5-34f886a250d2
title: Fsutil
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 08/21/2018
ms.openlocfilehash: 717c287995be2ab56bd49f2f24d46001f77e0e68
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80843906"
---
# <a name="fsutil"></a>Fsutil

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7

는 FAT (파일 할당 테이블) 및 NTFS 파일 시스템 (예: 재분석 지점의 관리, 스파스 파일 관리 또는 볼륨 분리)과 관련 된 작업을 수행 합니다. 매개 변수 없이 사용 하는 경우 **Fsutil** 은 지원 되는 하위 명령 목록을 표시 합니다. 

> [!Note] 
> Fsutil을 사용 하려면 관리자 또는 관리자 그룹의 구성원으로 로그온 해야 합니다. Fsutil 명령은 매우 강력 하며, Windows 운영 체제에 대 한 철저 한 지식이 있는 고급 사용자만 사용 해야 합니다.
>
>**Fsutil**을 실행 하기 전에 Linux 용 Windows 하위 시스템을 사용 하도록 설정 해야 합니다. PowerShell에서 관리자 권한으로 다음 명령을 실행 하 여이 선택적 기능을 사용 하도록 설정 합니다.
>
>```
> Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
>```
> 설치 되 면 컴퓨터를 다시 시작 하 라는 메시지가 표시 됩니다. 컴퓨터를 다시 시작한 후 관리자 권한으로 **Fsutil** 을 실행할 수 있습니다.

### <a name="parameters"></a>매개 변수

|하위 명령 |설명|
|---|---|
|[Fsutil 8dot3name](fsutil-8dot3name.md) | 예를 들어 시스템에서 짧은 이름 동작에 대 한 설정을 쿼리하거나 변경 하 여 8.3 문자 길이 파일 이름을 생성 합니다. 디렉터리 내의 모든 파일의 짧은 이름 제거 디렉터리를 검색 하 고 짧은 이름 디렉터리의 파일에서 제거 된 경우 영향을 받을 수 있는 레지스트리 키를 식별 합니다.|
|[Fsutil 동작](fsutil-behavior.md) |볼륨 동작을 쿼리하거나 설정 합니다.|
|[Fsutil 더티](fsutil-dirty.md)| 볼륨의 더티 비트 설정 된 볼륨의 더티 비트를 설정 하는지 여부를 쿼리 합니다. 볼륨의 더티 비트가 설정 됩니다, **않은** 자동으로 오류에 대 한 볼륨을 다음에 컴퓨터를 다시 확인 합니다.|
|[Fsutil 파일](fsutil-file.md)|사용자 이름 (디스크 할당량을 사용 하는 경우)을 사용 하 여 파일을 찾고, 파일에 할당 된 범위를 쿼리하고, 파일의 짧은 이름을 설정 하 고, 파일의 유효한 데이터 길이를 설정 하 고, 파일의 유효한 데이터 길이를 설정 하거나, 지정 된 크기의 새 파일을 만들거나, 지정 된 파일 ID에 대 한 파일 링크 이름을 찾습니다.|
|[Fsutil fsinfo](fsutil-fsinfo.md)|모든 드라이브를 나열 하 고 드라이브 종류, 볼륨 정보, NTFS 특정 볼륨 정보 또는 파일 시스템 통계를 쿼리 합니다.|
|[Fsutil hardlink create](fsutil-hardlink.md)|파일에 대 한 하드 링크를 나열 하거나 하드 링크를 만듭니다 (파일에 대 한 디렉터리 항목). 모든 파일을 하나 이상의 하드 링크 간주할 수 있습니다. NTFS 볼륨에서 각 파일에는 여러 하드 링크가 있을 수 있으므로 단일 파일이 여러 디렉터리 (또는 이름이 다른 같은 디렉터리에도 표시 될 수 있음)에 표시 될 수 있습니다. 동일한 파일을 참조 하는 모든 링크가 하므로 프로그램 링크 연 파일을 수정 합니다. 에 대 한 모든 링크를 삭제 한 후에 파일을 파일 시스템에서 삭제 됩니다. 하드 링크를 만든 후 프로그램에서 다른 파일 이름 처럼 사용할 수 있습니다.|
|[Fsutil objectid](fsutil-objectid.md)|파일 및 디렉터리와 같은 개체를 추적 하는 Windows 운영 체제에서 사용 되는 개체 식별자를 관리 합니다.|
|[Fsutil 할당량](fsutil-quota.md)|네트워크 기반 저장소를 보다 정확 하 게 제어할 수 있도록 NTFS 볼륨의 디스크 할당량을 관리 합니다. 디스크 할당량은 볼륨 단위로 구현 되며, 사용자 단위로 하드 및 소프트 저장소 제한을 모두 구현할 수 있습니다.|
|[Fsutil 복구](fsutil-repair.md)|볼륨의 자동 복구 상태를 쿼리하거나 설정 합니다. 자동 복구 NTFS는 **chkdsk.exe** 를 실행 하지 않고도 온라인으로 ntfs 파일 시스템의 손상을 해결 하려고 시도 합니다. 디스크 확인 시작 및 복구 완료 대기를 포함 합니다.|
|[Fsutil reparsepoint](fsutil-reparsepoint.md)|쿼리 또는 삭제 재분석 지점은 (사용자 제어 데이터를 포함 하는 정의 가능한 특성이 있는 NTFS 파일 시스템 개체) 재분석 지점은 입/출력 (i/o) 하위 시스템의 기능을 확장 하는 데 사용 됩니다. 디렉터리 연결 지점과 볼륨 탑재 지점에 사용 됩니다. 특정 파일에 해당 드라이버에 특별 한 것으로 표시 하 여 파일 시스템 필터 드라이버 사용 되기도 합니다.|
|[Fsutil 리소스](fsutil-resource.md)|보조 트랜잭션 리소스 관리자를 만들고 트랜잭션 리소스 관리자를 시작 또는 중지 하 고 트랜잭션 리소스 관리자 대 한 정보를 표시 하거나 해당 동작을 수정 합니다.|
|[Fsutil sparse](fsutil-sparse.md)|스파스 파일을 관리 합니다. 스파스 파일은 하나 이상의 영역에 할당 되지 않은 데이터를 포함 하는 파일입니다. 프로그램 0 값을 포함 하 여 바이트를 포함 하는 것이 할당 되지 않은 지역이 표시 됩니다. 그러나 디스크 공간이 없으면이 0을 나타내는 데 사용 됩니다. 모든 의미 있는 데이터 또는 0이 아닌 데이터는 할당 되지만 의미 없는 모든 데이터 (0으로 구성 된 데이터의 많은 문자열)는 할당 되지 않습니다. 스파스 파일을 읽으면 할당 된 데이터가 저장 된 것으로 반환 되 고 할당 되지 않은 데이터가 0으로 반환 됩니다 (기본적으로 C2 보안 요구 사항 사양에 따라). 할당을 취소할 수에서 아무 곳 이나 파일에서 데이터를 허용 하는 스파스 파일을 지원 합니다.|
|[Fsutil 계층화](fsutil-tiering.md)|플래그 설정/해제, 계층 목록 등의 저장소 계층 기능을 관리할 수 있습니다.|
|[Fsutil 트랜잭션](fsutil-transaction.md)|지정 된 트랜잭션을 커밋하거나 지정 된 트랜잭션을 롤백하거나 트랜잭션에 대 한 정보를 표시 합니다.|
|[Fsutil usn](fsutil-usn.md)|볼륨에 있는 파일의 모든 변경 내용에 대 한 영구적 로그를 제공 하는 USN (업데이트 시퀀스 번호) 변경 저널을 관리 합니다.|
|[Fsutil 볼륨](fsutil-volume.md)|볼륨을 관리합니다. 볼륨을 쿼리 하는 디스크에서 사용 가능한 공간을 분리 하거나 지정된 된 클러스터를 사용 하는 파일을 찾습니다.|
|[Fsutil wim](fsutil-wim.md)|WIM 지원 파일을 검색 하 고 관리 하는 함수를 제공 합니다.|

## <a name="see-also"></a>참고 항목
- [명령줄 구문 키](command-line-syntax-key.md)