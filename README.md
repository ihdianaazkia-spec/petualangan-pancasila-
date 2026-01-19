<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Petualangan Pancasila - Game Edukasi</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Comic Sans MS', 'Arial', sans-serif;
            background-color: #667eea;
            background-image: url('image/bweb.png');
            background-size: cover;
            background-repeat: no-repeat;
            background-attachment: scroll;
            background-position: center top;
            width: 100%;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        /* Container utama */
        .container {
            max-width: 400px;
            width: 100%;
            background: rgba(255, 255, 255, 0.5);
            border-radius: 30px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            overflow: hidden;
            animation: fadeIn 0.5s ease;
            backdrop-filter: blur(5px);
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: scale(0.9); }
            to { opacity: 1; transform: scale(1); }
        }

        /* Halaman */
        .page {
            display: none;
            padding: 30px;
            text-align: center;
            min-height: 500px;
        }

        .page.active {
            display: block;
            animation: slideIn 0.4s ease;
        }

        @keyframes slideIn {
            from { opacity: 0; transform: translateX(20px); }
            to { opacity: 1; transform: translateX(0); }
        }

        /* Header */
        .header {
            background: linear-gradient(135deg, #FF6B6B 0%, #EE5A6F 100%);
            padding: 20px;
            margin: -30px -30px 20px -30px;
            color: white;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }

        .header h1 {
            font-size: 28px;
            margin-bottom: 5px;
            font-weight: bold;
            text-shadow: 2px 2px 6px rgba(0,0,0,0.4);
        }

        .header p {
            font-size: 15px;
            opacity: 0.95;
            font-weight: 500;
        }

        /* Gambar */
        .img-wrapper {
            margin: 20px 0;
            position: relative;
        }

        .img-wrapper img {
            max-width: 100%;
            height: auto;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
            transition: transform 0.3s ease;
        }

        .img-wrapper img:hover {
            transform: scale(1.05);
        }

        /* Card pilihan sila */
        .sila-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
            margin: 20px 0;
            justify-items: center;
        }
        
        .sila-grid .sila-card:nth-child(5) {
            grid-column: 1 / -1;
            max-width: 200px;
        }

        .sila-card {
            background: linear-gradient(135deg, rgba(78, 205, 196, 0.5) 0%, rgba(255, 217, 61, 0.5) 100%);
            border-radius: 15px;
            padding: 20px 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 5px 15px rgba(0,0,0,0.15);
            border: 3px solid white;
            backdrop-filter: blur(3px);
        }

        .sila-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 25px rgba(0,0,0,0.2);
        }

        .sila-card img {
            width: 80px;
            height: 80px;
            margin-bottom: 10px;
            border-radius: 50%;
            border: 3px solid white;
        }

        .sila-card h3 {
            font-size: 16px;
            color: #1a1a1a;
            font-weight: bold;
            text-shadow: 1px 1px 2px rgba(255,255,255,0.5);
        }

        /* Status belajar */
        .progress {
            display: flex;
            justify-content: center;
            gap: 8px;
            margin: 20px 0;
        }

        .progress-dot {
            width: 15px;
            height: 15px;
            border-radius: 50%;
            background: #ddd;
            transition: all 0.3s ease;
        }

        .progress-dot.done {
            background: linear-gradient(135deg, #11998e 0%, #38ef7d 100%);
            transform: scale(1.2);
        }

        /* Konten penjelasan */
        .content {
            text-align: left;
            background: linear-gradient(135deg, #FFFFFF 0%, #F0F0F0 100%);
            padding: 20px;
            border-radius: 15px;
            margin: 20px 0;
            border: 2px solid #E0E0E0;
        }

        .content h2 {
            color: #D63031;
            margin-bottom: 15px;
            font-size: 22px;
            font-weight: bold;
            text-shadow: 1px 1px 2px rgba(0,0,0,0.1);
        }

        .content h3 {
            color: #0E86D4;
            margin-top: 15px;
            margin-bottom: 10px;
            font-size: 17px;
            font-weight: bold;
        }

        .content p, .content li {
            line-height: 1.8;
            color: #222;
            font-size: 15px;
            font-weight: 500;
        }

        .content ul {
            margin-left: 20px;
            margin-top: 10px;
        }

        /* Tombol */
        .btn {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 50px;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            margin: 10px 5px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
            transition: all 0.3s ease;
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 20px rgba(0,0,0,0.3);
        }

        .btn-secondary {
            background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
        }

        /* Sertifikat */
        .certificate {
            background: linear-gradient(135deg, #ffecd2 0%, #fcb69f 100%);
            padding: 30px;
            border-radius: 20px;
            border: 5px dashed #ff6b6b;
            margin: 20px 0;
        }

        .certificate h2 {
            color: #e74c3c;
            font-size: 22px;
            margin-bottom: 15px;
        }

        .certificate p {
            font-size: 16px;
            color: #333;
            margin: 10px 0;
        }

        .star {
            font-size: 40px;
            animation: rotate 2s infinite linear;
        }

        @keyframes rotate {
            from { transform: rotate(0deg); }
            to { transform: rotate(360deg); }
        }

        /* Animasi Balon Terbang */
        .balloons {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 1;
        }

        .balloon {
            position: absolute;
            font-size: 40px;
            animation: float 6s ease-in-out infinite;
        }

        .balloon:nth-child(1) { left: 10%; animation-delay: 0s; }
        .balloon:nth-child(2) { left: 30%; animation-delay: 1s; }
        .balloon:nth-child(3) { left: 50%; animation-delay: 2s; }
        .balloon:nth-child(4) { left: 70%; animation-delay: 0.5s; }
        .balloon:nth-child(5) { left: 85%; animation-delay: 1.5s; }

        @keyframes float {
            0% { transform: translateY(100vh) scale(0); opacity: 0; }
            10% { opacity: 1; }
            90% { opacity: 1; }
            100% { transform: translateY(-100vh) scale(1); opacity: 0; }
        }

        /* Animasi Bintang Berkedip */
        .sparkles {
            position: absolute;
            top: 10px;
            right: 10px;
            font-size: 20px;
            animation: sparkle 1.5s ease-in-out infinite;
        }

        @keyframes sparkle {
            0%, 100% { opacity: 1; transform: scale(1); }
            50% { opacity: 0.3; transform: scale(1.3); }
        }

        /* Animasi Bounce untuk tombol */
        .btn {
            animation: bounce 2s ease-in-out infinite;
        }

        @keyframes bounce {
            0%, 20%, 50%, 80%, 100% { transform: translateY(0); }
            40% { transform: translateY(-10px); }
            60% { transform: translateY(-5px); }
        }

        .btn:hover {
            animation: none;
            transform: translateY(-2px) scale(1.05);
        }

        /* Animasi Goyang untuk sila card */
        .sila-card {
            animation: wiggle 3s ease-in-out infinite;
        }

        .sila-card:nth-child(1) { animation-delay: 0s; }
        .sila-card:nth-child(2) { animation-delay: 0.2s; }
        .sila-card:nth-child(3) { animation-delay: 0.4s; }
        .sila-card:nth-child(4) { animation-delay: 0.6s; }
        .sila-card:nth-child(5) { animation-delay: 0.8s; }

        @keyframes wiggle {
            0%, 100% { transform: rotate(0deg); }
            25% { transform: rotate(-2deg); }
            75% { transform: rotate(2deg); }
        }

        .sila-card:hover {
            animation: none;
            transform: translateY(-10px) scale(1.05);
        }

        /* Card Belajar Semua - Design Spesial */
        .learn-all-card {
            background-image: url('image/cbelajar.png');
            background-size: cover;
            background-repeat: no-repeat;
            background-position: center;
            background-color: rgba(240, 147, 251, 0.8);
            border-radius: 20px;
            padding: 40px 25px;
            margin: 20px 0;
            cursor: pointer;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.4);
            transition: all 0.3s ease;
            border: 3px solid white;
            animation: pulse-glow 2s ease-in-out infinite;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 200px;
            gap: 12px;
        }

        @keyframes pulse-glow {
            0%, 100% {
                box-shadow: 0 10px 30px rgba(245, 87, 108, 0.4);
                transform: scale(1);
            }
            50% {
                box-shadow: 0 15px 40px rgba(245, 87, 108, 0.6);
                transform: scale(1.02);
            }
        }

        .learn-all-card:hover {
            transform: translateY(-8px) scale(1.05);
            box-shadow: 0 15px 40px rgba(245, 87, 108, 0.6);
            animation: none;
        }

        .learn-all-card h3 {
            color: white;
            font-size: 20px;
            margin: 0;
            text-shadow: 3px 3px 8px rgba(0,0,0,0.6);
            font-weight: bold;
            background: rgba(0, 0, 0, 0.4);
            padding: 12px 16px;
            border-radius: 10px;
            line-height: 1.3;
            text-align: center;
            min-width: 200px;
        }

        .learn-all-card p {
            color: white;
            font-size: 15px;
            margin: 0;
            opacity: 1;
            text-shadow: 3px 3px 8px rgba(0,0,0,0.6);
            font-weight: 500;
            background: rgba(0, 0, 0, 0.4);
            padding: 10px 14px;
            border-radius: 8px;
            text-align: center;
            line-height: 1.4;
            min-width: 200px;
        }

        .rocket-icon {
            font-size: 50px;
            animation: rocket-fly 2s ease-in-out infinite;
        }

        @keyframes rocket-fly {
            0%, 100% { transform: translateY(0px) rotate(-10deg); }
            50% { transform: translateY(-15px) rotate(-5deg); }
        }

        /* Tombol Lanjut di halaman Sila */
        .btn-next {
            background: linear-gradient(135deg, #11998e 0%, #38ef7d 100%);
            margin-top: 10px;
        }

        /* Animasi Progress Dot */
        .progress-dot.done {
            animation: pop 0.5s cubic-bezier(0.68, -0.55, 0.265, 1.55);
        }

        @keyframes pop {
            0% { transform: scale(0); }
            50% { transform: scale(1.4); }
            100% { transform: scale(1.2); }
        }

        /* Animasi Konfetti */
        .confetti {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 9999;
        }

        .confetti-piece {
            position: absolute;
            width: 10px;
            height: 10px;
            background: #f39c12;
            top: -10px;
            opacity: 0;
            animation: confetti-fall 3s ease-out forwards;
        }

        @keyframes confetti-fall {
            0% { transform: translateY(0) rotateZ(0deg); opacity: 1; }
            100% { transform: translateY(100vh) rotateZ(720deg); opacity: 0; }
        }

        /* Animasi Pulse untuk gambar */
        .img-wrapper img {
            animation: pulse 3s ease-in-out infinite;
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.02); }
        }

        .img-wrapper img:hover {
            animation: none;
            transform: scale(1.08);
        }

        /* Animasi Rainbow untuk header */
        .header {
            background: linear-gradient(45deg, #ff6b6b, #feca57, #48dbfb, #ff9ff3, #54a0ff, #00d2d3);
            background-size: 400% 400%;
            animation: rainbow 8s ease infinite;
        }

        @keyframes rainbow {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        /* Animasi Shake untuk sertifikat */
        .certificate {
            animation: shake 0.5s ease-in-out;
        }

        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            10%, 30%, 50%, 70%, 90% { transform: translateX(-5px); }
            20%, 40%, 60%, 80% { transform: translateX(5px); }
        }

        /* Emoji bergerak */
        .moving-emoji {
            display: inline-block;
            animation: wave 1s ease-in-out infinite;
        }

        @keyframes wave {
            0%, 100% { transform: rotate(0deg); }
            25% { transform: rotate(20deg); }
            75% { transform: rotate(-20deg); }
        }

        /* Responsive */
        @media (min-width: 600px) {
            .container {
                max-width: 500px;
            }
        }

        /* Footer Copyright */
        .copyright-footer {
            position: fixed;
            bottom: 10px;
            right: 15px;
            font-size: 11px;
            color: rgba(255, 255, 255, 0.7);
            text-align: right;
            z-index: 999;
            background: rgba(0, 0, 0, 0.3);
            padding: 8px 12px;
            border-radius: 5px;
            font-weight: 500;
        }

        .copyright-footer a {
            color: rgba(255, 255, 255, 0.9);
            text-decoration: none;
            font-weight: bold;
        }

        .copyright-footer a:hover {
            text-decoration: underline;
        }

        /* Game Styles */
        .level-card {
            background: white;
            border: 4px solid #dfe6e9;
            border-radius: 20px;
            padding: 20px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s;
            position: relative;
        }

        .level-card:hover {
            transform: scale(1.05);
            border-color: #6c5ce7;
            box-shadow: 0 10px 30px rgba(108, 92, 231, 0.3);
        }

        .level-card.completed {
            background: linear-gradient(135deg, #55efc4 0%, #00b894 100%);
            border-color: #00b894;
        }

        .level-symbol {
            font-size: 4em;
            margin-bottom: 10px;
        }

        .level-name {
            font-size: 1em;
            font-weight: bold;
            color: #2d3436;
            margin-top: 10px;
        }

        .option {
            background: white;
            border: 3px solid #dfe6e9;
            padding: 20px;
            border-radius: 15px;
            cursor: pointer;
            transition: all 0.3s;
            font-size: 1.1em;
            text-align: center;
        }

        .option:hover {
            border-color: #6c5ce7;
            transform: translateX(5px);
        }

        .option.selected {
            background: #a29bfe;
            color: white;
            border-color: #6c5ce7;
        }

        .option.correct {
            background: #55efc4;
            border-color: #00b894;
            color: #2d3436;
            animation: pulse 0.5s;
        }

        .option.wrong {
            background: #ff7675;
            border-color: #d63031;
            color: white;
            animation: shake 0.5s;
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.05); }
        }

        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            25% { transform: translateX(-10px); }
            75% { transform: translateX(10px); }
        }

        .feedback.correct {
            background: #55efc4;
            color: #00b894;
        }

        .feedback.wrong {
            background: #ff7675;
            color: #d63031;
        }

        .match-item {
            display: flex;
            align-items: center;
            gap: 15px;
            background: white;
            padding: 15px;
            border-radius: 15px;
            border: 3px solid #dfe6e9;
        }

        .match-text {
            flex: 1;
            font-size: 1.1em;
        }

        .match-buttons {
            display: flex;
            gap: 10px;
        }

        .match-btn {
            padding: 10px 20px;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.3s;
        }

        .match-btn.benar {
            background: #55efc4;
            color: #00b894;
        }

        .match-btn.salah {
            background: #ff7675;
            color: #d63031;
        }

        .match-btn:hover {
            transform: scale(1.1);
        }

        .match-btn.selected {
            box-shadow: 0 0 0 3px #6c5ce7;
        }

        #gameActions {
            display: none !important;
            gap: 15px;
            justify-content: center;
            margin-top: 20px;
        }

        #gameActions.show {
            display: flex !important;
        }

        /* Game 1 Styles - Match Image */
        .image-card {
            background: white;
            border: 3px solid #6c5ce7;
            border-radius: 15px;
            padding: 15px;
            text-align: center;
            cursor: move;
            transition: all 0.3s ease;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }

        .image-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(0,0,0,0.2);
        }

        .image-card.correct {
            border-color: #00b894;
            background: linear-gradient(135deg, #00d2d3 0%, #00b894 100%);
            color: white;
        }

        .image-card.dragging {
            opacity: 0.7;
            transform: scale(0.95);
        }

        .image-card img {
            width: 100%;
            max-height: 150px;
            margin: 10px 0;
            border-radius: 10px;
        }

        .image-card .number-badge {
            display: inline-block;
            background: #6c5ce7;
            color: white;
            width: 40px;
            height: 40px;
            border-radius: 50%;
            line-height: 40px;
            font-weight: bold;
            font-size: 1.2em;
            margin: 10px 0;
        }

        .image-card.correct .number-badge {
            background: #00b894;
        }

        /* Game 1 Question Styles */
        .question-box {
            background: linear-gradient(135deg, #a29bfe 0%, #6c5ce7 100%);
            color: white;
            padding: 20px;
            border-radius: 15px;
            margin: 20px 0;
            text-align: center;
            font-size: 1.3em;
            font-weight: bold;
        }

        .image-options {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
            gap: 15px;
            margin: 20px 0;
        }

        .image-option {
            background: white;
            border: 4px solid #dfe6e9;
            border-radius: 15px;
            padding: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }

        .image-option:hover {
            transform: scale(1.05);
            border-color: #6c5ce7;
            box-shadow: 0 8px 20px rgba(0,0,0,0.2);
        }

        .image-option.selected {
            border-color: #6c5ce7;
            background: linear-gradient(135deg, #a29bfe 0%, #6c5ce7 100%);
            box-shadow: 0 0 0 4px #a29bfe;
        }

        .image-option.correct {
            border-color: #00b894;
            background: linear-gradient(135deg, #00d2d3 0%, #00b894 100%);
        }

        .image-option.wrong {
            border-color: #d63031;
            background: linear-gradient(135deg, #ff7675 0%, #d63031 100%);
        }

        .image-option img {
            width: 100%;
            height: auto;
            border-radius: 10px;
            margin-bottom: 8px;
        }

        .image-option-label {
            font-weight: bold;
            color: #2d3436;
            font-size: 0.95em;
        }

        .image-option.selected .image-option-label,
        .image-option.correct .image-option-label,
        .image-option.wrong .image-option-label {
            color: white;
        }

        .image-feedback {
            background: white;
            padding: 20px;
            border-radius: 15px;
            margin: 20px 0;
            text-align: center;
            font-size: 1.2em;
            font-weight: bold;
            display: none;
        }

        .image-feedback.show {
            display: block;
        }

        .image-feedback.correct {
            background: linear-gradient(135deg, #00d2d3 0%, #00b894 100%);
            color: white;
        }

        .image-feedback.wrong {
            background: linear-gradient(135deg, #ff7675 0%, #d63031 100%);
            color: white;
        }

        /* Game 2 Styles - Tebak Bunyi Sila */
        .sound-question-box {
            background: linear-gradient(135deg, #a29bfe 0%, #6c5ce7 100%);
            color: white;
            padding: 16px 18px;
            border-radius: 15px;
            font-weight: bold;
            text-align: center;
            margin-bottom: 15px;
        }

        .sound-image-wrap {
            display: flex;
            justify-content: center;
            margin: 10px 0 20px 0;
        }

        .sound-image-wrap img {
            width: 140px;
            height: auto;
            border-radius: 15px;
            border: 3px solid white;
            box-shadow: 0 6px 18px rgba(0,0,0,0.2);
        }

        .sound-choice-grid {
            display: grid;
            gap: 12px;
        }

        .sound-choice {
            background: white;
            border: 3px solid #dfe6e9;
            border-radius: 12px;
            padding: 14px 12px;
            cursor: pointer;
            font-weight: bold;
            font-size: 1em;
            transition: all 0.3s ease;
            color: #2d3436;
            text-align: left;
        }

        .sound-choice:hover {
            transform: translateX(5px);
            border-color: #6c5ce7;
        }

        .sound-choice.selected {
            border-color: #6c5ce7;
            background: #a29bfe;
            color: white;
        }

        .sound-choice.correct {
            background: #55efc4;
            border-color: #00b894;
            color: #2d3436;
        }

        .sound-choice.wrong {
            background: #ff7675;
            border-color: #d63031;
            color: white;
        }

        .sound-choice:disabled {
            opacity: 0.6;
            cursor: not-allowed;
        }

        .sound-feedback-box {
            margin-top: 15px;
            padding: 12px;
            border-radius: 12px;
            text-align: center;
            font-weight: bold;
            display: none;
        }

        .sound-feedback-box.show {
            display: block;
        }

        .sound-feedback-box.correct {
            background: linear-gradient(135deg, #00d2d3 0%, #00b894 100%);
            color: white;
        }

        .sound-feedback-box.wrong {
            background: linear-gradient(135deg, #ff7675 0%, #d63031 100%);
            color: white;
        }
    </style>
</head>
<body>
    <!-- Balon-balon terbang -->
    <div class="balloons" id="balloons">
        <div class="balloon">🎈</div>
        <div class="balloon">🎈</div>
        <div class="balloon">🎈</div>
        <div class="balloon">🎈</div>
        <div class="balloon">🎈</div>
    </div>

    <!-- Container konfetti -->
    <div class="confetti" id="confetti"></div>

    <!-- Copyright Footer -->
    <div class="copyright-footer">
        � 2025-2026 Media Ajar Pancasila<br>
        <span style="font-size: 10px;">Milik Pengembang</span>
    </div>

    <div class="container">
        <!-- Halaman Pembuka -->
        <div id="page-intro" class="page active">
            <div class="sparkles">✨✨</div>
            <div class="header">
                <h1>🇮🇩 Belajar Pancasila Yuk! 🇮🇩</h1>
                <p>Media pembelajaran interaktif untuk anak SD</p>
            </div>
            <div class="img-wrapper">
                <img src="image/pancasila.png" alt="Lambang Pancasila">
            </div>
            <div class="content">
                <h2>Selamat Datang, Adik-adik!</h2>
                <p>Yuk, kita belajar tentang <strong>Pancasila</strong>, dasar negara Indonesia yang kita cintai!</p>
                <p>Pancasila memiliki <strong>5 sila</strong> yang mengajarkan kita cara hidup yang baik.</p>
                <p>Siap belajar? Ayo kita mulai petualangan seru kita!</p>
            </div>
            <button class="btn" onclick="goToPage('menu')">Mulai Belajar! <span class="moving-emoji">🚀</span></button>
            <button class="btn btn-secondary" onclick="goToGameMenu()" style="margin-top: 20px;">🎮 Mainkan Game Edukasi</button>
        </div>

        <!-- Halaman Menu Pilihan Sila -->
        <div id="page-menu" class="page">
            <div class="sparkles">⭐✨</div>
            <div class="header">
                <h1>Pilih Sila yang Mau Dipelajari</h1>
                <p>Klik gambar untuk belajar</p>
            </div>
            
            <!-- Progress tracker -->
            <div class="progress">
                <div class="progress-dot" id="dot-1"></div>
                <div class="progress-dot" id="dot-2"></div>
                <div class="progress-dot" id="dot-3"></div>
                <div class="progress-dot" id="dot-4"></div>
                <div class="progress-dot" id="dot-5"></div>
            </div>

            <div class="sila-grid">
                <div class="sila-card" onclick="goToSila(1)">
                    <img src="image/lsila1.png" alt="Sila 1">
                    <h3>Sila Ke-1</h3>
                </div>
                <div class="sila-card" onclick="goToSila(2)">
                    <img src="image/lsila2.png" alt="Sila 2">
                    <h3>Sila Ke-2</h3>
                </div>
                <div class="sila-card" onclick="goToSila(3)">
                    <img src="image/lsila3.png" alt="Sila 3">
                    <h3>Sila Ke-3</h3>
                </div>
                <div class="sila-card" onclick="goToSila(4)">
                    <img src="image/lsila4.png" alt="Sila 4">
                    <h3>Sila Ke-4</h3>
                </div>
                <div class="sila-card" onclick="goToSila(5)">
                    <img src="image/lsila5.png" alt="Sila 5">
                    <h3>Sila Ke-5</h3>
                </div>
            </div>

            <!-- Card Belajar Semua -->
            <div class="learn-all-card" onclick="startAutoLearn()">
                <div class="rocket-icon">🚀</div>
                <h3>Ayo Belajar Semua Sila!</h3>
                <p>Belajar dari Sila 1 sampai 5 secara berurutan</p>
            </div>

            <button class="btn btn-secondary" onclick="checkCompletion()">Selesai Belajar <span class="moving-emoji"></span></button>
            <button class="btn" onclick="goToPage('intro')" style="margin-top: 10px; background: linear-gradient(135deg, #a29bfe 0%, #6c5ce7 100%);">🏠 Kembali ke Halaman Utama</button>
        </div>

        <!-- Halaman Sila 1 -->
        <div id="page-sila1" class="page">
            <div class="header">
                <h1>Sila Ke-1</h1>
            </div>
            <div class="img-wrapper">
                <img src="image/sila1.png" alt="Sila 1">
            </div>
            <div class="content">
                <h2>Ketuhanan Yang Maha Esa</h2>
                <p><strong>Artinya:</strong> Kita percaya kepada Tuhan Yang Maha Esa dan menghormati semua agama.</p>
                
                <h3>Contoh Sikap di Sekolah:</h3>
                <ul>
                    <li>Berdoa sebelum dan sesudah belajar</li>
                    <li>Menghormati teman yang berbeda agama</li>
                    <li>Tidak mengganggu teman yang sedang beribadah</li>
                    <li>Rajin belajar agama dan mengamalkannya</li>
                </ul>
            </div>
            <button class="btn" onclick="handleSilaNavigation(1)">Kembali ke Menu 🏠</button>
            <button class="btn btn-next" onclick="goToNextSila(1)">Lanjut ke Sila 2 ➡️</button>
        </div>

        <!-- Halaman Sila 2 -->
        <div id="page-sila2" class="page">
            <div class="header">
                <h1>Sila Ke-2</h1>
            </div>
            <div class="img-wrapper">
                <img src="image/sila2.png" alt="Sila 2">
            </div>
            <div class="content">
                <h2>Kemanusiaan yang Adil dan Beradab</h2>
                <p><strong>Artinya:</strong> Kita harus memperlakukan semua orang dengan baik, adil, dan sopan.</p>
                
                <h3>Contoh Sikap di Sekolah:</h3>
                <ul>
                    <li>Menolong teman yang kesusahan</li>
                    <li>Tidak membeda-bedakan teman</li>
                    <li>Berbicara dengan sopan kepada siapa saja</li>
                    <li>Menghargai pendapat orang lain</li>
                </ul>
            </div>
            <button class="btn" onclick="handleSilaNavigation(2)">Kembali ke Menu 🏠</button>
            <button class="btn btn-next" onclick="goToNextSila(2)">Lanjut ke Sila 3 ➡️</button>
        </div>

        <!-- Halaman Sila 3 -->
        <div id="page-sila3" class="page">
            <div class="header">
                <h1>Sila Ke-3</h1>
            </div>
            <div class="img-wrapper">
                <img src="image/sila3.png" alt="Sila 3">
            </div>
            <div class="content">
                <h2>Persatuan Indonesia</h2>
                <p><strong>Artinya:</strong> Kita harus bersatu sebagai bangsa Indonesia meskipun berbeda suku, agama, dan budaya.</p>
                
                <h3>Contoh Sikap di Sekolah:</h3>
                <ul>
                    <li>Berteman dengan semua teman tanpa pilih-pilih</li>
                    <li>Bekerja sama dalam kelompok</li>
                    <li>Menjaga nama baik sekolah</li>
                    <li>Ikut upacara dengan tertib</li>
                </ul>
            </div>
            <button class="btn" onclick="handleSilaNavigation(3)">Kembali ke Menu 🏠</button>
            <button class="btn btn-next" onclick="goToNextSila(3)">Lanjut ke Sila 4 ➡️</button>
        </div>

        <!-- Halaman Sila 4 -->
        <div id="page-sila4" class="page">
            <div class="header">
                <h1>Sila Ke-4</h1>
            </div>
            <div class="img-wrapper">
                <img src="image/sila4.png" alt="Sila 4">
            </div>
            <div class="content">
                <h2>Kerakyatan yang Dipimpin oleh Hikmat Kebijaksanaan dalam Permusyawaratan/Perwakilan</h2>
                <p><strong>Artinya:</strong> Kita menyelesaikan masalah dengan musyawarah dan menghargai keputusan bersama.</p>
                
                <h3>Contoh Sikap di Sekolah:</h3>
                <ul>
                    <li>Memilih ketua kelas dengan cara voting</li>
                    <li>Mendengarkan pendapat teman saat diskusi</li>
                    <li>Menerima keputusan yang sudah disepakati bersama</li>
                    <li>Menyelesaikan masalah dengan bicara baik-baik</li>
                </ul>
            </div>
            <button class="btn" onclick="handleSilaNavigation(4)">Kembali ke Menu 🏠</button>
            <button class="btn btn-next" onclick="goToNextSila(4)">Lanjut ke Sila 5 ➡️</button>
        </div>

        <!-- Halaman Sila 5 -->
        <div id="page-sila5" class="page">
            <div class="header">
                <h1>Sila Ke-5</h1>
            </div>
            <div class="img-wrapper">
                <img src="image/sila5.png" alt="Sila 5">
            </div>
            <div class="content">
                <h2>Keadilan Sosial bagi Seluruh Rakyat Indonesia</h2>
                <p><strong>Artinya:</strong> Semua orang Indonesia harus diperlakukan dengan adil dan mendapat kesempatan yang sama.</p>
                
                <h3>Contoh Sikap di Sekolah:</h3>
                <ul>
                    <li>Tidak pelit berbagi dengan teman</li>
                    <li>Membantu teman yang kurang mampu</li>
                    <li>Tidak sombong karena lebih pintar atau kaya</li>
                    <li>Memberikan kesempatan yang sama untuk semua teman</li>
                </ul>
            </div>
            <button class="btn" onclick="handleSilaNavigation(5)">Kembali ke Menu 🏠</button>
            <button class="btn btn-next" onclick="finishAutoLearn()">Selesai!</button>
        </div>

        <!-- Halaman Penutup -->
        <div id="page-closing" class="page">
            <div class="sparkles">✨⭐🎉</div>
            <div class="header">
                <h1>🎊 Selamat! 🎊</h1>
                <p>Kamu sudah selesai belajar!</p>
            </div>
            <div class="img-wrapper">
                <img src="image/penutup.png" alt="Penutup">
            </div>
            <div class="certificate">
                <div class="star">⭐</div>
                <h2>Kamu Hebat!</h2>
                <p>Kamu sudah mempelajari semua nilai Pancasila!</p>
                <p><strong>Sekarang, yuk amalkan nilai-nilai Pancasila dalam kehidupan sehari-hari!</strong></p>
                <div class="star">⭐</div>
            </div>
            <div class="content">
                <h3>Ingat ya, adik-adik:</h3>
                <p>Pancasila bukan hanya untuk dihafal, tapi untuk <strong>diamalkan setiap hari</strong>. Mari kita jadi anak Indonesia yang baik!</p>
            </div>
            <button class="btn" onclick="goToPage('intro')">Belajar Lagi <span class="moving-emoji">🔄</span></button>
        </div>

        <!-- Game Menu Screen -->
        <div id="page-game-menu" class="page">
            <div class="sparkles">⭐✨</div>
            <div class="header">
                <h1>🎮 Game Pancasila</h1>
                <p>Pilih game favoritmu!</p>
            </div>

            <div class="level-grid" id="levelGrid" style="display: grid; grid-template-columns: 1fr; gap: 20px; margin-top: 30px;">
                <div class="level-card" onclick="startGameMatchImage()">
                    <div class="level-symbol">🖼️</div>
                    <div style="font-size: 1.5em; font-weight: bold; color: #6c5ce7;">Game 1</div>
                    <div class="level-name">Tebak Sila Dari Gambar</div>
                    <div style="font-size: 0.9em; color: #555; margin-top: 10px;">Pilih gambar yang sesuai dengan soal!</div>
                </div>
                <div class="level-card" onclick="startGameSoundMatch()">
                    <div class="level-symbol">🎵</div>
                    <div style="font-size: 1.5em; font-weight: bold; color: #6c5ce7;">Game 2</div>
                    <div class="level-name">Tebak Bunyi Sila</div>
                    <div style="font-size: 0.9em; color: #555; margin-top: 10px;">Lihat gambar, pilih bunyi silanya!</div>
                </div>
            </div>

            <button class="btn" onclick="goToPage('intro')" style="margin-top: 30px; width: 100%;">? Kembali ke Menu Utama</button>
        </div>

        <!-- Game Screen -->
        <div id="page-game-screen" class="page">
            <div class="stats" style="background: linear-gradient(135deg, #ffeaa7 0%, #fdcb6e 100%); display: flex; justify-content: space-around; margin: 0 0 20px 0; padding: 15px; border-radius: 15px;">
                <div style="display: flex; align-items: center; gap: 8px; font-size: 1em; font-weight: bold; color: #2d3436;">
                    <span>? Skor:</span>
                    <span id="currentScore">0</span>
                </div>
                <div style="display: flex; align-items: center; gap: 8px; font-size: 1em; font-weight: bold; color: #2d3436;">
                    <span>❤️ Nyawa:</span>
                    <span id="currentLives">3</span>
                </div>
            </div>

            <div class="penjelasan-box" id="silaInfo" style="background: linear-gradient(135deg, #a29bfe 0%, #6c5ce7 100%); color: white; padding: 20px; border-radius: 15px; margin: 20px 0; font-size: 1.1em; text-align: center;"></div>

            <div class="quiz-container" style="background: #f8f9fa; padding: 25px; border-radius: 20px; margin-top: 20px;">
                <div class="question" id="question" style="font-size: 1.4em; font-weight: bold; color: #2d3436; margin-bottom: 25px; text-align: center;"></div>
                <div class="options" id="options" style="display: grid; gap: 15px;"></div>
                <div id="feedback" style="margin-top: 20px; padding: 20px; border-radius: 15px; text-align: center; font-size: 1.2em; font-weight: bold; display: none;"></div>
            </div>

            <div class="mini-game" id="miniGame" style="margin-top: 30px; display: none;">
                <h3 style="text-align: center; color: #6c5ce7; margin-bottom: 15px;">🎯 Mini Game</h3>
                <p style="text-align: center; font-size: 1.1em; margin-bottom: 20px;" id="miniGameInstruction"></p>
                <div class="match-items" id="matchItems" style="display: grid; gap: 15px; margin-top: 20px;"></div>
                <div style="display: flex; gap: 15px; justify-content: center; margin-top: 20px;">
                    <button class="btn" onclick="checkMiniGame()">Cek Jawaban</button>
                </div>
            </div>

            <div id="gameActions">
                <button class="btn" onclick="goToGameMenu()" style="flex: 1;">Kembali ke Menu</button>
                <button class="btn" onclick="nextLevel()" style="flex: 1;">Level Berikutnya ➡️</button>
            </div>
        </div>

        <!-- GAME 1: Match Image Screen -->
        <div id="page-game-match-image" class="page">
            <div class="header">
                <h1>🖼️ Game 1: Tebak Sila Dari Gambar!</h1>
                <p>Pilih gambar yang sesuai dengan pertanyaan!</p>
            </div>

            <div id="matchImageGame" style="margin: 20px 0;">
                <!-- Akan diisi oleh JavaScript -->
            </div>

            <div style="background: linear-gradient(135deg, #ffeaa7 0%, #fdcb6e 100%); padding: 15px; border-radius: 15px; margin: 20px 0; text-align: center; font-weight: bold; color: #2d3436;">
                <span id="imageGameScore">Soal: <span id="imageGameCurrentQuestion">1</span>/5 | Benar: <span id="imageGameCorrect">0</span></span>
            </div>

            <div style="display: flex; gap: 15px; justify-content: center;">
                <button class="btn" onclick="goToGameMenu()">Kembali</button>
            </div>
        </div>

        <!-- GAME 2: Sound Match Screen -->
        <div id="page-game-sound-match" class="page">
            <div class="header">
                <h1>Game 2: Tebak Bunyi Sila</h1>
                <p>Lihat gambar, lalu pilih bunyi sila yang benar!</p>
            </div>

            <div id="soundMatchGame" style="background: #f8f9fa; padding: 20px; border-radius: 15px; margin: 20px 0;">
                <div class="sound-question-box" id="soundQuestion"></div>
                <div class="sound-image-wrap">
                    <img id="soundQuestionImage" src="" alt="Gambar Sila">
                </div>
                <div class="sound-choice-grid" id="soundChoices"></div>
                <div class="sound-feedback-box" id="soundFeedback"></div>
                <button class="btn" id="soundNextBtn" onclick="nextSoundQuestion()" style="display: none; width: 100%; margin-top: 15px;">Soal Berikutnya</button>
            </div>

            <div style="background: linear-gradient(135deg, #ffeaa7 0%, #fdcb6e 100%); padding: 15px; border-radius: 15px; margin: 20px 0; text-align: center; font-weight: bold; color: #2d3436;">
                <span>Skor: <span id="soundGameScoreValue">0</span> ⭐ | Benar: <span id="soundGameCorrect">0</span>/5</span>
            </div>

            <button class="btn" onclick="goToGameMenu()" style="width: 100%;">Kembali ke Menu</button>
        </div>

        <!-- Game Finish Screen -->
        <div id="page-game-finish" class="page">
            <div style="text-align: center; padding: 40px;">
                <div style="font-size: 6em; animation: bounce 1s infinite;">🎉</div>
                <h2 class="title" style="color: #6c5ce7;">Selamat!</h2>
                <p style="font-size: 1.3em; margin: 20px 0;">Kamu telah menyelesaikan semua level!</p>
                <div class="final-score" id="finalScore" style="font-size: 2em; color: #6c5ce7; margin: 20px 0; font-weight: bold;"></div>
                <p style="font-size: 1.1em; color: #666; margin: 20px 0;">Kamu sudah menguasai Pancasila dengan baik! 🌟</p>
                <button class="btn" onclick="resetGame()">Main Lagi</button>
            </div>
        </div>
    </div>

    <script>
        // ============ GAME DATA & STATE - DEKLARASI AWAL ============
        const pancasilaData = [
            {
                sila: 1,
                nama: "Ketuhanan Yang Maha Esa",
                lambang: "?",
                penjelasan: "Sila pertama mengajarkan kita untuk percaya dan taat kepada Tuhan Yang Maha Esa serta menghormati agama orang lain.",
                quiz: [
                    {
                        pertanyaan: "Apa arti sila pertama Pancasila?",
                        pilihan: [
                            { text: "Percaya dan taat kepada Tuhan Yang Maha Esa", benar: true },
                            { text: "Menghormati orang tua saja", benar: false },
                            { text: "Rajin belajar di sekolah", benar: false },
                            { text: "Selalu membaca buku", benar: false }
                        ]
                    },
                    {
                        pertanyaan: "Bunyi dari Sila ke 1 adalah...",
                        pilihan: [
                            { text: "a. Ketuhanan Yang Maha Esa", benar: true },
                            { text: "b. Kemanusiaan Yang Adil dan Beradab", benar: false },
                            { text: "c. Persatuan Indonesia", benar: false },
                            { text: "d. Kerakyatan Yang Dipimpin oleh Hikmat Kebijaksanaan", benar: false }
                        ]
                    }
                ],
                miniGame: [
                    { text: "Berdoa sebelum makan", benar: true },
                    { text: "Menghormati tempat ibadah", benar: true },
                    { text: "Mengganggu orang yang sedang beribadah", benar: false },
                    { text: "Mengejek agama teman", benar: false }
                ]
            },
            {
                sila: 2,
                nama: "Kemanusiaan Yang Adil dan Beradab",
                lambang: "🔗",
                penjelasan: "Sila kedua mengajarkan kita untuk memperlakukan semua orang dengan adil, baik, dan tidak membeda-bedakan.",
                quiz: [
                    {
                        pertanyaan: "Contoh sikap yang mencerminkan sila kedua adalah...",
                        pilihan: [
                            { text: "Menolong teman yang kesusahan", benar: true },
                            { text: "Memilih-milih teman", benar: false },
                            { text: "Membully teman yang berbeda", benar: false },
                            { text: "Hanya bermain dengan teman kaya", benar: false }
                        ]
                    }
                ],
                miniGame: [
                    { text: "Membantu orang tanpa pamrih", benar: true },
                    { text: "Berbuat adil kepada siapa saja", benar: true },
                    { text: "Membeda-bedakan teman berdasarkan kaya atau miskin", benar: false },
                    { text: "Mengejek teman yang berbeda", benar: false }
                ]
            },
            {
                sila: 3,
                nama: "Persatuan Indonesia",
                lambang: "🌳",
                penjelasan: "Sila ketiga mengajarkan kita untuk mencintai tanah air, menjaga persatuan, dan tidak memecah belah bangsa.",
                quiz: [
                    {
                        pertanyaan: "Bagaimana cara kita menerapkan sila ketiga?",
                        pilihan: [
                            { text: "Menjaga persatuan dan kesatuan bangsa", benar: true },
                            { text: "Hanya berteman dengan suku yang sama", benar: false },
                            { text: "Tidak peduli dengan Indonesia", benar: false },
                            { text: "Memecah belah teman-teman", benar: false }
                        ]
                    }
                ],
                miniGame: [
                    { text: "Berteman dengan siapa saja tanpa membeda-bedakan suku", benar: true },
                    { text: "Mengikuti upacara bendera dengan khidmat", benar: true },
                    { text: "Mengejek adat daerah lain", benar: false },
                    { text: "Hanya mau berteman dengan suku sendiri", benar: false }
                ]
            },
            {
                sila: 4,
                nama: "Kerakyatan Yang Dipimpin oleh Hikmat Kebijaksanaan",
                lambang: "🌟",
                penjelasan: "Sila keempat mengajarkan kita untuk bermusyawarah dan menghargai pendapat orang lain dalam mengambil keputusan.",
                quiz: [
                    {
                        pertanyaan: "Apa yang harus dilakukan saat ada masalah di kelas?",
                        pilihan: [
                            { text: "Bermusyawarah bersama untuk mencari solusi", benar: true },
                            { text: "Memaksakan kehendak sendiri", benar: false },
                            { text: "Tidak peduli dan biarkan saja", benar: false },
                            { text: "Bertengkar dengan teman", benar: false }
                        ]
                    }
                ],
                miniGame: [
                    { text: "Mendengarkan pendapat teman saat diskusi", benar: true },
                    { text: "Mengambil keputusan dengan voting yang adil", benar: true },
                    { text: "Memaksakan pendapat sendiri kepada teman", benar: false },
                    { text: "Tidak mau mendengarkan pendapat orang lain", benar: false }
                ]
            },
            {
                sila: 5,
                nama: "Keadilan Sosial bagi Seluruh Rakyat Indonesia",
                lambang: "🌾",
                penjelasan: "Sila kelima mengajarkan kita untuk berbagi, tolong-menolong, dan tidak hidup boros agar semua orang sejahtera.",
                quiz: [
                    {
                        pertanyaan: "Contoh penerapan sila kelima di sekolah adalah...",
                        pilihan: [
                            { text: "Berbagi bekal dengan teman yang tidak membawa", benar: true },
                            { text: "Pelit dan tidak mau berbagi", benar: false },
                            { text: "Hidup boros dan sombong", benar: false },
                            { text: "Hanya peduli pada diri sendiri", benar: false }
                        ]
                    }
                ],
                miniGame: [
                    { text: "Membantu teman yang kesusahan", benar: true },
                    { text: "Tidak hidup boros dan hemat", benar: true },
                    { text: "Tidak mau berbagi dengan teman", benar: false },
                    { text: "Sombong dengan kekayaan sendiri", benar: false }
                ]
            }
        ];

        let gameState = {
            currentLevel: 0,
            score: 0,
            lives: 3,
            completedLevels: [],
            miniGameAnswers: {}
        };

        // Variabel untuk pembelajaran mode
        let silasDone = {
            1: false,
            2: false,
            3: false,
            4: false,
            5: false
        };
        let autoLearnMode = false;

        // Fungsi untuk berpindah halaman
        function goToPage(pageId) {
            // Sembunyikan semua halaman
            let pages = document.querySelectorAll('.page');
            pages.forEach(p => p.classList.remove('active'));
            
            // Tampilkan halaman yang dipilih
            document.getElementById('page-' + pageId).classList.add('active');
            
            // Update progress dots jika kembali ke menu
            if (pageId === 'menu') {
                updateProgress();
            }
        }

        // Fungsi untuk ke halaman sila
        function goToSila(num) {
            // Tandai sila sudah dipelajari
            silasDone[num] = true;
            
            // Pindah ke halaman sila
            goToPage('sila' + num);
        }

        // Fungsi mulai belajar otomatis (berurutan)
        function startAutoLearn() {
            autoLearnMode = true;
            // Reset semua progress
            for (let i = 1; i <= 5; i++) {
                silasDone[i] = false;
                let dot = document.getElementById('dot-' + i);
                dot.classList.remove('done');
            }
            // Mulai dari sila 1
            goToSila(1);
        }

        // Fungsi lanjut ke sila berikutnya (mode otomatis)
        function goToNextSila(currentSila) {
            if (autoLearnMode && currentSila < 5) {
                let nextSila = currentSila + 1;
                // Update progress
                updateProgress();
                // Lanjut ke sila berikutnya
                setTimeout(() => {
                    goToSila(nextSila);
                }, 300);
            }
        }

        // Fungsi navigasi dari halaman sila (deteksi mode)
        function handleSilaNavigation(silaNum) {
            updateProgress();
            if (autoLearnMode) {
                // Jika mode otomatis, tanya apakah mau lanjut atau keluar
                let confirm = window.confirm('Kamu sedang belajar berurutan!\n\nMau lanjut belajar sila berikutnya? Klik OK\nMau kembali ke menu? Klik Cancel');
                if (confirm && silaNum < 5) {
                    goToNextSila(silaNum);
                } else {
                    autoLearnMode = false;
                    goToPage('menu');
                }
            } else {
                // Mode manual, langsung ke menu
                goToPage('menu');
            }
        }

        // Fungsi selesai belajar otomatis
        function finishAutoLearn() {
            if (autoLearnMode) {
                // Update progress terakhir
                updateProgress();
                // Trigger konfetti
                createConfetti();
                // Reset mode
                autoLearnMode = false;
                // Ke halaman penutup
                setTimeout(() => {
                    goToPage('closing');
                }, 500);
            }
        }

        // Fungsi update progress dots
        function updateProgress() {
            for (let i = 1; i <= 5; i++) {
                let dot = document.getElementById('dot-' + i);
                if (silasDone[i]) {
                    dot.classList.add('done');
                }
            }
        }

        // Fungsi cek apakah semua sila sudah dipelajari
        function checkCompletion() {
            let allDone = true;
            for (let i = 1; i <= 5; i++) {
                if (!silasDone[i]) {
                    allDone = false;
                    break;
                }
            }

            if (allDone) {
                // Trigger konfetti
                createConfetti();
                goToPage('closing');
            } else {
                alert('Yuk, pelajari semua sila dulu ya! 😊\n\nMasih ada sila yang belum kamu baca.');
            }
        }

        // Fungsi membuat efek konfetti
        function createConfetti() {
            let confettiContainer = document.getElementById('confetti');
            confettiContainer.innerHTML = ''; // Reset
            
            let colors = ['#ff6b6b', '#feca57', '#48dbfb', '#ff9ff3', '#54a0ff', '#00d2d3'];
            
            for (let i = 0; i < 50; i++) {
                let confetti = document.createElement('div');
                confetti.className = 'confetti-piece';
                confetti.style.left = Math.random() * 100 + '%';
                confetti.style.background = colors[Math.floor(Math.random() * colors.length)];
                confetti.style.animationDelay = Math.random() * 0.5 + 's';
                confettiContainer.appendChild(confetti);
            }

            // Hapus konfetti setelah animasi selesai
            setTimeout(() => {
                confettiContainer.innerHTML = '';
            }, 3000);
        }

        // Fungsi toggle balon (show/hide)
        function toggleBalloons(show) {
            let balloons = document.getElementById('balloons');
            balloons.style.display = show ? 'block' : 'none';
        }

        // Fungsi berpindah halaman - UNIVERSAL untuk semua halaman
        function goToPage(pageId) {
            // Sembunyikan semua halaman
            let pages = document.querySelectorAll('.page');
            pages.forEach(p => p.classList.remove('active'));
            
            // Tampilkan halaman yang dipilih
            document.getElementById('page-' + pageId).classList.add('active');
            
            // Update progress dots jika kembali ke menu pembelajaran
            if (pageId === 'menu') {
                updateProgress();
            }

            // Tampilkan balon di halaman intro dan menu pembelajaran saja
            if (pageId === 'intro' || pageId === 'menu') {
                toggleBalloons(true);
            } else {
                toggleBalloons(false);
            }
        }

        // Inisialisasi - tampilkan balon di awal
        toggleBalloons(true);

        // ============ GAME FUNCTIONS ============

        function goToGameMenu() {
            goToPage('game-menu');
        }

        // GAME 1: MATCH IMAGE GAME
        let imageGameState = {
            currentQuestion: 0,
            score: 0,
            correct: 0,
            answered: {},
            shuffledOptions: [] // Untuk menyimpan urutan gambar yang ter-shuffle
        };

        const imageGameQuestions = [
            { answer: 1, question: "Mana gambar Sila ke 1?" },
            { answer: 2, question: "Mana gambar Sila ke 2?" },
            { answer: 3, question: "Mana gambar Sila ke 3?" },
            { answer: 4, question: "Mana gambar Sila ke 4?" },
            { answer: 5, question: "Mana gambar Sila ke 5?" }
        ];

        // Fungsi untuk mengacak array
        function shuffleArray(array) {
            const arr = [...array];
            for (let i = arr.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [arr[i], arr[j]] = [arr[j], arr[i]];
            }
            return arr;
        }

        function startGameMatchImage() {
            imageGameState = { currentQuestion: 0, score: 0, correct: 0, answered: {}, shuffledOptions: [] };
            renderImageQuestion();
            goToPage('game-match-image');
        }

        function renderImageQuestion() {
            const container = document.getElementById('matchImageGame');
            container.innerHTML = '';

            const currentQ = imageGameQuestions[imageGameState.currentQuestion];
            
            // Shuffle pilihan gambar untuk soal ini - ACAK SETIAP KALI
            imageGameState.shuffledOptions = shuffleArray([1, 2, 3, 4, 5]);

            const html = `
                <div class="question-box">
                    ${currentQ.question}
                </div>
                <div class="image-options" id="imageOptionsList">
                    <!-- Gambar akan diisi di sini dalam urutan acak -->
                </div>
                <div class="image-feedback" id="imageFeedback"></div>
                <div style="display: flex; gap: 15px; justify-content: center; margin-top: 20px;">
                    <button class="btn" id="nextImageBtn" onclick="nextImageQuestion()" style="display: none;">Soal Berikutnya ➡️</button>
                </div>
            `;
            container.innerHTML = html;

            // Render opsi gambar dengan urutan yang di-shuffle
            const optionsList = document.getElementById('imageOptionsList');
            imageGameState.shuffledOptions.forEach((silaNumber) => {
                const option = document.createElement('div');
                option.className = 'image-option';
                option.id = 'image-option-' + silaNumber;
                if (imageGameState.answered[imageGameState.currentQuestion] === silaNumber) {
                    option.classList.add('selected');
                }
                option.innerHTML = `
                    <img src="image/lsila${silaNumber}.png" alt="Sila ${silaNumber}">
                `;
                option.onclick = () => selectImageAnswer(silaNumber);
                optionsList.appendChild(option);
            });

            updateImageGameDisplay();
        }

        function selectImageAnswer(silaNumber) {
            const currentQ = imageGameQuestions[imageGameState.currentQuestion];
            const options = document.querySelectorAll('.image-option');
            const feedback = document.getElementById('imageFeedback');
            const nextBtn = document.getElementById('nextImageBtn');

            // Disable all options
            options.forEach(opt => opt.onclick = null);

            imageGameState.answered[imageGameState.currentQuestion] = silaNumber;

            // Update visual
            options.forEach((opt) => {
                const optionSilaNum = parseInt(opt.id.replace('image-option-', ''));
                
                if (optionSilaNum === silaNumber) {
                    if (silaNumber === currentQ.answer) {
                        opt.classList.add('correct');
                        opt.classList.remove('selected');
                        feedback.className = 'image-feedback correct show';
                        feedback.innerHTML = '? Benar! Kamu hebat!';
                        imageGameState.correct++;
                        imageGameState.score += 20;
                    } else {
                        opt.classList.add('wrong');
                        opt.classList.remove('selected');
                        feedback.className = 'image-feedback wrong show';
                        feedback.innerHTML = `? Salah! Jawaban yang benar:<br><img src="image/lsila${currentQ.answer}.png" alt="Sila ${currentQ.answer}" style="width: 120px; height: auto; margin-top: 10px; border-radius: 10px;">`;
                    }
                } else if (optionSilaNum === currentQ.answer) {
                    opt.classList.add('correct');
                }
            });

            nextBtn.style.display = 'block';
            updateImageGameDisplay();
        }

        function nextImageQuestion() {
            imageGameState.currentQuestion++;
            if (imageGameState.currentQuestion < imageGameQuestions.length) {
                renderImageQuestion();
            } else {
                finishImageGame();
            }
        }

        function finishImageGame() {
            const container = document.getElementById('matchImageGame');
            container.innerHTML = `
                <div style="text-align: center; padding: 40px 20px;">
                    <div style="font-size: 4em; margin-bottom: 20px;">🎉</div>
                    <h2 style="color: #6c5ce7; font-size: 1.8em; margin-bottom: 20px;">Selesai!</h2>
                    <div style="background: linear-gradient(135deg, #ffeaa7 0%, #fdcb6e 100%); padding: 20px; border-radius: 15px; margin: 20px 0;">
                        <div style="font-size: 1.3em; font-weight: bold; color: #2d3436;">
                            Skor Akhir: ${imageGameState.score} ?
                        </div>
                        <div style="font-size: 1.1em; color: #2d3436; margin-top: 10px;">
                            Benar: ${imageGameState.correct}/5
                        </div>
                    </div>
                    <button class="btn" onclick="goToGameMenu()" style="margin-top: 20px; width: 100%;">Kembali ke Menu Game</button>
                </div>
            `;
        }

        function updateImageGameDisplay() {
            document.getElementById('imageGameCurrentQuestion').textContent = imageGameState.currentQuestion + 1;
            document.getElementById('imageGameCorrect').textContent = imageGameState.correct;
        }
        // GAME 2: TEBAK BUNYI SILA
        const silaTexts = [
            { sila: 1, text: "Ketuhanan Yang Maha Esa" },
            { sila: 2, text: "Kemanusiaan Yang Adil dan Beradab" },
            { sila: 3, text: "Persatuan Indonesia" },
            { sila: 4, text: "Kerakyatan yang dipimpin oleh hikmat kebijaksanaan dalam permusyawaratan/perwakilan" },
            { sila: 5, text: "Keadilan Sosial bagi Seluruh Rakyat Indonesia" }
        ];

        const soundGameQuestions = silaTexts.map(item => ({
            sila: item.sila,
            text: item.text,
            image: `image/lsila${item.sila}.png`
        }));

        let soundGameState = {
            score: 0,
            correct: 0,
            currentIndex: 0,
            answered: false,
            selected: null,
            options: []
        };
        function startGameSoundMatch() {
            soundGameState = {
                score: 0,
                correct: 0,
                currentIndex: 0,
                answered: false,
                selected: null,
                options: []
            };

            const container = document.getElementById('soundMatchGame');
            if (container) {
                container.innerHTML = `
                    <div class="sound-question-box" id="soundQuestion"></div>
                    <div class="sound-image-wrap">
                        <img id="soundQuestionImage" src="" alt="Gambar Sila">
                    </div>
                    <div class="sound-choice-grid" id="soundChoices"></div>
                    <div class="sound-feedback-box" id="soundFeedback"></div>
                    <button class="btn" id="soundNextBtn" onclick="nextSoundQuestion()" style="display: none; width: 100%; margin-top: 15px;">Soal Berikutnya</button>
                `;
            }

            goToPage('game-sound-match');
            renderSoundGame();
        }

        function buildSoundOptions(correctSila) {
            const correct = silaTexts.find(item => item.sila === correctSila);
            const others = silaTexts.filter(item => item.sila !== correctSila);
            const pickOthers = shuffleArray(others).slice(0, 3);
            return shuffleArray([correct, ...pickOthers]);
        }

        function renderSoundGame() {
            const question = soundGameQuestions[soundGameState.currentIndex];
            if (!question) {
                finishSoundGame();
                return;
            }

            const questionEl = document.getElementById('soundQuestion');
            const imageEl = document.getElementById('soundQuestionImage');
            const choicesEl = document.getElementById('soundChoices');
            const feedbackEl = document.getElementById('soundFeedback');
            const nextBtn = document.getElementById('soundNextBtn');

            if (!questionEl || !imageEl || !choicesEl || !feedbackEl || !nextBtn) {
                return;
            }

            questionEl.textContent = `Bunyi dari Sila ke-${question.sila} adalah...`;
            imageEl.src = question.image;

            if (soundGameState.options.length === 0) {
                soundGameState.options = buildSoundOptions(question.sila);
            }

            choicesEl.innerHTML = '';
            const letters = ['A', 'B', 'C', 'D'];
            soundGameState.options.forEach((opt, index) => {
                const btn = document.createElement('button');
                btn.className = 'sound-choice';
                btn.textContent = `${letters[index]}. ${opt.text}`;
                btn.disabled = soundGameState.answered;

                if (soundGameState.answered) {
                    if (opt.sila === question.sila) {
                        btn.classList.add('correct');
                    } else if (soundGameState.selected === opt.sila) {
                        btn.classList.add('wrong');
                    }
                } else {
                    btn.onclick = () => answerSoundGame(opt.sila);
                }

                choicesEl.appendChild(btn);
            });

            if (soundGameState.answered) {
                const isCorrect = soundGameState.selected === question.sila;
                feedbackEl.className = `sound-feedback-box show ${isCorrect ? 'correct' : 'wrong'}`;
                feedbackEl.textContent = isCorrect
                    ? 'Benar!'
                    : `Salah! Jawaban yang benar adalah: ${question.text}`;
                nextBtn.style.display = 'block';
                nextBtn.textContent = soundGameState.currentIndex === soundGameQuestions.length - 1
                    ? 'Selesai'
                    : 'Soal Berikutnya';
            } else {
                feedbackEl.className = 'sound-feedback-box';
                feedbackEl.textContent = '';
                nextBtn.style.display = 'none';
            }

            updateSoundGameDisplay();
        }

        function answerSoundGame(answerSila) {
            if (soundGameState.answered) {
                return;
            }

            const question = soundGameQuestions[soundGameState.currentIndex];
            soundGameState.answered = true;
            soundGameState.selected = answerSila;

            if (answerSila === question.sila) {
                soundGameState.correct++;
                soundGameState.score += 20;
            }

            renderSoundGame();
        }

        function nextSoundQuestion() {
            soundGameState.currentIndex++;
            soundGameState.answered = false;
            soundGameState.selected = null;
            soundGameState.options = [];

            if (soundGameState.currentIndex < soundGameQuestions.length) {
                renderSoundGame();
            } else {
                finishSoundGame();
            }
        }

        function finishSoundGame() {
            const container = document.getElementById('soundMatchGame');
            if (!container) {
                return;
            }
            container.innerHTML = `
                <div style="text-align: center; padding: 30px 20px;">
                    <h2 style="color: #6c5ce7; font-size: 1.8em; margin-bottom: 15px;">Selesai!</h2>
                    <div style="background: linear-gradient(135deg, #ffeaa7 0%, #fdcb6e 100%); padding: 18px; border-radius: 15px; margin: 20px 0;">
                        <div style="font-size: 1.2em; font-weight: bold; color: #2d3436;">
                            Skor Akhir: ${soundGameState.score}
                        </div>
                        <div style="font-size: 1.1em; color: #2d3436; margin-top: 10px;">
                            Benar: ${soundGameState.correct}/5
                        </div>
                    </div>
                    <button class="btn" onclick="goToGameMenu()" style="margin-top: 10px; width: 100%;">Kembali ke Menu Game</button>
                </div>
            `;
        }

        function updateSoundGameDisplay() {
            const scoreEl = document.getElementById('soundGameScoreValue');
            const correctEl = document.getElementById('soundGameCorrect');
            if (scoreEl) {
                scoreEl.textContent = soundGameState.score;
            }
            if (correctEl) {
                correctEl.textContent = soundGameState.correct;
            }
        }

        function resetGame() {
            gameState = {
                currentLevel: 0,
                score: 0,
                lives: 3,
                completedLevels: [],
                miniGameAnswers: {}
            };
            goToPage('intro');
        }
    </script>
</body>
</html>

