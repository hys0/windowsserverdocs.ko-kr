---
title: 탑재 지점 폴더 경로를 드라이브에 할당
description: 이 문서에서는 (드라이브 문자가 아닌) 탑재 지점 폴더 경로를 드라이브에 할당하는 방법을 설명합니다.
keywords: 가상화, 보안, 맬웨어
ms.date: 06/07/2019
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 1255eadd50adb0eaaf44774e150d69f6dad8adae
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386054"
---
# <a name="assign-a-mount-point-folder-path-to-a-drive"></a>탑재 지점 폴더 경로를 드라이브에 할당

> **적용 대상:** Windows 10, Windows 8.1, Windows Server(반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

디스크 관리를 사용하여 (드라이브 문자가 아닌) 탑재 지점 폴더 경로를 드라이브에 할당할 수 있습니다. 탑재 지점 폴더 경로는 기본 또는 동적 NTFS 볼륨의 빈 폴더만 가능합니다.

## <a name="assigning-a-mount-point-folder-path-to-a-drive"></a>탑재 지점 폴더 경로를 드라이브에 할당

> [!NOTE]
> **Backup Operators** 또는 **Administrators** 그룹의 구성원이어야 이 단계를 완료할 수 있습니다.

#### <a name="to-assign-a-mount-point-folder-path-to-a-drive-by-using-the-windows-interface"></a>Windows 인터페이스를 사용하여 탑재 지점 폴더 경로를 드라이브에 할당

1.  디스크 관리자에서 탑재 지점 폴더 경로를 할당하고자 하는 파티션 또는 볼륨을 마우스 오른쪽 단추로 클릭합니다. 
2. **드라이브 문자 및 경로 변경**을 클릭한 다음, **추가**를 클릭합니다. 
3. **다음의 빈 NTFS 폴더에 탑재**를 클릭합니다.
4. NTFS 볼륨의 빈 폴더 경로를 입력하거나 **찾아보기**를 클릭하여 찾습니다.

#### <a name="to-assign-a-mount-point-folder-path-to-a-drive-using-a-command-line"></a>명령줄을 사용하여 탑재 지점 폴더 경로 할당

1.  명령 프롬프트를 열고 `diskpart`를 입력합니다.

2.  **DISKPART** 프롬프트에서 `list volume`을 입력하고 경로를 할당하고자 하는 볼륨 번호를 메모합니다.

3.  **DISKPART** 프롬프트에서 `select volume <volumenumber>`를 입력합니다. 

4. 경로를 할당하고자 하는 단순 볼륨 *volumenumber*를 선택합니다.

5.  **DISKPART** 프롬프트에서 `assign [mount=<path>]`를 입력합니다.

#### <a name="to-remove-a-mount-point-folder-path-to-a-drive"></a>탑재 지점 폴더 경로를 드라이브에서 제거

-   탑재 지점 폴더 경로를 제거하려면 경로를 클릭한 다음, **제거**를 클릭합니다.

| 값 | 설명 |
| --- | --- |
| **list volume** | 모든 디스크에 기본 및 동적 볼륨 목록을 표시합니다. |
| **select volume**        | 볼륨 번호가 <em>volumenumber</em>인 지정된 볼륨을 선택하고 포커스를 설정합니다. 지정된 볼륨이 없는 경우 **select** 명령이 포커스가 설정된 현재 볼륨 목록을 표시합니다. 번호, 드라이브 문자 또는 탑재 지점 폴더 경로로 볼륨을 지정할 수 있습니다. 기본 디스크에서 볼륨을 선택하면 해당 파티션에도 포커스를 설정합니다.|
| **assign** | <ul><li> 드라이브 문자 또는 탑재 지점 폴더 경로를 포커스가 설정된 볼륨에 할당합니다. 지정된 드라이브 문자 또는 탑재 지점 폴더 경로가 없는 경우 다음 이용 가능한 드라이브 문자가 할당됩니다. 드라이브 문자 또는 탑재 지점 폴더 경로가 이미 사용 중인 경우 오류가 발생합니다.</li>  <li>**assign** 명령을 사용하면 이동식 드라이브에 연결된 드라이브 문자를 변경할 수 있습니다.</li> <li> 부팅 볼륨 또는 페이징 파일을 포함하는 볼륨에 드라이브 문자를 할당할 수 없습니다. 또한 OEM(Original Equipment Manufacturer) 파티션, EFI 시스템 파티션 또는 기본 데이터 파티션을 제외한 모든 GPT 파티션에 드라이브 문자를 할당할 수 없습니다.</li></ul> |
| **mount=** <em>path</em> | 탑재된 드라이브가 상주할 빈 채로 존재하는 NTFS 폴더를 지정합니다.  |

## <a name="additional-considerations"></a>추가 고려 사항

-   로컬 또는 원격 컴퓨터를 관리하는 경우 컴퓨터에서 NTFS 폴더를 찾아볼 수 있습니다.
-   탑재 지점 폴더 경로는 기본 또는 동적 NTFS 볼륨의 빈 폴더만 가능합니다.
-   탑재 지점 폴더 경로를 수정하려면 경로를 제거한 다음, 새 위치를 사용하여 새 폴더 경로를 만듭니다. 탑재 지점 폴더 경로를 직접 수정할 수 없습니다.
-   탑재 지점 폴더 경로를 드라이브에 할당할 때 **이벤트 뷰어**를 사용하여 탑재 지점 폴더 경로 오류를 나타내는 클러스터 서비스 오류 또는 경고에 대한 시스템 로그를 확인합니다. 이러한 오류는 **소스** 열에서 **ClusSvc**로, **범주** 열에서 **실제 디스크 리소스**로 나열됩니다.
-   [mountvol](https://go.microsoft.com/fwlink/?linkid=64111) 명령을 사용하여 탑재된 드라이브를 만들 수도 있습니다.

## <a name="see-also"></a>참고 항목
-   [명령줄 구문 표기법](https://technet.microsoft.com/library/cc742449(v=ws.11).aspx)


