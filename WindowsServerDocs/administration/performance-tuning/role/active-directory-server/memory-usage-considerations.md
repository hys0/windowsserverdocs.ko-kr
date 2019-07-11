---
title: AD DS 성능 튜닝의 메모리 사용 시 고려 사항
description: Windows Server 2012 R2, 2016 및 2019 실행 하는 도메인 컨트롤러에서 Lsass.exe 프로세스 메모리 사용량입니다.
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: v-tea; lindakup
author: Teresa-Motiv
ms.date: 7/3/2019
ms.openlocfilehash: dd33124d7d480f3670fa2781f567eaaa28abbce6
ms.sourcegitcommit: be243a92f09048ca80f85d71555ea6ee3751d712
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67799785"
---
# <a name="memory-usage-considerations-for-ad-ds-performance-tuning"></a>AD DS 성능 튜닝에 대 한 메모리 사용 시 고려 사항

이 문서에서는 몇 가지 기본 사항을 로컬 보안 기관 하위 시스템 서비스 (LSASS, Lsass.exe 프로세스 라고도), LSASS의 구성에 대 한 모범 사례 및 메모리 사용량에 대 한 기대를 설명 합니다. 이 문서에서는 Dc (도메인 컨트롤러)에서 LSASS 성능 및 메모리 사용 분석 지침으로 사용 해야 합니다. 이 문서의 정보를 조정 하 고 서버 및 Dc이이 엔진을 최적화 하기 위해 구성 하는 방법에 대 한 질문이 있는 경우에 유용할 수 있습니다.  

LSASS는 로컬 보안 기관 (LSA) 도메인 인증의 관리 및 Active Directory 관리 하는 일을 담당 합니다. 또한 Active Directory 엔진을 제어 및 LSASS 클라이언트와 서버 모두에 대 한 인증을 처리 합니다. LSASS는 다음 구성 요소를 담당 합니다.  

- 로컬 보안 기관
- NetLogon 서비스
- 보안 계정 관리자 (SAM) 서비스
- LSA 서버 서비스
- SSL(Secure Sockets Layer)
- Kerberos v5 인증 프로토콜
- NTLM 인증 프로토콜
- LSA로 로드 하는 다른 인증 패키지

Active Directory 데이터베이스 서비스 (NTDSAI.dll) Extensible Storage Engine (ESE, ESENT.dll)를 사용 하 여 작동합니다.

DC에서 LSASS 메모리 사용에 대 한 시각적인 다이어그램을 다음과 같습니다.

![LSASS 메모리를 사용 하는 구성 요소 다이어그램](media/domain-controller-lsass-memory-usage.png)  

LSASS는 DC에서 사용 하는 메모리의 양을 Active Directory 사용에 따라 증가 합니다. 데이터를 쿼리할 때 메모리에 캐시 됩니다. 결과적으로,는 Active Directory 데이터베이스 (NTDS.dit) 파일의 크기 보다 큰 메모리 양을 사용 하 여 LSASS 보려는 보통입니다.

다이어그램에서 볼 수 있듯이, LSASS 메모리 사용량 ESE 데이터베이스 버퍼 캐시, ESE 버전 저장소 등의 여러 부분으로 나눌 수 있습니다. 이 문서의 나머지 부분에서는 이러한 각 부분에 대 한 정보를 제공합니다.

## <a name="ese-database-buffer-cache"></a>ESE 데이터베이스 버퍼 캐시  
LSASS 내에서 가장 큰 변수 메모리 사용량 ESE 데이터베이스 버퍼 캐시 됩니다. 캐시의 크기는 전체 데이터베이스의 크기를 1MB 미만에서 까지입니다. 큰 캐시 성능을 개선 하기 때문에 Active Directory (ESENT)에 대 한 데이터베이스 엔진에서는 캐시를 최대한 크게 유지 하려고 합니다. ESE 데이터베이스 버퍼 캐시의 최대 크기는 컴퓨터의 메모리 압력을 사용 하 여 캐시의 크기에 따라 다르지만, *만* 컴퓨터에 설치 하는 실제 RAM으로 제한 합니다. 다른 메모리가 중 없음 인으로 캐시는 Active Directory dit 데이터베이스 파일의 크기를 증가할 수 있습니다. 더 캐시할 수 있는 데이터베이스의 향상 된 DC의 성능이 됩니다.  
  
> [!NOTE]
> 데이터베이스 크기 보다 작으면 사용 가능한 RAM, 64 비트 시스템에서 캐싱 알고리즘 데이터베이스를 작동 하는 방식으로 인해 30 ~ 40% 데이터베이스 캐시 데이터베이스 크기 보다 큰 증가할 수 있습니다.

## <a name="ese-version-store"></a>ESE 버전 저장소

ESE 버전 저장소 (위의 다이어그램에서 빨간색 부분)에 의해 변수 메모리 사용량이 있습니다. 사용 되는 메모리의 양을 이전 버전의 Windows 또는 Windows Server 2019 있는지 여부에 따라 달라 집니다.

- Windows Server 2019 predating Windows Server 버전에서는 ESE 버전은 64 비트 컴퓨터에서 LSASS (Cpu 수)에 따라 메모리의 약 400MB까지 사용할 수는 기본적으로 저장 합니다. 버전 저장소 사용 방법에 대 한 자세한 내용은 다음 ASKDS 블로그 Ryan Ries 게시물을 참조 하세요. [버전 저장소를 호출 하 고을 벗어나는 모든 버킷](https://techcommunity.microsoft.com/t5/Ask-the-Directory-Services-Team/The-Version-Store-Called-and-They-8217-re-All-Out-of-Buckets/ba-p/400415)합니다.

- Windows Server 2019에서이 간단 하 고 ESE 버전 저장소 크기가 400MB의 최소 및 최대 4GB를 사용 하 여 실제 RAM의 10%로 계산 되므로 NTDS 서비스 처음 시작 하는 경우. 이 대 한 유용한 정보 및 버전 저장소 문제 해결, Ryan Ries에서 다른 훌륭한 블로그를 참조 하세요. [심층 분석: Active Directory ESE 버전 저장소 서버 2019 변경](https://techcommunity.microsoft.com/t5/Ask-the-Directory-Services-Team/Deep-Dive-Active-Directory-ESE-Version-Store-Changes-in-Server/ba-p/400510)합니다.

## <a name="other-memory-use"></a>다른 메모리 사용

마지막으로, 코드, 스택, 힙 및 다양 한 고정된 크기 데이터 구조 (예를 들어 스키마 캐시)가 있습니다. LSASS는 메모리의 양을 컴퓨터의 부하에 따라 달라질 수 있습니다. 실행 중인 스레드 수가 늘어나면 메모리 스택 수가 그렇습니다. 평균적으로 LSASS 고정된 이러한 구성 요소에 대 한 메모리의 100MB 300MB를 사용합니다. 더 많은 RAM이 설치 되 면 LSASS RAM 및 가상 메모리를 적게 사용할 수 있습니다.

**제한 또는 도메인 컨트롤러에서 프로그램의 수를 최소화 하거나 적절 한 경우 추가 RAM을 추가 합니다.**

최적의 성능을 위해 LSASS 지정된 DC에서 최대한 많은 RAM을 사용 합니다. LSASS이 다른 프로세스에 대 한 요청으로 해당 RAM 포기할지를 지정 합니다. 컴퓨터에서 실행 될 수 있는 다른 프로세스를 고려 하는 동안 LSASS의 성능을 최적화 하는 개념이입니다. 확인 프로그램 목록을 모니터링 에이전트를 포함 합니다. 일부 고객은 별도 에이전트는 상당한 RAM 리소스를 사용할 수 있는 다양 한 서버 기능에 대 한 경우 일부 사용자가 있는 몇 가지 세부 정보 아래 많은 WMI 쿼리를 발행 됩니다.

이 때문에 및 성능을 향상 시키기 위해 것을 제한 하는 DC에서 프로그램의 수를 최소화 하는 것이 좋습니다. 메모리 요청이 없으면 LSASS Active Directory 데이터베이스를 캐시 하 고 따라서 성능을 최적화 하기 위해이 메모리를 사용 합니다.

DC에 성능 문제를 발견 되 면 상당한 메모리 사용률을 사용 하 여 프로세스에 대 한를 시청할 수도 있습니다. 이러한 해결 해야 할 문제가 있을 수 있습니다. Microsoft 구성 요소 포함 될 수 있습니다. 최근 서비스 업데이트를 사용 하 여 유지할 수 있는지 확인 하십시오&mdash;Microsoft DC 성능에 도움이 되는 품질 업데이트의 일부로 과도 한 메모리 사용률에 대 한 솔루션을 포함 합니다.

사용 프로필에 따라 중요 한 RAM을 사용할 수 있는 기본 제공 OS 기능 가지가 있습니다.

- **파일 서버**합니다. Dc는 SYSVOL 및 Netlogon 공유, 그룹 정책 및 정책 및 시작/로그온 스크립트를 서비스에 대 한 파일 서버 이기도 합니다.
  그러나 Dc를 사용 하 여 다른 파일 콘텐츠를 서비스 고객에 게 표시 합니다. SMB 파일 서버 활성 클라이언트를 추적 하는 RAM을 사용할 수는 있지만 무엇 보다도, 파일 콘텐츠는 증가 및 RAM에 대 한 경쟁 ESE 데이터베이스 캐시와 OS 파일 캐시.  

- **WMI 쿼리**합니다. 모니터링 솔루션에는 종종 많은 WMI 쿼리 확인합니다. 개별 쿼리를 실행 하는 저렴 한 될 수 있습니다. 종종이 Windows를 관리 하는 다양 한 이벤트 로그에서 새 이벤트를 추출 하는 모니터링 솔루션으로 특히 일부 오버 헤드를 초래 하는 호출 볼륨입니다.  

  대부분의 볼륨을 생성 하는 이벤트 로그는 일반적으로 보안 이벤트 로그입니다. 및 보안 관리자가 특히 Dc에서에서 수집 하려는 이벤트 로그 이기도 합니다.  

  WMI 서비스에는 쿼리를 최적화 하는 동적 메모리 할당 체계를 사용 합니다. 따라서 WMI 서비스는 많은 양의 메모리를 ESE 데이터베이스 캐시를 사용 하 여 경쟁 다시 할당할 수 있습니다.  
