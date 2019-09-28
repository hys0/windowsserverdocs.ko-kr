---
title: AD DS 성능 튜닝의 메모리 사용량 고려 사항
description: Windows Server 2012 R2, 2016 및 2019를 실행 하는 도메인 컨트롤러의 Lsass.exe 프로세스에의 한 메모리 사용량입니다.
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: v-tea; lindakup
author: Teresa-Motiv
ms.date: 7/3/2019
ms.openlocfilehash: 55ac47d835874ddb8e160603f08cbafa985aad2a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71370293"
---
# <a name="memory-usage-considerations-for-ad-ds-performance-tuning"></a>AD DS 성능 조정에 대 한 메모리 사용 고려 사항

이 문서에서는 LSASS(Local Security Authority Subsystem Service) (lsass, Lsass.exe 프로세스 라고도 함)의 몇 가지 기본 사항을 설명 하 고, LSASS 구성에 대 한 모범 사례와 메모리 사용에 대 한 기대 사항을 설명 합니다. 이 문서는 Dc (도메인 컨트롤러)의 LSASS 성능 및 메모리 사용을 분석 하는 방법에 대 한 지침으로 사용 해야 합니다. 이 문서의 정보는이 엔진을 최적화 하기 위해 서버 및 Dc를 조정 하 고 구성 하는 방법에 대 한 질문이 있는 경우 유용할 수 있습니다.  

LSASS는 LSA (로컬 보안 기관) 도메인 인증 및 Active Directory 관리를 관리 하는 일을 담당 합니다. LSASS는 클라이언트와 서버 모두에 대 한 인증을 처리 하며 Active Directory 엔진도 제어 합니다. LSASS는 다음 구성 요소를 담당 합니다.  

- 로컬 보안 기관
- NetLogon 서비스
- SAM (보안 계정 관리자) 서비스
- LSA 서버 서비스
- SSL(Secure Sockets Layer)
- Kerberos v5 인증 프로토콜
- NTLM 인증 프로토콜
- LSA로 로드 되는 기타 인증 패키지

Active Directory database services (NTDSAI)는 확장 가능한 저장소 엔진 (ESE, ESENT)에서 작동 합니다.

DC에서의 LSASS 메모리 사용에 대 한 시각적 다이어그램은 다음과 같습니다.

![LSASS 메모리를 사용 하는 구성 요소 다이어그램](media/domain-controller-lsass-memory-usage.png)  

LSASS가 DC에서 사용 하는 메모리 양은 Active Directory 사용량에 따라 늘어납니다. 데이터를 쿼리하면 메모리에 캐시 됩니다. 따라서 Active Directory 데이터베이스 파일 (ntds.dit)의 크기 보다 큰 메모리 양을 사용 하 여 LSASS를 확인 하는 것이 일반적입니다.

다이어그램에 표시 된 것 처럼 LSASS 메모리 사용량은 ESE 데이터베이스 버퍼 캐시, ESE 버전 저장소 등을 비롯 한 여러 부분으로 나눌 수 있습니다. 이 문서의 나머지 부분에서는 이러한 각 부분에 대 한 통찰력을 제공 합니다.

## <a name="ese-database-buffer-cache"></a>ESE 데이터베이스 버퍼 캐시  
LSASS 내에서 가장 큰 가변 메모리 사용은 ESE 데이터베이스 버퍼 캐시입니다. 캐시 크기는 1mb 미만에서 전체 데이터베이스 크기까지 지정할 수 있습니다. 캐시가 클수록 성능이 향상 되므로 ESENT (Active Directory) 용 데이터베이스 엔진은 캐시를 최대한 크게 유지 하려고 합니다. 캐시 크기는 컴퓨터의 메모리 압력에 따라 달라 지지만 ESE 데이터베이스 버퍼 캐시의 최대 크기는 컴퓨터에 설치 된 실제 RAM에 *의해서만 제한 됩니다* . 다른 메모리가 부족 한 경우 캐시는 Active Directory ntds.dit 데이터베이스 파일의 크기에 따라 커질 수 있습니다. 캐시할 수 있는 데이터베이스가 많을 수록 DC의 성능은 향상 됩니다.  
  
> [!NOTE]
> 데이터베이스 캐싱 알고리즘이 작동 하는 방식 때문에 데이터베이스 크기가 사용 가능한 RAM 보다 작은 64 비트 시스템에서는 데이터베이스 캐시가 데이터베이스 크기를 30 ~ 40% 보다 크게 늘릴 수 있습니다.

## <a name="ese-version-store"></a>ESE 버전 저장소

ESE 버전 저장소 (위 다이어그램의 빨간색 부분)에 따라 메모리 사용이 가변적입니다. 사용 되는 메모리 양은 Windows Server 2019 또는 이전 버전의 Windows가 있는지 여부에 따라 달라 집니다.

- Windows server 2019 이상 Windows Server에서는 기본적으로 LSASS가 ESE 버전 저장소에 대 한 64 비트 컴퓨터의 메모리 (Cpu 수에 따라)를 최대 400MB까지 사용할 수 있습니다. 버전 저장소를 사용 하는 방법에 대 한 자세한 내용은 Ryan Ries의 다음 ASKDS 블로그 게시물을 참조 하세요. [이라는 버전 저장소는 모두 버킷 외부에](https://techcommunity.microsoft.com/t5/Ask-the-Directory-Services-Team/The-Version-Store-Called-and-They-8217-re-All-Out-of-Buckets/ba-p/400415)있습니다.

- Windows Server 2019에서는이 작업이 간소화 되 고, NTDS 서비스가 처음 시작 될 때 ESE 버전 저장소 크기는 최소한 400MB와 최대 4GB의 실제 RAM 10%로 계산 됩니다. 이 및 버전 저장소 문제 해결에 대 한 자세한 내용은 Ryan Ries의 다른 유용한 블로그를 참조 하십시오. [ 심층 이해: 서버 2019 @ no__t의 ESE 버전 저장소 변경 Active Directory-0.

## <a name="other-memory-use"></a>기타 메모리 사용

마지막으로 코드, 스택, 힙 및 다양 한 고정 크기 데이터 구조 (예: 스키마 캐시)가 있습니다. LSASS에서 사용 하는 메모리 양은 컴퓨터의 부하에 따라 다를 수 있습니다. 실행 중인 스레드 수가 늘어나면 메모리 스택 수가 늘어납니다. 평균적으로 LSASS는 이러한 고정 구성 요소에 대해 100의 메모리를 300 MB까지 사용 합니다. 더 많은 양의 RAM이 설치 된 경우 LSASS는 더 많은 RAM을 사용 하 고 가상 메모리를 줄일 수 있습니다.

**도메인 컨트롤러의 프로그램 수를 제한 하거나 최소화 하거나 적절 한 RAM을 추가 합니다.**

최적의 성능을 위해 LSASS는 지정 된 DC에서 최대한 많은 RAM을 사용 합니다. LSASS는 다른 프로세스에서 요구 하는 RAM을 내어 줍니다 합니다. 컴퓨터에서 실행 될 수 있는 다른 프로세스를 계속 고려 하면서 LSASS의 성능을 최적화 하는 것이 좋습니다. 조사할 프로그램 목록에는 모니터링 에이전트가 포함 됩니다. 일부 고객에 게는 상당한 RAM 리소스를 소비할 수 있는 다양 한 서버 기능에 대 한 별도의 에이전트가 있습니다. 일부는 다음과 같은 몇 가지 세부 정보를 제공 하는 많은 WMI 쿼리를 실행할 수 있습니다.

이로 인해 성능이 향상 되기 때문에 DC의 프로그램 수를 제한 하거나 최소화 하는 것이 좋습니다. 메모리 요청이 없는 경우 LSASS는이 메모리를 사용 하 여 Active Directory 데이터베이스를 캐시 하므로 최적의 성능을 달성할 수 있습니다.

DC에 성능 문제가 있는 경우 메모리 사용률이 큰 프로세스를 감시 해야 합니다. 문제를 해결 해야 하는 문제가 있을 수 있습니다. 여기에는 Microsoft 구성 요소가 포함 될 수 있습니다. 최신 서비스 업데이트를 유지 해야 합니다. @ no__t-0Microsoft는 품질 업데이트의 일부로 과도 한 메모리 사용률에 대 한 솔루션을 포함 하 여 DC 성능을 향상 시킬 수 있도록 합니다.

사용 프로필에 따라 상당한 RAM을 사용할 수 있는 기본 제공 OS 기능이 있습니다.

- **파일 서버**. 또한 Dc는 SYSVOL 및 Netlogon 공유를 위한 파일 서버, 정책 및 시작/로그온 스크립트를 위한 그룹 정책 및 스크립트를 제공 합니다.
  그러나 고객은 Dc를 사용 하 여 다른 파일 콘텐츠를 처리 하는 것을 볼 수 있습니다. 그러면 SMB 파일 서버는 RAM을 사용 하 여 활성 클라이언트를 추적 하지만, 파일 콘텐츠는 OS 파일 캐시가 증가 하 고 RAM에 대 한 ESE 데이터베이스 캐시와 경쟁할 수 있습니다.  

- **WMI 쿼리**. 모니터링 솔루션은 종종 많은 WMI 쿼리를 만듭니다. 개별 쿼리를 실행 하는 것이 비용이 저렴 합니다. 특히 모니터링 솔루션이 Windows에서 관리 하는 다양 한 이벤트 로그에서 새 이벤트를 추출 하는 경우에는 약간의 오버 헤드가 발생 하는 호출의 양이 종종 있습니다.  

  대부분의 볼륨을 생성 하는 이벤트 로그는 일반적으로 보안 이벤트 로그입니다. 또한이는 특히 Dc에서 보안 관리자가 수집 하려고 하는 이벤트 로그입니다.  

  WMI 서비스는 쿼리를 최적화 하는 동적 메모리 할당 체계를 사용 합니다. 따라서 WMI 서비스에서 많은 메모리를 할당 하 고 ESE 데이터베이스 캐시와 경쟁할 수 있습니다.  
