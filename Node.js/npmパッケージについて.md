
---
## 学んだこと
//41
- プロジェクトを共有する際はnode_modulesではなく、package.jsonのみを共有すればよい。
- package.jsonがnpmの必要なバージョンを定義して保持している。
- "weboack" : "^5.0.0" -> ^（キャレット）がついていると、その先頭バージョン（５）の中で、最も新しいマイナーバージョンをインストールする
- 厳密なバージョン管理をしたい場合はpackage-lock.jsonを参照する。このときは
  npm ci　でインストールする

//42
- package.jsonの中でdevDependenciesでインストールしたパッケージを記述
- scriptsの中にdev,start,...とコマンドを記述し、その先にパッケージを記述
- npm run dev/start/...でパッケージを実行

```json
{
  "name": "npm-script",
  "version": "1.0.0",
  "main": "main.js",
  "type": "module",
  "private": true,
  
  "scripts": {
    "dev": "node main.js",
    "start": "live-server index.html --port=3000"
  },
  
  "author": "",
  "license": "ISC",
  "keywords": [],
  "description": "",
  "dependencies": {
    "is-odd": "^3.0.1"
  },
  "devDependencies": {
    "live-server": "^1.2.2"
  }
}
//実行
//npm start -> live-serverが起動
```
//43
- node_modulesを見つけられる階層（start->node_modules->bin,,,,ならstartディレクトリにいるとき）ならnpxコマンドが使える
- =>グローバルパッケージでインストールすればどのディレクトリにいても使用できる
- 