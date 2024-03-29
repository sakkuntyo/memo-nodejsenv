
# 環境構築(Windows)
1. 以下から nvm の nvm-setup.exe を ダウンロードしてインストール

https://github.com/coreybutler/nvm-windows/releases

nvm ・・・ nodejs の バージョン管理ツール

2. powershell で nvm コマンドがインストールされた事を確認
```
> nvm
Running version 1.1.10.

Usage:

  nvm arch                     : Show if node is running in 32 or 64 bit mode.
  nvm current                  : Display active version.
  nvm install <version> [arch] : The version can be a specific version, "latest" for the latest current version, or "lts" for the
                                 most recent LTS version. Optionally specify whether to install the 32 or 64 bit version (defaults
                                 to system arch). Set [arch] to "all" to install 32 AND 64 bit versions.
                                 Add --insecure to the end of this command to bypass SSL validation of the remote download server.
  nvm list [available]         : List the node.js installations. Type "available" at the end to see what can be installed. Aliased as ls.
  nvm on                       : Enable node.js version management.
  nvm off                      : Disable node.js version management.
  nvm proxy [url]              : Set a proxy to use for downloads. Leave [url] blank to see the current proxy.
                                 Set [url] to "none" to remove the proxy.
  nvm node_mirror [url]        : Set the node mirror. Defaults to https://nodejs.org/dist/. Leave [url] blank to use default url.
  nvm npm_mirror [url]         : Set the npm mirror. Defaults to https://github.com/npm/cli/archive/. Leave [url] blank to default url.
  nvm uninstall <version>      : The version must be a specific version.
  nvm use [version] [arch]     : Switch to use the specified version. Optionally use "latest", "lts", or "newest".
                                 "newest" is the latest installed version. Optionally specify 32/64bit architecture.
                                 nvm use <arch> will continue using the selected version, but switch to 32/64 bit mode.
  nvm root [path]              : Set the directory where nvm should store different versions of node.js.
                                 If <path> is not set, the current root will be displayed.
  nvm [--]version              : Displays the current running version of nvm for Windows. Aliased as v.
```

3. nvm で nodejs を インストールする
```
> nvm install 18.15.0
```

4. インストール済の nodejs から使用するバージョンを指定
```
> nvm use 18.15.0
```

5. nodejs がインストールされた事を確認
```
> node -v
v18.15.0
```

6. visual studio code をダウンロードしてインストール、オプションは全て気にせず次へ、でok

https://code.visualstudio.com/docs/?dv=win

7. git を 以下でインストール
```
> winget install --id Git.Git -e --source winget
```

8. PowerShell を起動しなおして、git がインストールされた事を確認
```
> git -v
git version 2.38.1.windows.1
```

# bot の導入から起動 (Windows)

サンプルアプリ: https://github.com/sakkuntyo/discord-sktrythmjs2

1. discord developer から色々設定していく
    1. アプリケーション作成
    2. intent 全て許可
    3. Client ID と トークンのコピー
    4. URL作成(bot と application.command)

この後から PowerShell で以下を実行していく

2. コードの clone

```PowerShell
mkdir C:\sktrythmjs2
cd C:\sktrythmjs2
git clone https://github.com/sakkuntyo/discord-sktrythmjs2
cd C:\sktrythmjs2\discord-sktrythmjs2
npm install
```

3. コードのビルド(Typescript)

```PowerShell
npm run compile
```

4. コードの実行

```PowerShell
npm run start
```

5. OSと同時に起動する様にする

管理者権限で PowerShell を起動して以下実行

```PowerShell
Set-ExecutionPolicy Unrestricted
```

```PowerShell
npm install -g pm2-windows-startup pm2
pm2 start .\build\main.js --name=rythm2
pm2-startup install
pm2 save
```

6. OSと同時に起動するアプリの一覧

```PowerShell
pm2 list
```

7. OSと同時に起動しない様にする

```PowerShell
pm2 delete rythm2
pm2 save
```

8. 再起動

```PowerShell
pm2 restart
```
