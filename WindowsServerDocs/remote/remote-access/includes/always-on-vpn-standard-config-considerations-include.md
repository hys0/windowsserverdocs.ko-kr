## <a name="standard-configuration-considerations"></a>표준 구성 고려 사항

Always On VPN에 다양 한 구성 옵션이 있습니다. 그러나 VPN 구성을 선택 하는 다음 정보를 포함 하지만.

-   **연결 유형입니다.** 연결 프로토콜 선택은 중요 하며 최종적으로 밀접 사용할 인증 유형을 사용 하 여. 사용 가능한 터널링 프로토콜에 대 한 자세한 내용은 참조 하세요 [VPN 연결 형식](https://docs.microsoft.com/windows/security/identity-protection/vpn/vpn-connection-type/)합니다.

-   **라우팅입니다.** 이 컨텍스트에서 라우팅 규칙 사용자 VPN에 연결 하는 동안 다른 네트워크 경로 사용할 수 있는지 여부를 결정 합니다.

    -   _분할 터널링_ 인터넷과 같은 다른 네트워크에 동시에 액세스할 수 있습니다.

    -   _강제 터널링_ 모든 트래픽이 VPN을 통해 단독으로 이동 해야 하 고 다른 네트워크에 대 한 동시 액세스를 허용 하지 않습니다.

-   **트리거.** _트리거_ (예를 들어 앱이 열릴 때, 장치, 수동으로 사용자가 설정 된 경우)는 VPN 연결이 시작 방법과 시기를 결정 합니다. 트리거 옵션에 대해서는 [VPN 프로필 자동 트리거 옵션](https://docs.microsoft.com/windows/security/identity-protection/vpn/vpn-auto-trigger-profile/)합니다.

-   **장치 또는 사용자 인증입니다.** Always On VPN 장치 인증서 및 라는 기능을 통해 장치에서 시작 된 연결 사용 [장치 터널](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/vpn-device-tunnel-config)합니다. 자동으로 시작할 수 있습니다 연결과 비슷한 DirectAccess 인프라 터널 연결을 지속 됩니다.

>[!TIP]
>DirectAccess에서 Always On VPN으로 마이그레이션할 경우에 어떤 있습니다를 펼친 다음 여기에서 비교할 수 있는 구성 옵션을 사용 하 여 시작 하는 것이 좋습니다.

사용자 인증서를 사용 하 여 Always On VPN 클라이언트는 자동으로 연결 하지만 사용자 수준 (로그인 한 후 사용자) 대신 (이전 사용자 로그인) 장치 수준입니다. 환경을 사용자에 게 계속 원활 하 게 되었지만 Windows Hello 같은 고급 인증 메커니즘을 지원 합니다.