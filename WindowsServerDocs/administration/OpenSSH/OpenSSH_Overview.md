---
ms.date: 01/07/2019
contributor: damaerteMSFT
author: maertendMSFT
keywords: OpenSSH SSH, Win32-OpenSSH
title: Windows에서 OpenSSH
ms.product: w10
ms.openlocfilehash: 68ced1ff133495d7658e486e7e72321e18857b21
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59843364"
---
# <a name="openssh-in-windows"></a>Windows에서 OpenSSH

OpenSSH는 Linux의 관리자 및 다른 비-Windows 사용 되는 원격 시스템의 플랫폼 간 관리에 대 한 SSH (보안 셸) 도구의 오픈 소스 버전입니다. OpenSSH가 2018 년을 기준으로 Windows에 추가 되었습니다 및 Windows 10 및 Windows Server 2019에 포함 됩니다. 

SSH는 여기서은 클라이언트 시스템에서 사용자가 작업 하 고 관리 되는 원격 시스템 서버는 클라이언트-서버 아키텍처를 기반으로 합니다. OpenSSH는 다양 한 구성 요소와 도구가 원격 시스템 관리에 안전 하 고 간단한 접근 방식을 제공 하도록 설계를 포함 합니다. 포함 하 여:

* 원격으로 관리 되는 시스템에서 실행 해야 하는 SSH 서버 구성 요소인 sshd.exe 
* 사용자의 로컬 시스템에서 실행 되는 SSH 클라이언트 구성 요소인 ssh.exe
* ssh-keygen.exe 생성, 관리 및 SSH에 대 한 인증 키를 변환 합니다. 
* ssh-agent.exe 공개 키 인증에 사용 되는 개인 키를 저장 합니다.
* ssh-add.exe 서버에서 허용 목록에 개인 키 추가
* ssh-keyscan.exe 보조 기능에서 호스트의 공용 SSH 호스트 키를 수집 합니다.
* 보안 파일 전송 프로토콜을 제공 하 고 SSH를 통해 실행 하는 서비스란 sftp.exe
* scp.exe는 SSH에서 실행 되는 파일 복사 유틸리티

이 섹션의 설명서를 설치 및 Windows 관련 구성 및 사용 사례를 포함 하 여 Windows에서 OpenSSH 사용 방법에 중점을 둡니다. 항목은 다음과 같습니다.
* 설치 하 고 OpenSSH 2019 Windows Server 및 Windows 10에 대 한 제거

OpenSSH의 일반적인 기능에 대 한 자세한 추가 설명서는 온라인으로 제공 [OpenSSH.com](https://www.openssh.com/manual.html)합니다. 

마스터 [OpenSSH 오픈 소스 프로젝트](https://www.openssh.com) OpenBSD 프로젝트는 개발자에 의해 관리 됩니다. 에이 프로젝트의 Microsoft 포크 [Github](https://github.com/PowerShell/openssh-portable)합니다.
Windows OpenSSH에 대 한 피드백 반가운 일 이며에서 Github 문제를 생성 하 여 제공할 수 있습니다 우리의 [OpenSSH Github 리포지토리](https://github.com/PowerShell/openssh-portable)합니다. 
