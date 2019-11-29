---
ms.date: 01/07/2019
contributor: damaerteMSFT
author: maertendMSFT
keywords: OpenSSH, SSH, Win32-OpenSSH
title: Windows의 OpenSSH
ms.product: w10
ms.openlocfilehash: c6563fbe4fe69acad4d295a3f7fe166e92d38444
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280056"
---
# <a name="openssh-in-windows"></a>Windows의 OpenSSH

OpenSSH는 Linux 및 다른 비 Windows 관리자가 원격 시스템의 플랫폼 간 관리를 위해 사용하는 SSH(Secure Shell) 도구의 오픈 소스 버전입니다. OpenSSH는 2018년 가을부터 Windows에 추가되었으며 Windows 10 및 Windows Server 2019에 포함되어 있습니다. 

SSH는 사용자가 작업 중인 시스템이 클라이언트이고, 관리되고 있는 원격 시스템이 서버인 클라이언트-서버 구조를 기반으로 합니다. OpenSSH에는 다음을 포함하여, 원격 시스템 관리에 대해 직관적인 보안 접근 방식을 제공하도록 디자인된 다양한 구성 요소 및 도구가 포함되어 있습니다.

* sshd.exe는 원격으로 관리되는 시스템에서 실행되어야 하는 SSH 서버 구성 요소입니다. 
* ssh.exe는 사용자의 로컬 시스템에서 실행되는 SSH 클라이언트 구성 요소입니다.
* ssh-keygen.exe는 SSH를 위한 인증 키를 생성, 관리 및 변환합니다. 
* ssh-agent.exe는 공개 키 인증을 위해 사용되는 프라이빗 키를 저장합니다.
* ssh-add.exe는 서버에서 허용되는 목록에 프라이빗 키를 추가합니다.
* ssh-keyscan.exe는 여러 호스트로부터 공개 SSH 호스트 키 수집을 돕습니다.
* sftp.exe는 보안 파일 전송 프로토콜을 제공하고 SSH로 실행되는 서비스입니다.
* scp.exe는 SSH로 실행되는 파일 복사 유틸리티입니다.

이 섹션의 설명은 설치, Windows 관련 구성 및 사용 사례를 포함하여 Windows에서의 OpenSSH 사용 방법을 집중적으로 설명합니다. 포함된 항목은 다음과 같습니다.
* Windows Server 2019 및 Windows 10을위 한 OpenSSH 설치 및 제거

일반적인 OpenSSH 기능에 대한 자세한 내용은 [OpenSSH.com](https://www.openssh.com/manual.html)에서 온라인으로 제공됩니다. 

마스터 [OpenSSH 오픈 소스 프로젝트](https://www.openssh.com)는 OpenBSD 프로젝트에서 개발자에 의해 관리됩니다. 이 프로젝트의 Microsoft 포크는 [GitHub](https://github.com/PowerShell/openssh-portable)에 있습니다.
Windows OpenSSH에 대한 의견이 있으면 저희 [OpenSSH GitHub 리포지토리](https://github.com/PowerShell/openssh-portable)에서 GitHub 문제를 생성하여 알려주시기 바랍니다. 
