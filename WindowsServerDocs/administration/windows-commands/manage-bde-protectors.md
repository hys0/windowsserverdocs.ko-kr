---
title: manage-bde 보호기
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1f9b22c5-cc93-45df-9165-bedee94998da
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 08/06/2018
ms.openlocfilehash: c248a5d7c6a25ccb6fa2917358223fd255a3c600
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820633"
---
# <a name="manage-bde-protectors"></a>manage-bde: 보호기

> 적용 대상: Windows Server(반기 채널), Windows Server 2016

BitLocker 암호화 키에 사용 되는 보호 방법을 관리 합니다.
## <a name="syntax"></a>구문
```
manage-bde -protectors [{-get|-add|-delete|-disable|-enable|-adbackup|-aadbackup}] <Drive> [-computername <Name>] [{-?|/?}] [{-help|-h}]
```
#### <a name="parameters"></a>매개 변수

|   매개 변수   |                                                                                                                                                                                           설명                                                                                                                                                                                            |
|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     -가져오기      |                                                                                                                                            드라이브에서 사용 하도록 설정 하는 모든 키 보호 방법을 표시 하 고 해당 형식 및 ID (식별자)를 제공 합니다.                                                                                                                                             |
|     -추가      |                                                                                                                                   추가 [매개 변수 추가](manage-bde-protectors.md#BKMK_addprotectors)를 사용 하 여 지정 된 키 보호 방법을 추가 합니다.                                                                                                                                    |
|    -삭제    | BitLocker에서 사용 되는 키 보호 방법을 삭제 합니다. 모든 키 보호기 하지 않는 한 드라이브에서 제거 됩니다 선택적 [-매개 변수를 삭제](manage-bde-protectors.md#BKMK_deleteprotectors) 삭제 하려면 보호 기능을 지정 하는 데 사용 됩니다. 드라이브에 마지막 보호기 삭제 될 때 BitLocker 보호 드라이브의 데이터에 액세스할 수 없는지 확인 손실 실수로 비활성화 됩니다. |
|   -사용 하지 않도록 설정    |                      사용자는 누구나 하 여 암호화 키 사용 가능한 드라이브에 보안이 설정 되지 않은 암호화 된 데이터에 액세스 하는 보호를 사용 하지 않습니다. 없는 키 보호기 제거 됩니다. 보호 하지 않는 한 Windows 부팅 될 다음에 다시 시작 될 것임 선택적 [-매개 변수를 사용 하지 않도록 설정](manage-bde-protectors.md#BKMK_disableprot) 다시 부팅 횟수를 지정 하는 데 사용 됩니다.                       |
|    -사용 하도록 설정    |                                                                                                                             드라이브에서 보안 되지 않은 암호화 키를 제거 하 여 보호를 사용 합니다. 모든 구성 된 키 보호기는 드라이브에 적용 됩니다.                                                                                                                             |
|   -adbackup   |                                                                          Active Directory 도메인 서비스 (AD DS)에 지정 된 드라이브에 대 한 모든 복구 정보를 백업 합니다. 단일 복구 키만 AD DS를 백업 하려면 추가 **-id** 매개 변수를 백업 하는 특정 복구 키 ID를 지정 합니다.                                                                           |
|  -aadbackup   |                                                                            Azure Active Directory (Azure Ad)에 지정 된 드라이브에 대 한 모든 복구 정보를 백업 합니다. Azure AD에 단일 복구 키만 백업 하려면 **-id** 매개 변수를 추가 하 고 백업할 특정 복구 키의 id를 지정 합니다.                                                                             |
|    <Drive>    |                                                                                                                                                                          드라이브 문자를 뒤에 콜론을 나타냅니다.                                                                                                                                                                          |
| -computername |                                                                                                              다른 컴퓨터에서 BitLocker 보호를 수정 하는 데 manage-bde.exe를 사용 하도록 지정 합니다. 사용할 수도 있습니다 **-cn** 이 명령의 축약된 버전으로 합니다.                                                                                                              |
|    <Name>     |                                                                                                                 BitLocker 보호를 수정할 수 있는 컴퓨터의 이름을 나타냅니다. 사용 가능한 값에는 컴퓨터의 NetBIOS 이름 및 컴퓨터의 IP 주소 포함 됩니다.                                                                                                                  |
|   -? 또는 /?    |                                                                                                                                                                            명령 프롬프트에 대 한 간단한 도움말을 표시 합니다.                                                                                                                                                                            |
|  -help 또는-h  |                                                                                                                                                                          명령 프롬프트에서 전체 도움말을 표시 합니다.                                                                                                                                                                           |

### <a name="-add-syntax-and-parameters"></a><a name=BKMK_addprotectors></a>-구문 및 매개 변수를 추가 합니다.
```
manage-bde  -protectors  -add [<Drive>] [-forceupgrade] [-recoverypassword <NumericalPassword>] [-recoverykey <pathToExternalKeydirectory>]
[-startupkey <pathToExternalKeydirectory>] [-certificate {-cf <pathToCertificateFile>|-ct <CertificateThumbprint>}] [-tpm] [-tpmandpin]
[-tpmandstartupkey <pathToExternalKeydirectory>] [-tpmandpinandstartupkey <pathToExternalKeydirectory>] [-password][-adaccountorgroup <securityidentifier> [-computername <Name>]
[{-?|/?}] [{-help|-h}]
```

|          매개 변수           |                                                                                                                                                                                   설명                                                                                                                                                                                   |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|           <Drive>            |                                                                                                                                                                 드라이브 문자를 뒤에 콜론을 나타냅니다.                                                                                                                                                                  |
|      -recoverypassword       |                                                                                                                                    숫자 암호 보호기를 추가 합니다. 사용할 수도 있습니다 **-rp** 이 명령의 축약된 버전으로 합니다.                                                                                                                                     |
|     <NumericalPassword>      |                                                                                                                                                                        복구 암호를 나타냅니다.                                                                                                                                                                        |
|         -recoverykey         |                                                                                                                                복구를 위한 외부 키 보호기를 추가 합니다. 사용할 수도 있습니다 **-날짜별** 이 명령의 축약된 버전으로 합니다.                                                                                                                                 |
| <pathToExternalKeydirectory> |                                                                                                                                                               복구 키에 디렉터리 경로를 나타냅니다.                                                                                                                                                                |
|         -시작          |                                                                                                                                 시작에 대 한 외부 키 보호기를 추가 합니다. 사용할 수도 있습니다 **-sk** 이 명령의 축약된 버전으로 합니다.                                                                                                                                 |
| <pathToExternalKeydirectory> |                                                                                                                                                                시작 키에 디렉터리 경로를 나타냅니다.                                                                                                                                                                |
|         -인증서         |                                                                                                                               데이터 드라이브에 대 한 공개 키 보호기를 추가 합니다. 사용할 수도 있습니다 **-cert** 이 명령의 축약된 버전으로 합니다.                                                                                                                               |
|             -cf              |                                                                                                                                              인증서 파일을 공개 키 인증서를 제공 하는 것을 지정 합니다.                                                                                                                                              |
|   <pathToCertificateFile>    |                                                                                                                                                             인증서 파일의 디렉터리 경로를 나타냅니다.                                                                                                                                                              |
|             -ct              |                                                                                                                                           공개 키 인증서를 식별 하는 인증서 지문이 사용될지를 지정 합니다.                                                                                                                                           |
|   <CertificateThumbprint>    |                                                       사용 하려는 인증서의 지문 속성의 값을 지정 합니다. 예를 들어 인증서 지문 값 a9 09 50 2d d8 2a e4 14 33 e6 f8 38 86 b0 0d 42 77 a3 2a 7b를 a909502dd82ae41433e6f83886b00d4277a32a7b로 지정 해야 합니다.                                                        |
|          -tpmandpin          |                                                                                           운영 체제 드라이브에 대 한 신뢰할 수 있는 플랫폼 모듈 (TPM) 및 개인 식별 번호 (PIN) 보호기를 추가 합니다. 사용할 수도 있습니다 **-tp** 이 명령의 축약된 버전으로 합니다.                                                                                           |
|      -tpmandstartupkey       |                                                                                                                    운영 체제 드라이브에 대 한 TPM 및 시작 키 보호기를 추가 합니다. 사용할 수도 있습니다 **-tsk** 이 명령의 축약된 버전으로 합니다.                                                                                                                    |
|   -tpmandpinandstartupkey    |                                                                                                                운영 체제 드라이브에 대 한 TPM, PIN 및 시작 키 보호기를 추가 합니다. 사용할 수도 있습니다 **-tpsk** 이 명령의 축약된 버전으로 합니다.                                                                                                                 |
|          -암호           |                                                                                                                              데이터 드라이브에 대 한 암호 키 보호기를 추가 합니다. 사용할 수도 있습니다 **-pw** 이 명령의 축약된 버전으로 합니다.                                                                                                                              |
|      -adaccountorgroup       | 볼륨에 대 한 SID (보안 식별자) 기반 id 보호기를 추가 합니다.  사용할 수도 있습니다 **-sid** 이 명령의 축약된 버전으로 합니다. **중요:** 기본적으로 WMI 또는 manage-bde를 사용 하 여 ADAccountOrGroup 보호기를 원격으로 추가할 수 없습니다.  배포에이 보호기를 원격으로 추가 하는 기능이 필요한 경우 제한 된 위임을 사용 하도록 설정 해야 합니다. |
|        -computername         |                                                                                                       Manage-bde를 사용 하 여 다른 컴퓨터에서 BitLocker 보호를 수정 하도록 지정 합니다. 사용할 수도 있습니다 **-cn** 이 명령의 축약된 버전으로 합니다.                                                                                                       |
|            <Name>            |                                                                                                         BitLocker 보호를 수정할 수 있는 컴퓨터의 이름을 나타냅니다. 사용 가능한 값에는 컴퓨터의 NetBIOS 이름 및 컴퓨터의 IP 주소 포함 됩니다.                                                                                                         |

### <a name="-delete-syntax-and-parameters"></a><a name=BKMK_deleteprotectors></a>-구문 및 매개 변수를 삭제 합니다.
```
manage-bde  -protectors  -delete <Drive> [-type {recoverypassword|externalkey|certificate|tpm|tpmandstartupkey|tpmandpin|tpmandpinandstartupkey|Password|Identity}]
[-id <KeyProtectorID>] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

|       매개 변수        |                                                                              설명                                                                               |
|------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|        <Drive>         |                                                             드라이브 문자를 뒤에 콜론을 나타냅니다.                                                             |
|         -유형          |                               삭제할 키 보호기를 식별 합니다. 사용할 수도 있습니다 **-t** 이 명령의 축약된 버전으로 합니다.                               |
|    recoverypassword    |                                                 모든 복구 암호 키 보호기를 삭제 해야 함을 지정 합니다.                                                 |
|      externalkey       |                                        드라이브와 연결 된 모든 외부 키 보호기를 삭제 해야 함을 지정 합니다.                                         |
|      인증서(certificate)       |                                       드라이브와 연결 된 모든 인증서 키 보호기를 삭제 해야 함을 지정 합니다.                                       |
|          tpm           |                                        드라이브와 연결 된 모든 TPM 전용 키 보호기를 삭제 해야 함을 지정 합니다.                                         |
|    tpmandstartupkey    |                                드라이브와 연결 된 모든 TPM 및 시작 키 기반 키 보호기를 삭제 해야 함을 지정 합니다.                                |
|       tpmandpin        |                                    드라이브와 연결 된 모든 TPM 및 PIN 기반 키 보호기를 삭제 해야 함을 지정 합니다.                                    |
| tpmandpinandstartupkey |                             드라이브와 연결 된 모든 TPM, PIN 및 시작 키 보호기를 삭제 해야 함을 지정 합니다.                             |
|        password        |                                        드라이브와 연결 된 모든 암호 키 보호기를 삭제 해야 함을 지정 합니다.                                         |
|        identity        |                                        드라이브와 연결 된 모든 identity 키 보호기를 삭제 해야 함을 지정 합니다.                                         |
|          -id           |                키 식별자를 사용 하 여 삭제할 키 보호기를 식별 합니다. 이 매개 변수는 다른 옵션에는 **-형식** 매개 변수입니다.                 |
|    <KeyProtectorID>    |        삭제 하는 드라이브에는 개별 키 보호기를 식별 합니다. Id 키 보호기를 사용 하 여 표시할 수는 **관리 bde-보호기-가져오기** 명령입니다.         |
|     -computername      | 다른 컴퓨터에서 BitLocker 보호를 수정 하는 데 manage-bde.exe를 사용 하도록 지정 합니다. 사용할 수도 있습니다 **-cn** 이 명령의 축약된 버전으로 합니다. |
|         <Name>         |    BitLocker 보호를 수정할 수 있는 컴퓨터의 이름을 나타냅니다. 사용 가능한 값에는 컴퓨터의 NetBIOS 이름 및 컴퓨터의 IP 주소 포함 됩니다.     |
|        -? 또는 /?        |                                                               명령 프롬프트에 대 한 간단한 도움말을 표시 합니다.                                                               |
|      -help 또는-h       |                                                             명령 프롬프트에서 전체 도움말을 표시 합니다.                                                              |

### <a name="-disable-syntax-and-parameters"></a><a name=BKMK_disableprot></a>-구문 및 매개 변수를 사용 하지 않도록 설정
```
manage-bde  -protectors  -disable <Drive> [-RebootCount <integer 0 - 15>] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

|   매개 변수   |                                                                                                                                                                                                                   설명                                                                                                                                                                                                                    |
|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    <Drive>    |                                                                                                                                                                                                  드라이브 문자를 뒤에 콜론을 나타냅니다.                                                                                                                                                                                                  |
|  RebootCount  | Windows 8부터은 운영 체제 볼륨의 보호가 일시 중단 되었으며 Windows가 다시 시작 된 후 RebootCount 매개 변수에 지정 된 횟수 만큼 일시 중단 되도록 지정 합니다. 보호를 무기한으로 일시 중단 하려면 0을 지정 합니다. 이 매개 변수에서 BitLocker 보호는 자동으로 지정 하지 않으면 Windows를 다시 시작할 때 다시 시작 합니다. 사용할 수도 있습니다 **-rc** 이 명령의 축약된 버전으로 합니다. |
| -computername |                                                                                                                                      다른 컴퓨터에서 BitLocker 보호를 수정 하는 데 manage-bde.exe를 사용 하도록 지정 합니다. 사용할 수도 있습니다 **-cn** 이 명령의 축약된 버전으로 합니다.                                                                                                                                      |
|    <Name>     |                                                                                                                                         BitLocker 보호를 수정할 수 있는 컴퓨터의 이름을 나타냅니다. 사용 가능한 값에는 컴퓨터의 NetBIOS 이름 및 컴퓨터의 IP 주소 포함 됩니다.                                                                                                                                          |
|   -? 또는 /?    |                                                                                                                                                                                                    명령 프롬프트에 대 한 간단한 도움말을 표시 합니다.                                                                                                                                                                                                    |
|  -help 또는-h  |                                                                                                                                                                                                  명령 프롬프트에서 전체 도움말을 표시 합니다.                                                                                                                                                                                                   |

## <a name="examples"></a>예
**-보호기** 명령을 사용 하 여 인증서 파일에 의해 식별 되는 인증서 키 보호기를 E 드라이브에 추가 하는 방법을 보여 줍니다.
```
manage-bde  -protectors  -add E: -certificate  -cf c:\File Folder\Filename.cer
```
**-보호기** 명령을 사용 하 여 도메인 및 사용자 이름으로 식별 되는 **adaccountorgroup** 키 보호기를 E 드라이브에 추가 하는 방법을 보여 줍니다.
```
manage-bde  -protectors  -add E: -sid DOMAIN\user
```
컴퓨터를 3 번 다시 부팅할 때까지 보호를 사용 하지 않도록 설정 하는 **보호기** 명령을 사용 하는 방법을 설명 합니다.
```
manage-bde  -protectors  -disable C: -rc 3
```
**-보호기** 명령을 사용 하 여 C 드라이브의 모든 TPM 및 시작 키 기반 키 보호기를 삭제 하는 방법을 설명 합니다.
```
manage-bde  -protectors -delete C: -type tpmandstartupkey
```
**-보호기** 명령을 사용 하 여 C 드라이브에 대 한 모든 복구 정보를 AD DS 백업 하는 방법을 보여 줍니다.
```
manage-bde  -protectors  -adbackup C:
```
## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md)
-   [manage-bde](manage-bde.md)
