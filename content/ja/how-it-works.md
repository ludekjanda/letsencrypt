---
title: 動作の仕組み
linkTitle: Let's Encrypt の動作のしくみ
slug: how-it-works
lastmod: 2024-06-26
show_lastmod: 1
---


Let's&nbsp;Encrypt と [ACME プロトコル](https://tools.ietf.org/html/rfc8555)の目標は、HTTPS サーバーのセットアップと、ブラウザが信頼する証明書の自動的な取得を、人間の仲介なしに可能にすることです。  この目標は、ウェブサーバー上で証明書管理エージェントを実行することで実現されます。

この技術がどのような仕組みなのかを理解するために、Let's&nbsp;Encrypt をサポートする証明書管理エージェントを使用して `https://example.com/` を設定する過程を見ていきましょう。

このプロセスには2つのステップがあります。  1つ目は、CA に対して、ウェブサーバーがドメインをコントロールしていることを証明するプロセスです。  2つ目は、そのドメインに対して、エージェントが証明書のリクエスト・更新・無効化を行うプロセスです。

## ドメインの検証

Let's&nbsp;Encrypt はサーバーの管理者を公開鍵で特定します。  エージェントソフトウェアが Let's&nbsp;Encrypt と初めて通信するとき、新しいキーペアを生成し、Let's&nbsp;Encrypt CA に対して、1つ以上のドメインがコントロールしていることを証明します。  これは、アカウントを作成し、そのアカウントにドメインを追加する、という伝統的な CA プロセスと同様です。

このプロセスを始めるために、エージェントは Let's&nbsp;Encrypt CA に対して、自分が `example.com` をコントロールしていることを証明するためには何をすればいいか、と質問します。  Let's&nbsp; Encrypt CA はリクエストされたドメイン名を見て、1つ以上のチャレンジのセットを答えます。   エージェントがドメインをコントロールしていることを証明する方法は複数あるためです。  たとえば、CA はエージェントに対して、以下のような選択肢を与えます。

* `example.com` 以下の DNS で指定した情報を公開すること、あるいは、
* `http://example.com/` 上の well-known な URI で指定した HTTP リソースを公開すること

チャレンジの間に、Let's&nbsp;Encrypt CA はエージェントに対してノンスを与えます。エージェントは秘密鍵を使ってこのノンスに署名する必要があります。これにより、エージェントがキーペアをコントロールしていることも証明します。

<div class="howitworks-figure">
<img alt="example.com を検証するためのチャレンジのリクエスト"
     src="/images/howitworks_challenge.png"/>
</div>

エージェント・ソフトウェアは、提示されたチャレンジのうちの1つをクリアします。   今、上の例で提示された2つ目のチャレンジをエージェントがクリアできるとしましょう。このとき、エージェントは `http://example.com` のサイト上の特定のパスにファイルを1つ生成します。  また、エージェントは提示されたノンスに秘密鍵を使って署名します。  エージェントがこれらのステップをクリアしたら、CA に検証の準備ができたことを伝えます。

そして、[複数のネットワークの観点](/2020/02/19/multi-perspective-validation)からチャレンジが解決されていることを確認するのが CA の仕事です。  CA はノンスの署名が正しいことを検証し、ウェブサーバーからファイルをダウンロードし、その中に期待どおりのコンテンツが含まれているかどうかを確認します。

<div class="howitworks-figure">
<img alt="example.com の代表として振る舞うための認証リクエスト"
     src="/images/howitworks_authorization.png"/>
</div>

もし、ノンスに書かれた署名が有効であり、チャレンジがクリアされたならば、公開鍵を持つエージェントは `example.com` に対する証明書の管理を行うことを認証されたことになります。  私たちは、このエージェントが使用するキーペアのことを、`example.com`に対して「認証されたキーペア」と呼びます。


## 証明書の発行と無効化

一度エージェントが認証されたキーペアを取得したら、証明書のリクエスト・更新・無効化は簡単です。証明書管理メッセージを生成し、認証されたキーペアで署名して送信すればいいだけです。

ドメインの証明書を取得するには、エージェントは Let's&nbsp;Encrypt CA に対して、`example.com` の証明書を発行する依頼と公開鍵を含めた、PKCS#10 [証明書署名リクエスト (Certificate Signing Request)](https://tools.ietf.org/html/rfc2986) を作ります。  通常、CSR の中には、CSR に同梱された公開鍵に対応する秘密鍵による署名が含まれています。  さらに、エージェントは CSR 全体を `example.com` に対して認証されたキーで署名します。これにより、Let's&nbsp;Encrypt CA は CSR が認証されていることを確認できます。

Let's&nbsp;Encrypt CA がこのリクエストを受け取ると、両方の署名を検証します。  すべてが問題なければ、 `example.com` の証明書を発行し、CSR に同梱されていた公開鍵で暗号化してエージェントへ送り返します。 CA は、公開された多数の証明書透明性 (Certificate Transparency、CT) ログにも証明書を送信します。 詳しくは[こちらのページ](https://certificate.transparency.dev/howctworks/#pki)を参照してください。

<div class="howitworks-figure">
<img alt="example.com に対する証明書のリクエスト"
     src="/images/howitworks_certificate.png"/>
</div>

無効化の作業も同じ方法で行われます。  エージェントは無効化リクエストを作り、`example.com`に対して認証されたキーペアで署名をして送ります。Let's&nbsp;Encrypt CA はリクエストが認証されているかどうかを検証します。  もしそうであれば、失効情報を通常の失効チャネル  (すなわち OCSP) に公開して、 ブラウザなどのリライングパーティーが、失効した証明書を受け入れるべきではないことを知ることができるようにします。

<div class="howitworks-figure">
<img alt="example.com に対する証明書の無効化リクエスト"
     src="/images/howitworks_revocation.png"/>
</div>

