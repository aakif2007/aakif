# ILTES KIDS Multi-Page Quiz Website

## `index.html` (Welcome Page)

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>ILTES KIDS Welcome</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      background: linear-gradient(to right, #ffecd2, #fcb69f);
      text-align: center;
    }
    .container {
      background: white;
      padding: 40px;
      border-radius: 20px;
      box-shadow: 0 8px 20px rgba(0,0,0,0.2);
    }
    h1 {
      color: #ff4081;
      animation: bounce 2s infinite;
    }
    h2 {
      color: #7b1fa2;
    }
    .icons {
      font-size: 3rem;
      margin: 20px 0;
      animation: floatIcons 2s infinite alternate;
    }
    button {
      padding: 15px 30px;
      font-size: 1.2rem;
      border: none;
      border-radius: 12px;
      background: #ff6f61;
      color: white;
      cursor: pointer;
    }
    button:hover {
      transform: scale(1.05);
    }
    @keyframes bounce {
      50% { transform: translateY(-10px); }
    }
    @keyframes floatIcons {
      from { transform: translateY(0); }
      to { transform: translateY(-10px); }
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>🌈 Welcome to ILTES KIDS 🌈</h1>
    <h2>Mentor: Masna 🌟</h2>
    <div class="icons">🍎 🎈 🌈 ⭐</div>
    <button onclick="goToQuiz()">Start Quiz</button>
  </div>

  <script>
    function goToQuiz() {
      window.location.href = "loading.html";
    }
  </script>
</body>
</html>
```

---

## `loading.html` (Transition Loading Page)

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Loading Quiz</title>
  <style>
    body {
      margin: 0;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      height: 100vh;
      background: linear-gradient(to right, #ffecd2, #fcb69f);
      font-family: Arial, sans-serif;
    }
    .apple {
      font-size: 5rem;
      animation: spinBounce 2s infinite;
    }
    @keyframes spinBounce {
      50% { transform: rotate(180deg) translateY(-20px); }
      100% { transform: rotate(360deg); }
    }
  </style>
</head>
<body>
  <div class="apple">🍎</div>
  <h2>Loading Questions...</h2>

  <script>
    setTimeout(() => {
      window.location.href = "quiz.html";
    }, 2500);
  </script>
</body>
</html>
```

---

## `quiz.html` (Questions Page)

```html
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
    .color-box {
      width: 150px;
      height: 150px;
      margin: 20px auto;
      border-radius: 15px;
      border: 4px solid #333;
    }
    button {
      display: block;
      width: 100%;
      margin: 10px 0;
      padding: 12px;
      border: none;
      border-radius: 10px;
      background: #42a5f5;
      color: white;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <div class="quiz-container">
    <h1>🎨 Kids Colors Quiz 🎨</h1>
    <div id="question"></div>
    <div class="color-box" id="colorBox"></div>
    <div id="answers"></div>
  </div>

  <script>
    const questions = [
      { color: 'red', question: 'What is the color of an apple?', options: ['Red','Blue','Green','Yellow'], answer: 'Red' },
      { color: 'yellow', question: 'What is the color of a banana?', options: ['Yellow','Blue','Black','Pink'], answer: 'Yellow' },
      { color: 'purple', question: 'What is the color of grapes?', options: ['Purple','Orange','Green','Red'], answer: 'Purple' }
    ];

    let currentQuestion = 0;
    let score = 0;

    function loadQuestion() {
      const q = questions[currentQuestion];
      document.getElementById('question').textContent = q.question;
      document.getElementById('colorBox').style.backgroundColor = q.color;
      const answers = document.getElementById('answers');
      answers.innerHTML = '';

      q.options.forEach(option => {
        const btn = document.createElement('button');
        btn.textContent = option;
        btn.onclick = () => checkAnswer(option);
        answers.appendChild(btn);
      });
    }

    function checkAnswer(selected) {
      if (selected === questions[currentQuestion].answer) score++;
      currentQuestion++;

      if (currentQuestion < questions.length) {
        window.location.href = 'loading.html';
        sessionStorage.setItem('questionIndex', currentQuestion);
        sessionStorage.setItem('score', score);
      } else {
        document.querySelector('.quiz-container').innerHTML = `
          <h2>Quiz Finished! 🎊</h2>
          <p>Your Score: ${score}/${questions.length}</p>
          <button onclick="window.location.href='index.html'">Play Again</button>
        `;
      }
    }

    window.onload = () => {
      currentQuestion = parseInt(sessionStorage.getItem('questionIndex')) || 0;
      score = parseInt(sessionStorage.getItem('score')) || 0;
      loadQuestion();
    };
  </script>
</body>
</html>
```

---

## GitHub Upload Instructions

* Upload all 3 files into one repository:

  * `index.html`
  * `loading.html`
  * `quiz.html`
* Enable GitHub Pages in repository settings.
* Your website will now have:

  * Welcome page
  * Start Quiz button
  * Loading animation between pages
  * Separate quiz page
  * Smooth kid-friendly experience.
