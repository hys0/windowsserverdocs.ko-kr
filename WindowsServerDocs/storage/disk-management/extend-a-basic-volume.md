---
title: 기본 볼륨 확장
description: 이 문서에서는 기본 및 논리 드라이브에 공간을 추가하고 기본 볼륨을 확장하는 방법을 설명합니다.
ms.date: 10/12/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: c20e2da3e629743ab4d4d4cf1da16a6e69093ecf
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192576"
---
# <a name="extend-a-basic-volume"></a>기본 볼륨 확장

> **적용 대상:** Windows 10, Windows 8.1, Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

기존 기본 파티션 및 논리 드라이브를 동일한 디스크의 할당되지 않은 인접 공간으로 확장하여 더 많은 공간을 추가할 수 있습니다. 기본 볼륨을 확장하려면 원시(파일 시스템으로 포맷되지 않음) 상태이거나 NTFS 파일 시스템으로 포맷된 상태여야 합니다. 확장된 파티션에 포함된 인접한 사용 가능한 공간 내에 논리 드라이브를 확장할 수 있습니다. 확장된 파티션의 사용 가능한 공간을 초과하여 논리 드라이브를 확장한 경우 확장된 파티션이 확장되어 논리 드라이브를 포함합니다.

논리 드라이브 및 부트 또는 시스템 볼륨의 경우 볼륨을 인접한 공간으로만 확장할 수 있으며 디스크는 동적 디스크로만 업그레이드될 수 있습니다. 기타 볼륨의 경우 볼륨을 인접하지 않은 공간으로 확장할 수 있지만 디스크를 동적 디스크로 변환하라는 메시지가 표시됩니다.

## <a name="extending-a-basic-volume"></a>기본 볼륨 확장

-   [Windows 인터페이스를 사용 하 여](#to-extend-a-basic-volume-using-the-windows-interface)
-   [명령줄을 사용 하 여](#to-extend-a-basic-volume-using-a-command-line)

#### <a name="to-extend-a-basic-volume-using-the-windows-interface"></a>Windows 인터페이스를 사용하여 기본 볼륨 확장

1. 디스크 관리자에서 확장하고자 하는 기본 볼륨을 마우스 오른쪽 단추로 클릭합니다.

2. **볼륨 확장**을 클릭합니다.

3. 화면상의 지침을 따릅니다.

#### <a name="to-extend-a-basic-volume-using-a-command-line"></a>명령줄을 사용하여 기본 볼륨 확장

1. 명령 프롬프트를 열고 `diskpart`를 입력합니다.

2. **DISKPART** 프롬프트에서 `list volume`을 입력합니다. 확장하고자 하는 기본 볼륨을 메모합니다.

3. **DISKPART** 프롬프트에서 `select volume <volumenumber>`을 입력합니다. 이를 통해 동일한 디스크의 인접한 비어 있는 공간으로 확장하고자 하는 기본 볼륨 *volumenumber*을 선택합니다.

4. **DISKPART** 프롬프트에서 `extend [size=<size>]`을 입력합니다. 이를 통해 선택한 볼륨을 MB(메가바이트) *크기*로 확장합니다.

| 값 | 설명 |
| --- | --- |
| <p>**볼륨 목록**</p> | <p>모든 디스크에 기본 및 동적 볼륨 목록을 표시합니다.</p> |
| <p>**볼륨 선택**</p> | <p>볼륨 번호가 <em>volumenumber</em>인 지정된 볼륨을 선택하고 포커스를 설정합니다. 지정된 볼륨이 없는 경우 **select** 명령이 포커스가 설정된 현재 볼륨 목록을 표시합니다. 번호, 드라이브 문자 또는 탑재 지점 경로로 볼륨을 지정할 수 있습니다. 기본 디스크에서 볼륨을 선택하면 해당 파티션에도 포커스를 설정합니다.</p> |
| <p>**extend**</p> | <p><ul><li>포커스가 설정된 볼륨을 다음으로 인접한 할당되지 않은 공간으로 확장합니다. 기본 볼륨의 경우 할당되지 않은 공간이 동일한 디스크에 있어야 하고, 포커스가 설정된 파티션보다 더 높은 섹터 오프셋이어야 합니다. 동적 단순 또는 스팬 볼륨은 모든 동적 디스크의 모든 빈 공간으로 확장될 수 있습니다. 이 명령을 사용하여 기존 볼륨을 새로 만든 공간으로 확장할 수 있습니다.</p></li ><p><li>이전에 파티션을 NTFS 파일 시스템으로 포맷한 경우 파일 시스템은 자동적으로 확장되어 더 큰 파티션을 차지합니다. 데이터는 손실되지 않습니다. 이전에 파티션을 NTFS 이외의 파일 시스템으로 포맷한 경우 명령은 실패하고 파티션은 변경되지 않습니다.</p></li></ul>|
| <p>**size=** <em>size</em></p> | <p>현재 파티션에 추가할 공간 크기(MB, 메가바이트)입니다. 크기를 지정하지 않는 경우 디스크가 확장되어 인접한 할당되지 않은 공간을 모두 차지합니다.</p> |

## <a name="additional-considerations"></a>추가 고려 사항

-   디스크에 부팅 또는 시스템 파티션이 없는 경우 볼륨을 비부팅 또는 비시스템 디스크로 확장할 수 있지만 디스크는 동적 디스크로 변환됩니다(업그레이드될 수 있는 경우).

## <a name="see-also"></a>관련 항목

-   [명령줄 구문 표기법](https://technet.microsoft.com/library/cc742449(v=ws.11).aspx)
