---
title: AD FS 사용 하 여 id 위임 시나리오
description: 이 시나리오에서는 액세스 제어 검사를 수행 하려면 id 위임 체인을 필요로 하는 백 엔드 리소스에 액세스 해야 하는 응용 프로그램을 설명 합니다.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: b82d5fd749ac874d09bc54123727aaf902c4d778
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819854"
---
# <a name="identity-delegation-scenario-with-ad-fs"></a>AD FS 사용 하 여 id 위임 시나리오


[.NET Framework 4.5부터 Windows Identity Foundation (WIF)에 완전히 통합 되었기 때문에.NET Framework입니다. WIF WIF 3.5에서이 항목에서 다루는의 버전은 사용 되지 않습니다 및.NET Framework 3.5 SP1 또는.NET Framework 4에 대해 개발할 때에 사용 해야 합니다. .NET Framework 4.5에서는 라고도 WIF 4.5에서 WIF에 대 한 자세한 설명서를 참조 Windows Identity Foundation.NET Framework 4.5 개발 가이드에서.] 

이 시나리오에서는 액세스 제어 검사를 수행 하려면 id 위임 체인을 필요로 하는 백 엔드 리소스에 액세스 해야 하는 응용 프로그램을 설명 합니다. 간단한 id 위임 체인 초기 호출자에 직접 실행 호출자의 id 정보를 일반적으로 구성 됩니다.

현재 Windows 플랫폼에서 Kerberos 위임 모델을 사용 하 여 백 엔드 리소스를 액세스할 수 있으며 초기 호출자의 필요가 및 직접 실행 호출자의 id로만 이 모델은 일반적으로 신뢰할 수 있는 하위 시스템 모델 라고 합니다. WIF는 행위자 속성을 사용 하 여 위임 체인에서 직접 실행 호출자 뿐만 아니라 초기 호출자의 id를 유지 합니다.

다음 다이어그램은 Fabrikam 직원이 Contoso.com 응용 프로그램에서 노출 하는 리소스를 액세스 하는 일반적인 id 위임 시나리오를 보여 줍니다.

![ID](media/ad-fs-identity-delegation/id1.png)

이 시나리오에 참여 하는 가상의 사용자가 다음과 같습니다.

- Frank: Fabrikam 직원을 Contoso 리소스에 액세스 하고자 합니다.
- Daniel: Contoso 응용 프로그램 개발자에 게 응용 프로그램에서 필요한 변경 작업을 구현 합니다.
- Adam: Contoso IT 관리자입니다.

이 시나리오에서는 관련된 구성 요소는:

- web1: 웹 응용 프로그램 링크를 사용 하 여 초기 호출자의 위임 된 id를 요구 하는 백 엔드 리소스입니다. 이 응용 프로그램은 ASP.NET을 사용 하 여 빌드됩니다.
- 직접 실행 호출자의 함께 초기 호출자의 위임 된 id를 요구 하는 SQL Server에 액세스 하는 웹 서비스입니다. 이 서비스는 WCF를 사용 하 여 빌드됩니다.
- sts1: STS는 클레임 공급자의 역할 이므로 (web1) 응용 프로그램에서 예상 되는 클레임을 내보냅니다. 이 Fabrikam.com 및 응용 프로그램을 사용 하 여 트러스트를 설정 했습니다.
- sts2: STS가 Fabrikam.com에 대 한 id 공급자의 역할을은 Fabrikam 직원이 사용 하 여 인증 하는 끝점을 제공 합니다. 것은 Fabrikam 직원이 Contoso.com의 리소스에 액세스할 수 있도록 Contoso.com 사용 하 여 트러스트를 설정 합니다.

>[!NOTE] 
>용어에 사용 되는 경우가이 시나리오에서 "ActAs 토큰이", STS에서 발급 한 사용자의 id를 포함 하는 토큰을 가리킵니다. 행위자 속성 STS의 id가 들어 있습니다.

이전 다이어그램에 표시 된 대로이 시나리오의 흐름은 다음과 같습니다.


1. Contoso 응용 프로그램은 Fabrikam 직원의 id와 행위자 속성에서 직접 실행 호출자의 id를 포함 하는 ActAs 토큰을 가져올 구성 됩니다. Daniel 응용 프로그램에 이러한 변경 내용을 구현 했습니다.
2. ActAs 토큰이 백 엔드 서비스로 전달 하는 Contoso 응용 프로그램 구성 됩니다. Daniel 응용 프로그램에 이러한 변경 내용을 구현 했습니다.
3. Contoso 웹 서비스는 ActAs 토큰이 sts1를 호출 하 여 유효성을 검사 하도록 구성 됩니다. Adam sts1을 위임 요청을 처리 하는 데 있었습니다.
4. Fabrikam 사용자 Frank는 Contoso 응용 프로그램에 액세스 하 고 백 엔드 리소스에 대 한 액세스를 제공 됩니다.

## <a name="set-up-the-identity-provider-ip"></a>Id 공급자 (IP) 설정

Frank Fabrikam.com 관리자에 대 한 사용 가능한 가지 세 가지 옵션이 있습니다.


1. 구매 및 Active Directory® Federation Services (AD FS)와 같은 STS 제품을 설치 합니다.
2. LiveID STS와 같은 클라우드 STS 제품을 구독 합니다.
3. WIF를 사용 하 여 사용자 지정 STS를 작성 합니다.

이 샘플 시나리오에서 Frank option1 선택한 IP-STS로 AD FS 설치 가정 합니다. 그는 또한 \windowsauth, 사용자를 인증 하 라는 끝점을 구성 합니다. AD FS 제품 설명서를 참조 및 Adam의 경우 Contoso IT 관리자가 통신 하 여 Frank Contoso.com 도메인을 사용 하 여 트러스트를 설정 합니다.

## <a name="set-up-the-claims-provider"></a>클레임 공급자 설정

옵션에 사용할 수 있으며 Contoso.com 관리자 Adam의 경우 동일 id 공급자에 대해 이전에 설명한 대로 합니다. 이 샘플 시나리오에 대 한 가정는 Adam 옵션 1 선택 RP-STS로 AD FS 2.0을 설치 합니다.

## <a name="set-up-trust-with-the-ip-and-application"></a>IP 및 응용 프로그램을 사용 하 여 트러스트를 설정

AD FS 설명서를 보면 Adam Fabrikam.com 및 응용 프로그램 간의 트러스트를 설정 합니다.

## <a name="set-up-delegation"></a>위임 설정

AD FS 위임 처리를 제공합니다. AD FS 설명서를 보면 Adam ActAs 토큰이 처리할 수 있도록 합니다.

## <a name="application-specific-changes"></a>응용 프로그램 관련 변경 내용

기존 응용 프로그램에 id 위임에 대 한 지원을 추가 하려면 다음과 같이 변경 수행 되어야 합니다. Daniel 이러한 변경을 수행 하려면 WIF를 사용 합니다.


- Sts1에서 받은 해당 web1 부트스트랩 토큰을 캐시 합니다.
- 발급된 된 토큰을 사용 하 여 CreateChannelActingAs 사용 하 여 백 엔드 웹 서비스에 채널을 만듭니다.
- 백 엔드 서비스의 메서드를 호출 합니다.

## <a name="cache-the-bootstrap-token"></a>부트스트랩 토큰 캐시

부트스트랩 토큰은 STS에서 발급 한 초기 토큰 및 응용 프로그램에서 클레임을 추출 합니다. 이 샘플 시나리오에서 Frank, 사용자에 대 한 sts1에 의해 발급 된이 토큰이이 및 응용 프로그램 캐시 합니다. 다음 코드 샘플 ASP.NET 응용 프로그램에서 토큰 검색을 부트스트랩 하는 방법을 보여 줍니다.

```
// Get the Bootstrap Token
SecurityToken bootstrapToken = null;

IClaimsPrincipal claimsPrincipal = Thread.CurrentPrincipal as IClaimsPrincipal;
if ( claimsPrincipal != null )
{
    IClaimsIdentity claimsIdentity = (IClaimsIdentity)claimsPrincipal.Identity;
    bootstrapToken = claimsIdentity.BootstrapToken;
}
```
메서드를 제공 하는 WIF [CreateChannelActingAs](https://msdn.microsoft.com/library/ee733863.aspx)는 ActAs 요소로 지정 된 보안 토큰을 사용 하 여 토큰 발급 요청을 확대 하는 지정 된 형식의 채널을 만듭니다. 이 메서드를 부트스트랩 토큰을 전달 하 고 반환 된 채널에서 필요한 서비스 메서드를 호출 합니다. 이 샘플 시나리오에서 Frank의 신원이 합니다 [행위자](https://msdn.microsoft.com/library/microsoft.identitymodel.claims.iclaimsidentity.actor.aspx) web1의 id로 설정 하는 속성입니다.

다음 코드 조각을 사용 하 여 웹 서비스를 호출 하는 방법을 보여 줍니다 [CreateChannelActingAs](https://msdn.microsoft.com/library/ee733863.aspx) 다음 반환 된 채널에서 ComputeResponse, 서비스의 메서드 중 하나를 호출 합니다.

```
// Get the channel factory to the backend service from the application state
ChannelFactory<IService2Channel> factory = (ChannelFactory<IService2Channel>)Application[Global.CachedChannelFactory];

// Create and setup channel to talk to the backend service
IService2Channel channel;
lock (factory)
{
// Setup the ActAs to point to the caller's token so that we perform a 
// delegated call to the backend service
// on behalf of the original caller.
    channel = factory.CreateChannelActingAs<IService2Channel>(callerToken);
}

string retval = null;

// Call the backend service and handle the possible exceptions
try
{
    retval = channel.ComputeResponse(value);
    channel.Close();
} catch (Exception exception)
{
    StringBuilder sb = new StringBuilder();
    sb.AppendLine("An unexpected exception occurred.");
    sb.AppendLine(exception.StackTrace);
    channel.Abort();
    retval = sb.ToString();
}

```
## <a name="web-service-specific-changes"></a>웹 서비스에의 한 변경

웹 서비스 WCF를 사용 하 여 작성 되 고 적절 한 발급자 주소와 바인딩을 IssuedSecurityTokenParameters를 사용 하 여 구성 되 면 WIF에 대 한 사용 하므로 ActAs의 유효성을 검사 WIF에 의해 자동으로 처리 됩니다. 

웹 서비스 응용 프로그램에 필요한 특정 메서드를 노출 합니다. 서비스에 필요한 특정 코드 변경이 없습니다. 다음 코드 샘플에 IssuedSecurityTokenParameters 사용 하 여 웹 서비스의 구성을 보여 줍니다.

```
// Configure the issued token parameters with the correct settings
IssuedSecurityTokenParameters itp = new IssuedSecurityTokenParameters( "http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV1.1" );
itp.IssuerMetadataAddress = new EndpointAddress( "http://localhost:6000/STS/mex" );
itp.IssuerAddress = new EndpointAddress( "http://localhost:6000/STS" );

// Create the security binding element
SecurityBindingElement sbe = SecurityBindingElement.CreateIssuedTokenForCertificateBindingElement( itp );
sbe.MessageSecurityVersion = MessageSecurityVersion.WSSecurity11WSTrust13WSSecureConversation13WSSecurityPolicy12BasicSecurityProfile10;

// Create the HTTP transport binding element
HttpTransportBindingElement httpBE = new HttpTransportBindingElement();

// Create the custom binding using the prepared binding elements
CustomBinding binding = new CustomBinding( sbe, httpBE );

using ( ServiceHost host = new ServiceHost( typeof( Service2 ), new Uri( "http://localhost:6002/Service2" ) ) )
{
    host.AddServiceEndpoint( typeof( IService2 ), binding, "" );
    host.Credentials.ServiceCertificate.SetCertificate( "CN=localhost", StoreLocation.LocalMachine, StoreName.My );

// Enable metadata generation via HTTP GET
    ServiceMetadataBehavior smb = new ServiceMetadataBehavior();
    smb.HttpGetEnabled = true;
    host.Description.Behaviors.Add( smb );
    host.AddServiceEndpoint( typeof( IMetadataExchange ), MetadataExchangeBindings.CreateMexHttpBinding(), "mex" );

// Configure the service host to use WIF
    ServiceConfiguration configuration = new ServiceConfiguration();
    configuration.IssuerNameRegistry = new TrustedIssuerNameRegistry();

    FederatedServiceCredentials.ConfigureServiceHost( host, configuration );

    host.Open();

    Console.WriteLine( "Service2 started, press ENTER to stop ..." );
    Console.ReadLine();

    host.Close();
}
```

## <a name="next-steps"></a>다음 단계
[AD FS 개발](../../ad-fs/AD-FS-Development.md)  
