# Googleフォーム連携セットアップガイド

このドキュメントは、idealjapanのウェブサイトとGoogleフォームを連携させるための詳細なセットアップ手順を提供します。

## 1. Googleフォームの作成

### 1.1 新しいフォームを作成

1. Google アカウントでログインし、https://forms.google.com/ にアクセスします
2. 「+」または「空白」をクリックして新しいフォームを作成します
3. フォームのタイトル（例: 「お問い合わせフォーム」）と説明を入力します

### 1.2 質問を追加

以下の3つの質問を追加します：

1. **お名前**:
   - 質問タイプ: 「短文回答」
   - 「必須」スイッチをオンにする

2. **メールアドレス**:
   - 質問タイプ: 「短文回答」 
   - 「必須」スイッチをオンにする
   - 「回答の検証」をクリックして「メールアドレス」を選択

3. **メッセージ**:
   - 質問タイプ: 「段落」（長文回答）
   - 「必須」スイッチをオンにする

### 1.3 設定を確認

1. 右上の「設定」アイコンをクリックします
2. 「全般」タブで適切な設定を選択します
3. 「回答」タブで「回答を収集する」がオンになっていることを確認します
4. 「保存」をクリックします

## 2. フォームIDと項目IDの取得

### 2.1 フォームIDを取得

1. フォームの編集画面でURLを確認します（例: `https://docs.google.com/forms/d/e/[フォームID]/viewform`）
2. `[フォームID]` の部分がフォームIDです（例: `1FAIpQLSdl6ByHUV6Y86z99F1fLaEvDI0Y3NQwu39LGUqz43XS6tP2lQ`）

### 2.2 項目IDを取得

1. ブラウザでフォームを開きます
2. 右クリック→「ページのソースを表示」を選択します
3. 各項目のHTMLを探し、`name="entry.XXXXXXXX"` の形式でIDを見つけます
   - お名前: `entry.272636910`
   - メールアドレス: `entry.1174798617`
   - メッセージ: `entry.141114066`

## 3. リダイレクト設定

**重要**: フォーム送信後にウェブサイトに戻ってくるための設定を行います。

1. Googleフォームの編集画面で「設定」アイコンをクリックします
2. 「プレゼンテーション」タブを選択します
3. 「確認メッセージ」セクションで、「カスタム確認メッセージを表示する」を選択します
4. 必要なメッセージを入力します（例: 「送信ありがとうございます。担当者から連絡いたします。」）
5. 「回答送信後に表示するページ」として、以下のURLを設定します:
   ```
   https://www.example.com/index.html#form-success
   ```
   （「example.com」は実際のウェブサイトのドメインに置き換えてください）

## 4. HTMLファイルの更新

`contact-form.html` ファイル内のiframeのsrc属性を、作成したGoogleフォームのURLに更新します：

```html
<iframe id="google-form-iframe" 
  src="https://docs.google.com/forms/d/e/[YOUR_FORM_ID]/viewform?embedded=true" 
  width="100%" height="650" frameborder="0" marginheight="0" marginwidth="0">
  読み込み中...
</iframe>
```

`[YOUR_FORM_ID]` を実際のフォームIDに置き換えてください。

## 5. トラブルシューティング

### 5.1 フォームが送信されない場合

- ブラウザのコンソール（F12キー）でエラーメッセージを確認します
- Google フォームのURLが正しいか確認します
- iframeのセキュリティ設定により制限がかかっていないか確認します

### 5.2 送信後のリダイレクトが機能しない場合

- リダイレクトURLが正しく設定されているか確認します
- URLにハッシュタグ（#form-success）が含まれているか確認します
- JavaScriptのコンソールでエラーメッセージがないか確認します

## 6. 参考リンク

- [Google Forms API ドキュメント](https://developers.google.com/forms/api/guides)
- [iframeのセキュリティに関する情報](https://developer.mozilla.org/ja/docs/Web/HTML/Element/iframe)
- [クロスオリジンリソース共有 (CORS) について](https://developer.mozilla.org/ja/docs/Web/HTTP/CORS)