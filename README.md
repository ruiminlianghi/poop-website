# poop-website
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>肠道物语 - 你的私人肠胃精灵</title>
    <style>
        body {
            font-family: 'PingFang SC', 'Microsoft YaHei', sans-serif;
            background-color: #f4f9f4; /* 清新的浅绿色背景 */
            color: #333;
            max-width: 400px;
            margin: 0 auto;
            padding: 20px;
            text-align: center;
        }
        h1 { color: #5c8d5d; font-size: 24px; }
        .subtitle { font-size: 14px; color: #777; margin-bottom: 20px; }
        .card {
            background: white;
            border-radius: 15px;
            padding: 15px;
            margin-bottom: 20px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.05);
        }
        .options {
            display: flex;
            justify-content: space-around;
            flex-wrap: wrap;
            gap: 10px;
        }
        .option-btn {
            background: #f0f0f0;
            border: 2px solid transparent;
            border-radius: 10px;
            padding: 10px;
            cursor: pointer;
            width: 30%;
            font-size: 12px;
            transition: 0.3s;
        }
        .option-btn.selected {
            background: #e3f2fd;
            border-color: #5c8d5d;
            font-weight: bold;
        }
        .emoji { font-size: 24px; display: block; margin-bottom: 5px; }
        button.submit-btn {
            background-color: #5c8d5d;
            color: white;
            border: none;
            padding: 12px 30px;
            border-radius: 25px;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            width: 100%;
            box-shadow: 0 4px 6px rgba(92, 141, 93, 0.3);
        }
        button.submit-btn:hover { background-color: #4a754b; }
        #result-box {
            display: none;
            margin-top: 20px;
            padding: 20px;
            background: #fff8e1;
            border-radius: 15px;
            border-left: 5px solid #ffb300;
            text-align: left;
            font-size: 15px;
            line-height: 1.6;
        }
        .disclaimer { font-size: 10px; color: #aaa; margin-top: 30px; }
    </style>
</head>
<body>

    <h1>🌿 肠道物语</h1>
    <div class="subtitle">记录今天，为了更畅快的明天</div>

    <div class="card">
        <h3>1. 今天的形状是？</h3>
        <div class="options" id="shape-options">
            <div class="option-btn" onclick="selectOption('shape', 'hard')"><span class="emoji">🐿️</span>坚硬颗粒</div>
            <div class="option-btn" onclick="selectOption('shape', 'normal')"><span class="emoji">🍌</span>完美香蕉</div>
            <div class="option-btn" onclick="selectOption('shape', 'soft')"><span class="emoji">🍦</span>糊状软便</div>
            <div class="option-btn" onclick="selectOption('shape', 'watery')"><span class="emoji">💦</span>水花四溅</div>
        </div>
    </div>

    <div class="card">
        <h3>2. 它的色号是？</h3>
        <div class="options" id="color-options">
            <div class="option-btn" onclick="selectOption('color', 'brown')"><span class="emoji">🟤</span>经典棕</div>
            <div class="option-btn" onclick="selectOption('color', 'green')"><span class="emoji">🟢</span>蔬菜绿</div>
            <div class="option-btn" onclick="selectOption('color', 'black_red')"><span class="emoji">⚫</span>暗黑/带红</div>
        </div>
    </div>

    <button class="submit-btn" onclick="analyzePoop()">✨ 召唤肠胃精灵分析 ✨</button>

    <div id="result-box">
        <strong>🧚 肠胃精灵说：</strong>
        <div id="result-text"></div>
    </div>

    <div class="disclaimer">免责声明：本程序仅供生活娱乐与膳食参考，AI精灵不是医生，如有严重不适请及时就医。</div>

    <script>
        let currentShape = '';
        let currentColor = '';

        // 处理点击选择的样式
        function selectOption(type, value) {
            if(type === 'shape') currentShape = value;
            if(type === 'color') currentColor = value;

            // 清除同类别的选中状态
            let container = document.getElementById(`${type}-options`);
            let buttons = container.getElementsByClassName('option-btn');
            for(let btn of buttons) {
                btn.classList.remove('selected');
            }
            // 给当前点击的加上选中状态
            event.currentTarget.classList.add('selected');
        }

        // 分析逻辑（If-Else 规则引擎）
        function analyzePoop() {
            if(!currentShape || !currentColor) {
                alert("精灵需要你选好形状和颜色哦！");
                return;
            }

            let result = "";

            // 优先判断颜色（高优警报）
            if(currentColor === 'black_red') {
                result = "哎呀，颜色有点特殊！如果最近没有吃猪血、铁剂或者红心火龙果，肠胃精灵建议你最好去看看医生哦，排除一下消化道出血的可能。安全第一！🏥";
            } 
            // 正常颜色的形状判断
            else {
                if(currentShape === 'hard') {
                    result = "羊粪球警报！⚠️ 你的肠道现在像撒哈拉沙漠一样干涸。精灵建议：今天马上吨吨吨喝够 2000ml 水，狂吃芹菜、西梅或者火龙果，把膳食纤维拉满！";
                } else if (currentShape === 'normal') {
                    result = "完美！🎉 这是一坨教科书级别的健康便便！你的肠胃精灵今天在你的肚子里跳起了华尔兹。请继续保持你现在的神仙饮食习惯！";
                } else if (currentShape === 'soft') {
                    result = "有点偏软哦~ 可能是肚子稍微受了点凉，或者吃了太多油腻的东西。建议今天吃点清淡的，给肠胃放个小假吧。🍵";
                } else if (currentShape === 'watery') {
                    result = "拉肚子啦！😭 肠胃精灵现在很虚弱。请注意补充电解质水防止脱水。如果持续腹泻，记得吃药或者看医生哦！今天绝对要告别辛辣刺激！";
                }
                
                // 附加绿色便便的提示
                if(currentColor === 'green' && currentShape !== 'watery') {
                    result += "<br><br>💡 附带一提：呈绿色说明食物通过肠道太快啦，或者你昨天吃了一整座森林的绿叶菜？别担心，通常是正常的！";
                }
            }

            // 显示结果
            document.getElementById('result-text').innerHTML = result;
            document.getElementById('result-box').style.display = 'block';
        }
    </script>
</body>
</html>
