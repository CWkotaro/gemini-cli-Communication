事前準備 instructionsディレクトリ配下を任意の箇所に置く
tmpディレクトリを作成しておく

xxxxx---instructions---+--boss.md
      |-tmp            |--president.md
                       |--worker.md

                       
起動方法
 ステップ 1: 各エージェント用のPowerShellウィンドウを開く


  合計で少なくとも4つのPowerShellウィンドウを開きます。


   * President (あなた自身): 1つ
   * Boss Agent: 1つ
   * Worker Agent 1: 1つ
   * Worker Agent 2: 1つ
      (必要に応じて Worker Agent 3 なども追加できます)

  手順:


   1. Windows Terminal を開きます。
   2. 新しいタブ（Ctrl + Shift + T）または新しいウィンドウ（Ctrl + Shift + N）で、PowerShell プロファイルを選択して、合計4つ以上のPowerShellセッションを準備します。

  ステップ 2: 各PowerShellウィンドウでプロジェクトルートに移動する

  開いたすべてのPowerShellウィンドウで、以下のコマンドを実行してプロジェクトのルートディレクトリに移動します。



   1 cd C:\AIOCR\Claude-Code-Communication-main\Claude-Code-Communication-main


  ステップ 3: 各エージェントを起動する

  各PowerShellウィンドウで、対応するエージェントの役割をGeminiに指示します。


   1. Boss Agent のウィンドウ:
       * このPowerShellウィンドウで、Geminiに以下のプロンプトを入力し、Enterを押します。

   1         You are the boss agent. Your instructions are in instructions/boss.md. Read them and begin your autonomous operation immediately.

       * Geminiは instructions/boss.md を読み込み、その指示に従って ./tmp/request.txt ファイルの監視を開始します。

   2. Worker Agent 1 のウィンドウ:
       * このPowerShellウィンドウで、Geminiに以下のプロンプトを入力し、Enterを押します。


   1         You are worker agent 1. Your instructions are in instructions/worker.md. Read them and begin your autonomous operation immediately.
             
       * Geminiは instructions/worker.md を読み込み、その指示に従って ./tmp/task_worker1.txt ファイルの監視を開始します。


   3. Worker Agent 2 のウィンドウ:
       * このPowerShellウィンドウで、Geminiに以下のプロンプトを入力し、Enterを押します。

   1         You are worker agent 2. Your instructions are in instructions/worker.md. Read them and begin your autonomous operation immediately.

       * Geminiは instructions/worker.md を読み込み、その指示に従って ./tmp/task_worker2.txt ファイルの監視を開始します。

      (Worker Agent 3 を起動する場合は、同様に `worker agent 3` と指示します。)


  ステップ 4: President (あなた自身) としてプロジェクトを開始する

  President (あなた自身) のPowerShellウィンドウで、以下のコマンドを実行して、Bossエージェントに最初の指示を与えます。



   1 echo "Create a simple 'Hello World' website in a project folder named 'hello-world-site'." > ./tmp/request.txt


   * このコマンドは、C:\AIOCR\Claude-Code-Communication-main\Claude-Code-Communication-main\tmp ディレクトリ内に request.txt というファイルを作成し、その中にあなたの指示を書き込みます。


  ステップ 5: プロジェクトの進行を監視する


   * Boss Agent のウィンドウを観察してください。request.txt を検知し、削除し、プロジェクト計画を作成し、Workerにタスクを割り当て始めるはずです。
   * Worker Agent のウィンドウを観察してください。Bossから割り当てられたタスクを検知し、実行し、完了報告を返すはずです。
   * C:\AIOCR\Claude-Code-Communication-main\Claude-Code-Communication-main\tmp ディレクトリの中身を定期的に確認してください。request.txt が消えたり、task_workerX.txt や done_workerX.txt
     が現れたり消えたりするのを確認できます。
   * Bossエージェントが作成する新しいプロジェクトディレクトリ（例: C:\AIOCR\Claude-Code-Communication-main\Claude-Code-Communication-main\workspace\hello-world-site）の中身も確認してください。

  ---

  重要な注意点:


   * instructions/worker.md 内の eval "$TASK_INSTRUCTION" コマンドは、Bossから受け取った文字列をそのままシェルコマンドとして実行します。これは非常に強力ですが、悪意のあるコマンドが実行されるリスクも伴います。このデモ
     の範囲内では問題ありませんが、実際の運用では注意が必要です。
   * エージェントはファイルシステムを監視し続けるため、停止するには各Geminiインスタンスを終了させる必要があります（通常は Ctrl+C）。
