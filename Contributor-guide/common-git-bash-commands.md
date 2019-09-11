---
title: GitHub와 함께 사용 하기 위한 일반적인 Git Bash 명령
description: GitHub를 사용할 때 Git Bash에서 가장 자주 사용 되는 명령의 목록입니다.
author: eross-msft
ms.author: lizross
ms.date: 05/06/2019
ms.openlocfilehash: 4ce5d4d8ce382e9ba421c20595715ec473cca241
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70865000"
---
# <a name="common-git-bash-commands"></a>일반적인 Git Bash 명령

이러한 명령 중 일부는 콘텐츠 만들기 및 편집 프로세스에서 사용 하는 시기에 따라 Git Bash에서 가장 많이 사용 되는 명령입니다.

## <a name="master-branch-related"></a>마스터 분기 관련

항상 master를 모든 새 분기의 기본으로 사용 해야 합니다.

| 명령 | 설명 |
|---------|-------------|
| `git checkout master` | 다른 분기의 마스터로 전환 |
| `git pull upstream master` | 프로덕션 리포지토리에서 master의 로컬 복사본을 업데이트 합니다. |

## <a name="branch-related"></a>분기 관련

| 명령 | 설명 |
|---------|-------------|
| `git branch` | 기존 분기 보기 |
| `git checkout -B <name-of-branch>` | 새 분기 만들기 |
| `git checkout <name-of-branch>` | 다른 분기로 변경 |
| `git status` | 분기에서 일어나는 일 확인 |
| `git branch -D <name-of-branch>` | 기존 분기를 삭제 합니다. |

## <a name="check-in-related-done-as-a-group-in-order"></a>체크 인 관련 (순서 대로 그룹으로 수행 됨)

| 명령 | 설명 |
|---------|-------------|
| `git add --all` | 작업을 저장 한 후 분기에 추가 합니다. |
| `git commit -m “public comment, including quotes”` | 분기에 대 한 변경 내용 커밋 |
| `git pull upstream master` | 프로덕션 리포지토리에서 master의 로컬 복사본을 업데이트 합니다. |
| `git push origin <name-of-branch>` | 로컬 분기의 원격 버전으로 푸시 |