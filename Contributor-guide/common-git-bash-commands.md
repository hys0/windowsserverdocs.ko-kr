---
title: GitHub 사용에 대 한 일반적인 Git Bash 명령
description: 목록 Git bash를 GitHub를 사용 하 여 작업할 때 가장 자주 사용 되는 명령의 일부입니다.
author: eross-msft
ms.author: lizross
ms.date: 05/06/2019
ms.openlocfilehash: 210acaf2b7911892bcfd81b6bbe1975f141308a1
ms.sourcegitcommit: 7e54a1bcd31cd2c6b18fd1f21b03f5cfb6165bf3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65461695"
---
# <a name="common-git-bash-commands"></a>일반적인 Git Bash 명령

Git Bash, 콘텐츠 생성에 사용 됩니다 하는 경우에 따라 및 편집 과정에서에서 대부분 사용 되는 명령의 일부입니다.

## <a name="master-branch-related"></a>마스터 분기와 관련 된

항상 새 분기에 대 한 기반으로 마스터를 사용 해야 합니다.

| Command | 설명 |
|---------|-------------|
| `git checkout master` | 다른 분기에서 master로 전환 |
| `git pull upstream master` | 프로덕션 리포지토리에서 마스터의 로컬 복사본을 업데이트 |

## <a name="branch-related"></a>분기 관련

| Command | 설명 |
|---------|-------------|
| `git branch` | 기존 분기를 참조 하세요. |
| `git checkout -B <name-of-branch>` | 새 분기 만들기 |
| `git checkout <name-of-branch>` | 다른 분기로 변경 |
| `git status` | 어떤 일이 일어나는지 분기 확인 |
| `git branch -D <name-of-branch>` | (있도록에 모르는) 기존 분기를 삭제 합니다. |

## <a name="check-in-related-done-as-a-group-in-order"></a>검사에서 관련 (순서 대로 그룹으로 수행)

| Command | 설명 |
|---------|-------------|
| `git add --all` | 작업을 저장 한 후에 분기 추가 |
| `git commit -m “public comment, including quotes”` | 분기에 변경 내용을 적용합니다 |
| `git pull upstream master` | 프로덕션 리포지토리에서 마스터의 로컬 복사본을 업데이트 |
| `git push origin <name-of-branch>` | 로컬 분기의 원격 버전에 푸시 |