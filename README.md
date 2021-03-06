## Kojs3
競技プログラミング用オンラインジャッジシステム  
(C) 2021 - 2022 Tatsuto Yamamoto

## レポジトリ(コード置き場)
- [スコアサーバー バックエンド (TypeScript)](https://github.com/laminne/kojs3-backend)
- [スコアサーバー フロントエンド (HTML+TypeScript)](https://github.com/laminne/kojs3-front)
- [コンテナマネージャ (Go)](https://github.com/laminne/kojs3-worker-manager)
- [ジャッジ/コード実行部分 (Go)](https://github.com/laminne/kojs3-worker)
- [キュー監視スクリプト (TypeScript)](https://github.com/laminne/kojs3-queue-manager)

## 実行のフロー

![https://kroki.io/plantuml/svg/eNqVks1OAjEUhfd9igbXvgALF8alj8AGkehEMxCCiUvbGw0IRCSQaKIg_mIMwwJHMCA8zKUz-BZ2ZiK_nRE3TdN-5_T03ksopcloKq3FtGRUT1OECkIToY2QQd5wN1myBBURAHlrQkhgCeLS5gmhv3zRdkVnCOcIVYSChJB3ER4I2Ukc09BWInYQT4Xo2ra2t5_ePDyKK9wd3k3RRd5B_uka3pG4vkulCSHKn9D1DVX6MLWbZaueQWa46fryEHnp-4QhzxGFQGkTprPi0fBWNK_8xL_FoTMiYdTG9by4_Br1HsmUWMBFtjAXkxkR3VMiy9smR34hQyMbIHsRg1Prtbbo5Vt-_yy-khUcp42yy405lpfGZkfkKn8_oG72fMHHvXvZMOIHr27k_T3YKLD5zPAsbLNoVW-caMMysut_DNJEGTxFqhGfEUd0hGe3kh_Oyt5kDlF4Jz8TQFub](https://kroki.io/plantuml/svg/eNqVks1OAjEUhfd9igbXvgALF8alj8AGkehEMxCCiUvbGw0IRCSQaKIg_mIMwwJHMCA8zKUz-BZ2ZiK_nRE3TdN-5_T03ksopcloKq3FtGRUT1OECkIToY2QQd5wN1myBBURAHlrQkhgCeLS5gmhv3zRdkVnCOcIVYSChJB3ER4I2Ukc09BWInYQT4Xo2ra2t5_ePDyKK9wd3k3RRd5B_uka3pG4vkulCSHKn9D1DVX6MLWbZaueQWa46fryEHnp-4QhzxGFQGkTprPi0fBWNK_8xL_FoTMiYdTG9by4_Br1HsmUWMBFtjAXkxkR3VMiy9smR34hQyMbIHsRg1Prtbbo5Vt-_yy-khUcp42yy405lpfGZkfkKn8_oG72fMHHvXvZMOIHr27k_T3YKLD5zPAsbLNoVW-caMMysut_DNJEGTxFqhGfEUd0hGe3kh_Oyt5kDlF4Jz8TQFub)

## 実装言語
- スコアサーバー
    - バックエンド: TypeScript (Express.js)
    - フロントエンド: TypeScript (ライブラリなし)
- マネージャ,ジャッジ部分: Golang

### 実行コンテナ制御

コード実行環境はDocker(コンテナ型仮想環境)を利用  
実行コンテナの作成,起動,削除などの操作はGo向けDocker公式ライブラリを利用  

### キューイング/ 分散化
実行サーバーを冗長化/スケールアウトさせることが可能  
コンテナマネージャはGinによる小さなWebAPIとして動作しており,  
ステートレスに動作するためスケールが容易

### 攻撃対策
- Dockerコンテナをネットワークから分離
- メモリ制限はコンテナ側で行っている為MLE(メモリ制限超過)した場合コンテナごと落ちる
- フォーク爆弾(再帰的にプロセスを増やし、コンピュータをフリーズさせるウイルス的プログラムの一種)対策としてpidLimitを512に制限

## 仕様
### 対応言語

- [x]  C (GCC GNUC11)
- [x]  C (Clang C11)
- [x]  C++ (g++ GNUC++11)
- [x]  C++ (Clang++ C++11)
- [x]  Ruby (CRuby 3.x)
- [x]  JavaScript (nodejs 14.x)

## コード量 (参考データ)
4月5日時点  
```
-------------------------------------------------------------------------------
言語                       ファイル数            空行        コメント          コード
-------------------------------------------------------------------------------
TypeScript                      39            132            116           1115
Go                              12             63             20            503
HTML                            11             44             32            422
-------------------------------------------------------------------------------
SUM:                            62            239            168           2040
-------------------------------------------------------------------------------
```
