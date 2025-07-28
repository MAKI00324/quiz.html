<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>更年期体質タイプ別・やせ習慣診断</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Hiragino Kaku Gothic Pro', 'ヒラギノ角ゴ Pro', 'Yu Gothic Medium', '游ゴシック Medium', YuGothic, '游ゴシック体', 'Meiryo', sans-serif;
            background: linear-gradient(135deg, #ff9a56 0%, #ff6b35 50%, #f7931e 100%);
            min-height: 100vh;
            padding: 10px;
            line-height: 1.6;
        }
        
        .container {
            max-width: 500px;
            margin: 0 auto;
            background: white;
            border-radius: 16px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.15);
            overflow: hidden;
        }
        
        .header {
            background: linear-gradient(135deg, #ff9a56, #ff6b35);
            color: white;
            padding: 20px;
            text-align: center;
        }
        
        .header h1 {
            font-size: clamp(18px, 5vw, 24px);
            margin-bottom: 8px;
            font-weight: 700;
        }
        
        .header p {
            font-size: clamp(12px, 3.5vw, 14px);
            opacity: 0.95;
        }
        
        .content {
            padding: 20px;
        }
        
        .question-container {
            margin-bottom: 25px;
        }
        
        .question {
            font-size: clamp(16px, 4vw, 18px);
            font-weight: 600;
            margin-bottom: 15px;
            color: #333;
            line-height: 1.5;
        }
        
        .options {
            display: flex;
            flex-direction: column;
            gap: 10px;
        }
        
        .option {
            padding: 15px;
            border: 2px solid #e8e8e8;
            border-radius: 12px;
            cursor: pointer;
            transition: all 0.2s ease;
            background: #fafafa;
            font-size: clamp(14px, 3.5vw, 16px);
            line-height: 1.4;
            word-break: keep-all;
            overflow-wrap: break-word;
        }
        
        .option:hover {
            border-color: #ff9a56;
            background: #fff5f0;
            transform: translateY(-1px);
        }
        
        .option.selected {
            border-color: #ff9a56;
            background: #ff9a56;
            color: white;
        }
        
        .result-container {
            display: none;
            text-align: center;
        }
        
        .result-type {
            font-size: clamp(20px, 5vw, 28px);
            margin-bottom: 15px;
            padding: 15px;
            border-radius: 12px;
            font-weight: 700;
            line-height: 1.3;
        }
        
        .type-metabolic { background: linear-gradient(135deg, #ff6b6b, #ff8e8e); color: white; }
        .type-water { background: linear-gradient(135deg, #4ecdc4, #7dd3c0); color: white; }
        .type-appetite { background: linear-gradient(135deg, #feca57, #ff9ff3); color: white; }
        .type-sleep { background: linear-gradient(135deg, #a8edea, #fed6e3); color: #333; }
        .type-hormone { background: linear-gradient(135deg, #d299c2, #fef9d7); color: #333; }
        
        .habits-list {
            text-align: left;
            margin: 20px 0;
        }
        
        .habits-list h3 {
            color: #ff6b35;
            margin-bottom: 12px;
            font-size: clamp(16px, 4vw, 18px);
            font-weight: 600;
        }
        
        .habits-list ul {
            list-style: none;
            padding: 0;
        }
        
        .habits-list li {
            display: flex;
            align-items: flex-start;
            padding: 10px 0;
            border-bottom: 1px solid #f0f0f0;
            font-size: clamp(14px, 3.5vw, 15px);
            line-height: 1.5;
        }
        
        .habits-list li:last-child {
            border-bottom: none;
        }
        
        .habits-list li::before {
            content: "✓";
            display: flex;
            align-items: center;
            justify-content: center;
            width: 18px;
            height: 18px;
            background: #ff9a56;
            color: white;
            border-radius: 50%;
            font-size: 10px;
            font-weight: bold;
            margin-right: 10px;
            margin-top: 2px;
            flex-shrink: 0;
        }
        
        .exercise-box {
            padding: 15px;
            background: #fff5f0;
            border-radius: 10px;
            border-left: 4px solid #ff9a56;
            font-size: clamp(14px, 3.5vw, 15px);
            line-height: 1.5;
        }
        
        .advice-box {
            margin-top: 20px;
            padding: 15px;
            background: linear-gradient(135deg, #ffeaa7, #fab1a0);
            border-radius: 10px;
            font-size: clamp(14px, 3.5vw, 15px);
            line-height: 1.6;
        }
        
        .btn {
            background: linear-gradient(135deg, #ff9a56, #ff6b35);
            color: white;
            border: none;
            padding: 12px 24px;
            border-radius: 25px;
            font-size: clamp(14px, 3.5vw, 16px);
            cursor: pointer;
            margin: 15px 5px;
            transition: all 0.2s ease;
            font-weight: 600;
        }
        
        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(255, 154, 86, 0.3);
        }
        
        .progress-bar {
            width: 100%;
            height: 6px;
            background: #e8e8e8;
            border-radius: 3px;
            margin-bottom: 20px;
            overflow: hidden;
        }
        
        .progress {
            height: 100%;
            background: linear-gradient(90deg, #ff9a56, #ff6b35);
            transition: width 0.3s ease;
            border-radius: 3px;
        }
        
        .illustration {
            width: 100px;
            height: 100px;
            margin: 15px auto;
            position: relative;
        }
        
        /* イラストのスタイル調整 */
        .metabolic-icon, .water-icon, .appetite-icon, .sleep-icon, .hormone-icon {
            width: 100%;
            height: 100%;
            border-radius: 50%;
            position: relative;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 35px;
        }
        
        .metabolic-icon {
            background: linear-gradient(135deg, #ff6b6b, #ff8e8e);
            animation: pulse 2s infinite;
        }
        
        .water-icon {
            background: linear-gradient(135deg, #4ecdc4, #7dd3c0);
            animation: wave 3s ease-in-out infinite;
        }
        
        .appetite-icon {
            background: linear-gradient(135deg, #feca57, #ff9ff3);
            animation: bounce 2s infinite;
        }
        
        .sleep-icon {
            background: linear-gradient(135deg, #a8edea, #fed6e3);
            animation: float 4s ease-in-out infinite;
        }
        
        .hormone-icon {
            background: linear-gradient(135deg, #d299c2, #fef9d7);
            animation: shimmer 3s infinite;
        }
        
        /* アニメーション（控えめに調整） */
        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.05); }
        }
        
        @keyframes wave {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-5px); }
        }
        
        @keyframes bounce {
            0%, 20%, 50%, 80%, 100% { transform: translateY(0); }
            40% { transform: translateY(-5px); }
            60% { transform: translateY(-2px); }
        }
        
        @keyframes float {
            0%, 100% { transform: translateY(0px) rotate(0deg); }
            50% { transform: translateY(-8px) rotate(1deg); }
        }
        
        @keyframes shimmer {
            0% { transform: scale(1) rotate(0deg); }
            25% { transform: scale(1.03) rotate(0.5deg); }
            50% { transform: scale(1) rotate(0deg); }
            75% { transform: scale(1.03) rotate(-0.5deg); }
            100% { transform: scale(1) rotate(0deg); }
        }
        
        /* スマホ対応の追加調整 */
        @media (max-width: 480px) {
            body {
                padding: 5px;
            }
            
            .container {
                border-radius: 12px;
            }
            
            .content {
                padding: 15px;
            }
            
            .option {
                padding: 12px;
            }
            
            .illustration {
                width: 80px;
                height: 80px;
            }
            
            .metabolic-icon, .water-icon, .appetite-icon, .sleep-icon, .hormone-icon {
                font-size: 28px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>💪 更年期体質タイプ別診断</h1>
            <p>簡単な質問に答えて、あなたに最適なやせ習慣を見つけよう！</p>
        </div>
        
        <div class="content">
            <div class="progress-bar">
                <div class="progress" id="progress"></div>
            </div>
            
            <div id="quiz-container">
                <!-- 質問がここに動的に表示される -->
            </div>
            
            <div class="result-container" id="result-container">
                <div id="result-type" class="result-type"></div>
                <div id="result-content"></div>
                <button class="btn" onclick="restartQuiz()">もう一度診断する</button>
            </div>
        </div>
    </div>

    <script>
        const questions = [
            {
                question: "最近の体重変化について教えてください",
                options: [
                    { text: "徐々に増えて戻らない", scores: { metabolic: 3, hormone: 2 } },
                    { text: "急激に増えた", scores: { hormone: 3, metabolic: 1 } },
                    { text: "日によって変動が激しい", scores: { water: 3, appetite: 1 } },
                    { text: "食べた分だけ増える", scores: { appetite: 3, metabolic: 1 } }
                ]
            },
            {
                question: "現在の食事パターンは？",
                options: [
                    { text: "量は普通だが太りやすくなった", scores: { metabolic: 3, hormone: 1 } },
                    { text: "間食・夜食が多い", scores: { appetite: 3, sleep: 1 } },
                    { text: "むくみやすい食事が多い", scores: { water: 3 } },
                    { text: "食事時間が不規則", scores: { sleep: 2, hormone: 2 } }
                ]
            },
            {
                question: "運動について当てはまるものは？",
                options: [
                    { text: "運動してもなかなか効果が出ない", scores: { metabolic: 3, hormone: 1 } },
                    { text: "疲れやすくて運動する気になれない", scores: { sleep: 3, metabolic: 1 } },
                    { text: "運動後にむくみが気になる", scores: { water: 2, sleep: 1 } },
                    { text: "運動するとすぐお腹が空く", scores: { appetite: 3 } }
                ]
            },
            {
                question: "睡眠の状態はいかがですか？",
                options: [
                    { text: "よく眠れている", scores: { metabolic: 1, water: 1, appetite: 1 } },
                    { text: "寝つきが悪い・途中で起きる", scores: { sleep: 3, hormone: 2 } },
                    { text: "朝起きてもむくんでいる", scores: { water: 3, sleep: 1 } },
                    { text: "夜遅くまで食べてしまう", scores: { appetite: 2, sleep: 2 } }
                ]
            },
            {
                question: "ストレスや感情の変化について",
                options: [
                    { text: "イライラして食べ過ぎてしまう", scores: { appetite: 3, hormone: 1 } },
                    { text: "疲れやすく気分が落ち込む", scores: { sleep: 3, hormone: 2 } },
                    { text: "体調に波がある", scores: { hormone: 3, water: 1 } },
                    { text: "特に変化なし", scores: { metabolic: 1 } }
                ]
            }
        ];

        const typeInfo = {
            metabolic: {
                name: "🔥 代謝低下タイプ",
                description: "基礎代謝が落ちて太りやすくなっています",
                habits: [
                    "1日10分の軽い筋トレから始める（椅子を使ったスクワットなど）",
                    "タンパク質を意識（卵、魚、大豆製品を毎食1品）",
                    "階段を使う・一駅歩くなど日常に運動を取り入れる",
                    "週2回、20分のウォーキング",
                    "炭水化物は夜少なめ、朝昼はしっかり摂る"
                ],
                exercise: "椅子スクワット（1日10回×2セット）、壁腕立て伏せ、かかと上げ運動",
                className: "type-metabolic"
            },
            water: {
                name: "💧 水分代謝不良タイプ",
                description: "むくみやすく、体重変動が激しい状態です",
                habits: [
                    "お風呂でふくらはぎマッサージ（5分）",
                    "湯船に浸かる習慣（週3回、15分程度）",
                    "塩分控えめ調理（出汁や香辛料で味付け）",
                    "バナナ・アボカド・ほうれん草などカリウム食材を意識",
                    "ヨーグルト・納豆・キムチなど発酵食品を1日1品"
                ],
                exercise: "足首回し（朝晩各20回）、ふくらはぎ伸ばし、ゆっくり散歩",
                className: "type-water"
            },
            appetite: {
                name: "🍽️ 食欲コントロール難タイプ",
                description: "ストレス食いや間食がやめられない状態です",
                habits: [
                    "あすけんで食事写真を撮る習慣",
                    "間食は小皿に出して食べる（袋から直接NG）",
                    "食事前にコップ1杯の水を飲む",
                    "野菜・きのこ・海藻を毎食プラス",
                    "深呼吸・散歩・音楽など食べる以外のストレス発散"
                ],
                exercise: "食後の軽い散歩（10分）、ラジオ体操、好きな音楽に合わせて体を動かす",
                className: "type-appetite"
            },
            sleep: {
                name: "😴 睡眠・疲労蓄積タイプ",
                description: "睡眠の質低下や慢性疲労で動けない状態です",
                habits: [
                    "寝る1時間前からスマホを置く",
                    "朝起きたら窓を開けて深呼吸（5分）",
                    "夕食は寝る3時間前までに済ませる",
                    "バナナ・牛乳・ナッツなど睡眠に良い食材",
                    "午後のコーヒーは控える"
                ],
                exercise: "朝起きたら背伸び3回、寝る前にゆっくり首回し（左右5回ずつ）",
                className: "type-sleep"
            },
            hormone: {
                name: "🌸 ホルモンバランス乱れタイプ",
                description: "急激な体重増加や体脂肪率上昇が見られます",
                habits: [
                    "豆腐・納豆・豆乳を1日1品取り入れる",
                    "同じ時間に起きて同じ時間に寝る",
                    "オリーブオイル・ナッツなど良質な脂質を適量",
                    "色とりどりの野菜・果物でビタミン補給",
                    "無理しすぎず自分のペースを大切に"
                ],
                exercise: "座ったまま肩回し（前後各10回）、立ち上がって両手を上にゆっくり伸ばす",
                className: "type-hormone"
            }
        };

        let currentQuestion = 0;
        let scores = { metabolic: 0, water: 0, appetite: 0, sleep: 0, hormone: 0 };

        function startQuiz() {
            currentQuestion = 0;
            scores = { metabolic: 0, water: 0, appetite: 0, sleep: 0, hormone: 0 };
            showQuestion();
        }

        function showQuestion() {
            const container = document.getElementById('quiz-container');
            const progress = document.getElementById('progress');
            
            progress.style.width = `${((currentQuestion) / questions.length) * 100}%`;
            
            if (currentQuestion < questions.length) {
                const q = questions[currentQuestion];
                container.innerHTML = `
                    <div class="question-container">
                        <div class="question">Q${currentQuestion + 1}. ${q.question}</div>
                        <div class="options">
                            ${q.options.map((option, index) => `
                                <div class="option" onclick="selectOption(${index})">${option.text}</div>
                            `).join('')}
                        </div>
                    </div>
                `;
            } else {
                showResult();
            }
        }

        function selectOption(optionIndex) {
            const option = questions[currentQuestion].options[optionIndex];
            
            // スコアを加算
            for (let type in option.scores) {
                scores[type] += option.scores[type];
            }
            
            // 選択した選択肢をハイライト
            document.querySelectorAll('.option').forEach(opt => opt.classList.remove('selected'));
            document.querySelectorAll('.option')[optionIndex].classList.add('selected');
            
            // 次の質問へ
            setTimeout(() => {
                currentQuestion++;
                showQuestion();
            }, 500);
        }

        function showResult() {
            const progress = document.getElementById('progress');
            progress.style.width = '100%';
            
            // 最高スコアのタイプを判定
            let maxScore = 0;
            let resultType = 'metabolic';
            
            for (let type in scores) {
                if (scores[type] > maxScore) {
                    maxScore = scores[type];
                    resultType = type;
                }
            }
            
            const typeData = typeInfo[resultType];
            
            // イラストのクラス名を決定
            const iconClasses = {
                metabolic: 'metabolic-icon',
                water: 'water-icon', 
                appetite: 'appetite-icon',
                sleep: 'sleep-icon',
                hormone: 'hormone-icon'
            };
            
            // 各タイプの絵文字を設定
            const typeEmojis = {
                metabolic: '💪',
                water: '💧', 
                appetite: '🍽️',
                sleep: '😴',
                hormone: '🌸'
            };
            
            document.getElementById('quiz-container').style.display = 'none';
            document.getElementById('result-container').style.display = 'block';
            
            document.getElementById('result-type').innerHTML = typeData.name;
            document.getElementById('result-type').className = `result-type ${typeData.className}`;
            
            document.getElementById('result-content').innerHTML = `
                <div class="illustration">
                    <div class="${iconClasses[resultType]}">${typeEmojis[resultType]}</div>
                </div>
                
                <p style="font-size: clamp(14px, 3.5vw, 16px); margin-bottom: 20px; line-height: 1.6; color: #555;">${typeData.description}</p>
                
                <div class="habits-list">
                    <h3>📋 おすすめやせ習慣</h3>
                    <ul>
                        ${typeData.habits.map(habit => `<li>${habit}</li>`).join('')}
                    </ul>
                </div>
                
                <div class="habits-list">
                    <h3>🏃‍♀️ おすすめ運動</h3>
                    <div class="exercise-box">${typeData.exercise}</div>
                </div>
                
                <div class="advice-box">
                    <strong>💡 Makiさんからのアドバイス</strong><br>
                    50代のダイエットは時間がかかりますが、継続すれば必ずカラダは変わります！
                    自分のペースで、無理のない範囲から始めてくださいね。
                </div>
            `;
        }

        function restartQuiz() {
            document.getElementById('quiz-container').style.display = 'block';
            document.getElementById('result-container').style.display = 'none';
            startQuiz();
        }

        // 初期化
        startQuiz();
    </script>
</body>
</html>
