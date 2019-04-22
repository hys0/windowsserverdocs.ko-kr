---
title: QoS 정책 오류 및 이벤트 메시지
description: 이 항목에서는 Windows Server 2016의 서비스 품질 (QoS) 정책에 대 한 오류 및 이벤트 메시지의 목록을 제공합니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 76974e10-6a57-4533-83be-cfd5a0d364a3
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 774d9473beed1da861c6827357710133aeaca15e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59824054"
---
# <a name="qos-policy-error-and-event-messages"></a>QoS 정책 오류 및 이벤트 메시지

>적용 대상: Windows Server (반기 채널), Windows Server 2016

다음은 QoS 정책과 관련 된 오류 및 이벤트 메시지입니다.  
  
## <a name="informational-messages"></a>정보 메시지  

다음은 QoS 정책 정보 메시지의 목록입니다.

|||  
|-|-|  
|**MessageId**|16500|  
|**Severity**|정보|  
|**SymbolicName**|EVENT_EQOS_INFO_MACHINE_POLICY_REFRESH_NO_CHANGE|  
|**언어**|영어|  
|**메시지**|컴퓨터 QoS 정책을 새로 고쳤습니다. 변경 내용이 없습니다.|  
  
|||  
|-|-|  
|**MessageId**|16501|  
|**Severity**|정보|  
|**SymbolicName**|EVENT_EQOS_INFO_MACHINE_POLICY_REFRESH_WITH_CHANGE|  
|**언어**|영어|  
|**메시지**|컴퓨터 QoS 정책을 새로 고쳤습니다. 정책이 변경 되었습니다.|  
  
|||  
|-|-|  
|**MessageId**|16502|  
|**Severity**|정보|  
|**SymbolicName**|EVENT_EQOS_INFO_USER_POLICY_REFRESH_NO_CHANGE|  
|**언어**|영어|  
|**메시지**|사용자 QoS 정책을 새로 고쳤습니다. 변경 내용이 없습니다.|  
  
|||  
|-|-|  
|**MessageId**|16503|  
|**Severity**|정보|  
|**SymbolicName**|EVENT_EQOS_INFO_USER_POLICY_REFRESH_WITH_CHANGE|  
|**언어**|영어|  
|**메시지**|사용자 QoS 정책을 새로 고쳤습니다. 정책이 변경 되었습니다.|  
  
|||  
|-|-|  
|**MessageId**|16504|  
|**Severity**|정보|  
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_NOT_CONFIGURED|  
|**언어**|영어|  
|**메시지**|인바운드 TCP 처리량 수준에 대 한 고급 QoS 설정을 새로 고쳤습니다. 값 설정 QoS 정책에서 지정 하지 않았습니다. 로컬 컴퓨터 기본 적용 됩니다.|  
  
|||  
|-|-|  
|**MessageId**|16505|  
|**Severity**|정보|  
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_OFF|  
|**언어**|영어|  
|**메시지**|인바운드 TCP 처리량 수준에 대 한 고급 QoS 설정을 새로 고쳤습니다. 수준 0 (최소 처리량)는 값을 설정 합니다.|  
  
|||  
|-|-|  
|**MessageId**|16506|  
|**Severity**|정보|  
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_HIGHLY_RESTRICTED|  
|**언어**|영어|  
|**메시지**|인바운드 TCP 처리량 수준에 대 한 고급 QoS 설정을 새로 고쳤습니다. 값을 설정 하는 것은 수준 1입니다.|  
  
|||  
|-|-|  
|**MessageId**|16507|  
|**Severity**|정보|  
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_RESTRICTED|  
|**언어**|영어|  
|**메시지**|인바운드 TCP 처리량 수준에 대 한 고급 QoS 설정을 새로 고쳤습니다. 값을 설정 하는 것은 수준 2입니다.|  
  
|||  
|-|-|  
|**MessageId**|16508|  
|**Severity**|정보|  
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_NORMAL|  
|**언어**|영어|  
|**메시지**|인바운드 TCP 처리량 수준에 대 한 고급 QoS 설정을 새로 고쳤습니다. 수준 3 (최대 처리량)는 값을 설정 합니다.|  
  
|||  
|-|-|  
|**MessageId**|16509|  
|**Severity**|정보|  
|**SymbolicName**|EVENT_EQOS_INFO_APP_MARKING_NOT_CONFIGURED|  
|**언어**|영어|  
|**메시지**|새로 고침 성공 DSCP 표시에 대 한 고급 QoS 설정 보다 우선합니다. 값 설정 지정 하지 않았습니다. 응용 프로그램 QoS 정책 독립적으로 DSCP 값을 설정할 수 있습니다.|  
  
|||  
|-|-|  
|**MessageId**|16510|  
|**Severity**|정보|  
|**SymbolicName**|EVENT_EQOS_INFO_APP_MARKING_IGNORED|  
|**언어**|영어|  
|**메시지**|새로 고침 성공 DSCP 표시에 대 한 고급 QoS 설정 보다 우선합니다. 응용 DSCP 표시 요청이 무시 됩니다. QoS 정책에 대 한 DSCP 값을 설정할 수 있습니다.|  
  
|||  
|-|-|  
|**MessageId**|16511|  
|**Severity**|정보|  
|**SymbolicName**|EVENT_EQOS_INFO_APP_MARKING_ALLOWED|  
|**언어**|영어|  
|**메시지**|새로 고침 성공 DSCP 표시에 대 한 고급 QoS 설정 보다 우선합니다. 응용 프로그램 QoS 정책 독립적으로 DSCP 값을 설정할 수 있습니다.|  
  
|||  
|-|-|  
|**MessageId**|16512|  
|**Severity**|정보|  
|**SymbolicName**|EVENT_EQOS_INFO_LOCAL_SETTING_DONT_USE_NLA|  
|**언어**|영어|  
|**메시지**|도메인 네트워크 범주를 기반으로 QoS 정책의 선택적 응용 프로그램에 더 이상 사용 되지 않습니다. QoS 정책과 모든 네트워크 인터페이스에 적용 됩니다.|  
  
## <a name="warning-messages"></a>경고 메시지

다음은 QoS 정책 경고 메시지의 목록입니다.

|||  
|-|-|  
|**MessageId**|16600|  
|**Severity**|경고|  
|**SymbolicName**|EVENT_EQOS_WARNING_TEST_1|  
|**언어**|영어|  
|**메시지**|EQOS: * * * 테스트\*\*\*[에 문자열 하나를 사용 하 여] "%2".|  
  
|||  
|-|-|  
|**MessageId**|16601|  
|**Severity**|경고|  
|**SymbolicName**|EVENT_EQOS_WARNING_TEST_2|  
|**언어**|영어|  
|**메시지**|EQOS: * * * 테스트\*\*\*[, string1이 두 문자열을 사용 하 여] "%2" [, string2가] "%3".|  
  
|||  
|-|-|  
|**MessageId**|16602|  
|**Severity**|경고|  
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_VERSION|  
|**언어**|영어|  
|**메시지**|컴퓨터 QoS 정책을 "%2"에 잘못 된 버전 번호가 있습니다. 이 정책이 적용 되지 않습니다.|  
  
|||  
|-|-|  
|**MessageId**|16603|  
|**Severity**|경고|  
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_VERSION|  
|**언어**|영어|  
|**메시지**|사용자 "%2" QoS 정책에 잘못 된 버전 번호가 있습니다. 이 정책이 적용 되지 않습니다.|  
  
|||  
|-|-|  
|**MessageId**|16604|  
|**Severity**|경고|  
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_PROFILE_NOT_SPECIFIED|  
|**언어**|영어|  
|**메시지**|컴퓨터 "%2" QoS 정책을 DSCP 값 또는 스로틀 속도 지정 하지 않습니다. 이 정책이 적용 되지 않습니다.|  
  
|||  
|-|-|  
|**MessageId**|16605|  
|**Severity**|경고|  
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_PROFILE_NOT_SPECIFIED|  
|**언어**|영어|  
|**메시지**|사용자 "%2" QoS 정책을 DSCP 값 또는 스로틀 속도 지정 하지 않습니다. 이 정책이 적용 되지 않습니다.|  
  
|||  
|-|-|  
|**MessageId**|16606|  
|**Severity**|경고|  
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_QUOTA_EXCEEDED|  
|**언어**|영어|  
|**메시지**|컴퓨터 QoS 정책의 최대 수를 초과 합니다. QoS 정책 "%2" 및 후속 컴퓨터 QoS 정책이 적용 되지 않습니다.|  
  
|||  
|-|-|  
|**MessageId**|16607|  
|**Severity**|경고|  
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_QUOTA_EXCEEDED|  
|**언어**|영어|  
|**메시지**|사용자 QoS 정책의 최대 수를 초과 합니다. QoS 정책 "%2" 및 후속 사용자 QoS 정책이 적용 되지 않습니다.|  
  
|||  
|-|-|  
|**MessageId**|16608|  
|**Severity**|경고|  
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_CONFLICT|  
|**언어**|영어|  
|**메시지**|컴퓨터 "%2" QoS 정책을 다른 QoS 정책을 사용 하 여 잠재적으로 충돌합니다. 에 대 한 정책이 적용 되는 규칙에 대 한 설명서를 참조 하세요.|  
  
|||  
|-|-|  
|**MessageId**|16609|  
|**Severity**|경고|  
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_CONFLICT|  
|**언어**|영어|  
|**메시지**|사용자 "%2" QoS 정책을 다른 QoS 정책을 사용 하 여 잠재적으로 충돌합니다. 에 대 한 정책이 적용 되는 규칙에 대 한 설명서를 참조 하세요.|  
  
|||  
|-|-|  
|**MessageId**|16610|  
|**Severity**|경고|  
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_NO_FULLPATH_APPNAME|  
|**언어**|영어|  
|**메시지**|컴퓨터 "%2" QoS 정책을 응용 프로그램 경로 처리할 수 없으므로 무시 되었습니다. 응용 프로그램 경로 유효 하지 않게 될 수 있습니다, 그리고는 잘못 된 드라이브 문자를 포함 또는 매핑된 네트워크 드라이브를 포함 합니다.|  
  
|||  
|-|-|  
|**MessageId**|16611|  
|**Severity**|경고|  
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_NO_FULLPATH_APPNAME|  
|**언어**|영어|  
|**메시지**|QoS 정책을 "%2" 사용자는 응용 프로그램 경로 처리할 수 없으므로 무시 되었습니다. 응용 프로그램 경로 유효 하지 않게 될 수 있습니다, 그리고는 잘못 된 드라이브 문자를 포함 또는 매핑된 네트워크 드라이브를 포함 합니다.|  
  
## <a name="error-messages"></a>오류 메시지  

다음은 QoS 정책 오류 메시지의 목록입니다.

|||  
|-|-|  
|**MessageId**|16700|  
|**Severity**|Error|  
|**SymbolicName**|EVENT_EQOS_ERROR_MACHINE_POLICY_REFERESH|  
|**언어**|영어|  
|**메시지**|컴퓨터 QoS 정책을 새로 고치지 못했습니다. 오류 코드: "%2".|  
  
|||  
|-|-|  
|**MessageId**|16701|  
|**Severity**|Error|  
|**SymbolicName**|EVENT_EQOS_ERROR_USER_POLICY_REFERESH|  
|**언어**|영어|  
|**메시지**|사용자 QoS 정책을 새로 고치지 못했습니다. 오류 코드: "%2".|  
  
|||  
|-|-|  
|**MessageId**|16702|  
|**Severity**|Error|  
|**SymbolicName**|EVENT_EQOS_ERROR_OPENING_MACHINE_POLICY_ROOT_KEY|  
|**언어**|영어|  
|**메시지**|QoS는 QoS 정책에 대 한 컴퓨터 수준 루트 키를 열지 못했습니다. 오류 코드: "%2".|  
  
|||  
|-|-|  
|**MessageId**|16703|  
|**Severity**|Error|  
|**SymbolicName**|EVENT_EQOS_ERROR_OPENING_USER_POLICY_ROOT_KEY|  
|**언어**|영어|  
|**메시지**|QoS는 QoS 정책에 대 한 사용자 수준 루트 키를 열지 못했습니다. 오류 코드: "%2".|  
  
|||  
|-|-|  
|**MessageId**|16704|  
|**Severity**|Error|  
|**SymbolicName**|EVENT_EQOS_ERROR_MACHINE_POLICY_KEYNAME_TOO_LONG|  
|**언어**|영어|  
|**메시지**|QoS 정책을 사용 하는 컴퓨터에 허용 된 최대 이름 길이 초과합니다. 잘못 된 정책 컴퓨터 수준 QoS 정책 루트 키 인덱스 "%2"를 사용 하 여 아래에 나열 됩니다.|  
  
|||  
|-|-|  
|**MessageId**|16705|  
|**Severity**|Error|  
|**SymbolicName**|EVENT_EQOS_ERROR_USER_POLICY_KEYNAME_TOO_LONG|  
|**언어**|영어|  
|**메시지**|QoS 정책을 사용자에 허용 된 최대 이름 길이 초과합니다. 잘못 된 정책-사용자 수준 QoS 정책 루트 키 인덱스 "%2"를 사용 하 여 아래에 나열 됩니다.|  
  
|||  
|-|-|  
|**MessageId**|16706|  
|**Severity**|Error|  
|**SymbolicName**|EVENT_EQOS_ERROR_MACHINE_POLICY_KEYNAME_SIZE_ZERO|  
|**언어**|영어|  
|**메시지**|QoS 정책을 사용 하는 컴퓨터에 길이가 0 인 이름이 있습니다. 잘못 된 정책 컴퓨터 수준 QoS 정책 루트 키 인덱스 "%2"를 사용 하 여 아래에 나열 됩니다.|  
  
|||  
|-|-|  
|**MessageId**|16707|  
|**Severity**|Error|  
|**SymbolicName**|EVENT_EQOS_ERROR_USER_POLICY_KEYNAME_SIZE_ZERO|  
|**언어**|영어|  
|**메시지**|QoS 정책을 사용자에는 길이가 0 인 이름이 있습니다. 잘못 된 정책-사용자 수준 QoS 정책 루트 키 인덱스 "%2"를 사용 하 여 아래에 나열 됩니다.|  
  
|||  
|-|-|  
|**MessageId**|16708|  
|**Severity**|Error|  
|**SymbolicName**|EVENT_EQOS_ERROR_OPENING_MACHINE_POLICY_SUBKEY|  
|**언어**|영어|  
|**메시지**|QoS는 QoS 정책 사용 하는 컴퓨터에 대 한 레지스트리 하위 키를 열지 못했습니다. 정책을은 컴퓨터 수준 QoS 정책 루트 키 인덱스 "%2"를 사용 하 여 아래에 나열 됩니다.|  
  
|||  
|-|-|  
|**MessageId**|16709|  
|**Severity**|Error|  
|**SymbolicName**|EVENT_EQOS_ERROR_OPENING_USER_POLICY_SUBKEY|  
|**언어**|영어|  
|**메시지**|QoS는 QoS 정책 사용자에 대 한 레지스트리 하위 키를 열지 못했습니다. 정책-사용자 수준 QoS 정책 루트 키 인덱스 "%2"를 사용 하 여 아래에 나열 됩니다.|  
  
|||  
|-|-|  
|**MessageId**|16710|  
|**Severity**|Error|  
|**SymbolicName**|EVENT_EQOS_ERROR_PROCESSING_MACHINE_POLICY_FIELD|  
|**언어**|영어|  
|**메시지**|QoS 읽거나 컴퓨터 QoS 정책 "%3"에 대 한 "%2" 필드의 유효성을 검사 하지 못했습니다.|  
  
|||  
|-|-|  
|**MessageId**|16711|  
|**Severity**|Error|  
|**SymbolicName**|EVENT_EQOS_ERROR_PROCESSING_USER_POLICY_FIELD|  
|**언어**|영어|  
|**메시지**|QoS 읽거나 QoS 정책 "%3" 사용자 "%2" 필드의 유효성을 검사 하지 못했습니다.|  
  
|||  
|-|-|  
|**MessageId**|16712|  
|**Severity**|Error|  
|**SymbolicName**|EVENT_EQOS_ERROR_SETTING_TCP_AUTOTUNING|  
|**언어**|영어|  
|**메시지**|QoS 읽거나 인바운드 TCP 처리량 수준에서 오류 코드를 설정 하지 못했습니다: "%2".|  
  
|||  
|-|-|  
|**MessageId**|16713|  
|**Severity**|Error|  
|**SymbolicName**|EVENT_EQOS_ERROR_SETTING_APP_MARKING|  
|**언어**|영어|  
|**메시지**|QoS 읽거나 DSCP 표시를 설정 하지 못했습니다 오류 코드 설정을 재정의: "%2".|  

이 가이드의 다음 항목을 참조 하세요 [QoS 정책 Frequently Asked Questions](qos-policy-faq.md)합니다.

이 가이드의 첫 번째 항목을 참조 하세요 [의 QoS (서비스 품질) 정책을](qos-policy-top.md)합니다.
