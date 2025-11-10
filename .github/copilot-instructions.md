# Vue.js 映画レビューアプリ - Copilot Instructions

## プロジェクト概要
Vue.js 3 + Viteを使用した映画の感想を記録・管理するアプリケーション

## アーキテクチャ

### コンポーネント構成
- **App.vue**: ルートコンポーネント。映画データの状態管理と子コンポーネント間の連携
- **MovieForm.vue**: 映画追加フォーム。バリデーションと入力制御を含む
- **MovieList.vue**: 映画一覧の表示とグリッドレイアウト
- **MovieCard.vue**: 個別の映画カード。評価表示と削除機能

### データフロー
1. `App.vue`が`movies`配列をリアクティブな状態として管理
2. `MovieForm`が新しい映画を`add-movie`イベントで通知
3. `App.vue`が映画を追加し、`MovieList`にpropsで渡す
4. `MovieCard`が削除イベントを発火し、親コンポーネントまで伝播

## 開発ワークフロー

### セットアップ
```bash
npm install        # 依存関係のインストール
npm run dev        # 開発サーバー起動 (http://localhost:5173)
npm run build      # 本番ビルド
```

### 重要な規約
- **Composition API使用**: `<script setup>`構文を採用
- **リアクティブデータ**: `ref()`を使用した状態管理
- **イベント通信**: 親子間のデータフローは`emit`で実装
- **スタイル**: Scoped CSSとグラデーション背景を多用

### コンポーネント拡張時の注意点
- 新しいコンポーネントは`src/components/`に配置
- propsとemitsは明示的に定義する
- レスポンシブデザイン（768px breakpoint）を考慮

## 今後の拡張
- データ永続化（localStorage/API連携）
- 編集・検索機能の追加
- 画像アップロード機能
