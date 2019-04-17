---
title: "Windows Server 2016에 대 한 일반 데이터 보호 규정 (GDPR) 여행을 시작"
description: "이 문서를 사용 하 여 GDPR 파악 하 고 제품에 대 한 Microsoft 준수 쪽으로 시작 하는 데 도움을 제공 합니다."
keywords: "개인 정보, GDPR"
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.technology:
- techgroup-security
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 09/25/2017
ms.author: nirb
ms.openlocfilehash: e68b8d926f7749f7fcecf5f3752822c54db5ce76
ms.sourcegitcommit: c5aa1eedd1383b8b8f6b8fcb0af995c28277002a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2018
---
# <a name="beginning-your-general-data-protection-regulation-gdpr-journey-for-windows-server"></a>Windows Server에 대 한 일반 데이터 보호 규정 (GDPR) 여행을 시작 

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 문서에서는 란를 포함 하 여 GDPR에 대 한 정보를 제공 하 고 호환 되는 데 도움이 되는 제품 Microsoft 제공 합니다.

## <a name="introduction"></a>소개
2018 년 5 월 25 일에 유럽 개인 정보 보호 법률은 개인 정보 권리, 보안 및 준수에 대 한 새로운 전체 모음 설정 적용 때문입니다.

일반 데이터 보호 규정 또는 GDPR를 보호 하 고 활성화 개인의 개인 정보 권리에 대해 기본적으로입니다. GDPR 설정 엄격한 글로벌 개인 요구 사항을 관리 하 고 개별 선택을 유지 하는 동안 개인 데이터를 보호 하는 방법 관리 등 데이터 전송, 처리 또는 저장 된에 관계 없이 합니다.

Microsoft와 고객은 이제는 GDPR의 개인 정보 보호 목표를 달성 하기 여행을 합니다. Microsoft는 개인 정보 기본 오른쪽 이며 고 GDPR 명확 하 고 개별 개인 정보 권리를 사용 하도록 설정에 대 한 중요 한 단계 앞으로 생각 생각 합니다. 하지만 GDPR 조직 전 세계에서 중요 한 변경 사항이 필요 합니다는 또한 인식 했습니다.

노력 하 고 GDPR 내에서 고객 지원지 않습니다 어떻게 설정한는 [다운로드 GDPR 준수 Microsoft 클라우드](https://blogs.microsoft.com/on-the-issues/2017/02/15/get-gdpr-compliant-with-the-microsoft-cloud/#hv52B68OZTwhUj2c.99) 블로그 게시물에서의 개인 정보 보호 책임자 [Brendon Lynch](https://blogs.microsoft.com/on-the-issues/author/brendonlynch/) 및 [Earning 사용자 일반 데이터 보호 규정 계약상 정책을를 신뢰](https://blogs.microsoft.com/on-the-issues/2017/04/17/earning-trust-contractual-commitments-general-data-protection-regulation/#6QbqoGWXCLavGM63.99)"블로그 게시물에서 [풍부한 Sauer](https://blogs.microsoft.com/on-the-issues/author/rsauer/) -Microsoft 부사장 및 그 일반 자문 합니다.

하지만 GDPR 준수에 여행을 어려울 수 있습니다 여기서 하는 데 도움이 됩니다. GDPR에 대 한 자세한 내용은 우리의 약속 및 모험을 시작 하는 방법을 참조 하세요는 [Microsoft 보안 센터의 GDPR 섹션](https://www.microsoft.com/en-us/trustcenter/privacy/gdpr)합니다.

## <a name="gdpr-and-its-implications"></a>GDPR와 그 의미
GDPR 수집, 사용 하는 방법을 개인 데이터를 관리에 중요 한 변경 사항이 필요할 수 있는 복잡 한 규정입니다. Microsoft는 전력이 복잡 한 규정을 준수 고객 지원 및 여정을 파트너는 관련해 서는 GDPR에 대 한 준비를 합니다.

GDPR 부과 상품을 제공 하는 조직에서 규칙 및 서비스 하는 유럽 연합과 (EU) 또는에서 수집 하 고, 해당 회사는 어디에 관계 없이 EU 거주자에 연결 된 데이터를 분석 합니다. 중 고 GDPR의 핵심 요소 다음과 같습니다.

- **향상 된 개인 개인 정보 권리입니다.** 올바른 부정확 개체 자신의 개인 데이터를 처리 하기 위해 데이터를 지우려면 하 고 창을 끌고 나 해당 데이터를 자신의 개인 데이터에 대 한 액세스 권한이 함으로써 거주자를 위한 EU 데이터 보호를 강화 합니다.

- **개인 데이터를 보호 하기 위한 의무 증가 합니다.** 를 제공 하는 개인 데이터를 처리 하는 조직의 강화 책임 규정 준수의 책임 명확성을 높였습니다.

- **개인 데이터를 필수 위반 보고 있습니다.** 개인 데이터를 제어 하는 권리와 freedoms 개인 과도 지연을 않고도 해당 감독 기관에 해당 하는 위험할 보고서 개인 데이터를 침해 하며 인식 될 가능, 이전 72 시간이 지난 후 한 번에 나타나는 침해로 합니다.

같이 할 수는 GDPR 수 중요 한에 영향을 미칠 비즈니스, 잠재적으로 개인 정보 취급 방침을 업데이트, 구현 and 데이터 보호 컨트롤을 강화 하 고 알림 절차 위반, 매우 투명 정책을 배포 필요 더 많은 투자 IT 학습 하 고 있습니다. Microsoft Windows 10 효과적으로 하는 데 도움이 되 고 효율적으로 이러한 요구 사항 중 몇 가지 해결 수 있습니다.

## <a name="personal-and-sensitive-data"></a>중요 한 개인 데이터
GDPR 준수 하기 위해 사용자의 일환으로, 어떻게는 규정 정의 중요 한 개인 데이터와 이러한 정의 관계 조직에서 저장 된 데이터를 이해 하 해야 합니다. 에 따라 수 검색 데이터를 작성 위치 처리 이해 관리 하 고 저장 합니다.

GDPR 개인 데이터를 관련 정보 식별 또는 식별 자연 스러운 사용자를 고려 합니다. (예: 법적 이름) 직접 식별 및 간접 식별 하는 포함 될 수 있습니다 (와 같은 특정 정보를 이용 하 여 확인란의 선택을 취소는 바로 여러분 데이터 참조). GDPR도 정확 하 게 개인 데이터의 개념 온라인 식별자 (예: 모바일 디바이스 Id IP 주소)를 포함 하는 한 위치 데이터.

GDPR 유전자 데이터 (예: 있는 개별 유전자 시퀀스) 및 생체 인식 데이터에 대 한 특정 정의 소개합니다. 유전 데이터와 함께 다른 생체 인식 데이터 하위 범주의 개인 데이터 (인종 또는 민족 음악 원본, 정치 의견, 종교적인 유적지를 보호 또는 철학적 신념 또는 거래 연합과 멤버십 공개 개인 정보: 건강, 또는 대 한 데이터가 관한 데이터를 사용자의 성별 생활 또는 성적 취향)는 GDPR 아래에서 중요 한 개인 데이터를 처리 됩니다. 중요 한 개인 데이터 향상 된 보호 기능을 제공 되어 및 일반적으로 처리 이러한 데이터가 사용 되는 개인의 명시적인 동의 요구 합니다.

### <a name="examples-of-info-relating-to-an-identified-or-identifiable-natural-person-data-subject"></a>예를 식별 또는 식별 자연 사람 (데이터 주제)와 관련 된 정보
이 목록은 정보 GDPR 통해 정리 하는 여러 가지 유형의 예로 제공 합니다. 이 목록은 합니다.

-   이름

-   Id 번호 (예: SSN)

-   위치 데이터 (예: 가정 주소)

-   온라인 식별자 (예: 메일 주소, 화면 이름, IP 주소, 디바이스 Id)

-   Pseudonymous 데이터 (예:, 키를 사용 하 여 개인 식별)

-   유전 데이터 (예:의 개별 생물학적 샘플)

-   생체 인식 데이터 (예: 지문, 얼굴 인식)

## <a name="getting-started-on-the-journey-towards-gdpr-compliance"></a>GDPR 준수 주말로 가면서 여행을 시작 하기
얼마나는 관여를 부여 GDPR 호환 좋습니다 준비 집행 시작 될 때까지 기다렸다가 하지 않습니다. 개인 정보 및 데이터 관리 방법 이제 검토 해야 있습니다. 네 가지 주요 단계에 집중 하 여 GDPR 준수에 모험을 시작 하는 것이 좋습니다.

-   **검색 합니다.** 어떤 개인 데이터는 사용자의 신원을 확인 하 고 있는 합니다. 

-   **관리 합니다.** 어떻게 개인 데이터를 제어 사용 되 고에 액세스 합니다.

-   **보호 합니다.** 보안 컨트롤 방지 감지 하 고 문제와 데이터 위반에 응답을 설정 합니다.  

-   **보고서 합니다.** 보고서 데이터 위반 데이터 요청에 역할 하며 서류 유지 합니다.

    ![4 주요 GDPR 단계 함께 작동 하는 방법에 대해 다이어그램](../media/GDPR-Windows-Server-Overview/gdpr-steps-diagram.png)

각 단계 예 도구, 리소스 및 기능 해당 단계의 요구 사항을 충족할 수 있도록 사용할 수 있는 다양 한 Microsoft 솔루션을 설정 했습니다. 이 문서 아닙니다 포괄적인 "방법은" 자세한 내용을 확인 하려면 사용자에 대 한 링크가 포함 하 고 더 많은 정보를 사용할 수 있는 [Microsoft 보안 센터의 GDPR 섹션](https://www.microsoft.com/en-us/trustcenter/privacy/gdpr)합니다.

## <a name="windows-server-security-and-privacy"></a>Windows Server 보안 및 개인 정보
GDPR 개인 데이터와 처리 시스템을 보호 하기 위해 해당 기술 부문과 창의 조직의 보안 조치를 구현 해야 합니다. GDPR 컨텍스트에서 실제 및 가상 서버 환경 잠재적으로 처리 하는 중요 한 개인 데이터. 처리는 작업이 나 데이터 수집, 저장 및 검색 등의 작업 집합을 것일 수 있습니다.

이 조건을 충족 하 고 적절 한 기술적인 보안 조치를 구현 하는 기능 오늘 점점 더 악의적인 IT 환경에서 얼굴 위협 반영 해야 합니다. 오늘 보안 위협 환경 및 있는 공격적인 위협 중 하나입니다. 몇 년 동안 이전, 악성 공격자 주로 일시적으로 오프 라인 시스템에 출시 되었습니다 또는 공격을 통해 인식 커뮤니티의에 집중. 그때 이후로 침입자 동기 수익 창출, 디바이스 및 데이터 인질 소유자의 요구 몸값 비용을 지불 될 때까지 길게 포함 하 여 쪽으로 이동 했습니다.

최신 공격 점점 더 큰 지식 도난;에 집중. 금융 손실 될 수 있는 대상으로 시스템 저하 있으며 이제 개인이, 회사 및 국립 관심사 전 세계의 보안 위협 cyberterrorism도 있습니다. 이러한 공격자 매우 숙련된 개인 및 누구 일부 국가 상태에 큰 예산과 것 처럼 보이는 무제한 인사 사용에는 보안 전문가 됩니다. 이러한 위협 요소이 과제가 충족할 수 있는 방법이 필요 합니다.

이러한 위협 제어 수를 사용 하는 모든 개인 정보나 중요 한 데이터를 유지 하 여 기능을 위험이 할 뿐만 아니라 전체 비즈니스 중대 위험 수도 있습니다. 연구소 McKinsey, Ponemon, Verizon, 및 Microsoft에서 최근 데이터를 것이 좋습니다.

- 데이터 위반은 GDPR 기대할 보고 유형의 평균 비용은 $3.5 분입니다.

- 이러한 침해 63% 약하거나 도난당 한 암호는는 GDPR 프로시저 해야 주소를 포함 합니다.

- 새로운 넘는 300, 000 맬웨어 샘플 생성 되 고 하기 작업 주소 데이터 보호 과제가 매일 손가락을 펼치고.

한 번 인터넷의 검은 재앙 라는 최근 Ransomware 공격와 같이 사용자 심각한 갖습니다 추가 요금을 결제할 유지할 수 있는 더 큰 대상 후 공격자 것입니다. GDPR 데스크톱 및 노트북을 풍부한 대상 정말 중요 한 개인 데이터를 포함 하는 등 시스템를 지연 시키는 포함 되어 있습니다.

두 가지 주요 원칙이 안내 하 고 지침에 따라 Windows 개발 계속:

- **보안 합니다.** 고객을 대신 하 여 소프트웨어 및 서비스를 저장 하는 데이터는 피해 로부터 보호 하 고 사용 하거나 적절 한 방식 수정할 수 해야 합니다. 보안 모델을 이해 하 고 해당 응용 프로그램에 빌드 개발자를 위한 쉽게 있어야 합니다.

- **개인 정보 보호 합니다.** 사용자가 해당 데이터가 사용 되는 방식을 제어에 있어야 합니다. 정보 사용에 대 한 정책을 사용자 명확 하 게 됩니다. 사용자가 시간을 최대한 활용 하는 정보를 받는 경우 제어 여야 합니다. 사용자가 지정 수신자 정보 메일 사용을 제어 포함 하 여 적절 한 사용 하기 쉬운 있어야 합니다.

Microsoft는 이러한 원칙은 Microsoft의 CEO Satya Nadella 하 여 최근으로 했음을 알아차렸을 것에 대해 확고 유지 

> "_어떤 것 들은 일관성을 전 세계를 계속 변경 하 고 이래 발전: 보안 및 개인 정보 보호에 대 한 고객의 요구 합니다. _"

작업 중 만드는, 액세스, 처리 저장 및 개인으로 받을 수 있는 데이터를 관리 실제 및 가상 서버 역할을 이해 GDPR을 준수 하는 GDPR 아래에서 중요 한 데이터는 중요 한으로 합니다. Windows Server는 개인 데이터를 보호 기술 부문과 창의 조직의 보안 적절 한 조치를 구현 하는 GDPR 요구 사항을 준수 하는 데 도움이 되는 기능을 제공 합니다.

Windows Server 2016 보안 환경과에 모양-; 없는 아키텍처 원칙은입니다. 및 네 주체에 가장 잘 이해할 수 있습니다.

- **보호 합니다.** 지속적인 포커스와 혁신에 예방 조치입니다. 알려진된 공격 및 알려진된 맬웨어를 차단 합니다.

- **검색 합니다.** 포괄적인 공격 빠른 답변을 점 비정상적인 유용한 도구를 모니터링 합니다.

- **응답 합니다.** 앞에 응답 하 고 복구 기술 이용 깊이 전문 문의 합니다.

- **격리 합니다.** 운영 체제의 구성 요소 및 데이터 비밀 파악 하 고 관리자 권한으로 제한 호스트 건강 측정 정밀 하 게 합니다.

Windows server, 보호, 검색 및 종류의 데이터 위반에 일으킬 수 있는 공격 으로부터 보호 기능에 크게 향상 됩니다. 내에서 GDPR 위반 알림 주위 엄격한 요구 사항을 제공 되 면 데스크톱 및 노트북 시스템 잘 방어은 무단 낮아집니다 비용이 위반 분석 및 알림 될 수 있는 위험 발생할 수 있습니다.

다음 섹션에서 Windows Server GDPR 준수 여행의 "보호" 단계으로 맞는 기능을 제공 하는 방법을 볼 수 있습니다. 이러한 기능 세 가지 보호 시나리오에 속합니다.

- **자격 증명을 보호 하 고 관리자 권한이 제한 합니다.** Windows Server 2016 시스템을 사용 하는 시작 지점으로 침입 추가 대 한 것을 방지 하려면 이러한 변경을 구현 하는 데 도움이 됩니다.

- **앱 및 인프라 실행 운영 체제를 보호 합니다.** Windows Server 2016 외부 공격자가 악성 소프트웨어를 실행 취약성을 이용 하거나 차단 하는 데 도움이 보호 계층을 제공 합니다.

- **Virtualization 보안을 유지 합니다.** Windows Server 2016 가상 컴퓨터를 보호 하 고 패브릭 보호를 사용 하 여 안전 하 게 가상화를 수 있습니다. 이렇게 하면 암호화 하 고 신뢰할 수 있는 호스트 패브릭, 악의적인 공격 으로부터 보호 더 나은에서 가상 컴퓨터를 실행할 수 있습니다.

특정 GDPR 요구 사항에 대 한 언급 된 자세한 내용을 아래에 설명 된 이러한 기능을 무결성 및 운영 체제와 데이터의 보안을 유지 하는 데 도움이 되는 고급 디바이스 보호 기능을 기반으로 합니다.

내에서 GDPR 주요 프로 비전 됩니다 디자인 및 기본적으로 데이터 보호 되며이 프로 비전에 맞게 못하는 돕는 BitLocker 디바이스 암호화 등 Windows 10 기능 수 있습니다. BitLocker는 하드웨어 기반, 보안 관련 기능을 제공 하는 신뢰할 수 있는 TPM (플랫폼 모듈) 기술을 사용 합니다. 암호화 프로세서 칩이 변조을 위해 여러 물리적 보안 메커니즘 포함 되어 있으며 악성 소프트웨어 tpm 보안 기능을 조작할 수 없습니다.

칩 변조을 위해 여러 물리적 보안 메커니즘 포함 되어 있으며 악성 소프트웨어 tpm 보안 기능을 조작할 수 없습니다. 주요 이점 TPM 기술을 사용 하 여 몇 가지 할 수 있습니다.

-   생성 하 고, 저장, 암호화 키의 사용을 제한 합니다.

-   자신에 구울 TPM 고유한 RSA 키를 사용 하 여 플랫폼 디바이스 인증을 위한 TPM 기술을 사용 합니다.

-   보안 측정 단위를 저장 함으로써 플랫폼 무결성을 유지 하는 데 도움이 됩니다.

작동 데이터 위반 없이 관련 된 추가 고급 장치 보호 무결성 맬웨어를 확인 하 여 시스템을 시작 하기 전에 시스템 방어 수 없으면 유지 하기 위해 Windows 신뢰할 수 있는 부팅 포함 되어 있습니다.

## <a name="windows-server-supporting-your-gdpr-compliance-journey"></a>Windows Server: GDPR 준수 여정 지원
Windows Server의 핵심 기능 효율적으로 GDPR 필요한 호환성에 대 한 보안 및 개인 정보 보호 메커니즘 구현할 수 있습니다. 이러한 기능을 사용 하면 준수 보증 하지는 동안 작업을 수행 하 여 활동 지원 됩니다.

서버 운영 체제 위치 데이터를 도용 하려는 비즈니스 중단 될 수 있는 공격 으로부터 보호 계층을 만들 수 있는 새로운 기회 affording 조직의 인프라에 전략적 계층 합니다. GDPR 디자인을 Data Protection, 액세스 제어 하 여 개인 정보 보호 등의 주요 측면 내에서 서버 수준 IT 인프라 해결 해야 합니다.

Id, 운영 체제 및 virtualization 계층을 보호 하기 위해 노력, Windows Server 2016 도움이 시스템에 불법 액세스 하는 데 일반적인 공격 경로 차단: 도난당 자격 증명, 맬웨어 및 손상된 virtualization 패브릭 합니다. 비즈니스 위험 감소를 외에도 보안 구성 요소에 기본 제공 Windows Server 2016 도움말 키 정부 및 industry에 대 한 준수 요구 사항을 충족 보안 규정. 

자격 증명을 손상 맬웨어를 실행 하 고 유지에서 감지 되지 공격자가의 기능이 제한 고 실행 하는 모든 클라우드에서 VM으로 Windows Server 데이터 센터에 더 잘 보호할 수 있도록 이러한 id, 운영 체제 및 virtualization 보호 프로그램 네트워크 선택 합니다. 마찬가지로, Hyper-v 호스트 배포할 때 Windows Server 2016 제공 보호 가상 컴퓨터 및 분산된 방화벽을 통해 사용자는 가상화 환경에 대 한 보안 보증 기능입니다. Windows Server 2016 서버 운영 체제 적극적으로 datacenter 보안 참여 됩니다.

### <a name="protect-your-credentials-and-limit-administrator-privileges"></a>자격 증명을 보호 하 고 관리자 권한이 제한 
개인 정보에 액세스를 제어 하 고 데이터를 처리 하는 시스템 관리자 액세스를 포함 하 여 특정 요구 사항이 GDPR으로 영역입니다. 권한 있는 id는 더 높은 도메인 관리자, Enterprise 관리자, 로컬 관리자 또는 고급 사용자 그룹의 회원 인 사용자 계정에 같은 권한을 모든 계정을 없습니다. 이러한 신원을 권한이 부여 않은 직접 시스템 또는 보안 정책이 로컬 본체에서 사용자 권한 할당 노드에 나열 된 권리를 종료 백업 같은 계정을 포함할 수도 있습니다.

일반적인 액세스 제어 원칙 및는 GDPR와 같은 줄에로 잠재적인 공격자가 손상에서 이러한 특권된 id를 보호 해야 합니다. 먼저 어떻게 신원을 손상 될; 이해 하는 다음 공격자 이러한 권한 있는 id에 액세스 하지 못하도록 계획할 수 있습니다.

#### <a name="how-do-privileged-identities-get-compromised"></a>어떻게 수행 권한 있는 신원은 손상 된?
조직 지침을 보호 하기 위해 없는 경우 권한이 있는 신원은 손상 받을 수 있습니다. 예는 다음과 같습니다.

- **필요한 것 보다 더 많은 권한을 합니다.** 가장 일반적인 문제 중 하나는 사용자가 자신의 작업 기능을 수행 하는 데 필요한 하는 것 보다 더 많은 권한을입니다. 예를 들어, 사용자 DNS 관리 하는 광고 관리자 수도 있습니다. 대부분의 경우 서로 다른 관리 수준을 구성할 하지 않으려면이 수행 됩니다. 하지만 이러한 계정은 손상 되 면 공격자가 자동으로 권한을 올려 합니다.

- **지속적으로 관리자 권한으로 로그인 합니다.** 또 다른 일반적인 문제는 사용자가 관리자 권한으로 사용할 수 시간 제한 없이입니다. 이것은 가장 일반적인 데스크톱 특권된 계정을 사용 하 여 컴퓨터에 로그인, 로그온 한 상태를 유지 하 고 특권된 계정을 사용 하 여 웹을 검색 하 고 메일을 사용 하 여 IT 전문가와 (일반적인 IT 클라우드 작업 기능). 무제한 권한이 있는 계정 공격에 더욱 취약 계정에서는 기간과 계정을 손상 될 가능성이 증가 합니다.

- **사회 공학적 연구 합니다.** 대부분의 위협을 자격 증명 조직 연구 하 여 시작 하 고 사회 공학적 통해 수행 합니다. 예를 들어, 공격자 조직의 네트워크에 액세스할 수 있는 손상 합법적 계정 (하지만 계정 향상 된 것은 아닙니다) 메일 피싱 공격을 수행할 수 있습니다. 네트워크에 추가 연구 수행 하 고 관리 작업을 수행할 수 있는 권한이 있는 계정을 확인할 수 공격자 유효한이 계정을 사용 합니다. 

- **관리자 권한으로 계정 활용 합니다.** 네트워크에 정상, 상승 되지 사용자 계정으로도 공격자 관리자 권한으로 계정에 대 한 액세스를 얻을 수 있습니다. 이렇게 하면의 일반적인 방법 중 하나 해시를 통과 또는 토큰을 통과 공격 사용 하 여 때문입니다. 에 대 한 자세한 내용은 Pass-the-해시와 기타 자격 증명 도용의 기술을 리소스를 참조는 [Pass-the-해시 (PtH) 페이지](https://technet.microsoft.com/en-us/dn785092.aspx)합니다.

물론를 식별 하 고 매일 생성 되는 새로운 방법을) (와 권한 있는 신원을 손상 공격자 사용할 수 있는 다른 방법 됩니다. 따라서 것이 중요 공격자는 특권된 id에 액세스 하는 기능을 줄이기 위해 최소 권한 계정에 로그인 하는 사용자에 대 한 정보를 설정 합니다. 다음 섹션에서는 Windows Server 이러한 위험을 완화 수 있는 기능을 설명 합니다.

#### <a name="just-in-time-admin-jit-and-just-enough-admin-jea"></a>적시에 관리자 (JIT)와 관리자만 충분히 (JEA)
동안 해시를 통과 또는 티켓을 통과 공격 으로부터 보호 하는 것이 중요 관리자 자격 증명 사회 공학적, 불만이 직원 및 무작위 포함 한 다른 방법으로 도난당 할 수 있습니다. 그러므로 자격 증명 가능한 한 분리를 외에 원하는 손상 될 경우 관리자 수준 권한이 reach을 제한 하는 방법을 합니다.

오늘, 책임 하나의 영역을 사용 중인 경우에 너무 많은 관리자 계정 권한이 과도 됩니다. 예를 들어, 누가 매우 특수 집합이 DNS 서버를 관리할 수 있는 권한이 필요한, DNS 관리자가 도메인 관리자 수준 권한이 부여 자주 됩니다. 또한,이 자격 증명 광고형에 대 한 권한이 부여 되므로, 제한은 사용 기간에 합니다.

불필요 한 도메인 관리자 수준 권한이 있는 모든 계정 자격 증명을 손상 침입자에 노출을 증가 합니다. 공격에 대 한 노출 영역을 최소화 하려면 관리자 필요한 작업을 수행할 수 있는 권한 및 완료 하는 데 필요한 시간은 창에 대해서만 특정 집합을 제공 하려고 합니다.

방금 충분히 관리 및 시간 거의 사용 관리를 관리자 필요한 시간이 정확 하 게 창에 대 한 필요 특정 권한을 요청할 수 있습니다. DNS 관리자에 대 한 예를 들어, PowerShell 바로 충분히 관리 사용 하 여 만들 수 있습니다 DNS 관리에 사용할 수 있는 명령 제한 된 집합입니다.

관리자 DNS 서버 자신의 중 하나에 대 한 업데이트를 확인 하는 경우 Microsoft Identity Manager 2016을 사용 하 여 DNS 관리에 대 한 액세스를 요청 것 많이 있습니다. 요청 워크플로 요청한 권한을 부여 하기 전에 사용자의 신원을 확인 하는 관리자 휴대폰 호출할 수 2 단계 인증을 등 승인 프로세스 포함 될 수 있습니다. 한 번 허용 해당 DNS 권한을 제공 PowerShell 역할에 대 한 액세스 DNS 특정 시간 범위에 대 한 됩니다.

DNS 관리자 자격 증명은 도난당 한 경우이 시나리오를 가정 합니다. 먼저 자격 증명을 사용 하는 연결 관리자 권한이 없는 이후 공격자 DNS 서버-또는 기타 시스템 – 변경 하려면에 액세스할 수 수 없을입니다. 공격자 DNS 서버에 대 한 권한을 요청할 경우, 번째 단계 인증은 요청 신원을 확인 합니다. 켜져 있지 않으면 가능성이 공격자 DNS 관리자 휴대폰에 있는지, 이후 인증 실패 합니다. 것 시스템에서 공격자 잠그고 경고 IT 조직 자격 증명 손상 될 수 있습니다.

또한 많은 조직 사용 하는 무료 [로컬 관리자 암호 솔루션 (랩)](http://aka.ms/laps) 는 서버 및 클라이언트 시스템에 대 한 간단한 하면서 강력한 JIT 관리 메커니즘으로 합니다. 랩 기능은 도메인에 가입 컴퓨터의 로컬 계정 암호 관리 기능을 제공 합니다. 암호 저장 및 되는 Active Directory (AD)으로 보호과 액세스 제어 목록 () 하므로 적합 한 사용자 수 읽거나의 원래 대로 요청 합니다.

언급 했 듯이 [Windows 자격 증명 도용의 Mitigation 가이드](https://www.microsoft.com/en-us/download/confirmation.aspx?id=54095), 

> "_도구와 방법은 범죄자 자격 증명 도용의 수행를 사용 하 여 다시 사용할 수 있도록 공격 개선, 악성 공격자 발견 하는 것 목표를 달성 하기 쉽게 합니다. 자주 자격 증명 도용의 효과적인 완화 필요 피플, 프로세스 및 기술 해결 하는 전체론적 접근 방식을 운영 방법을 또는 사용자 자격 증명 노출에 의존 합니다. 이러한 공격 공격자가 확장 하거나 조직 있어야 위반 신속 하 게 전략 공격자 자유롭게 이동 하지 않도록 있으며에서 감지 되지 않습니다을 구현 하 여 하므로 액세스를 유지 하 여 시스템을 손상 시킬 후 자격 증명 가로채기 뿐만 아니라 사용 하 여 손상 된 네트워크 선택 합니다. _"

Windows Server에 대 한 중요 한 디자인 고려 자격 증명 도용의 완화 된-특히 자격 증명 파생 되었습니다. Credential Guard 파생된 자격 증명 도용 및 Windows의 중요 한 아키텍처 변경이 구현 하 여 다시 사용에 대 한 향상 된 보안 제거 하는 데 도움이 되도록 설계 크게 제공 하드웨어 기반 격리 공격을 방지 하기 위해 보다 합니다.

보안 virtualization 기반, 자격 증명 도용의 공격 기술 및 많은에 사용 되는 도구를 사용 하 여 파생된 자격 증명은 보호 하는 Windows Defender Credential Guard, NTLM Kerberos을 사용 하는 동안 대상된 공격 차단 됩니다. 관리자 권한이 있는 운영 체제에서 실행 되는 맬웨어 보안 virtualization 기반에 의해 보호 되는 비밀 추출 수 없습니다. 지속적인 위협 공격는 Windows Defender Credential Guard 강력한 mitigation 이지만, 새 공격 기술을 가능성이 shift Device Guard 합니다.

#### <a name="windows-defender-credential-guard"></a>Windows Defender Credential Guard
Windows Defender Credential Guard 격리할 자격 증명 정보, 암호 해시 또는 Kerberos 티켓 차단 되 고에서 차단 virtualization 기반 보안을 사용 합니다. 완전히 새로운 격리 LSA 로컬 보안 기관을 () 프로세스를 운영 체제의 나머지 부분에 액세스할 수 있는 사용 합니다. 격리 된 LSA에서 사용 하는 모든 바이너리 해시를 통과 유형 공격 완전히 효과가 만드는 보호 환경에서 시작 하기 전에 한지 확인 하는 인증서를 로그인 합니다.

Windows Defender Credential Guard 사용합니다.

- Virtualization 기반 보안 (필수)입니다. 또한 필요합니다.

    - 64 비트 CPU

    - CPU virtualization 확장 이용 확장된 페이지 표

    - Windows 하이퍼바이저

- 보안 부팅 (필수).

- TPM 2.0 중 하나 이산 또는 펌웨어 (기본-하드웨어 구속력 제공)

Windows Defender Credential Guard 자격 증명 및 Windows Server 2016 Windows Server 2016. Windows Defender Credential Guard 요구 사항에 대 한 자세한 내용은 참조 [보호 파생 Windows Defender로 도메인 자격 증명 Credential Guard](https://docs.microsoft.com/en-us/windows/access-protection/credential-guard/credential-guard).

#### <a name="windows-defender-remote-credential-guard"></a>Windows Defender 원격 Credential Guard
Windows Defender 원격 Credential Guard Windows 10 1주년 업데이트는 원격 데스크톱 연결을 가진 사용자를 위한 자격 증명을 보호 합니다. 이전에 원격 데스크톱 서비스를 사용 하 여 모든 사람이 해야 로컬 컴퓨터에 로그온 하 고 다음 다시 대상 시스템에 대 한 원격 연결을 수행 하는 것에 로그온 해야 합니다. 이 두 번째 로그인 자격 증명 해시를 통과 노출 대상 컴퓨터에 전달 또는 티켓을 통과 공격 합니다.

Windows Defender 원격 Credential Guard와 Windows Server 2016 구현 단일 로그온 원격 데스크톱 세션에 대 한 제거에서 사용자 이름 및 암호를 다시 입력을 요구 합니다. 대신 로컬 컴퓨터에 로그온 할 때 사용한 자격 증명을 활용 합니다. Windows Defender 원격 Credential Guard을 사용 하 여 원격 데스크톱 클라이언트 및 서버 다음 요구 사항을 충족 해야 합니다.

- 동일한 또는 보안 관계 도메인에 두고 Active Directory 도메인에 가입 있어야 합니다.

- Kerberos 인증을 사용 해야 합니다.

- 적어도 실행 중 이어야 Windows 10 버전 1607 또는 Windows Server 2016.  

- 원격 데스크톱 클래식 Windows 앱이 필요 합니다. 원격 데스크톱 유니버설 Windows 플랫폼 앱 Credential Guard Windows Defender 원격 지원 하지 않습니다.

레지스트리 설정이 원격 데스크톱 서버 및 그룹 정책 또는 원격 데스크톱 클라이언트 매개 변수와 원격 데스크톱 연결에 사용 하 여 Windows Defender 원격 Credential Guard 사용할 수 있습니다. Windows Defender 원격 Credential Guard 사용에 대 한 자세한 내용은 참조 [원격 데스크톱 보호 자격 증명을 Windows Defender 원격 Credential Guard](https://docs.microsoft.com/en-us/windows/access-protection/remote-credential-guard). Windows Defender Credential Guard와 함께 사용할 수 있습니다 Windows Defender 원격 Credential Guard에서 권한 신원을 보호 하기 위해 Windows Server 2016.

### <a name="secure-the-operating-system-to-run-your-apps-and-infrastructure"></a>운영 체제를 infrastructure 및 앱을 실행할 보호
또한, 사이버 위협이 방지 찾기 및 맬웨어 공격 subverting 인프라 표준 작동 방식으로 제어할 수 있는 차단 필요 합니다. 공격자 운영 체제 또는 응용 프로그램을 실행할 미리 결정 비, 실행 불가능 방식에서 액세스할 수, 가능성이 악성 조치를 취해야 해당 시스템을 사용 중인지 합니다. Windows Server 2016 외부 공격자 취약성을 이용 또는 악성 소프트웨어를 실행 하는 보호 계층을 제공 합니다. 운영 체제 시스템 침해 나타내는 작업 관리자를 경고 하 여 인프라와 응용 프로그램 보호 활성 역할을 걸립니다.

#### <a name="windows-defender-device-guard"></a>Windows Defender Device Guard
Windows Server 2016 서버에만 신뢰할 수 있는 소프트웨어를 실행할 수 있는지 확인 하기 위해 Windows Defender Device Guard 포함 되어 있습니다. Virtualization 기반 보안을 사용 하 고 바이너리 조직의 정책에 따라 시스템에서 실행할 수 제한할 수 있습니다. 실행 지정된 바이너리 이외의 항목 하려고 하면, Windows Server 2016 되지 않도록 차단 하 고 관리자 잠재적인 위반 되었음을 볼 수 있도록 시도가 실패 한를 기록 합니다. 위반 알림 요구 사항을 준수 GDPR에 대 한 중요 한 부분입니다.

PowerShell 시스템에서 실행할 수 있는 스크립트 승인할 수 있도록 Windows Defender Device Guard 통합도 되어 있습니다. 이전 버전의 Windows Server에서 관리자 정책을 코드 파일에서을 삭제 하 여 코드 무결성 집행을 무시할 수 있습니다. Windows Server 2016 정책을 서명 인증서에 액세스할 수 있는 개인만 정책을 변경할 수 있도록 조직에서 로그인 하는 정책을 구성할 수 있습니다.

#### <a name="control-flow-guard"></a>흐름 보호 제어 
Windows Server 2016에는 기본적으로 방지 일부 클래스 메모리 손상 공격에 포함 되어 있습니다. 서버 패치의 중요 한 이지만 기회가 항상 식별 되지 않은 있는 보안 문제에 대 한 맬웨어를 개발할 수 있습니다. 가장 일반적인 이용 이러한의 취약성에 대 한 방법 중 일부는 비정상적인 또는 익스트림 데이터를 실행 중인 프로그램을 제공 하기 위해입니다. 예를 들어, 공격자 수 취약점 버퍼가 오버플로 영역에 대 한 응답 프로그램에 의해 예약 되어 오버런 예상 보다 프로그램에 추가 정보를 입력 하 여 합니다. 이 기능 포인터를 저장할 수 있는 옆에 있는 메모리를 손상 될 수 있습니다.

프로그램이이 기능을 통해 통화, 공격자가 지정 된 의도 하지 않은 위치에 그런 다음 이동할 수 있습니다. 이러한 공격 프로그래밍 (JOP) 공격 점프 향하는 라고도 합니다. 플로 보호 제어 강력한 제약 실행 – 특히 간접 어떤 응용 프로그램이 코드 될 수에 배치 하 여 JOP 공격을 방지 전화 지침입니다. 응용 프로그램에서 간접 통화 유효한 대상인 기능 집합을 식별 무게는 가벼우며 보안 검사를 추가 합니다. 응용 프로그램이 실행 되 면 이러한 간접 통화 대상 유효한 지 확인 합니다.

실행 시 제어 플로 보호 검사가 실패 하면, Windows Server 2016 즉시 종료 프로그램을 잘못 된 주소를 직접 전화 하려고 하는 모든 악용 중단 됩니다. 플로 보호 제어 Device Guard는 중요 한 추가 보호 계층을 제공합니다. 흰 나열 된 응용 프로그램을 손상 된 경우 수 실행 Device Guard 선택 되지 않도록 하려면 Device Guard 심사를 볼 수 있으므로 응용 프로그램 서명 되지 및 것으로 간주 됩니다 신뢰할 수 있습니다.

하지만 제어 플로 보호 응용 프로그램이 아닌 미리 결정, 실행 불가능 주문에서 실행 되는 여부를 확인할 수, 때문에 공격 실패 하 게, 손상 된 응용 프로그램을 실행 합니다. 함께 이러한 보호 확인 맬웨어 Windows Server 2016에서 실행 중인 소프트웨어에 삽입 하 공격자 매우 어렵습니다.

개발자의 개인 데이터를 처리 되는 응용 프로그램은 해당 응용 프로그램에서 제어 플로 보호 (구성)를 사용 하도록 설정 해야 합니다. 이 기능을 사용할 수 있는 Microsoft Visual Studio 2015 년 하 고 "구성 인식" 버전의 Windows에서 자동으로 실행 등의 x86와 x64 데스크톱 및 Windows 10 및 Windows 8.1 Update (KB3000850). 코드를의 모든 부분에 대 한 구성 구성 함께 사용 하도록 설정 하 고 구성 사용 하도록 설정 하지 않은 코드가 제대로 실행 됩니다 활성화 필요가 없습니다. 하지만 구성 모든 코드를 사용 하도록 설정 하지 보호의 간격을 열 수 있습니다. 또한 구성 코드가 작동 하는 잘 "구성 인식 하지 못하는" 버전의 Windows에서 사용할 수 이므로 완전히 호환 됩니다.

#### <a name="windows-defender-antivirus"></a>Windows Defender 바이러스 백신
Windows Server 2016 산업 선도적인, 현재 감지 기능을 Windows Defender 알려진된 맬웨어를 차단 하는 포함 됩니다. Windows Defender 바이러스 백신 (AV) 서버에 설치 되지 않도록 어떤 종류의 악성 코드 방지 하기 위해 Windows Defender Device Guard 및 제어 플로 보호와 함께 작동 합니다. 기본적으로 켜져 – 관리자가 작동을 시작 하기 위해 어떤 조치도 취할 필요가 없습니다. Windows Server 2016에는 다양 한 서버 역할을 지원 하기 위해 Windows Defender AV 최적화도 됩니다. 과거에는 공격자 PowerShell 같은 셸 사용 되는 이진 악성 코드를 시작 합니다. Windows Server 2016 PowerShell은 코드를 시작 하기 전에 맬웨어를 검사 하려면 Windows Defender AV 통합 되었습니다.

Windows Defender AV 데스크톱, 노트북, 서버에 대 한 보안 및 맬웨어 방지 관리 기능을 제공 하는 기본 제공 맬웨어 방지 해결 방법입니다. Windows 8에 도입 된 후 Windows Defender AV 크게 향상 되었습니다. Windows Server에서 Windows Defender 바이러스 백신 다채로운 pronged 방법은 맬웨어 방지 프로그램을 개선 하기 위해 사용 합니다.

- **클라우드 제공 보호** 는 검색 및 맬웨어 사용한 적 하기 전에 하는 경우에 초 내 새로운 맬웨어를 차단 합니다.

- **다양 한 지역 상황에 맞는** 맬웨어를 식별 하는 방법을 개선 합니다. Windows Server 아니라 파일 및 프로세스 뿐만 아니라 콘텐츠 사진이에서 위치 저장 된, 같은 콘텐츠와 등에 대 한 Windows Defender AV 알립니다. 

- **전 세계 다양 한 센서** 강화할 Windows Defender AV 현재도 최신 맬웨어를 인식 합니다. 두 가지 방법으로 이렇게: 끝점에서 풍부한 로컬 상황에 맞는 데이터를 수집 하 고 중앙 해당 데이터를 분석 하 여 합니다.

- **맞춤법 조작** 맬웨어 공격 으로부터 자체 Windows Defender AV를 보호 하는 데 도움이 됩니다. 예를 들어, Windows Defender AV 신뢰할 수 없는 프로세스 고 Windows Defender AV 구성 요소, 그 레지스트리 키를 조작 하려고 수 없도록 보호 된 프로세스를 사용 합니다.

- **엔터프라이즈 수준 기능** 도구 및 Windows Defender AV 엔터프라이즈급 antimalware 솔루션을 만드는 데 필요한 구성 옵션 IT 전문가 제공 합니다.

#### <a name="enhanced-security-auditing"></a>강화 된 보안 감사 
Windows Server 2016 적극적으로 경고를 더 빠르게 공격에 사용할 수 있는 더 자세한 정보를 제공 하는 강화 된 보안 감사 잠재적인 위반 시도에 관리자 검색 및 법적 분석 합니다. 제어 플로 보호, Windows Defender Device Guard 및 시스템 위험에 노출 될 수를 확인 하려면 관리자 쉽게 한 위치에서 다른 보안 기능 이벤트를 기록 합니다.

새 이벤트 범주 다음과 같습니다.

- **감사 그룹 구성원 합니다.** 감사 그룹 구성원 토큰 정보에는 사용자의 로그인 수 있습니다. 이벤트 그룹 구성원은 열거 또는 로그인 세션 생성 되었습니다 PC에서 쿼리 때 생성 됩니다. 
 
- **PnP 활동에 감사 합니다.** 플러그 and 플레이 감지 맬웨어를 포함 될 수 있는 외부 디바이스-감사 수 있습니다. 시스템 하드웨어 변경 추적할 PnP 이벤트를 사용할 수 있습니다. 하드웨어 Id 공급 업체 목록이 이벤트에 포함 되어 있습니다.

Windows Server 2016 쉽게 <DICT__Microsoft Operations Management Suite>Microsoft Operations 관리 Suite와 같은 보안 인시던트 이벤트 (SIEM) 관리 시스템 통합 < / DICT__Microsoft Operations Management Suite > (OMS) 인텔리전스에 정보를 통합할 수 있는 잠재적 위험에 보고 합니다. 향상 된 감사 제공한 정보 깊이 보안 팀을 식별 하 고 더 빠르고 효율적인 잠재적 위험에 응답할 수 있습니다.

### <a name="secure-virtualization"></a>보안 virtualization
오늘 기업을 가상화 모든 Active Directory 도메인 컨트롤러에 SharePoint SQL Server에서에서 수행할 수 있습니다. Vm (가상 컴퓨터) 간단 하 게 쉽게 배포 서비스를 관리 및 자동화 인프라에 있습니다. 손상 된 virtualization 패브릭 하는 것은 매우 어렵습니다 –에 대 한 새로운 공격 되었을 관련해 서 보안을 하지만 지금까지 합니다. GDPR 관점에서 VM TPM 기술 사용 하 여 실제 서버 보호 것 처럼 Vm 보호 고려해 야 합니다.

Windows Server 2016 어떻게 기업 수 있는 보안 가상화, 가상 컴퓨터에서 실행 되는 직접 만들 수 있도록 하는 여러 기술을 포함 하 여 기본적으로 변경 패브릭; 저장, 네트워크 및 호스트 디바이스에서 실행 로부터 보호할 수 있습니다.

#### <a name="shielded-virtual-machines"></a>가상 컴퓨터 차폐
가상 컴퓨터 하므로 쉽게 마이그레이션 수 있도록 같은 내용이 백업과 복제, 또한 쉽게 수정 하 고 복사 합니다. 가상 컴퓨터 파일에만 이므로 저장소, 백업, 또는 다른 곳에 네트워크에서 보호 되지 않습니다. 다른 문제 패브릭 관리자 – 하는지 여부 메모리 관리자 또는 네트워크 관리자 인 모든 가상 컴퓨터에 대 한 액세스 것입니다.

손상 된 관리자 패브릭에 쉽게 가상 컴퓨터에서 손상 된 데이터에 발생할 수 있습니다. 손상 된 자격 증명을 사용 하 여 어떤 VM 파일을 복사 하는 USB 드라이브 같은 안내 하 고 조직에서 다른 시스템에서 해당 VM 파일에 액세스할 수 있는 공격자 작업을 수행 해야 됩니다. 이러한 도난당된 Vm 중 하나 Active Directory 도메인 컨트롤러를 예를 들어, 공격자 수 쉽게 콘텐츠를 보려면 하는 경우 기술을 사용 하 여 사용할 수 있도록 무작위 Active Directory 데이터베이스에 암호를 해독 결국 액세스 권한을 부여 다른 곳에 인프라 이내입니다.

Windows Server 2016 설명한 것 처럼 보호 Vm (가상 컴퓨터 보호) 시나리오 로부터 보호를 소개 합니다. 차폐 Vm BitLocker 암호화 가상 컴퓨터에 적용 되 고 신뢰할 수 있는 호스트 손상된 저장소, 네트워크 및 호스트 관리자 로부터 보호 하기 위해에 대해서만 실행 수 있도록 가상 TPM 장치를 포함 합니다. 차폐 Vm UEFI Unified Extensible Firmware Interface () 펌웨어를 지원 하며 가상 TPM는 생성 2 Vm를 사용 하 여 만들어집니다.

#### <a name="host-guardian-service"></a>보호자 서비스 호스트
Vm 보호와 함께 호스트 보호자 서비스 안전한 virtualization 패브릭을 만들기 위한 필수 구성 요소입니다. 일 전에 보호 VM 부팅 또는 호스트 하 게 마이그레이션하 두면 Hyper-v 호스트 건강 증명할 하는 것입니다. 키 Vm 보호에 대해 보유 하 고 보안 건강이 보장 될 때까지 해제 하지 않습니다. Hyper-v 호스트 증명할 호스트 보호자 서비스를 요청할 수 있는 두 가지입니다.

첫 번째 및 가장 안전한 하드웨어 신뢰할 수 있는 대입니다. 이 해결 방법에는 TPM 2.0 칩 및 UEFI 2.3.1 호스트에서 보호 Vm 실행 되 고 있는지 필요 합니다. 계획된 부팅을 제공 하기 위해이 하드웨어가 필요 및 운영 체제 커널 무결성 정보 호스트 보호자 서비스에서 Hyper-v 호스트 하도록 요구 하지 손상 되었습니다.

IT 조직에는 TPM 2.0 하드웨어 조직에는 사용 하지 않는 것이 좋습니다 될 수도 있는 관리자 신뢰할 수 있는 대를 사용 하는 방법도 합니다. 이 증명 모델은 쉽게 호스트 보안 그룹에 배치 간단 하 게 호스트 보호자 서비스 보호 Vm 보안 그룹의 회원 호스트에서 실행할 수 있도록 구성 되어 하기 때문에 배포할 수 있습니다. 이 방법으로 없이 복잡 한 측정 호스트 컴퓨터와 조작 되지 않았는지 확인 하는 합니다. 하지만 도보 Vm 도어에 USB 드라이브 또는 VM 무단된 호스트에서 실행할 수 있다는 것 암호화 되지 않은 가능성을 제거지 않습니다. 즉, VM 파일 이외의 지정된 그룹의 모든 시스템에서 실행 되지 않습니다. TPM 2.0 하드웨어 아직 없는 경우에 증명 관리자 신뢰할 수 있는로 시작 하 고로 전환 하 여 증명 하드웨어 신뢰할 수 있는 하드웨어를 업그레이드 수 있습니다.

#### <a name="virtual-machine-trusted-platform-module"></a>가상 컴퓨터 신뢰할 수 있는 플랫폼 모듈
Windows Server 2016 TPM 가상 컴퓨터에 대 한 수 있는 지원 등 BitLocker® 드라이브 암호화 기술을 고급 보안 가상 컴퓨터에서 지원 됩니다. Hyper-v 관리자 또는 Enable-VMTPM Windows PowerShell cmdlet 사용 하 여 모든 생성 2 Hyper-v 가상 컴퓨터가에 TPM 지원을 받을 수 있습니다.

호스트에 저장 또는 호스트 보호자 서비스에 저장 된 지역 암호화 키를 사용 하 여 가상 TPM (vTPM)를 보호할 수 있습니다. 따라서 호스트 보호자 서비스 더 많은 인프라에 필요한 추가 보호는 제공 합니다.

#### <a name="distributed-network-firewall-using-software-defined-networking"></a>분산된 네트워크 방화벽 소프트웨어 정의 된 네트워크를 사용 하 여
보호 가상화 환경에서 개선 하는 방법은 하 고 네트워크 Vm 작동 하는 데 필요한 특정 시스템 말할 수 있게 하는 방식에서입니다. 예를 들어, 응용 프로그램은 인터넷에 연결 하 필요 하지 않은, 경우 있습니다 수 분할 끄고 해당 시스템에서 외부 공격자 대상으로 제거 합니다. Windows Server 2016에 소프트웨어 정의 네트워킹 (SDN) 분산된 네트워크 방화벽을 사용 하 여 응용 프로그램을 보호할 수 있는 보안 정책이 동적으로 만들 수 있도록 포함 내부 또는 외부 네트워크에서 제공한 것임 공격 합니다. 이 분산된 네트워크 방화벽 보안 계층 응용 프로그램에서 네트워크를 분리할 수 있도록 하 여 추가 합니다. 정책은 사용자 가상 네트워크 infrastructure 내용, 격리 VM-to-VM 교통, VM-to-host 교통 또는 VM-to-Internet 교통 – 필요에 따라 여러 서브넷 간에 프로그래밍 방식으로 또는 손상 되었을 수 있는 개별 시스템에 대 한 합니다. 또한 Windows Server 2016 소프트웨어 정의 네트워킹 기능을 통해 라우팅하기 또는 Microsoft 이외의 가상 기기에 들어오는 교통 미러링할 수 있습니다. 예를 들어, Barracuda 가상 기기 추가 스팸 필터링 보호에 대 한 모든 메일 교통 보냅니다 하도록 선택할 수 있습니다. 이렇게 하면 쉽게 계층을의 추가 보안 모두 온-프레미스 또는 클라우드.

### <a name="other-gdpr-considerations-for-servers"></a>서버에 대 한 기타 GDPR 고려
GDPR 포함 명시적 요구 사항에 대 한 개인 데이터를 위반은 의미 위반 알림 "_위반을 실수로 또는 불법적인 소멸, 손실, 변경을, 무단된 공개, 또는에 대 한 액세스, 개인 데이터 보안 전송, 저장 하거나 처리할 합니다. _"  물론, 처음에 위반을 검색할 수 없는 경우 내 72 시간이 지난 후 엄격한 GDPR 알림 요구 사항에 맞게 앞으로 이동 하려면 시작할 수 없습니다.

Windows 보안 센터 흰색 종이에 언급 했 듯이 [게시물 위반: 고급 위협 요소를 다루는](http://wincom.blob.core.windows.net/documents/Post_Breach_Dealing_with_Advanced_Threats_Whitepaper.pdf,)

> "_사전 위반 달리 이후 위반 가정 위반 이미 발생 – 플라이트 레코더 및 범죄 장면 조사 하는 사람 (CSI) 역할을 합니다. 이후 Post-breach 팀 보안 정보를 제공 하 고 도구 세트 필요한를 식별 하기 위해 조사 표시 위아래 그렇지 않은 경우에 발견 하지 유지 됩니다 공격에 응답 합니다. _"

이 섹션의 Windows Server 하는 방법에 GDPR 위반 알림 조항을 준수 하기 살펴보겠습니다. 수집 되 고 사용자에 대 한 분석 하는 Microsoft를 사용할 수 있는 기본 위협 데이터를 이해로 시작 되 고 Windows Defender 고급 위협 보호 <DICT__Windows Defender Advanced Threat Protection>통해 방법 < / DICT__ Windows Defender Advanced Threat Protection > (ATP) 데이터를 사용자에 게 중요 한 될 수 있습니다.

#### <a name="insightful-security-diagnostic-data"></a>있으며 통찰력 보안 진단 데이터
2 년 거의 Microsoft가 되었습니다 위협으로 변환 플랫폼을 강화 하 고 고객을 보호 하도록 도와주는 유용한 인텔리전스 합니다. 오늘, 클라우드에서 제공 하는 거 대 한 컴퓨팅 장점을, 고객을 보호 하기 위해 위협 인텔리전스 의해 우리의 풍부한 분석 엔진을 사용 하는 새로운 방법 찾는 했습니다.

자동 및 수동 프로세스, 기계 학습 및 인간의 전문가의 조합을 적용 하 여 했습니다 수 실시간 자체에서 학습 하 고 발전 하는 지능형 보안 그래프를 만들, 우리의 집합적 시간을 줄일 감지 및에서 새 문제에 대응 제품입니다.

![Microsoft 인텔리전스 보안 그래프](../media/GDPR-Windows-Server-Overview/gdpr-intelligent-security-graph.png)

Microsoft가 위협 인텔리전스 범위에 걸쳐 리터럴로 데이터 요소 수십억: 35 십억 메시지 엔터프라이즈 1 십억 고객 매월, 검색 및 액세스 200 + 소비자 세그먼트 클라우드 서비스 및 십억 14 인증이 수행 매일 합니다. 이 데이터를 모두 받아볼 보안을 유지 생산성을 유지 하 고 있는 GDPR의 요구 사항을 충족 하 동적 방식으로 보호 하는 데 도움이 되는 지능형 보안 그래프를 만들 하기 위해 Microsoft가 사용자를 대신 하 여 함께 가져와서 됩니다.

#### <a name="detecting-attacks-and-forensic-investigation"></a>법적 조사 하 고 공격 검색
더 정교 하 고 대상으로 지정 될 cyberattacks 끝점 방어 최상의 결국 위반 될 수 있습니다. 두 개의 기능 잠재적인 위반 검색-Windows Defender Advanced Threat Protection (ATP) 및 Microsoft에 대 한 도움말 데 사용할 수 있습니다. 고급 위협 분석 (ATA)입니다.

Windows Defender Advanced Threat Protection (ATP)를 통해 검색 조사 하 고 고급 공격 하 고 네트워크에 데이터 위반에 응답할 수 있습니다. 데이터 위반 유형의 GDPR 기대 지속적인 기밀성, 무결성 및 개인 정보 및 처리 시스템의 사용 가능성 되도록 기술적 보안 조치를 통해 로부터 보호할 수 있습니다.

Windows Defender ATP의 주요 이점 간에 다음과 같습니다.

- **검색 하 여 검색할 수 없는 있습니다.** 모든 Microsoft 서비스를 통해 운영 체제 커널, Windows 보안 전문가 및 십억 1 컴퓨터와 신호 개 고유한 광학 깊숙이 기본 센서 합니다.

- **하지에 결합 되어 있습니다.** 에이전트가 고성능 및 영향을 최소화, 클라우드 기반입니다. 없이 배포를 쉽게 관리 합니다. 

- **Windows 보안에 대 한 유리 개의 창을 합니다.** Windows Defender ATP, Windows Defender 바이러스 백신 및 Windows Defender Device Guard 통합 보안 이벤트가 풍부 기계-시간 표시 막대의 6 개월을 살펴보세요.

- **Microsoft 그래프 전원 합니다.** Office 365 ATP 구독을 다시 추적 하 고 공격에 응답을 감지 하 고 exploration 통합 하는 Microsoft 인텔리전스 보안 그래프를 활용 합니다.

자세한 내용을 [Windows Defender ATP 크리에이터 업데이트 preview에서 새로운](https://blogs.microsoft.com/microsoftsecure/2017/03/13/whats-new-in-the-windows-defender-atp-creators-update-preview/)합니다.

ATA 조직에서 신원을 손상을 감지 하는 데 도움이 되는 온-프레미스 제품입니다. ATA 캡처하고 네트워크 교통 인증, 권한 및 정보 수집 (예: Kerberos, DNS, RPC, NTLM 및 기타 프로토콜) 프로토콜에 대 한 분석 수 있습니다. 이 데이터를 사용 하 여 예외 및 알려진된 공격 패턴을 검색할 수 있도록 네트워크에 사용자는 기타 기관과 대 한 행동 프로필을 만드는 데 ATA 합니다. 다음 표에 ATA에서 감지 공격 형식 있습니다.


|공격 유형 |설명 |
|---------|---------|
|악의적인 공격 |이러한 공격 공격을 포함 하 여 공격이 형식의 알려진된 목록에서 검색 하 여 검색는 다음과 같습니다.<ul><li>Pass the-티켓 (PtT)</li><li>단계-the-해시 (PtH)</li><li>The 해시 고가로</li><li>위조 PAC (MS14 068)</li><li>황금 티켓</li><li>악의적인 복제</li><li>검사</li><li>무작위</li><li>원격 실행</li></ul>감지할 수 있는 악의적인 공격의 전체 목록 및 설명 참조 [무엇 의심 스러운 활동 수 ATA 감지?](https://docs.microsoft.com/en-us/advanced-threat-analytics/understand-explore/ata-threats).|
|비정상적인 문제 |이러한 공격 행동 분석을 사용 하 여 검색 하 고 의심 스러운 활동을 비롯 한 사용자의 신원을 확인 하는 컴퓨터 사용 합니다.<ul><li>비정상적인 로그인</li><li>알 수 없는 위협</li><li>암호를 공유</li><li>긴 움직임</li></ul>|
|보안 문제 및 위험 |현재 네트워크 및 시스템 구성에 확인 하 여 이러한 공격 내용이 포함 하 여 다음과 같습니다.<ul><li>끊어진된 보안</li><li>약한 프로토콜</li><li>프로토콜 알려진된 문제</li></ul>|

권한 신원을 손상 하려고 할 때 공격자 발견할 수 있도록 ATA 사용할 수 있습니다. ATA 배포에 대 한 자세한 내용은 요금제, 디자인 및 배포 항목을 참조는 [위협 분석 고급 설명서](https://docs.microsoft.com/en-us/advanced-threat-analytics/)합니다.

## <a name="related-content-for-associated-windows-server-2016-solutions"></a>Windows Server 2016 솔루션을 연결된에 대 한 콘텐츠 관련된

- **Windows Defender 바이러스 백신:** https://www.youtube.com/watch?v=P1aNEy09NaI 및 https://docs.microsoft.com/en-us/windows/threat-protection/windows-defender-antivirus/windows-defender-antivirus-in-windows-10

- **Windows Defender Advanced Threat Protection:** https://www.youtube.com/watch?v=qxeGa3pxIwg 및 https://docs.microsoft.com/en-us/windows/threat-protection/windows-defender-atp/configure-server-endpoints-windows-defender-advanced-threat-protection

- **Windows Defender Device Guard:** https://www.youtube.com/watch?v=F-pTkesjkhI 및 https://docs.microsoft.com/en-us/windows/device-security/device-guard/device-guard-deployment-guide

- **Windows Defender Credential Guard:** https://www.youtube.com/watch?v=F-pTkesjkhI 및 https://docs.microsoft.com/en-us/windows/access-protection/credential-guard/credential-guard

- **제어 흐름 보호:** https://msdn.microsoft.com/en-us/library/windows/desktop/mt637065(v=vs.85).aspx

- **보안 및 보증:** https://docs.microsoft.com/en-us/windows-server/security/security-and-assurance

## <a name="disclaimer"></a>고 지 사항
이 문서는 Microsoft를 출판 일을 기준으로 해석으로 GDPR에 설명 합니다. 많은 GDPR 시간 소모한 하 고 해당 의도 및 의미에 대해 진심으 감사 받았습니다 여러분의 생각을 합니다. 하지만 GDPR의 응용 프로그램은 매우 사실 전용 되며 일부 측면과 GDPR의 해석 잘 settled 수 있습니다.

결과적으로,이 문서 정보 제공 목적 으로만 제공 하 고 해야 주려는 법적 조언을 또는 결정 하 고 조직에 GDPR 어떻게 적용 될 수 있습니다. 조직에만 적용 방식 및 방법에 대해 토론 GDPR, 합법적 한정 전문가 함께 작동 하도록 주십시오 준수 하는 가장 좋은 합니다.

MICROSOFT는, 암시적 또는 법적인이 문서의 보증도 하지 않습니다. 이 문서는 제공 "로-입니다." URL 및 기타 인터넷 사이트 참조가이 문서에 표시 된 뷰 및 정보 통지 없이 변경 될 수 있습니다.

이 문서 지적 속성 Microsoft 제품에 대 한 모든 법적 권한이 있는 사용자을 제공 하지 않습니다.  복사 하 여 참조만 목적 사용자는 내부적인이 문서를 사용할 수 있습니다.  

2017 년 9 월 게시합니다.<br>
버전 1.0<br>
© 2017 Microsoft 합니다. 모든 권리를 보유 합니다.


