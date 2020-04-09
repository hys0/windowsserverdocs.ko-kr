---
title: 협상, 세션 설정 및 트리 연결 오류
description: Negotiate, Session 설정 및 트리 연결 실패 문제를 해결 하는 방법을 소개 합니다.
author: Deland-Han
manager: dcscontentpm
ms.topic: article
ms.author: delhan
ms.date: 12/25/2019
ms.openlocfilehash: 13124176e530aa7b74d18a38c906bf5297be511e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80815386"
---
# <a name="negotiate-session-setup-and-tree-connect-failures"></a>협상, 세션 설정 및 트리 연결 오류

이 문서에서는 SMB 협상, 세션 설정 및 트리 연결 요청 중에 발생 하는 오류를 해결 하는 방법을 설명 합니다.

## <a name="negotiate-fails"></a>협상 실패

Smb 서버는 smb 클라이언트에서 SMB 협상 요청을 받습니다. 연결 시간이 초과 되 고 60 초 후에 다시 설정 됩니다. 약 200 마이크로초 후 ACK 메시지가 있을 수 있습니다.

이 문제는 일반적으로 바이러스 백신 프로그램으로 인해 발생 합니다.

Windows Server 2008 r 2를 사용 하는 경우이 문제에 대 한 핫픽스가 있습니다. SMB 클라이언트와 SMB 서버가 최신 상태 인지 확인 합니다.

## <a name="session-setup-fails"></a>세션 설정 실패

Smb 서버가 smb 클라이언트의 설정 요청을\_SMB 세션을 수신 하지만 응답 하지 못했습니다.

서버의 FQDN (정규화 된 도메인 이름) 또는 NetBIOS (Network Basic Input/Output System) 이름이 UNC (범용 명명 규칙) 경로에서 ' sed ' 인 경우 Windows는 인증에 Kerberos를 사용 합니다.

Negotiate 응답 후 서버에 대 한 CIFS (Common Internet File System) SPN (서비스 사용자 이름)에 대 한 Kerberos 티켓을 가져오려고 시도 합니다. SMB 클라이언트가 토큰을 획득 하는 경우 TCP 포트 88의 Kerberos 트래픽을 확인 하 여 Kerberos 오류가 없는지 확인 합니다.

> [!NOTE]
> Kerberos 사전 인증 중에 발생 하는 오류는 정상입니다. Kerberos 사전 인증 후에 발생 하는 오류 (인증이 작동 하지 않는 인스턴스)는 SMB 문제를 일으킨 오류입니다.

또한 다음과 같이 확인 합니다.

- SMB 세션에서 보안 blob을 확인 하 여 올바른 자격 증명이 전송 되었는지 확인 하는 설정 요청\_합니다.

- SMB 서버 이름 강화를 사용 하지 않도록 설정 합니다 (**SmbServerNameHardeningLevel = 0**).

- CNAME DNS 레코드를 통해 액세스할 때 SMB 서버에 SPN이 있는지 확인 합니다.

- SMB 서명이 작동 하는지 확인 합니다. 이는 이전 타사 장치에서 특히 중요 합니다.

## <a name="tree-connect-fails"></a>트리 연결 실패

사용자 계정 자격 증명에 폴더에 대 한 공유 및 NT 파일 시스템 (NTFS) 권한이 모두 있는지 확인 합니다.

[연결 요청\_SMB2 트리를 수신](https://docs.microsoft.com/openspecs/windows_protocols/ms-smb2/652e0c14-5014-4470-999d-b174d7b2da87)하는 3.3.5.7에서 일반적인 트리 연결 오류의 원인을 찾을 수 있습니다. 다음은 두 가지 일반적인 상태 코드에 대 한 해결 방법입니다.

\[상태가 잘못 된\_네트워크\_이름\_\]

공유가 서버에 있고 SMB 클라이언트 요청에서 철자가 정확한 지 확인 합니다.

\[상태\_액세스\_거부\]

공유에 사용 되는 디스크 및 폴더가 있고 액세스할 수 있는지 확인 하십시오.

SMBv3 이상을 사용 하는 경우 서버와 공유에 암호화가 필요 하지만 클라이언트가 암호화를 지원 하지 않는지 확인 합니다. 이렇게 하려면 다음 작업을 수행 합니다.

- 다음 명령을 실행 하 여 서버를 확인 합니다.

  ```PowerShell
  Get-SmbServerConfiguration | select Encrypt*
  ```

  EncryptData 및 RejectUnencryptedAccess가 true 이면 서버에서 암호화가 필요 합니다.

- 다음 명령을 실행 하 여 공유를 확인 합니다.

  ```PowerShell
  Get-SmbShare | select name, EncryptData  
  ```

  공유에서 EncryptData가 true이 고 서버에서 RejectUnencryptedAccess가 true 이면 공유에 암호화가 필요 합니다.

문제를 해결 하기 위해 다음 지침을 따르세요.

- Windows 8, Windows Server 2012 및 이후 버전의 Windows에서는 클라이언트 쪽 암호화 (SMBv3 이상)를 지원 합니다.

- Windows 7, Windows Server 2008 R2 및 이전 버전의 Windows에서는 클라이언트 쪽 암호화를 지원 하지 않습니다.

- Samba 및 타사 장치는 암호화를 지원 하지 않을 수 있습니다. 자세한 내용은 제품 설명서를 참조 해야 할 수 있습니다.

## <a name="references"></a>참조

자세한 내용은 다음 문서를 참조 하세요.

[SMB2 NEGOTIATE 요청을 받는 3.3.5.4](https://docs.microsoft.com/openspecs/windows_protocols/ms-smb2/b39f253e-4963-40df-8dff-2f9040ebbeb1)

[3.3.5.5를 수신 하는 SMB2 세션\_설정 요청](https://docs.microsoft.com/openspecs/windows_protocols/ms-smb2/e545352b-9f2b-4c5e-9350-db46e4f6755e)

[연결 요청\_SMB2 트리를 수신 하는 3.3.5.7](https://docs.microsoft.com/openspecs/windows_protocols/ms-smb2/652e0c14-5014-4470-999d-b174d7b2da87?redirectedfrom=MSDN)
