# ReactiveBash
ツンデレの女の子「bashたん」がコマンドを入力するたびに反応してから実行してくれます。

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
source run
~~~

## LLMサーバの導入例

初めてLLMサーバを導入する人のための導入例です。不要かと思いますが念のため。

本例はローカルでLLMを動かす場合なので、しゅっとしたパソコンが必要です。

OpenAI互換エンドポイントなので、ChatGPTに課金している人はそれでも大丈夫です（コードの7行目を書き換えてください）。

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
![\[~\]$ source ReactiveShell/run&#10; bashたん &gt; 準備はできてるわよ。ほら、ぼーっとしないで。さっさと指示出しなさいよね！&#10;\[~\]$ cd ReactiveShell/&#10; bashたん &gt; ふん、別に喜んでるわけじゃないけど、さっさと移動するんだから。&#10;\[ReactiveShell\]$ ls&#10; bashたん &gt; えっ、そんな簡単なこと聞くの？別に、特別に見てあげてるわけじゃないけどね。&#10;run&#10;\[ReactiveShell\]$ touch test.txt&#10; bashたん &gt; もう、何でそんなことばっかりするのよ。勝手に作ったんだから、文句言わないでよね。&#10;\[ReactiveShell\]$ echo &quot;helloworld&quot; &gt; test.txt&#10; bashたん &gt; はいはい、文字を書き込むだけなら簡単だけど。あんまり同じこと繰り返さないでよね。&#10;\[ReactiveShell\]$ ls -la&#10; bashたん &gt; うん、全部リストアップしたけど。見て、ちゃんとあるでしょ。当たり前じゃない。&#10;total 16&#10;drwxr-xr-x  2 usrname usrname  33 May  5 20:49 .&#10;drwx--x---+ 48 usrname usrname 4096 May  5 20:49 ..&#10;-rw-r--r--  1 usrname usrname 2596 May  5 20:29 run&#10;-rw-r--r--  1 usrname usrname  11 May  5 20:50 test.txt](sample.webp)

## 今後の構想
1. bash以外への対応

   自分がbashを使っているので目下bashのみですが、zshなどにも拡張できたらいいですね。
   
2. 他キャラの追加

   ほかのキャラクターとして、bashちゃんとbashさんを増やそうかなと考えています。

プロンプト部分は各人のお好みですが、それ以外の部分はPR歓迎です。

## その他

本コードは生成AIで生成したものを改変しました。生成AIのコードをわざわざgithubでシェアするものかは若干微妙だと思うんですが、代案が思いつかないこと、そもそも（もっと強い人ならともかく）自分が手書きしたコードを公開したところとて、という問題に立ち返る気がするので、一旦気にしない運用としています。
