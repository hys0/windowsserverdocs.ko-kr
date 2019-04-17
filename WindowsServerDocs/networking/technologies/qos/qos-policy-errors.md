---
title: 오류 QoS 정책 및 이벤트 메시지
description: 이 항목에서 Windows Server 2016 서비스의 품질 (QoS) 정책에 대 한 목록이 이벤트 및 오류 메시지를 제공합니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 76974e10-6a57-4533-83be-cfd5a0d364a3
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e2e890a7947d4f7de09159d7de606c0542f45045
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="qos-policy-error-and-event-messages"></a>오류 QoS 정책 및 이벤트 메시지

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

다음은 QoS 정책와 관련 된 이벤트 및 오류 메시지 합니다.  
  
## <a name="informational-messages"></a>알림 메시지  

다음은 QoS 정책 정보 메시지의 목록입니다.

|||  
|-|-|  
|**MessageId**|16500|  
|**심각도**|알림|  
|**심볼 이름**|EVENT_EQOS_INFO_MACHINE_POLICY_REFRESH_NO_CHANGE|  
|**언어**|영어|  
|**메시지**|컴퓨터 QoS 정책을 새로 고쳤습니다. 변경 내용이 감지 합니다.|  
  
|||  
|-|-|  
|**MessageId**|16501|  
|**심각도**|알림|  
|**심볼 이름**|EVENT_EQOS_INFO_MACHINE_POLICY_REFRESH_WITH_CHANGE|  
|**언어**|영어|  
|**메시지**|컴퓨터 QoS 정책을 새로 고쳤습니다. 정책 변경 되었습니다.|  
  
|||  
|-|-|  
|**MessageId**|16502|  
|**심각도**|알림|  
|**심볼 이름**|EVENT_EQOS_INFO_USER_POLICY_REFRESH_NO_CHANGE|  
|**언어**|영어|  
|**메시지**|사용자 QoS 정책을 새로 고쳤습니다. 변경 내용이 감지 합니다.|  
  
|||  
|-|-|  
|**MessageId**|16503|  
|**심각도**|알림|  
|**심볼 이름**|EVENT_EQOS_INFO_USER_POLICY_REFRESH_WITH_CHANGE|  
|**언어**|영어|  
|**메시지**|사용자 QoS 정책을 새로 고쳤습니다. 정책 변경 되었습니다.|  
  
|||  
|-|-|  
|**MessageId**|16504|  
|**심각도**|알림|  
|**심볼 이름**|EVENT_EQOS_INFO_TCP_AUTOTUNING_NOT_CONFIGURED|  
|**언어**|영어|  
|**메시지**|인바인드 TCP 처리량 수준에 대 한 고급 QoS 설정을 고쳤습니다. QoS 정책에서 값 설정을 지정 되지 않습니다. 로컬 컴퓨터 기본 적용 됩니다.|  
  
|||  
|-|-|  
|**MessageId**|16505|  
|**심각도**|알림|  
|**심볼 이름**|EVENT_EQOS_INFO_TCP_AUTOTUNING_OFF|  
|**언어**|영어|  
|**메시지**|인바인드 TCP 처리량 수준에 대 한 고급 QoS 설정을 고쳤습니다. 수준 0 (최소 처리량)은 값으로 설정 합니다.|  
  
|||  
|-|-|  
|**MessageId**|16506|  
|**심각도**|알림|  
|**심볼 이름**|EVENT_EQOS_INFO_TCP_AUTOTUNING_HIGHLY_RESTRICTED|  
|**언어**|영어|  
|**메시지**|인바인드 TCP 처리량 수준에 대 한 고급 QoS 설정을 고쳤습니다. 수준 1은 값으로 설정 합니다.|  
  
|||  
|-|-|  
|**MessageId**|16507|  
|**심각도**|알림|  
|**심볼 이름**|EVENT_EQOS_INFO_TCP_AUTOTUNING_RESTRICTED|  
|**언어**|영어|  
|**메시지**|인바인드 TCP 처리량 수준에 대 한 고급 QoS 설정을 고쳤습니다. 수준 2은 값으로 설정 합니다.|  
  
|||  
|-|-|  
|**MessageId**|16508|  
|**심각도**|알림|  
|**심볼 이름**|EVENT_EQOS_INFO_TCP_AUTOTUNING_NORMAL|  
|**언어**|영어|  
|**메시지**|인바인드 TCP 처리량 수준에 대 한 고급 QoS 설정을 고쳤습니다. 값 설정은 수준이 3 (최대 처리량)입니다.|  
  
|||  
|-|-|  
|**MessageId**|16509|  
|**심각도**|알림|  
|**심볼 이름**|EVENT_EQOS_INFO_APP_MARKING_NOT_CONFIGURED|  
|**언어**|영어|  
|**메시지**|DSCP 표시 QoS 고급 설정을 재정의 고쳤습니다. 값 설정을 지정 되지 않습니다. 응용 프로그램 DSCP 값 QoS 정책 별도로 설정할 수 있습니다.|  
  
|||  
|-|-|  
|**MessageId**|16510|  
|**심각도**|알림|  
|**심볼 이름**|EVENT_EQOS_INFO_APP_MARKING_IGNORED|  
|**언어**|영어|  
|**메시지**|DSCP 표시 QoS 고급 설정을 재정의 고쳤습니다. 응용 프로그램 DSCP 표시 요청 무시 됩니다. QoS 정책에 대 한 DSCP 값을 설정할 수 있습니다.|  
  
|||  
|-|-|  
|**MessageId**|16511|  
|**심각도**|알림|  
|**심볼 이름**|EVENT_EQOS_INFO_APP_MARKING_ALLOWED|  
|**언어**|영어|  
|**메시지**|DSCP 표시 QoS 고급 설정을 재정의 고쳤습니다. 응용 프로그램 DSCP 값 QoS 정책 별도로 설정할 수 있습니다.|  
  
|||  
|-|-|  
|**MessageId**|16512|  
|**심각도**|알림|  
|**심볼 이름**|EVENT_EQOS_INFO_LOCAL_SETTING_DONT_USE_NLA|  
|**언어**|영어|  
|**메시지**|네트워크 도메인 범주를 기반으로 QoS 정책 응용 비활성화 되었습니다. 모든 네트워크 인터페이스 QoS 정책이 적용 됩니다.|  
  
## <a name="warning-messages"></a>경고 메시지

다음은 QoS 정책 경고 메시지의 목록입니다.

|||  
|-|-|  
|**MessageId**|16600|  
|**심각도**|경고|  
|**심볼 이름**|EVENT_EQOS_WARNING_TEST_1|  
|**언어**|영어|  
|**메시지**|EQOS: * * * Testing\ * \ * \ * [, 하나] "%2" 합니다.|  
  
|||  
|-|-|  
|**MessageId**|16601|  
|**심각도**|경고|  
|**심볼 이름**|EVENT_EQOS_WARNING_TEST_2|  
|**언어**|영어|  
|**메시지**|EQOS: * * * Testing\ * \ * \ * [, 문자열 1 두 가지 문자열은] "%2" [, 문자열 2는] %3 합니다.|  
  
|||  
|-|-|  
|**MessageId**|16602|  
|**심각도**|경고|  
|**심볼 이름**|EVENT_EQOS_WARNING_MACHINE_POLICY_VERSION|  
|**언어**|영어|  
|**메시지**|컴퓨터 "%2" QoS 정책 잘못 된 버전 번호가 있습니다. 이 정책이 적용 되지 않습니다.|  
  
|||  
|-|-|  
|**MessageId**|16603|  
|**심각도**|경고|  
|**심볼 이름**|EVENT_EQOS_WARNING_USER_POLICY_VERSION|  
|**언어**|영어|  
|**메시지**|정책 QoS "%2" 사용자에 게 잘못 된 버전 번호가 합니다. 이 정책이 적용 되지 않습니다.|  
  
|||  
|-|-|  
|**MessageId**|16604|  
|**심각도**|경고|  
|**심볼 이름**|EVENT_EQOS_WARNING_MACHINE_POLICY_PROFILE_NOT_SPECIFIED|  
|**언어**|영어|  
|**메시지**|컴퓨터 "%2" QoS 정책 DSCP 값 또는 조절 속도 지정 하지 않습니다. 이 정책이 적용 되지 않습니다.|  
  
|||  
|-|-|  
|**MessageId**|16605|  
|**심각도**|경고|  
|**심볼 이름**|EVENT_EQOS_WARNING_USER_POLICY_PROFILE_NOT_SPECIFIED|  
|**언어**|영어|  
|**메시지**|사용자 "%2" QoS 정책 DSCP 값 또는 조절 속도 지정 하지 않습니다. 이 정책이 적용 되지 않습니다.|  
  
|||  
|-|-|  
|**MessageId**|16606|  
|**심각도**|경고|  
|**심볼 이름**|EVENT_EQOS_WARNING_MACHINE_POLICY_QUOTA_EXCEEDED|  
|**언어**|영어|  
|**메시지**|컴퓨터 QoS 정책 최대 수를 초과 있습니다. "%2" QoS 정책 및 이후 컴퓨터 QoS 정책이 적용 되지 않습니다.|  
  
|||  
|-|-|  
|**MessageId**|16607|  
|**심각도**|경고|  
|**심볼 이름**|EVENT_EQOS_WARNING_USER_POLICY_QUOTA_EXCEEDED|  
|**언어**|영어|  
|**메시지**|사용자 QoS 정책 최대 수를 초과 있습니다. "%2" QoS 정책 및 이후의 사용자 QoS 정책이 적용 되지 않습니다.|  
  
|||  
|-|-|  
|**MessageId**|16608|  
|**심각도**|경고|  
|**심볼 이름**|EVENT_EQOS_WARNING_MACHINE_POLICY_CONFLICT|  
|**언어**|영어|  
|**메시지**|컴퓨터 "%2" QoS 정책 충돌할 수 다른 QoS 정책을 있습니다. 규칙 정책이 적용 되는 대 한 설명서를 참조 하십시오.|  
  
|||  
|-|-|  
|**MessageId**|16609|  
|**심각도**|경고|  
|**심볼 이름**|EVENT_EQOS_WARNING_USER_POLICY_CONFLICT|  
|**언어**|영어|  
|**메시지**|사용자 "%2" QoS 정책 충돌할 수 다른 QoS 정책을 있습니다. 규칙 정책이 적용 되는 대 한 설명서를 참조 하십시오.|  
  
|||  
|-|-|  
|**MessageId**|16610|  
|**심각도**|경고|  
|**심볼 이름**|EVENT_EQOS_WARNING_MACHINE_POLICY_NO_FULLPATH_APPNAME|  
|**언어**|영어|  
|**메시지**|응용 프로그램 경로 처리할 수 없습니다 "%2" QoS 정책 컴퓨터 무시 되었습니다. 응용 프로그램 경로 유효 하지 않을, 잘못 된 드라이브 문자를 포함 하거나 매핑된 네트워크 드라이브 포함 될 수 있습니다.|  
  
|||  
|-|-|  
|**MessageId**|16611|  
|**심각도**|경고|  
|**심볼 이름**|EVENT_EQOS_WARNING_USER_POLICY_NO_FULLPATH_APPNAME|  
|**언어**|영어|  
|**메시지**|사용자 "%2" QoS 정책 응용 프로그램 경로 처리할 수 없기 때문에 했습니다. 응용 프로그램 경로 유효 하지 않을, 잘못 된 드라이브 문자를 포함 하거나 매핑된 네트워크 드라이브 포함 될 수 있습니다.|  
  
## <a name="error-messages"></a>오류 메시지  

다음은 QoS 정책 오류 메시지의 목록입니다.

|||  
|-|-|  
|**MessageId**|16700|  
|**심각도**|오류|  
|**심볼 이름**|EVENT_EQOS_ERROR_MACHINE_POLICY_REFERESH|  
|**언어**|영어|  
|**메시지**|컴퓨터 QoS 정책을 새로 고침 하지 못했습니다. 오류 코드: "%2" 합니다.|  
  
|||  
|-|-|  
|**MessageId**|16701|  
|**심각도**|오류|  
|**심볼 이름**|EVENT_EQOS_ERROR_USER_POLICY_REFERESH|  
|**언어**|영어|  
|**메시지**|사용자 QoS 정책을 새로 고침 하지 못했습니다. 오류 코드: "%2" 합니다.|  
  
|||  
|-|-|  
|**MessageId**|16702|  
|**심각도**|오류|  
|**심볼 이름**|EVENT_EQOS_ERROR_OPENING_MACHINE_POLICY_ROOT_KEY|  
|**언어**|영어|  
|**메시지**|QoS는 QoS 정책에 대 한 시스템 수준의 루트 키 열지 하지 못했습니다. 오류 코드: "%2" 합니다.|  
  
|||  
|-|-|  
|**MessageId**|16703|  
|**심각도**|오류|  
|**심볼 이름**|EVENT_EQOS_ERROR_OPENING_USER_POLICY_ROOT_KEY|  
|**언어**|영어|  
|**메시지**|사용자 액세스 제어 루트 키 QoS 정책을를 열 수 QoS 하지 못했습니다. 오류 코드: "%2" 합니다.|  
  
|||  
|-|-|  
|**MessageId**|16704|  
|**심각도**|오류|  
|**심볼 이름**|EVENT_EQOS_ERROR_MACHINE_POLICY_KEYNAME_TOO_LONG|  
|**언어**|영어|  
|**메시지**|컴퓨터 QoS 정책 초과 최대 허용된 이름 길이 합니다. 시스템 수준의 QoS 정책 루트 키 "%2" 인덱스와 아래에 표시 됩니다.|  
  
|||  
|-|-|  
|**MessageId**|16705|  
|**심각도**|오류|  
|**심볼 이름**|EVENT_EQOS_ERROR_USER_POLICY_KEYNAME_TOO_LONG|  
|**언어**|영어|  
|**메시지**|사용자 QoS 정책 초과 최대 허용된 이름 길이 합니다. 사용자 수준 QoS 정책 루트 키 "%2" 인덱스와 아래에 표시 됩니다.|  
  
|||  
|-|-|  
|**MessageId**|16706|  
|**심각도**|오류|  
|**심볼 이름**|EVENT_EQOS_ERROR_MACHINE_POLICY_KEYNAME_SIZE_ZERO|  
|**언어**|영어|  
|**메시지**|컴퓨터 QoS 정책에 0 길이 이름입니다. 시스템 수준의 QoS 정책 루트 키 "%2" 인덱스와 아래에 표시 됩니다.|  
  
|||  
|-|-|  
|**MessageId**|16707|  
|**심각도**|오류|  
|**심볼 이름**|EVENT_EQOS_ERROR_USER_POLICY_KEYNAME_SIZE_ZERO|  
|**언어**|영어|  
|**메시지**|사용자 QoS 정책에 0 길이 이름입니다. 사용자 수준 QoS 정책 루트 키 "%2" 인덱스와 아래에 표시 됩니다.|  
  
|||  
|-|-|  
|**MessageId**|16708|  
|**심각도**|오류|  
|**심볼 이름**|EVENT_EQOS_ERROR_OPENING_MACHINE_POLICY_SUBKEY|  
|**언어**|영어|  
|**메시지**|QoS는 레지스트리 하위 컴퓨터 QoS 정책에 대해 열고 하지 못했습니다. 정책은 시스템 수준의 QoS 정책 루트 키 "%2" 인덱스와 아래에 표시 됩니다.|  
  
|||  
|-|-|  
|**MessageId**|16709|  
|**심각도**|오류|  
|**심볼 이름**|EVENT_EQOS_ERROR_OPENING_USER_POLICY_SUBKEY|  
|**언어**|영어|  
|**메시지**|QoS는 레지스트리 하위 QoS 정책 사용자에 대해 열고 하지 못했습니다. 정책은은 사용자 수준 QoS 정책 루트 키 "%2" 인덱스와 아래에 표시 됩니다.|  
  
|||  
|-|-|  
|**MessageId**|16710|  
|**심각도**|오류|  
|**심볼 이름**|EVENT_EQOS_ERROR_PROCESSING_MACHINE_POLICY_FIELD|  
|**언어**|영어|  
|**메시지**|QoS는 QoS 정책 %3 컴퓨터에 대 한 "%2" 필드 읽거나 확인 하지 못했습니다.|  
  
|||  
|-|-|  
|**MessageId**|16711|  
|**심각도**|오류|  
|**심볼 이름**|EVENT_EQOS_ERROR_PROCESSING_USER_POLICY_FIELD|  
|**언어**|영어|  
|**메시지**|QoS 읽거나 사용자 %3 QoS 정책에 대 한 "%2" 필드 확인 하지 못했습니다.|  
  
|||  
|-|-|  
|**MessageId**|16712|  
|**심각도**|오류|  
|**심볼 이름**|EVENT_EQOS_ERROR_SETTING_TCP_AUTOTUNING|  
|**언어**|영어|  
|**메시지**|QoS 읽거나 인바인드 TCP 처리량에 오류 코드를 설정 하지 못했습니다. "%2" 합니다.|  
  
|||  
|-|-|  
|**MessageId**|16713|  
|**심각도**|오류|  
|**심볼 이름**|EVENT_EQOS_ERROR_SETTING_APP_MARKING|  
|**언어**|영어|  
|**메시지**|오류 코드 설정 읽거나 DSCP 표시 설정 하지 못했습니다 QoS 재정의: "%2" 합니다.|  

이 가이드에 다음 항목에 대 한 참고 [QoS 정책 질문과 대답](qos-policy-faq.md)합니다.

이 가이드의 첫 번째 항목을 참조 하세요. [(QoS) 서비스 품질 정책](qos-policy-top.md)합니다.
