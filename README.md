# ReactiveBash
ツンデレの女の子「bashたん」がコマンドを入力するたびに反応を返してくれます。

## 前提
1. LLMサーバの導入・起動
   
   LLMサーバがエンドポイント```http://localhost:8080/v1/completion```で反応を返してくれる状態にある必要があります。

   ~~~bash
   # 導入例（起動例は ## 使い方 を参照）
   # モデルのダウンロード
   mkdir -p ~/llama
   cd ~/llama
   curl -L -O https://huggingface.co/unsloth/gemma-4-E4B-it-GGUF/resolve/main/gemma-4-E4B-it-Q4_K_M.gguf
   # LLMサーバのインストール
   yay -S llama.cpp
   ~~~

2. その他依存しているものの導入
   - jq
     
     JSONパーサです。

     ~~~bash
     sudo pacman -S jq
     ~~~
     
   - bash-preexec
     
     公開元：[rcaloras/bash-preexec](https://github.com/rcaloras/bash-preexec/)
     
     bashのカスタマイズスクリプトです。一回のコマンド入力に一回の反応を返すための判定に使っています。
     スクリプトでは、```$HOME```に```./bash-preexec.sh```があることを前提に、```source```で読み込んでいます。```.bashrc```等ですでに読んでいるひとや、ほかの場所にファイルを置いておきたいひとは、適宜修正してください。

     ~~~bash
     curl https://raw.githubusercontent.com/rcaloras/bash-preexec/master/bash-preexec.sh -o ~/.bash-preexec.sh
     ~~~

## 使い方

ファイル```run```をインポートするだけです。

~~~bash
# 例
llama-server -m /path/to/the/LLM/model > /dev/null 2>&1 &
source ~/ReactiveShell/run
~~~

## 実行例
[sample.webp]

