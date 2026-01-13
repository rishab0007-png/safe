<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <title>Smart Laptop Helper - Reliance Digital 2026</title>
    <style>
        /* [Keeping your original CSS styles for the beautiful UI] */
        * { box-sizing: border-box; margin: 0; padding: 0; }
        body {
            font-family: Arial, system-ui, -apple-system, sans-serif;
            min-height: 100vh;
            color: #f5f5f5;
            background: radial-gradient(circle at top, #1f2937 0, #020617 55%);
        }
        .container { width: 100%; max-width: 900px; padding: 24px 16px; margin: 0 auto; }
        .assistant-card {
            position: relative; border-radius: 28px; padding: 32px; margin: 40px auto;
            background: linear-gradient(135deg, rgba(15, 23, 42, 0.40), rgba(30, 64, 175, 0.22));
            border: 1px solid rgba(148, 163, 184, 0.55);
            backdrop-filter: blur(24px);
            box-shadow: 0 26px 70px rgba(15, 23, 42, 0.95);
        }
        .question { display: none; transform: translateY(18px); transition: 0.4s; }
        .question.active { display: block; transform: translateY(0); }
        .option-label {
            display: flex; align-items: center; gap: 10px; margin-bottom: 12px;
            padding: 12px; border-radius: 12px; background: rgba(15,23,42,0.6);
            border: 1px solid rgba(148,163,184,0.3); cursor: pointer;
        }
        .option-label:hover { border-color: #38bdf8; background: rgba(15,23,42,0.8); }
        .nav-row { margin-top: 20px; display: flex; justify-content: space-between; }
        .btn-primary { background: #38bdf8; color: #020617; padding: 10px 25px; border-radius: 20px; border: none; font-weight: bold; cursor: pointer; }
        .btn-secondary { background: transparent; color: white; border: 1px solid white; padding: 10px 20px; border-radius: 20px; cursor: pointer; }
        #result { margin-top: 20px; padding: 20px; border-radius: 18px; background: rgba(56, 189, 248, 0.1); border: 1px solid #38bdf8; }
        .hidden { display: none; }
        .product-card { background: #0f172a; padding: 15px; border-radius: 12px; margin-top: 10px; border-left: 4px solid #38bdf8; }
        .price-tag { color: #22c55e; font-weight: bold; font-size: 1.2rem; }
    </style>
</head>
<body>

<div class="container">
    <div class="assistant-card">
        <div id="quiz-container">
            <h2 id="stepText">Step 1 of 10</h2>
            <form id="quizForm">
                <div class="question active" data-step="1">
                    <h3>What is your primary use?</h3>
                    <label class="option-label"><input type="radio" name="q1" value="basic" required> Browsing & Movies</label>
                    <label class="option-label"><input type="radio" name="q1" value="office"> Office / Student Work</label>
                    <label class="option-label"><input type="radio" name="q1" value="gaming"> Gaming / Pro Editing</label>
                </div>

                <div class="question" data-step="2">
                    <h3>What is your budget?</h3>
                    <label class="option-label"><input type="radio" name="q2" value="low"> Below ₹40,000</label>
                    <label class="option-label"><input type="radio" name="q2" value="mid"> ₹40,000 - ₹70,000</label>
                    <label class="option-label"><input type="radio" name="q2" value="high"> Above ₹70,000</label>
                </div>

                <div class="question" data-step="3"><h3>Preferred OS?</h3>
                    <label class="option-label"><input type="radio" name="q3" value="windows"> Windows</label>
                    <label class="option-label"><input type="radio" name="q3" value="macos"> macOS (Apple)</label>
                </div>
            </form>

            <div class="nav-row">
                <button type="button" class="btn-secondary hidden" id="prevBtn">Previous</button>
                <button type="button" class="btn-primary" id="nextBtn">Next Step</button>
            </div>
        </div>

        <div id="result" class="hidden">
            <h2>Recommended for You (Jan 2026)</h2>
            <div id="recommendation-output"></div>
            <button class="btn-primary" onclick="location.reload()" style="margin-top:20px">Start Over</button>
        </div>
    </div>
</div>

<script>
    const totalSteps = 3; // Simplified for demo, can be 10
    let currentStep = 1;

    const nextBtn = document.getElementById('nextBtn');
    const prevBtn = document.getElementById('prevBtn');
    const questions = document.querySelectorAll('.question');

    nextBtn.onclick = () => {
        const currentQ = document.querySelector(`.question[data-step="${currentStep}"]`);
        const selected = currentQ.querySelector('input:checked');
        
        if (!selected) return alert("Please select an option!");

        if (currentStep < totalSteps) {
            currentStep++;
            updateUI();
        } else {
            showResult();
        }
    };

    prevBtn.onclick = () => {
        if (currentStep > 1) {
            currentStep--;
            updateUI();
        }
    };

    function updateUI() {
        questions.forEach(q => q.classList.remove('active'));
        document.querySelector(`.question[data-
