# ReactiveBash
ツンデレの女の子「bashたん」ほかがコマンドを入力するたびに反応してから実行してくれます。

## 説明
### 依存しているもの
1. LLMサーバ

   LLMサーバがエンドポイント```http://localhost:8080/v1/completion```で反応を返してくれる状態にある必要があります

2. jq

   みんな大好きJSONパーサ

   ~~~bash
   pacman -S jq
   ~~~

4. bash-preexec

   公開元：[rcaloras/bash-preexec](https://github.com/rcaloras/bash-preexec/)

   bashのカスタマイズスクリプトです。一回のコマンド入力に一回の反応を返すための判定に使っています。

   コード内では```source ~/.bash-preexec.sh```しているため、適宜書き換えてください。

### 実行

~~~bash
source run cyan  # bashたんを呼び出し
source run pink  # bashさんを呼び出し
source run yellow  # bashちゃんを呼び出し

source run  # 引数未指定の場合はcyanにフォールバック

exec bash  # 終了するにはbashを再読み込み
~~~

## LLMサーバの導入例

初めてLLMサーバを導入する人のための導入例です。不要かと思いますが念のため。

本例はローカルでLLMを動かす場合なので、しゅっとしたパソコンが必要です。

OpenAI互換エンドポイントなので、ChatGPTに課金している人はそれでも大丈夫です（コードの36行目を書き換えてください）。

~~~bash
# モデルのダウンロード
mkdir -p ~/llm_model
cd ~/llm_model
curl -L -O https://huggingface.co/unsloth/gemma-4-E4B-it-GGUF/resolve/main/gemma-4-E4B-it-Q4_K_M.gguf

# llama.cppのビルド・インストール
yay -S llama.cpp

# llama-serverの起動
llama-server -m ~/llm_model/gemma-4-E4B-it-Q4_K_M.gguf > /dev/null 2>&1 &
~~~

## 実行例

bashたん

![\[~\]$ source ReactiveShell/run&#10; bashたん &gt; 準備はできてるわよ。ほら、ぼーっとしないで。さっさと指示出しなさいよね！&#10;\[~\]$ cd ReactiveShell/&#10; bashたん &gt; ふん、別に喜んでるわけじゃないけど、さっさと移動するんだから。&#10;\[ReactiveShell\]$ ls&#10; bashたん &gt; えっ、そんな簡単なこと聞くの？別に、特別に見てあげてるわけじゃないけどね。&#10;run&#10;\[ReactiveShell\]$ touch test.txt&#10; bashたん &gt; もう、何でそんなことばっかりするのよ。勝手に作ったんだから、文句言わないでよね。&#10;\[ReactiveShell\]$ echo &quot;helloworld&quot; &gt; test.txt&#10; bashたん &gt; はいはい、文字を書き込むだけなら簡単だけど。あんまり同じこと繰り返さないでよね。&#10;\[ReactiveShell\]$ ls -la&#10; bashたん &gt; うん、全部リストアップしたけど。見て、ちゃんとあるでしょ。当たり前じゃない。&#10;total 16&#10;drwxr-xr-x  2 usrname usrname  33 May  5 20:49 .&#10;drwx--x---+ 48 usrname usrname 4096 May  5 20:49 ..&#10;-rw-r--r--  1 usrname usrname 2596 May  5 20:29 run&#10;-rw-r--r--  1 usrname usrname  11 May  5 20:50 test.txt](sample.webp)

bashちゃん、bashさん

![\[github\]\$ source ReactiveBash/run yellow&#10;&nbsp;bashちゃん &gt; やった！やっと来たね！わぁ、準備OKだよ！えーっと、さあ！ぼーっとしてないで、何か面白いことしてよ！&#10;\[github\]\$ cd ReactiveBash/&#10;&nbsp;bashちゃん &gt; わーい！ReactiveBashフォルダに入ったんだね！ 次は何するの？&#10;\[ReactiveBash\]\$ ls&#10;&nbsp;bashちゃん &gt; たくさんのファイルとディレクトリが見えたよ！何か気になるものある？✨&#10;README.md&nbsp; run&nbsp; sample.webp&#10;\[ReactiveBash\]\$ touch test.txt&#10;&nbsp;bashちゃん &gt; test.txtが新しくできたよ！これで何か試せるね！&#10;\[ReactiveBash\]\$ echo \"helloworld\" &gt; test.txt&#10;&nbsp;bashちゃん &gt; よし！test.txtの中に\"helloworld\"が入ったよ！すごい！&#10;\[ReactiveBash\]\$ exec bash&#10;&nbsp;bashちゃん &gt; あ、もう終わり！？えーっ、またすぐにね！&#10;\[ReactiveBash\]\$ cd ..&#10;\[github\]\$&#10;\[github\]\$ source ReactiveBash/run pink&#10;&nbsp;bashさん &gt; 準備はバッチリだから、遠慮せずに言ってね。一緒にゆっくり進めていこう。&#10;\[github\]\$ cd ReactiveBash/&#10;&nbsp;bashさん &gt; あら、ディレクトリ移動ね。じゃあ、ReactiveBashフォルダの中へお邪魔しちゃおうかしら？✨&#10;\[ReactiveBash\]\$ ls&#10;&nbsp;bashさん &gt; ふふ、中身を見せてくれるのね。はい、確認したわ。ファイルとフォルダがズラッと並んでいるわよ&#10;README.md&nbsp; run&nbsp; sample.webp&nbsp; test.txt&#10;\[ReactiveBash\]\$ touch test.txt&#10;&nbsp;bashさん &gt; はい、新しいファイル「test.txt」を作ってくれたのね。これで何か試せるわね♪&#10;\[ReactiveBash\]\$ echo \"helloworld\" &gt; touch.txt&#10;&nbsp;bashさん &gt; 「helloworld」をtouch.txtに書き込んだのね。これでちゃんと保存されたわよ&#10;\[ReactiveBash\]\$ exec bash&#10;&nbsp;bashさん &gt; あら、もうおしまい？もし、なんか困ったことがあったらいつでも呼んで。](sample2.webp)

bashたんたちが5秒以内に反応をくれない場合、ふつうにコードを実行することになっています。

## 応用

bashたんたちはコーディングアシスタントではなく、ただ反応を返してくれるだけのひとたちですが、叩かれたコマンドを文字列として眺めてコメントをしているので、使いようによってはコマンドを調べることもできます。ただし、本来の目的の都合上出力を50字以内にするようプロンプトで指示しているので、あまり複雑な出力は期待できません。~~プロンプトエンジニアリングが上手なひとなら回避できるのかも……？~~ ← max-token指定してるから無理じゃんね

![\[ReactiveBash\]\$ source run&#10;&nbsp;bashたん &gt; 準備はできてるわよ。ほら、ぼーっとしないで。さっさと指示出しなさいよね&#10;\[ReactiveBash\]\$ \"bashで現在の作業ディレクトリにあるファイルをすべて\$HOMEに移動するコマンドを教えてほしい\"&#10;&nbsp;bashたん &gt; 別に当たり前のことだけど、mv \* \$HOME って入力すればいいじゃん！&#10;bash: bashで現在の作業ディレクトリにあるファイルをすべて/home/sumomoに移動するコマンドを教えてほしい: No such file or directory](sample3.webp)

## 今後の構想
1. bash以外への対応

   自分がbashを使っているので目下bashのみですが、zshなどにも拡張できたらいいですね。
   
~~2. 他キャラの追加~~

   ~~ほかのキャラクターとして、bashちゃんとbashさんを増やそうかなと考えています。~~

   -> 実装しました

プロンプト部分は各人のお好みですが、それ以外の部分はPR歓迎です。

## その他

本コードは生成AIで生成したものを改変しました。生成AIのコードをわざわざgithubでシェアするものかは若干微妙だと思うんですが、代案が思いつかないこと、そもそも（もっと強い人ならともかく）自分が手書きしたコードを公開したところとて、という問題に立ち返る気がするので、一旦気にしない運用としています。
