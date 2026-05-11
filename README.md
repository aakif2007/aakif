<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Kids Colors Quiz</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: linear-gradient(to right, #ffecd2, #fcb69f);
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      margin: 0;
    }

    .quiz-container {
      background: white;
      padding: 30px;
      border-radius: 20px;
      box-shadow: 0 8px 20px rgba(0,0,0,0.2);
      max-width: 500px;
      width: 90%;
      text-align: center;
    }

    h1 {
      color: #ff6f61;
    }

    .question {
      font-size: 1.5rem;
      margin: 20px 0;
    }

    .color-box {
      width: 150px;
      height: 150px;
      margin: 20px auto;
      border-radius: 15px;
      border: 4px solid #333;
    }

    .answers button {
      display: block;
      width: 100%;
      margin: 10px 0;
      padding: 12px;
      font-size: 1.1rem;
      border: none;
      border-radius: 10px;
      cursor: pointer;
      background: #6ec6ff;
      color: white;
      transition: 0.3s;
    }

    .answers button:hover {
      background: #42a5f5;
    }

    .score {
      font-size: 1.3rem;
      color: #4caf50;
      margin-top: 20px;
    }

    .restart-btn {
      margin-top: 20px;
      background: #ff9800;
    }

    .restart-btn:hover {
      background: #fb8c00;
    }
  </style>
</head>
<body>
  <div class="quiz-container">
    <h1>🎨 Kids Colors Quiz 🎨</h1>
    <div id="quiz">
      <div class="question" id="question">What color is this?</div>
      <div class="color-box" id="colorBox"></div>
      <div class="answers" id="answers"></div>
    </div>
    <div class="score" id="score"></div>
  </div>

  <script>
    const questions = [
      { type: 'color', color: 'red', question: 'What color is this?', options: ['Red', 'Blue', 'Green', 'Yellow'], answer: 'Red' },
      { type: 'object', color: 'red', question: 'What is the color of an apple?', options: ['Red', 'Blue', 'Purple', 'White'], answer: 'Red' },
      { type: 'color', color: 'blue', question: 'What color is this?', options: ['Purple', 'Orange', 'Blue', 'Pink'], answer: 'Blue' },
      { type: 'object', color: 'yellow', question: 'What is the color of a banana?', options: ['Green', 'Yellow', 'Blue', 'Black'], answer: 'Yellow' },
      { type: 'color', color: 'green', question: 'What color is this?', options: ['Green', 'Black', 'Brown', 'White'], answer: 'Green' },
      { type: 'object', color: 'orange', question: 'What is the color of an orange fruit?', options: ['Purple', 'Orange', 'Blue', 'Pink'], answer: 'Orange' },
      { type: 'color', color: 'yellow', question: 'What color is this?', options: ['Red', 'Yellow', 'Gray', 'Blue'], answer: 'Yellow' },
      { type: 'object', color: 'purple', question: 'What is the color of grapes?', options: ['Purple', 'Green', 'Orange', 'Red'], answer: 'Purple' },
      { type: 'color', color: 'purple', question: 'What color is this?', options: ['Purple', 'Green', 'Orange', 'Red'], answer: 'Purple' }
    ];

    let currentQuestion = 0;
    let score = 0;

    const colorBox = document.getElementById('colorBox');
    const answersDiv = document.getElementById('answers');
    const scoreDiv = document.getElementById('score');
    const questionText = document.getElementById('question');

    function loadQuestion() {
      const q = questions[currentQuestion];
      questionText.textContent = q.question;
      colorBox.style.backgroundColor = q.color;
      answersDiv.innerHTML = '';

      q.options.forEach(option => {
        const btn = document.createElement('button');
        btn.textContent = option;
        btn.onclick = () => checkAnswer(option);
        answersDiv.appendChild(btn);
      });
    }

    function checkAnswer(selected) {
      if (selected === questions[currentQuestion].answer) {
        score++;
        alert('🎉 Correct!');
      } else {
        alert('❌ Oops! Correct answer: ' + questions[currentQuestion].answer);
      }

      currentQuestion++;

      if (currentQuestion < questions.length) {
        loadQuestion();
      } else {
        showResults();
      }
    }

    function showResults() {
      document.getElementById('quiz').innerHTML = `
        <h2>Quiz Finished! 🎊</h2>
        <p>You scored ${score} out of ${questions.length}</p>
        <button class="restart-btn" onclick="restartQuiz()">Play Again</button>
      `;
    }

    function restartQuiz() {
      currentQuestion = 0;
      score = 0;
      document.getElementById('quiz').innerHTML = `
        <div class="question" id="question">What color is this?</div>
        <div class="color-box" id="colorBox"></div>
        <div class="answers" id="answers"></div>
      `;

      window.location.reload();
    }

    loadQuestion();
  </script>
</body>
</html>
