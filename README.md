from flask import Flask, render_template, request, redirect, url_for

app = Flask(__name__)

@app.route('/', methods=['GET', 'POST'])
def index():
    if request.method == 'POST':
        answer = request.form.get('answer')
        if answer == 'yes':
            return render_template('yes.html')
        # If "No" is clicked, redirect back to same page (question repeats)
        return redirect(url_for('index'))
    
    return render_template('index.html')

if __name__ == '__main__':
    app.run(debug=True, host='0.0.0.0', port=5000)
    <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Will You Be Mine? 💕</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Dancing+Script:wght@400;700&display=swap');
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Dancing Script', cursive;
            background: linear-gradient(135deg, #ff9a9e 0%, #fecfef 50%, #fecfef 100%);
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            overflow: hidden;
        }
        
        .container {
            text-align: center;
            background: rgba(255, 255, 255, 0.95);
            padding: 60px 40px;
            border-radius: 30px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.1);
            max-width: 500px;
            backdrop-filter: blur(10px);
            animation: fadeInUp 1s ease-out;
        }
        
        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        
        h1 {
            font-size: 3.5em;
            color: #e91e63;
            margin-bottom: 20px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.1);
        }
        
        p {
            font-size: 1.5em;
            color: #555;
            margin-bottom: 50px;
            line-height: 1.4;
        }
        
        .buttons {
            display: flex;
            gap: 20px;
            justify-content: center;
            flex-wrap: wrap;
        }
        
        button {
            padding: 18px 40px;
            font-size: 1.4em;
            font-family: 'Dancing Script', cursive;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-weight: 700;
            min-width: 140px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.2);
        }
        
        .yes-btn {
            background: linear-gradient(45deg, #4CAF50, #45a049);
            color: white;
        }
        
        .yes-btn:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 35px rgba(76, 175, 80, 0.4);
        }
        
        .no-btn {
            background: linear-gradient(45deg, #f44336, #da190b);
            color: white;
        }
        
        .no-btn:hover {
            transform: translateY(-5px) scale(1.05);
            box-shadow: 0 15px 35px rgba(244, 67, 54, 0.4);
            animation: shake 0.5s ease-in-out;
        }
        
        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            25% { transform: translateX(-10px); }
            75% { transform: translateX(10px); }
        }
        
        .hearts {
            position: absolute;
            width: 100%;
            height: 100%;
            pointer-events: none;
            overflow: hidden;
        }
        
        .heart {
            position: absolute;
            font-size: 20px;
            color: #ff69b4;
            animation: float 6s ease-in-out infinite;
        }
        
        @keyframes float {
            0% {
                transform: translateY(100vh) rotate(0deg);
                opacity: 1;
            }
            100% {
                transform: translateY(-100px) rotate(360deg);
                opacity: 0;
            }
        }
    </style>
</head>
<body>
    <div class="hearts" id="hearts"></div>
    
    <div class="container">
        <h1>💖 Will You Be Mine? 💖</h1>
        <p style="font-size: 1.3em;">Do you want to be my girlfriend forever? 🌹</p>
        
        <form method="POST">
            <div class="buttons">
                <button type="submit" name="answer" value="yes" class="yes-btn">💕 YES 💕</button>
                <button type="submit" name="answer" value="no" class="no-btn">❌ NO ❌</button>
            </div>
        </form>
    </div>

    <script>
        // Floating hearts animation
        function createHeart() {
            const heart = document.createElement('div');
            heart.className = 'heart';
            heart.innerHTML = '💖';
            heart.style.left = Math.random() * 100 + 'vw';
            heart.style.animationDuration = (Math.random() * 3 + 3) + 's';
            document.getElementById('hearts').appendChild(heart);
            
            setTimeout(() => {
                heart.remove();
            }, 6000);
        }
        
        setInterval(createHeart, 300);
    </script>
</body>
</html>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>She Said YES! 🎉</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Dancing+Script:wght@400;700&display=swap');
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Dancing Script', cursive;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            overflow: hidden;
        }
        
        .container {
            text-align: center;
            background: rgba(255, 255, 255, 0.95);
            padding: 60px 40px;
            border-radius: 30px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.2);
            max-width: 500px;
            animation: bounceIn 1.5s ease-out;
        }
        
        @keyframes bounceIn {
            0% {
                opacity: 0;
                transform: scale(0.3);
            }
            50% {
                opacity: 1;
                transform: scale(1.05);
            }
            70% {
                transform: scale(0.9);
            }
            100% {
                opacity: 1;
                transform: scale(1);
            }
        }
        
        h1 {
            font-size: 4em;
            background: linear-gradient(45deg, #ff6b6b, #4ecdc4, #45b7d1, #f9ca24);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-bottom: 20px;
            animation: rainbow 3s ease-in-out infinite alternate;
        }
        
        @keyframes rainbow {
            0% { filter: hue-rotate(0deg); }
            100% { filter: hue-rotate(360deg); }
        }
        
        .emoji-rain {
            font-size: 3em;
            margin: 30px 0;
            animation: celebrate 2s ease-in-out infinite;
        }
        
        @keyframes celebrate {
            0%, 100% { transform: scale(1) rotate(0deg); }
            50% { transform: scale(1.2) rotate(10deg); }
        }
        
        p {
            font-size: 1.6em;
            color: #333;
            margin-bottom: 30px;
            line-height: 1.4;
        }
        
        .restart-btn {
            padding: 15px 35px;
            font-size: 1.3em;
            background: linear-gradient(45deg, #ff6b6b, #4ecdc4);
            color: white;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            font-family: 'Dancing Script', cursive;
            font-weight: 700;
            transition: all 0.3s ease;
            box-shadow: 0 10px 25px rgba(0,0,0,0.2);
        }
        
        .restart-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 15px 35px rgba(0,0,0,0.3);
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>🎉 YES! 🎉</h1>
        <div class="emoji-rain">
            💖✨💕🌟💫💖✨💕
        </div>
        <p style="font-size: 1.8em; color: #e91e63; font-weight: 700;">
            I LOVE YOU FOREVER! 💕<br>
            You're my everything! 🌹
        </p>
        <p>You made me the happiest person alive! 🥰</p>
        <br>
        <a href="{{ url_for('index') }}" class="restart-btn">🔄 Try Again</a>
    </div>

    <!-- Confetti effect -->
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.5.1/dist/confetti.browser.min.js"></script>
    <script>
        // Confetti explosion
        confetti({
            particleCount: 100,
            spread: 70,
            origin: { y: 0.6 }
        });
        
        setTimeout(() => {
            confetti({
                particleCount: 100,
                angle: 60,
                spread: 55,
                origin: { x: 0 }
            });
            
            confetti({
                particleCount: 100,
                angle: 120,
                spread: 55,
                origin: { x: 1 }
            });
        }, 250);
    </script>
</body>
</html>
