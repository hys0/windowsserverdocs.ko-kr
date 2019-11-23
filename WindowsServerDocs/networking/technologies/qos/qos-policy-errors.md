---
title: QoS 정책 오류 및 이벤트 메시지
description: 이 항목에서는 Windows Server 2016의 QoS (서비스 품질) 정책에 대 한 오류 및 이벤트 메시지 목록을 제공 합니다.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 76974e10-6a57-4533-83be-cfd5a0d364a3
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 935bda5ab47f3e9a362c81a8aeb99ebf22095725
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405329"
---
# <a name="qos-policy-error-and-event-messages"></a>QoS 정책 오류 및 이벤트 메시지

>적용 대상: Windows Server(반기 채널), Windows Server 2016

다음은 QoS 정책과 관련 된 오류 및 이벤트 메시지입니다.  
  
## <a name="informational-messages"></a>정보 메시지  

다음은 QoS 정책 정보 메시지의 목록입니다.

|||  
|-|-|  
|**있어**|16500|  
|**Severity**|정보|  
|**SymbolicName**|EVENT_EQOS_INFO_MACHINE_POLICY_REFRESH_NO_CHANGE|  
|**언어**|영어|  
|**메시지**|컴퓨터 QoS 정책을 새로 고쳤습니다. 변경 내용이 검색 되지 않았습니다.|  
  
|||  
|-|-|  
|**있어**|16501|  
|**Severity**|정보|  
|**SymbolicName**|EVENT_EQOS_INFO_MACHINE_POLICY_REFRESH_WITH_CHANGE|  
|**언어**|영어|  
|**메시지**|컴퓨터 QoS 정책을 새로 고쳤습니다. 정책 변경이 검색 되었습니다.|  
  
|||  
|-|-|  
|**있어**|16502|  
|**Severity**|정보|  
|**SymbolicName**|EVENT_EQOS_INFO_USER_POLICY_REFRESH_NO_CHANGE|  
|**언어**|영어|  
|**메시지**|사용자 QoS 정책을 새로 고쳤습니다. 변경 내용이 검색 되지 않았습니다.|  
  
|||  
|-|-|  
|**있어**|16503|  
|**Severity**|정보|  
|**SymbolicName**|EVENT_EQOS_INFO_USER_POLICY_REFRESH_WITH_CHANGE|  
|**언어**|영어|  
|**메시지**|사용자 QoS 정책을 새로 고쳤습니다. 정책 변경이 검색 되었습니다.|  
  
|||  
|-|-|  
|**있어**|16504|  
|**Severity**|정보|  
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_NOT_CONFIGURED|  
|**언어**|영어|  
|**메시지**|인바운드 TCP 처리량 수준에 대 한 고급 QoS 설정이 성공적으로 새로 고침 되었습니다. 설정 값이 QoS 정책에서 지정 되지 않았습니다. 로컬 컴퓨터 기본값이 적용 됩니다.|  
  
|||  
|-|-|  
|**있어**|16505|  
|**Severity**|정보|  
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_OFF|  
|**언어**|영어|  
|**메시지**|인바운드 TCP 처리량 수준에 대 한 고급 QoS 설정이 성공적으로 새로 고침 되었습니다. 설정 값은 수준 0 (최소 처리량)입니다.|  
  
|||  
|-|-|  
|**있어**|16506|  
|**Severity**|정보|  
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_HIGHLY_RESTRICTED|  
|**언어**|영어|  
|**메시지**|인바운드 TCP 처리량 수준에 대 한 고급 QoS 설정이 성공적으로 새로 고침 되었습니다. 설정 값은 수준 1입니다.|  
  
|||  
|-|-|  
|**있어**|16507|  
|**Severity**|정보|  
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_RESTRICTED|  
|**언어**|영어|  
|**메시지**|인바운드 TCP 처리량 수준에 대 한 고급 QoS 설정이 성공적으로 새로 고침 되었습니다. 설정 값은 수준 2입니다.|  
  
|||  
|-|-|  
|**있어**|16508|  
|**Severity**|정보|  
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_NORMAL|  
|**언어**|영어|  
|**메시지**|인바운드 TCP 처리량 수준에 대 한 고급 QoS 설정이 성공적으로 새로 고침 되었습니다. 설정 값은 수준 3 (최대 처리량)입니다.|  
  
|||  
|-|-|  
|**있어**|16509|  
|**Severity**|정보|  
|**SymbolicName**|EVENT_EQOS_INFO_APP_MARKING_NOT_CONFIGURED|  
|**언어**|영어|  
|**메시지**|DSCP 표시 재정의에 대 한 고급 QoS 설정이 성공적으로 새로 고침 되었습니다. 설정 값이 지정 되지 않았습니다. 응용 프로그램은 QoS 정책과 독립적으로 DSCP 값을 설정할 수 있습니다.|  
  
|||  
|-|-|  
|**있어**|16510|  
|**Severity**|정보|  
|**SymbolicName**|EVENT_EQOS_INFO_APP_MARKING_IGNORED|  
|**언어**|영어|  
|**메시지**|DSCP 표시 재정의에 대 한 고급 QoS 설정이 성공적으로 새로 고침 되었습니다. 응용 프로그램 DSCP 표시 요청은 무시 됩니다. QoS 정책만 DSCP 값을 설정할 수 있습니다.|  
  
|||  
|-|-|  
|**있어**|16511|  
|**Severity**|정보|  
|**SymbolicName**|EVENT_EQOS_INFO_APP_MARKING_ALLOWED|  
|**언어**|영어|  
|**메시지**|DSCP 표시 재정의에 대 한 고급 QoS 설정이 성공적으로 새로 고침 되었습니다. 응용 프로그램은 QoS 정책과 독립적으로 DSCP 값을 설정할 수 있습니다.|  
  
|||  
|-|-|  
|**있어**|16512|  
|**Severity**|정보|  
|**SymbolicName**|EVENT_EQOS_INFO_LOCAL_SETTING_DONT_USE_NLA|  
|**언어**|영어|  
|**메시지**|도메인 네트워크 범주를 기반으로 하는 QoS 정책의 선택적 적용이 사용 하지 않도록 설정 되었습니다. QoS 정책이 모든 네트워크 인터페이스에 적용 됩니다.|  
  
## <a name="warning-messages"></a>경고 메시지

다음은 QoS 정책 경고 메시지의 목록입니다.

|||  
|-|-|  
|**있어**|16600|  
|**Severity**|경고|  
|**SymbolicName**|EVENT_EQOS_WARNING_TEST_1|  
|**언어**|영어|  
|**메시지**|지정 하도록 EQOS: * * * 테스트\*\*\*[, 한 문자열] "%2"이 (가) 있습니다.|  
  
|||  
|-|-|  
|**있어**|16601|  
|**Severity**|경고|  
|**SymbolicName**|EVENT_EQOS_WARNING_TEST_2|  
|**언어**|영어|  
|**메시지**|지정 하도록 EQOS: * * * 테스트\*\*\*[, 두 개의 문자열이 있습니다. 문자열 1은] "%2" [, 문자열 2:] "%3"입니다.|  
  
|||  
|-|-|  
|**있어**|16602|  
|**Severity**|경고|  
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_VERSION|  
|**언어**|영어|  
|**메시지**|컴퓨터 QoS 정책 "%2"의 버전 번호가 잘못 되었습니다. 이 정책은 적용 되지 않습니다.|  
  
|||  
|-|-|  
|**있어**|16603|  
|**Severity**|경고|  
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_VERSION|  
|**언어**|영어|  
|**메시지**|사용자 QoS 정책 "%2"의 버전 번호가 잘못 되었습니다. 이 정책은 적용 되지 않습니다.|  
  
|||  
|-|-|  
|**있어**|16604|  
|**Severity**|경고|  
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_PROFILE_NOT_SPECIFIED|  
|**언어**|영어|  
|**메시지**|컴퓨터 QoS 정책 "%2"이 (가) DSCP 값 또는 스로틀 비율을 지정 하지 않습니다. 이 정책은 적용 되지 않습니다.|  
  
|||  
|-|-|  
|**있어**|16605|  
|**Severity**|경고|  
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_PROFILE_NOT_SPECIFIED|  
|**언어**|영어|  
|**메시지**|사용자 QoS 정책 "%2"이 (가) DSCP 값 또는 스로틀 비율을 지정 하지 않습니다. 이 정책은 적용 되지 않습니다.|  
  
|||  
|-|-|  
|**있어**|16606|  
|**Severity**|경고|  
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_QUOTA_EXCEEDED|  
|**언어**|영어|  
|**메시지**|최대 컴퓨터 QoS 정책 수를 초과 했습니다. QoS 정책 "%2" 및 후속 컴퓨터 QoS 정책이 적용 되지 않습니다.|  
  
|||  
|-|-|  
|**있어**|16607|  
|**Severity**|경고|  
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_QUOTA_EXCEEDED|  
|**언어**|영어|  
|**메시지**|최대 사용자 QoS 정책 수를 초과 했습니다. QoS 정책 "%2" 및 후속 사용자 QoS 정책이 적용 되지 않습니다.|  
  
|||  
|-|-|  
|**있어**|16608|  
|**Severity**|경고|  
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_CONFLICT|  
|**언어**|영어|  
|**메시지**|컴퓨터 QoS 정책 "%2"이 (가) 다른 QoS 정책과 충돌할 수 있습니다. 적용 되는 정책에 대 한 규칙은 설명서를 참조 하세요.|  
  
|||  
|-|-|  
|**있어**|16609|  
|**Severity**|경고|  
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_CONFLICT|  
|**언어**|영어|  
|**메시지**|사용자 QoS 정책 "%2"이 (가) 다른 QoS 정책과 충돌할 수 있습니다. 적용 되는 정책에 대 한 규칙은 설명서를 참조 하세요.|  
  
|||  
|-|-|  
|**있어**|16610|  
|**Severity**|경고|  
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_NO_FULLPATH_APPNAME|  
|**언어**|영어|  
|**메시지**|응용 프로그램 경로를 처리할 수 없기 때문에 컴퓨터 QoS 정책 "%2"이 (가) 무시 되었습니다. 응용 프로그램 경로가 잘못 되었거나, 잘못 된 드라이브 문자를 포함 하거나, 네트워크 매핑된 드라이브를 포함 하 고 있습니다.|  
  
|||  
|-|-|  
|**있어**|16611|  
|**Severity**|경고|  
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_NO_FULLPATH_APPNAME|  
|**언어**|영어|  
|**메시지**|응용 프로그램 경로를 처리할 수 없기 때문에 사용자 QoS 정책 "%2"이 (가) 무시 되었습니다. 응용 프로그램 경로가 잘못 되었거나, 잘못 된 드라이브 문자를 포함 하거나, 네트워크 매핑된 드라이브를 포함 하 고 있습니다.|  
  
## <a name="error-messages"></a>오류 메시지  

다음은 QoS 정책 오류 메시지의 목록입니다.

|||  
|-|-|  
|**있어**|16700|  
|**Severity**|Error|  
|**SymbolicName**|EVENT_EQOS_ERROR_MACHINE_POLICY_REFERESH|  
|**언어**|영어|  
|**메시지**|컴퓨터 QoS 정책을 새로 고치지 못했습니다. 오류 코드: "%2".|  
  
|||  
|-|-|  
|**있어**|16701|  
|**Severity**|Error|  
|**SymbolicName**|EVENT_EQOS_ERROR_USER_POLICY_REFERESH|  
|**언어**|영어|  
|**메시지**|사용자 QoS 정책을 새로 고치지 못했습니다. 오류 코드: "%2".|  
  
|||  
|-|-|  
|**있어**|16702|  
|**Severity**|Error|  
|**SymbolicName**|EVENT_EQOS_ERROR_OPENING_MACHINE_POLICY_ROOT_KEY|  
|**언어**|영어|  
|**메시지**|Qos가 QoS 정책에 대 한 컴퓨터 수준 루트 키를 열지 못했습니다. 오류 코드: "%2".|  
  
|||  
|-|-|  
|**있어**|16703|  
|**Severity**|Error|  
|**SymbolicName**|EVENT_EQOS_ERROR_OPENING_USER_POLICY_ROOT_KEY|  
|**언어**|영어|  
|**메시지**|Qos가 QoS 정책에 대 한 사용자 수준 루트 키를 열지 못했습니다. 오류 코드: "%2".|  
  
|||  
|-|-|  
|**있어**|16704|  
|**Severity**|Error|  
|**SymbolicName**|EVENT_EQOS_ERROR_MACHINE_POLICY_KEYNAME_TOO_LONG|  
|**언어**|영어|  
|**메시지**|컴퓨터 QoS 정책이 허용 되는 최대 이름 길이를 초과 합니다. 잘못 된 정책은 인덱스 "%2"을 (를) 포함 하는 컴퓨터 수준 QoS 정책 루트 키 아래에 나열 됩니다.|  
  
|||  
|-|-|  
|**있어**|16705|  
|**Severity**|Error|  
|**SymbolicName**|EVENT_EQOS_ERROR_USER_POLICY_KEYNAME_TOO_LONG|  
|**언어**|영어|  
|**메시지**|사용자 QoS 정책이 허용 된 최대 이름 길이를 초과 합니다. 잘못 된 정책은 인덱스 "%2"이 (가) 있는 사용자 수준 QoS 정책 루트 키 아래에 나열 됩니다.|  
  
|||  
|-|-|  
|**있어**|16706|  
|**Severity**|Error|  
|**SymbolicName**|EVENT_EQOS_ERROR_MACHINE_POLICY_KEYNAME_SIZE_ZERO|  
|**언어**|영어|  
|**메시지**|컴퓨터 QoS 정책에는 길이가 0 인 이름이 있습니다. 잘못 된 정책은 인덱스 "%2"을 (를) 포함 하는 컴퓨터 수준 QoS 정책 루트 키 아래에 나열 됩니다.|  
  
|||  
|-|-|  
|**있어**|16707|  
|**Severity**|Error|  
|**SymbolicName**|EVENT_EQOS_ERROR_USER_POLICY_KEYNAME_SIZE_ZERO|  
|**언어**|영어|  
|**메시지**|사용자 QoS 정책에 길이가 0 인 이름이 있습니다. 잘못 된 정책은 인덱스 "%2"이 (가) 있는 사용자 수준 QoS 정책 루트 키 아래에 나열 됩니다.|  
  
|||  
|-|-|  
|**있어**|16708|  
|**Severity**|Error|  
|**SymbolicName**|EVENT_EQOS_ERROR_OPENING_MACHINE_POLICY_SUBKEY|  
|**언어**|영어|  
|**메시지**|QoS가 컴퓨터 QoS 정책에 대 한 레지스트리 하위 키를 열지 못했습니다. 이 정책은 인덱스 "%2"을 (를) 포함 하는 컴퓨터 수준 QoS 정책 루트 키 아래에 나열 됩니다.|  
  
|||  
|-|-|  
|**있어**|16709|  
|**Severity**|Error|  
|**SymbolicName**|EVENT_EQOS_ERROR_OPENING_USER_POLICY_SUBKEY|  
|**언어**|영어|  
|**메시지**|QoS가 사용자 QoS 정책에 대 한 레지스트리 하위 키를 열지 못했습니다. 이 정책은 인덱스 "%2"이 (가) 있는 사용자 수준 QoS 정책 루트 키 아래에 나열 됩니다.|  
  
|||  
|-|-|  
|**있어**|16710|  
|**Severity**|Error|  
|**SymbolicName**|EVENT_EQOS_ERROR_PROCESSING_MACHINE_POLICY_FIELD|  
|**언어**|영어|  
|**메시지**|QoS에서 컴퓨터 QoS 정책 "%3"에 대 한 "%2" 필드를 읽거나 유효성을 검사 하지 못했습니다.|  
  
|||  
|-|-|  
|**있어**|16711|  
|**Severity**|Error|  
|**SymbolicName**|EVENT_EQOS_ERROR_PROCESSING_USER_POLICY_FIELD|  
|**언어**|영어|  
|**메시지**|QoS가 사용자 QoS 정책 "%3"에 대 한 "%2" 필드를 읽거나 유효성을 검사 하지 못했습니다.|  
  
|||  
|-|-|  
|**있어**|16712|  
|**Severity**|Error|  
|**SymbolicName**|EVENT_EQOS_ERROR_SETTING_TCP_AUTOTUNING|  
|**언어**|영어|  
|**메시지**|QoS가 인바운드 TCP 처리량 수준을 읽거나 설정 하지 못했습니다. 오류 코드: "%2".|  
  
|||  
|-|-|  
|**있어**|16713|  
|**Severity**|Error|  
|**SymbolicName**|EVENT_EQOS_ERROR_SETTING_APP_MARKING|  
|**언어**|영어|  
|**메시지**|QoS에서 DSCP 표시 재정의 설정을 읽거나 설정 하지 못했습니다. 오류 코드: "%2".|  

이 가이드의 다음 항목에 대해서는 [QoS 정책 질문과 대답](qos-policy-faq.md)을 참조 하세요.

이 가이드의 첫 번째 항목은 [QoS (서비스 품질) 정책](qos-policy-top.md)을 참조 하세요.
