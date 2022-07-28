<p align="center"><img src="./app/assets/images/SealCircle.png" width="150px" height="150px" alt="aventium softworks"></p>

<h1 align="center">Helios Launcher</h1>

<em><h5 align="center">(formerly Electron Launcher)</h5></em>

[<p align="center"><img src="https://img.shields.io/github/workflow/status/KuronekoServer/KuronekoLauncher/Build.svg?style=for-the-badge" alt="gh actions">](https://github.com/KuronekoServer/KuronekoLauncher/actions) [<img src="https://img.shields.io/github/downloads/KuronekoServer/KuronekoLauncher/total.svg?style=for-the-badge" alt="downloads">](https://github.com/KuronekoServer/KuronekoLauncher/releases) <img src="https://forthebadge.com/images/badges/winter-is-coming.svg"  height="28px" alt="winter-is-coming"></p>

<p align="center">Join modded servers without worrying about installing Java, Forge, or other mods. We'll handle that for you.</p>

![Screenshot 1](https://i.imgur.com/6o7SmH6.png)
![Screenshot 2](https://i.imgur.com/x3B34n1.png)

## Features

* 🔒 完全なアカウント管理。
  * 複数のアカウントを追加し、簡単に切り替えることができます。
  * Microsoft (OAuth 2.0) + Mojang (Yggdrasil) 認証を完全にサポートします。
  * 認証情報は保存されず、Mojangに直接送信されます。
* 📂 効率的な資産管理
  * クライアントのアップデートが公開され次第、受け取ることができます。
  * ファイルは、起動前に検証されます。破損したファイルや不正なファイルは再ダウンロードされます。
* ☕ **Automatic Java validation.**
  * 互換性のないバージョンのJavaがインストールされている場合は、正しいものをインストールします *for you*.
  * ランチャーの実行には、Javaがインストールされている必要はありません。
* 📰 ランチャーにネイティブに組み込まれたニュースフィード。
* ⚙️ Javaコントロールパネルなど、直感的な設定管理が可能です。
* 全サーバーに対応。
  * サーバー構成の切り替えが簡単にできます。
  * 選択したサーバーのプレイヤー数を表示します。
* 自動アップデート。そうです、ランチャーが勝手にアップデートしてくれるのです。
*  Mojangのサービス状況を見ることができます。

これは完全なリストではありません。ランチャーをダウンロードしてインストールし、できることをすべて試してみてください。

#### Need Help? [Check the wiki.][wiki]

#### Like the project? Leave a ⭐ star on the repository!

## Downloads

You can download from [GitHub Releases](https://github.com/KuronekoServer/KuronekoLauncher/releases)

#### Latest Release

[![](https://img.shields.io/github/release/KuronekoServer/KuronekoLauncher.svg?style=flat-square)](https://github.com/KuronekoServer/KuronekoLauncher/releases/latest)

#### Latest Pre-Release
[![](https://img.shields.io/github/release/KuronekoServer/KuronekoLauncher/all.svg?style=flat-square)](https://github.com/KuronekoServer/KuronekoLauncher/releases)

**Supported Platforms**

[リリース](https://github.com/KuronekoServer/KuronekoLauncher/releases) タブからダウンロードする場合は、お使いのシステムに対応したインストーラーを選択してください。

| Platform | File |
| -------- | ---- |
| Windows x64 | `Helios-Launcher-setup-VERSION.exe` |
| macOS x64 | `Helios-Launcher-setup-VERSION-x64.dmg` |
| macOS arm64 | `Helios-Launcher-setup-VERSION-arm64.dmg` |
| Linux x64 | `Helios-Launcher-setup-VERSION.AppImage` |

## Console

コンソールを開くには、以下のキーバインドを使用します。

```console
ctrl + shift + i
```

コンソールタブが選択されていることを確認します。コンソールに何かを貼り付ける場合は、その内容が100%確実でない限り、貼り付けないでください。間違ったものを貼り付けると、機密情報が漏れる可能性があります。

#### Export Output to a File

コンソール出力をエクスポートしたい場合は、コンソール上の任意の場所を右クリックし、**Save as.**をクリックするだけです。

![console example](https://i.imgur.com/T5e73jP.png)


## Development

ここでは、基本的な開発環境のセットアップについて説明します。

### Getting Started

**System Requirements**

* [Node.js][nodejs] v16

---

**Clone and Install Dependencies**

```console
> git clone https://github.com/KuronekoServer/KuronekoLauncher.git
> cd HeliosLauncher
> npm install
```

---

**Launch Application**

```console
> npm start
```

---

**Build Installers**

現在のプラットフォームに合わせて構築すること。

```console
> npm run dist
```

特定のプラットフォーム向けに構築する。

| Platform    | Command              |
| ----------- | -------------------- |
| Windows x64 | `npm run dist:win`   |
| macOS       | `npm run dist:mac`   |
| Linux x64   | `npm run dist:linux` |

macOS用のビルドはWindows/Linuxでは動作しない場合があり、その逆も同様です。

---

### Visual Studio Code

ランチャーの開発は、すべて [Visual Studio Code][vscode].

以下を `.vscode/launch.json` に貼り付けます。

```JSON
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Debug Main Process",
      "type": "node",
      "request": "launch",
      "cwd": "${workspaceFolder}",
      "program": "${workspaceFolder}/node_modules/electron/cli.js",
      "args" : ["."],
      "outputCapture": "std"
    },
    {
      "name": "Debug Renderer Process",
      "type": "chrome",
      "request": "launch",
      "runtimeExecutable": "${workspaceFolder}/node_modules/.bin/electron",
      "windows": {
        "runtimeExecutable": "${workspaceFolder}/node_modules/.bin/electron.cmd"
      },
      "runtimeArgs": [
        "${workspaceFolder}/.",
        "--remote-debugging-port=9222"
      ],
      "webRoot": "${workspaceFolder}"
    }
  ]
}
```

これにより、2つのデバッグコンフィギュレーションが追加されます。

#### Debug Main Process

これにより、Electronの[main process][mainprocess]をデバッグすることができます。DevTools Windowを開くと、[renderer process][rendererprocess]のスクリプトをデバッグすることができます。

#### Debug Renderer Process

これにより、Electronの[renderer process][rendererprocess]をデバッグすることができます。そのためには、[Debugger for Chrome][chromedebugger]という拡張機能をインストールする必要があります。

このデバッグ設定を使用している間は、DevTools ウィンドウを開くことができないことに注意してください。Chromium は1つのデバッガしか許さないので、他のデバッガを開くとプログラムがクラッシュします。

---

### Note on Third-Party Usage

原作者のクレジットを表示し、原作者へのリンクを提供してください。これはフリーソフトです、最低限これだけはお願いします。

Microsoft認証の設定方法については、https://github.com/KuronekoServer/KuronekoLauncher/blob/master/docs/MicrosoftAuth.md を参照してください。

---

## Resources

* [Wiki][wiki]
* [Nebula (Create Distribution.json)][nebula]
* [v2 Rewrite Branch (Inactive)][v2branch]

開発者と連絡を取るには、Discordが最適です。

[![discord](https://discordapp.com/api/guilds/211524927831015424/embed.png?style=banner3)][discord]

---

### See you ingame.


[nodejs]: https://nodejs.org/en/ 'Node.js'
[vscode]: https://code.visualstudio.com/ 'Visual Studio Code'
[mainprocess]: https://electronjs.org/docs/tutorial/application-architecture#main-and-renderer-processes 'Main Process'
[rendererprocess]: https://electronjs.org/docs/tutorial/application-architecture#main-and-renderer-processes 'Renderer Process'
[chromedebugger]: https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome 'Debugger for Chrome'
[discord]: https://discord.gg/zNWUXdt 'Discord'
[wiki]: https://github.com/KuronekoServer/KuronekoLauncher/wiki 'wiki'
[nebula]: https://github.com/dscalzi/Nebula 'dscalzi/Nebula'
[v2branch]: https://github.com/KuronekoServer/KuronekoLauncher/tree/ts-refactor 'v2 branch'
