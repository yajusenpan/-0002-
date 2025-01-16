<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lorenz SZ 40/42 暗号機 シミュレーション</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            line-height: 1.6;
            margin: 20px;
            background-color: #000;  /* 背景色を黒に */
            color: #FF0000;  /* テキスト色を赤に */
        }
        h1 {
            text-align: center;
            color: #FF0000;  /* 見出しも赤に */
        }
        .container {
            max-width: 800px;
            margin: 0 auto;
            background-color: #222;  /* コンテナの背景を黒っぽく */
            padding: 20px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.7);
            border-radius: 10px;
        }
        label {
            font-weight: bold;
            color: #FF0000;  /* ラベルを赤に */
        }
        textarea {
            width: 100%;
            height: 100px;
            padding: 10px;
            margin: 10px 0;
            border: 1px solid #FF0000;  /* 枠線を赤に */
            border-radius: 5px;
            background-color: #333;  /* 入力エリアの背景を暗く */
            color: #FF0000;  /* 入力テキストを赤に */
        }
        button {
            padding: 10px 20px;
            background-color: #FF0000;  /* ボタン背景色を赤に */
            color: #000;  /* ボタンの文字色を黒に */
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        button:hover {
            background-color: #cc0000;  /* ボタンをホバー時に少し暗く */
        }
        .result {
            margin-top: 20px;
            font-size: 1.2em;
            padding: 10px;
            background-color: #333;  /* 結果エリアの背景を暗く */
            border: 1px solid #FF0000;  /* 枠線を赤に */
            border-radius: 5px;
            color: #FF0000;  /* 結果のテキストを赤に */
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Lorenz SZ 40/42 暗号機 シミュレーション</h1>

        <label for="message">メッセージを入力してください:</label>
        <textarea id="message" placeholder="メッセージを入力"></textarea>

        <button onclick="encryptMessage()">暗号化</button>
        <button onclick="decryptMessage()">解読</button>

        <div class="result" id="processedMessage">
            処理結果がここに表示されます。
        </div>
    </div>

    <script>
        // ローターのシンプルなシミュレーション
        const rotorPositions = [
            'ABCDEFGHIJKLMNOPQRSTUVWXYZ',   // ローター1
            'ZYXWVUTSRQPONMLKJIHGFEDCBA',   // ローター2（反転）
            'QWERTYUIOPLKJHGFDSAZXCVBNMASD', // ローター3（ランダムに配置）
        ];

        function encryptMessage() {
            let message = document.getElementById("message").value.toUpperCase().replace(/[^A-Z]/g, '');
            let encrypted = "";

            for (let i = 0; i < message.length; i++) {
                let char = message[i];
                let encryptedChar = encryptCharacter(char, i);
                encrypted += encryptedChar;
            }

            document.getElementById("processedMessage").innerText = "暗号化されたメッセージ: " + encrypted;
        }

        function decryptMessage() {
            let message = document.getElementById("message").value.toUpperCase().replace(/[^A-Z]/g, '');
            let decrypted = "";

            for (let i = 0; i < message.length; i++) {
                let char = message[i];
                let decryptedChar = decryptCharacter(char, i);
                decrypted += decryptedChar;
            }

            document.getElementById("processedMessage").innerText = "解読されたメッセージ: " + decrypted;
        }

        // メッセージ内の各文字を暗号化する関数
        function encryptCharacter(char, index) {
            let rotorIndex = index % rotorPositions.length;  // ローターを切り替える
            let rotor = rotorPositions[rotorIndex];
            let charIndex = rotor.indexOf(char);  // 文字をローター上で検索
            if (charIndex === -1) return char;  // 無効な文字が入力された場合（例えば記号）

            // 文字をローターで変換
            let encryptedChar = rotor[(charIndex + 1) % rotor.length];  // シンプルなシフト暗号化
            return encryptedChar;
        }

        // メッセージ内の各文字を解読する関数
        function decryptCharacter(char, index) {
            let rotorIndex = index % rotorPositions.length;  // ローターを切り替える
            let rotor = rotorPositions[rotorIndex];
            let charIndex = rotor.indexOf(char);  // 文字をローター上で検索
            if (charIndex === -1) return char;  // 無効な文字が入力された場合（例えば記号）

            // 文字をローターで逆変換
            let decryptedChar = rotor[(charIndex - 1 + rotor.length) % rotor.length];  // シンプルなシフト逆暗号化
            return decryptedChar;
        }
    </script>
</body>
</html>
