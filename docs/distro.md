# Distribution Index

[Nebula](https://github.com/KuronekoServer/Nebula)を使って、配布インデックスの生成を自動化することができます。

配布用インデックスはJSONで記述されます。インデックスの一般的な書式は、以下に掲示するとおりです。

```json
{
    "version": "1.0.0",
    "discord": {
        "clientId": "12334567890123456789",
        "smallImageText": "WesterosCraft",
        "smallImageKey": "seal-circle"
    },
    "rss": "https://westeroscraft.com/articles/index.rss",
    "servers": [
        {
            "id": "Example_Server",
            "name": "WesterosCraft Example Client",
            "description": "Example WesterosCraft server. Connect for fun!",
            "icon": "http://mc.westeroscraft.com/WesterosCraftLauncher/files/example_icon.png",
            "version": "0.0.1",
            "address": "mc.westeroscraft.com:1337",
            "minecraftVersion": "1.11.2",
            "discord": {
                "shortId": "Example",
                "largeImageText": "WesterosCraft Example Server",
                "largeImageKey": "server-example"
            },
            "mainServer": true,
            "autoconnect": true,
            "modules": [
                "Module Objects Here"
            ]
        }
    ]
}
```

## Distro Index Object

#### Example
```JSON
{
    "version": "1.0.0",
    "discord": {
        "clientId": "12334567890123456789",
        "smallImageText": "WesterosCraft",
        "smallImageKey": "seal-circle"
    },
    "rss": "https://westeroscraft.com/articles/index.rss",
    "servers": []
}
```

### `DistroIndex.version: string/semver`

インデックスフォーマットのバージョン。将来的に、更新を優雅にプッシュするために使われるでしょう。

### `DistroIndex.discord: object`

[Discord Rich Presence](https://discordapp.com/developers/docs/rich-presence/how-to)のグローバル設定です。

**Properties**

* `discord.clientId: string` - Discordに登録されているアプリケーションのクライアントID。
* `discord.smallImageText: string` - `smallImageKey` に対応するトゥートゥルトゥルです。
* `discord.smallImageKey: string` - 小さなプロフィールアートワークのためにアップロードされた画像の名前です。


### `DistroIndex.rss: string/url`

RSSフィードのURLです。ニュースの読み込みに使用します。

---

## Server Object

#### Example
```JSON
{
    "id": "Example_Server",
    "name": "WesterosCraft Example Client",
    "description": "Example WesterosCraft server. Connect for fun!",
    "icon": "http://mc.westeroscraft.com/WesterosCraftLauncher/files/example_icon.png",
    "version": "0.0.1",
    "address": "mc.westeroscraft.com:1337",
    "minecraftVersion": "1.11.2",
    "discord": {
        "shortId": "Example",
        "largeImageText": "WesterosCraft Example Server",
        "largeImageKey": "server-example"
    },
    "mainServer": true,
    "autoconnect": true,
    "modules": []
}
```

### `Server.id: string`

サーバーのIDです。ランチャーはMODの設定や選択したサーバーをIDで保存しています。IDが変更された場合、旧IDに関するデータは**全て消去されます**。

### `Server.name: string`

サーバーの名前です。これは、ユーザーがUIで見るものです。

### `Server.description: string`

サーバーの簡単な説明。ユーザーに情報を提供するためにUIに表示される。

### `Server.icon: string/url`

サーバーのアイコンへのURL。UIに表示されます。

### `Server.version: string/semver`

サーバー設定のバージョン。

### `Server.address: string/url`

サーバーのIPアドレスです。

### `Server.minecraftVersion: string`

サーバーが動作しているminecraftのバージョン。

### `Server.discord: object`

[Discord Rich Presence](https://discordapp.com/developers/docs/rich-presence/how-to)で使用するサーバー固有の設定です。

**Properties**

* `discord.shortId: string` - サーバーの短いID。ステータスの2行目に `Server: shortId` として表示される。
* `discord.largeImageText: string` - `largeImageKey` に対応するツールチップです。
* `discord.largeImageKey: string` - 大きなプロフィールアートワークのためにアップロードされた画像の名前です。

### `Server.mainServer: boolean`

配列の中の1つのサーバーだけが `mainServer` プロパティを有効にする必要があります。これはランチャーに、前に選択したサーバーが無効であったり、前に選択したサーバーがない場合に、このサーバーがデフォルトで選択されることを知らせます。このフィールドがどのサーバーにも定義されていない場合(これを避ける)、最初のサーバーがデフォルトとして選択されます。複数のサーバーで `mainServer` が有効になっている場合、ランチャーが最初に見つけたサーバーが有効な値となります。デフォルトでないサーバーは、このプロパティを明示的に false に設定するのではなく、省略することができます。

### `Server.autoconnect: boolean`

サーバーへの自動接続が可能かどうか。falseの場合、ユーザーが自動接続の設定を有効にしていても、サーバーは自動接続されない。

### `Server.modules: Module[]`

モジュールオブジェクトの配列。

---

## Module Object

モジュールとは、minecraft クライアントの実行に必要なファイルの一般的な表現です。

#### Example
```JSON
{
    "id": "com.example:artifact:1.0.0@jar.pack.xz",
    "name": "Artifact 1.0.0",
    "type": "Library",
    "artifact": {
        "size": 4231234,
        "MD5": "7f30eefe5c51e1ae0939dab2051db75f",
        "url": "http://files.site.com/maven/com/example/artifact/1.0.0/artifact-1.0.0.jar.pack.xz"
    },
    "subModules": [
        {
            "id": "examplefile",
            "name": "Example File",
            "type": "File",
            "artifact": {
                "size": 23423,
                "MD5": "169a5e6cf30c2cc8649755cdc5d7bad7",
                "path": "examplefile.txt",
                "url": "http://files.site.com/examplefile.txt"
            }
        }
    ]
}
```

親モジュールは maven スタイルで保存され、保存先のパスはその ID で解決されます。サブモジュールは `path` を宣言しているので、その値が使用されます。

### `Module.id: string`

モジュールの ID です。タイプ `File` でないすべてのモジュールは、maven 識別子を使用しなければなりません。バージョン情報と他のメタデータは、識別子から取得されます。maven スタイルで保存されるモジュールは、識別子を使用して保存先パスを解決します。Extension` を指定しない場合、デフォルトは `jar` です。

**Template**

`my.group:arifact:version@extension`

`my/group/artifact/version/artifact-version.extension`

**Example**

`net.minecraft:launchwrapper:1.12` OR `net.minecraft:launchwrapper:1.12@jar`

`net/minecraft/launchwrapper/1.12/launchwrapper-1.12.jar`

モジュールのアーティファクトが `path` プロパティを宣言していない場合、そのパスは ID から解決されます。

### `Module.name: string`

モジュールの名前です。UIで使用します。

### `Module.type: string`

モジュールのタイプ。

### `Module.required: Required`

**OPTIONAL**

モジュールが必須であるか否かを定義する。省略された場合、モジュールは必須となる。

タイプのモジュールにのみ適用される。
* `ForgeMod`
* `LiteMod`
* `LiteLoader`


### `Module.artifact: Artifact`

モジュールのダウンロードアーティファクト。

### `Module.subModules: Module[]`

**OPTIONAL**

このモジュールが宣言しているサブモジュールの配列。一般的に、他のファイルを必要とするファイルはサブモジュールとして宣言されます。簡単な例としては、MOD とその設定ファイルです。サブモジュールはまた、それ自身のサブモジュールを宣言することもできます。このファイルは再帰的に解析されるので、制限はありません。


## Artifact Object

モジュールのアーティファクトの形式は、いくつかの事柄に依存します。最も重要な要素は、そのファイルがどこに保存されるかです。もし、クライアントファイルのルートディレクトリに置かれる単純なファイルを提供するのであれば、上で宣言した `examplefile` モジュールのような形式にすることになるでしょう。このモジュールは `path` オプションを提供し、ファイルの保存先を直接設定することができます。最終的にダウンロードされるファイルには、 `path` だけが影響します。

その他、ライブラリやMODなど、mavenスタイルでファイルを保存したい場合があります。この場合、上記のサンプルのアーティファクトのように、モジュールを宣言する必要があります。モジュールの `id` は最終的なパスを解決するために使用され、事実上 `path` プロパティを置き換えます。これは maven フォーマットで提供する必要があります。これに関する詳細な情報は、 `id` プロパティのドキュメントに記載されています。

解決/提供されたパスは、モジュールの宣言型に応じて、ベースパスに追加されます。

| Type | Path |
| ---- | ---- |
| `ForgeHosted` | ({`commonDirectory`}/libraries/{`path` OR resolved}) |
| `LiteLoader` | ({`commonDirectory`}/libraries/{`path` OR resolved}) |
| `Library` | ({`commonDirectory`}/libraries/{`path` OR resolved}) |
| `ForgeMod` | ({`commonDirectory`}/modstore/{`path` OR resolved}) |
| `LiteMod` | ({`commonDirectory`}/modstore/{`path` OR resolved}) |
| `File` | ({`instanceDirectory`}/{`Server.id`}/{`path` OR resolved}) |

`commonDirectory` と `instanceDirectory` の値は、ランチャーの config.json に格納されています。

### `Artifact.size: number`

人工物の大きさです。

### `Artifact.MD5: string`

アーティファクトのMD5ハッシュ。これはローカルのアーティファクトを検証するために使用されます。

### `Artifact.path: string`

**OPTIONAL**

ファイルが保存される場所への相対パス。これは、モジュールの宣言されたタイプのベースパスに追加される。

これが指定されない場合、パスはモジュールの ID に基づいて解決される。

### `Artifact.url: string/url`

アーティファクトのダウンロードURL。

## Required Object

### `Required.value: boolean`

**OPTIONAL**

モジュールが必要な場合。このプロパティが省略された場合、デフォルトはtrueである。

### `Required.def: boolean`

**OPTIONAL**

モジュールがデフォルトで有効になっている場合。Required.value`がfalseでない限り、何の効果もありません。このプロパティが省略された場合、デフォルトはtrueになります。

---

## Module Types

### ForgeHosted

モジュールタイプ `ForgeHosted` は forge 自体を表します。現在、ランチャーは forge サーバーのみをサポートしており、vanilla サーバーは mojang ランチャーから接続することができます。Hosted` の部分がキーポイントで、これは forge モジュールが必要なライブラリをサブモジュールとして宣言しなければならないことを意味します。

例
```json
{
    "id": "net.minecraftforge:forge:1.11.2-13.20.1.2429",
    "name": "Minecraft Forge 1.11.2-13.20.1.2429",
    "type": "ForgeHosted",
    "artifact": {
        "size": 4450992,
        "MD5": "3fcc9b0104f0261397d3cc897e55a1c5",
        "url": "http://files.minecraftforge.net/maven/net/minecraftforge/forge/1.11.2-13.20.1.2429/forge-1.11.2-13.20.1.2429-universal.jar"
    },
    "subModules": [
        {
            "id": "net.minecraft:launchwrapper:1.12",
            "name": "Mojang (LaunchWrapper)",
            "type": "Library",
            "artifact": {
                "size": 32999,
                "MD5": "934b2d91c7c5be4a49577c9e6b40e8da",
                "url": "http://mc.westeroscraft.com/WesterosCraftLauncher/files/1.11.2/launchwrapper-1.12.jar"
            }
        }
    ]
}
```

forge のすべての必要なライブラリは、forge jar ファイルのルートにある `version.json` ファイルで宣言されています。これらのライブラリーはホストされなければならず、サブモジュールとして宣言されなければなりません（MUST）。

必要なライブラリがランチャーによって解決され、forge のサーバーからダウンロードされるような `Forge` タイプを追加する計画がありました。しかし、forge サーバーは時々ダウンするので、この計画は中途半端なまま停止されました。

---

### LiteLoader

モジュールタイプ `LiteLoader` は liteloader を表す。これはライブラリとして扱われ、ランタイムにクラスパスに追加される。liteloader が存在し、有効になっていると、特別な起動条件が実行されます。このモジュールはオプションで、 `ForgeMod` や `Litemod` モジュールと同様にトグルすることができる。

例
```json
{
    "id": "com.mumfrey:liteloader:1.11.2",
    "name": "Liteloader (1.11.2)",
    "type": "LiteLoader",
    "required": {
        "value": false,
        "def": false
    },
    "artifact": {
        "size": 1685422,
        "MD5": "3a98b5ed95810bf164e71c1a53be568d",
        "url": "http://mc.westeroscraft.com/WesterosCraftLauncher/files/1.11.2/liteloader-1.11.2.jar"
    },
    "subModules": [
        "All LiteMods go here"
    ]
}
```

---

### Library

モジュールタイプ `Library` は minecraft プロセスを開始するために必要なライブラリファイルを表します。各ライブラリモジュールは、ゲームプロセスを構築する際に `-cp` (クラスパス) 引数に動的に追加されます。

例

```json
{
    "id": "net.sf.jopt-simple:jopt-simple:4.6",
    "name": "Jopt-simple 4.6",
    "type": "Library",
    "artifact": {
        "size": 62477,
        "MD5": "13560a58a79b46b82057686543e8d727",
        "url": "http://mc.westeroscraft.com/WesterosCraftLauncher/files/1.11.2/jopt-simple-4.6.jar"
    }
}
```

---

### ForgeMod

モジュールタイプ `ForgeMod` は Forge Mod Loader (FML) によってロードされる mod を表します。これらのファイルは maven スタイルで保存され、forge の [Modlist format](https://github.com/MinecraftForge/FML/wiki/New-JSON-Modlist-format) を使って FML に渡されます。

例
```json
{
    "id": "com.westeroscraft:westerosblocks:3.0.0-beta-6-133",
    "name": "WesterosBlocks (3.0.0-beta-6-133)",
    "type": "ForgeMod",
    "artifact": {
        "size": 16321712,
        "MD5": "5a89e2ab18916c18965fc93a0766cc6e",
        "url": "http://mc.westeroscraft.com/WesterosCraftLauncher/prod-1.11.2/mods/WesterosBlocks.jar"
    }
}
```

---

### LiteMod

モジュールタイプ `LiteMod` は liteloader によってロードされる mod を表します。これらのファイルは maven スタイルで保存され、forge の [Modlist format](https://github.com/MinecraftForge/FML/wiki/New-JSON-Modlist-format) を使って liteloader に渡されます。liteloader の実装に関するドキュメントは [this issue](http://develop.liteloader.com/liteloader/LiteLoader/issues/34) にあります。

例
```json
{
    "id": "com.mumfrey:macrokeybindmod:0.14.4-1.11.2@litemod",
    "name": "Macro/Keybind Mod (0.14.4-1.11.2)",
    "type": "LiteMod",
    "required": {
        "value": false,
        "def": false
    },
    "artifact": {
        "size": 1670811,
        "MD5": "16080785577b391d426c62c8d3138558",
        "url": "http://mc.westeroscraft.com/WesterosCraftLauncher/prod-1.11.2/mods/macrokeybindmod.litemod"
    }
}
```

---

### File

モジュールタイプ `file` は、クライアントや他のモジュールなどが必要とする一般的なファイルを表します。これらのファイルはサーバのインスタンスディレクトリに格納される。

例

```json
{
    "id": "com.westeroscraft:westeroscraftrp:2017-08-16",
    "name": "WesterosCraft Resource Pack (2017-08-16)",
    "type": "file",
     "artifact": {
        "size": 45241339,
        "MD5": "ec2d9fdb14d5c2eafe5975a240202f1a",
        "path": "resourcepacks/WesterosCraft.zip",
        "url": "http://mc.westeroscraft.com/WesterosCraftLauncher/prod-1.11.2/resourcepacks/WesterosCraft.zip"
    }
}
```
