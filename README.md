# Lamda and api gateway

## LamdaとAPI Gatewayを使ってR


### (1)Lambaのダッシュボードを開きます。

<img src="./images/スクリーンショット 2024-10-24 15.22.20.png" alt="サンプル画像">


### (2)関数名を入力して、関数の作成ボタンを押します
一から作成を選択して、<br>
任意の関数名を設定します。<br>
今回は「timeout-response」にしています。<br>
関数名を入力したら、下にスクロールして「関数の作成」ボタンを押します。
今回はNode.jsをランタイムとして選択します。
<img src="./images/スクリーンショット 2024-10-24 15.33.57.png">

### (3)作成済みの画面

<img src="./images/スクリーンショット 2024-10-24 15.35.30.png">

### (4)レスポンスのコードを書いてdeployボタンを押す
画面下部のコードタブを開いて
以下のコードを挿入します。<br>
このコードは20秒後にstatus200でレスポンスを返すコードです。

```main.js
export const handler = async (event) => {
  const delay = 20;

  await new Promise((resolve) => setTimeout(resolve, delay * 1000));

  const response = {
    statusCode: 200,
    body: JSON.stringify(`This response was delayed by ${delay} seconds.`),
  };
  return response;
};

```

コードを書いたらDeployボタンを押します。

<img src="./images/スクリーンショット 2024-10-24 15.37.09.png">


### (5)Lambdaのタイムアウトの設定を変更する
画面下部の設定タブを開いて編集を押します
<img src="./images/スクリーンショット 2024-10-24 15.46.53.png">
タイムアウトを3分とか5分とかにしておきます。<br>
3秒のままだと、JSで書いたコードが意味をなしません。
<img src="./images/スクリーンショット 2024-10-24 15.47.03.png">

### (6)API Gatewayのダッシュボードを開く

<img src="./images/スクリーンショット 2024-10-24 15.51.01.png">
REST APIを選択します。
<img src="./images/スクリーンショット 2024-10-24 15.51.08.png">
新しいAPIを選択して、任意のAPI名をつけます。<br>
今回は「timeout-response」にしました。
<img src="./images/スクリーンショット 2024-10-24 15.51.23.png">
作成後のページがこちら
<img src="./images/スクリーンショット 2024-10-24 15.51.23.png">

### (7) API GatewayにLambdaを割り当てる
メソッドを作成ボタンを押します
<img src="./images/スクリーンショット 2024-10-24 15.54.02.png">
メソッドタイプGETを選択して、先ほど作ったLambda関数を選択します
<img src="./images/スクリーンショット 2024-10-24 15.54.24.png">
画面下部のメソッドを作成ボタンを押します。
<img src="./images/スクリーンショット 2024-10-24 15.54.32.png">
作成されました。<br>
APIをデプロイボタンを押します。
<img src="./images/スクリーンショット 2024-10-24 15.54.40.png">
新しいステージを選択して、任意の名前をつけます。<br>
そして、デプロイボタンを押します。
<img src="./images/スクリーンショット 2024-10-24 15.54.48.png">
デプロイされました。
<img src="./images/スクリーンショット 2024-10-24 15.55.02.png">
urlをコピペして、curlを実行します。
<img src="./images/スクリーンショット 2024-10-24 15.56.52.png">
作成後は削除してください。


