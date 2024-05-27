# EUDI Wallet に関するの調査

## 概要

- EUDI ウォレットは、eIDAS フレームワークの進化に基づいて設計されました。最初の eIDAS 規則は 2014 年に施行され、デジタル身分認証と信頼サービスに対する統一された EU の枠組みを提供することを目的としていました。2020 年、EU は eIDAS 規則の改訂（eIDAS 2）を進め、統一されたヨーロッパのデジタル ID インフラを構築することにしました。EUDI ウォレットは、この新しいインフラの中核要素として、すべての EU 市民がデジタル身分認証やさまざまなデジタルサービスへのアクセスを容易に行えるように、安全で便利なデジタル身分証明および文書管理ツールを提供することを目指しています。

## 開発言語

- Kotlin（Android）
- Swift（iOS）
- TypeScript（Web）
- Python（Backend）

## 基本機能

1. 身元確認
   - パブリックサービスへのアクセスや銀行口座の開設時に EUDI ウォレットを通じて自己の身元を確認できます。
2. 年齢確認
   - ソーシャルネットワークなどのプラットフォームにログインする際に、ユーザーが自分の年齢を証明できます。
3. 医療およびその他の重要なファイルの保管と表示
   - 医療処方箋、運転免許証、学位証明書などの重要文書を保管し、表示することができます。
4. 契約締結
   - ユーザーは EUDI ウォレットを使用してデジタル契約に署名できます。
5. 支払い認証
   - ユーザーが金融取引を行う際のデジタル的な支払い認証をサポートします。

## コアコンセプト

1. 個人身元データ（PID - Person Identification Data）
   - PID は、個人または法人の身元を確立するためのデータセットです。これには、個人を識別する情報、例えば氏名、生年月日、国籍などが含まれます。
2. デジタル属性証明（EAAs - Electronic Attestation of Attributes）
   - EAAs は、個人の様々な属性を検証するためのデジタル形式の証明です。例えば、医療処方箋、運転免許証、学位証明書などが EAAs として表示および検証されます。
3. 合格したデジタル属性証明（QEAA - Qualified Electronic Attestations of Attributes）
   - QEAAs は、特定の基準および法規要件を満たす EAAs で、合格した信頼サービスプロバイダーによって発行されます。これらの証明は個人または法人に関連付けられ、合格したデジタル署名またはデジタル印章で署名されます。

## eIDAS ARF(Architecture and Reference Framework) フレームワーク

1. エコシステム
   <br>
   <img src="./assets/ecosystem.png" width="50%">
   <br>
   - PID 提供者
     - ユーザーが EUDI ウォレットで身元を確認するための個人身元データ（PID）を発行します。PID とは、氏名や生年月日など、個人を特定するための基本情報です。
   - QEAA 提供者
     - 特定の基準と法規を満たす合格したデジタル属性証明（QEAA）を提供します。QEAA は、公的機関が認証した属性情報で、法的な証明力を持ちます。
   - EAA 提供者
     - ユーザーの異なる属性、例えば運転免許証や学位証明書などを検証するためのデジタル属性証明（EAA）を提供します。EAA は、個人の属性や資格をデジタル形式で証明します。
   - QES 提供者
     - 取引と文書の安全性と法的効力を保証するために、合格したデジタル署名サービスを提供します。QES は、電子署名の中でも特に高い信頼性と安全性を認証された署名です。
   - EUDI ウォレット提供者
     - ウォレットソリューションとサービスを提供し、ユーザーの日常使用と管理をサポートします。
   - 装置（オペレーティングシステム）製造業者
     - EUDI ウォレットアプリケーションをサポートする装置とオペレーティングシステムを提供します。
   - 検証者（Relying Party）
     - ユーザーが提供する PID/QEAA を検証する必要がある第三者、例えば銀行や政府機関です。
   - 信頼リスト提供者
     - すべての参加者とサービスが検証され信頼できることを保証する信頼リストを維持します。
2. 流れ
   <br>
   <img src="./assets/architecture.png" width="50%">
   <br>
   - ユーザーは、自身のデバイス上の EUDI ウォレットインスタンスを通じてウォレット機能を制御および活性化します。
   - ウォレットは、複数の提供者との相互作用を通じて PID および各種証明を取得し検証します。
   - ユーザーは、これらの情報を依存者に提示してサービスを受けるか取引を行います。

## 自作ウォレットのサポート

- 開発者がサーバー、クライアント、モバイルアプリ向けに自作ウォレットを構築できるようサポートしています。
  - モバイルアプリ
    - Kotlin（Android）
    - Swift（iOS）
  - サーバー、クライアント
    - TypeScript/Node.js、Python、Kotlin

## サポートされているクレデンシャル形式

1. PID（Personal Identifiable Data）
   - SD-JWT (Selective Disclosure JWT)
   - ISO mDL
2. ISO mDL (Mobile Driving License)
   - ISO/IEC 18013-5
3. 上記以外
   - JSON-LD + LD-Proofs

<br>
<img src="./assets/vc_format.png" width="50%">
<br>

## サポートされている通信・認証プロトコル規格

### 通信プロトコル

1. ISO/IEC 18013-5(Proximity)
   - 近接通信に使用され、特に身分証明書の安全な交換に適しています。

### 認証プロトコル

1. OAuth 2.0
2. OIDC (OpenID Connect)
3. SIOPv2(Self-Issued OpenID Provider v2)

### クレデンシャル交換プロトコル

1. OIDC4VCI (OpenID Connect for Verifiable Credential Issuance)
2. OIDC4VP (OpenID Connect for Verifiable Presentations)
3. DIF Presentation Exchange Protocol
4. Presentation Exchange Protocol
5. Issue Credential Protocol
6. Present Proof Protocol

## シーケンス図

```mermaid
sequenceDiagram
    participant User as User
    participant WalletApp as EUDI Wallet
    participant CredentialProvider as Issuer (PID/Attestation Provider)
    participant RelyingParty as Verifier

    User->>+WalletApp: インストール＆登録

    Note over WalletApp,CredentialProvider: OID4VCI
    Note over WalletApp,CredentialProvider: SD-JWT、ISO mDOC mDOC、JSON-LD + LD-Proofs
    WalletApp->>+CredentialProvider: 証明書をリクエスト
    CredentialProvider-->>-WalletApp: 証明書を発行

    Note over WalletApp,RelyingParty: OID4VP & SIOPv2、ISO/IEC 18013-5(Proximity)

    User->>+WalletApp: 証明書を選択
    WalletApp->>+RelyingParty: 証明書を提供
    RelyingParty-->>-WalletApp: 証明書を検証
    WalletApp-->>User: 検証結果を表示

    Note over WalletApp,CredentialProvider: 証明書の更新・削除
    User->>+WalletApp: 証明書の更新・削除をリクエスト
    WalletApp->>+CredentialProvider: 証明書の更新・削除のリクエストを提出
    CredentialProvider-->>-WalletApp: 証明書の更新・削除を実行

    Note over User,User: EUDIウォレットのアンインストール
    User->>+WalletApp: EUDIウォレットをアンインストール
    WalletApp-->>-User: アンインストールの確認
```

## ライブラリ

1. Android
   - [Wallet Core library](https://github.com/eu-digital-identity-wallet/eudi-lib-android-wallet-core)
   - [ISO 18013-5 Wallet Transfer library](https://github.com/eu-digital-identity-wallet/eudi-lib-android-iso18013-data-transfer)
   - [Presentation Exchange library](https://github.com/eu-digital-identity-wallet/eudi-lib-jvm-presentation-exchange-kt)
   - [SIOPv2 and OpenID4VP library](https://github.com/eu-digital-identity-wallet/eudi-lib-jvm-siop-openid4vp-kt)
   - [SD-JWT library](https://github.com/eu-digital-identity-wallet/eudi-lib-jvm-sdjwt-kt)
   - [OpenId4VCI library](https://github.com/eu-digital-identity-wallet/eudi-lib-jvm-openid4vci-kt)
   - [Wallet Documents Manager library](https://github.com/eu-digital-identity-wallet/eudi-lib-android-wallet-document-manager)
2. iOS
   - [Wallet Kit library](https://github.com/eu-digital-identity-wallet/eudi-lib-ios-wallet-kit)
   - [ISO/IEC 18013-5 Security library](https://github.com/eu-digital-identity-wallet/eudi-lib-ios-iso18013-security)
   - [ISO/IEC 18013-5 Wallet Data Transfer library](https://github.com/eu-digital-identity-wallet/eudi-lib-ios-iso18013-data-transfer)
   - [ISO/IEC 18013-5 Wallet Data Model library](https://github.com/eu-digital-identity-wallet/eudi-lib-ios-iso18013-data-model)
   - [Presentation Exchange library](https://github.com/eu-digital-identity-wallet/eudi-lib-ios-presentation-exchange-swift)
   - [SIOPv2 and OpenID4VP library](https://github.com/eu-digital-identity-wallet/eudi-lib-ios-siop-openid4vp-swift)
   - [SD-JWT library](https://github.com/eu-digital-identity-wallet/eudi-lib-sdjwt-swift)
   - [OpenId4VCI library](https://github.com/eu-digital-identity-wallet/eudi-lib-ios-openid4vci-swift)
   - [Wallet Storage library](https://github.com/eu-digital-identity-wallet/eudi-lib-ios-wallet-storage)

## コミュニティの活動状況

- EUDI Wallet は、European Digital Identity プロジェクトの一部として、欧州連合（EU）のデジタル戦略の推進に貢献するオープンソースプロジェクトです。GitHub での活動を見ると、EUDI Wallet のリポジトリは 331 のスターと 42 のフォークが寄せられ、プロジェクトへの広範な関心と活発な参加が示されています。また、46 件のオープンイシューと 7 件のプルリクエストが進行中であり、これらの数字から EUDI Wallet コミュニティの活動が非常に活発であることが示されています。

## サンプル

- Wallet(Holder)

  - [Android Demo](https://github.com/eu-digital-identity-wallet/eudi-app-android-wallet-ui)
    1. 前提条件
       - [Kotlin/Android 環境構築](https://kotlin.keicode.com/devenv/)
    2. 主なライブラリ
    3. 必要な設定 or 実装
    4. 操作手順
       - [Demo Download](<https://install.appcenter.ms/orgs/eu-digital-identity-wallet/apps/eudi-reference-android/distribution_groups/eudi%20wallet%20(demo)%20public>) または　[ローカル構築](https://github.com/eu-digital-identity-wallet/eudi-app-android-wallet-ui?tab=readme-ov-file#how-to-use-the-application)
       - [実行手順](https://github.com/eu-digital-identity-wallet/eudi-app-android-wallet-ui?tab=readme-ov-file#demo-videos)
  - [iOS Demo](https://github.com/eu-digital-identity-wallet/eudi-app-ios-wallet-ui)
    1. 前提条件
       - Xcode の用意
    2. 主なライブラリ
       - [Wallet Kit library](https://github.com/eu-digital-identity-wallet/eudi-lib-ios-wallet-kit)
       - [ISO/IEC 18013-5 Security library](https://github.com/eu-digital-identity-wallet/eudi-lib-ios-iso18013-security)
       - [ISO/IEC 18013-5 Wallet Data Transfer library](https://github.com/eu-digital-identity-wallet/eudi-lib-ios-iso18013-data-transfer)
       - [ISO/IEC 18013-5 Wallet Data Model library](https://github.com/eu-digital-identity-wallet/eudi-lib-ios-iso18013-data-model)
       - [Presentation Exchange library](https://github.com/eu-digital-identity-wallet/eudi-lib-ios-presentation-exchange-swift)
       - [SIOPv2 and OpenID4VP library](https://github.com/eu-digital-identity-wallet/eudi-lib-ios-siop-openid4vp-swift)
       - [OpenId4VCI library](https://github.com/eu-digital-identity-wallet/eudi-lib-ios-openid4vci-swift)
       - [Wallet Storage library](https://github.com/eu-digital-identity-wallet/eudi-lib-ios-wallet-storage)
    3. 必要な設定 or 実装
    4. [操作手順](https://github.com/eu-digital-identity-wallet/eudi-app-ios-wallet-ui/blob/main/README.md#how-to-use-the-application)

- Issuer
  1. [Python Demo](https://github.com/eu-digital-identity-wallet/eudi-srv-web-issuing-eudiw-py)
  2. [Kotlin Demo](https://github.com/eu-digital-identity-wallet/eudi-srv-pid-issuer)
- Verifier
  1. [Frontend](https://github.com/eu-digital-identity-wallet/eudi-web-verifier)
  2. [Backend Restful service](https://github.com/eu-digital-identity-wallet/eudi-srv-web-verifier-endpoint-23220-4-kt)

## 参考文献

- [reference-implementation](https://github.com/eu-digital-identity-wallet/.github/blob/main/profile/reference-implementation.md)
- [ARF(Architecture and Reference Framework)](https://github.com/eu-digital-identity-wallet/eudi-doc-architecture-and-reference-framework/blob/main/docs/arf.md)