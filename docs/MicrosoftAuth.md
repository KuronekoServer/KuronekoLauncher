# マイクロソフトの認証

Kuroneko Launcherは、Microsoftによる認証に完全対応しています。

## Acquiring an Azure Client ID

1. https://portal.azure.com に移動します
2. 検索バーで、**Azure Active Directory** と検索してください。
3. Azure Active Directory の左ペインの **アプリの登録** (Under *Manage*) に移動します。
4. 新規登録**をクリックします。
    - 名前**をランチャーの名前に設定します。
    - サポートされるアカウントの種類を、*任意の組織ディレクトリ（任意のAzure ADディレクトリ - Multitenant）および個人のMicrosoftアカウント（例：Skype、Xbox）*に設定します。
    - **Redirect URI** は空白にしてください。
    - アプリケーションを登録する。
5. アプリケーションの管理ページが表示されているはずです。そうでない場合は、**アプリの登録** に戻ってください。先ほど登録したアプリケーションを選択します。
6. 左ペインの**認証**をクリックします（*Manage*）。
7. clickで **Add Platform**.
    - *モバイルおよびデスクトップアプリケーション*を選択します。
    - **リダイレクトURI**として `https://login.microsoftonline.com/common/oauth2/nativeclient` を選択します.
    - **Configure** を選択し、プラットフォームの追加を完了します。
8. **概要** に戻ります。
9. コピー **アプリケーション (クライアント) ID**.


参考：https://docs.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app

## Adding the Azure Client ID to Kuroneko Launcher.

`app/assets/js/ipcconstants.js` の中に **`AZURE_CLIENT_ID`** があります。これを自分のアプリケーションのIDに設定します。

注：Azure Client ID は秘密値ではなく、**git に保存することができます**。
参考：https://stackoverflow.com/questions/57306964/are-azure-active-directorys-tenantid-and-clientid-considered-secrets

----

You can now authenticate with Microsoft through the ランチャーからマイクロソフトとの認証ができるようになりました。