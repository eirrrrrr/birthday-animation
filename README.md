<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Quiz and Animation</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f7f7f7;
      margin: 0;
      padding: 0;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      overflow: hidden;
    }
    #notification {
      background: #fff;
      border-radius: 10px;
      padding: 20px;
      box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
      text-align: center;
    }
    #input-field {
      width: 80%;
      padding: 10px;
      margin-top: 10px;
      border: 1px solid #ddd;
      border-radius: 5px;
    }
    .hidden {
      display: none;
    }
    .confetti {
      position: absolute;
      width: 10px;
      height: 10px;
      background-color: red;
      opacity: 0.7;
      animation: fall 2s infinite;
    }
    @keyframes fall {
      0% {
        transform: translateY(-100vh);
        opacity: 1;
      }
      100% {
        transform: translateY(100vh);
        opacity: 0;
      }
    }
  </style>
</head>
<body>
  <div id="notification">
    <h2 id="question">3 + 7 =</h2>
    <input id="input-field" type="text" placeholder="ketik angka saja">
  </div>

  <script>
    const notification = document.getElementById("notification");
    const question = document.getElementById("question");
    const inputField = document.getElementById("input-field");

    let currentStep = 0;

    const questions = [
      { question: "3 + 7 =", answer: "10", placeholder: "ketik angka saja" },
      {
        question: "Cristiano Ronaldo berasal dari klub sepak bola?",
        answer: "manchester united",
        placeholder: "ketik dengan huruf kecil",
      },
      {
        question: "Sapi minum apa?",
        answer: "air",
        placeholder: "ketik dengan huruf kecil",
      },
    ];

    inputField.addEventListener("keyup", (e) => {
      if (e.key === "Enter") {
        const userAnswer = inputField.value.trim();
        if (userAnswer.toLowerCase() === questions[currentStep].answer) {
          currentStep++;
          if (currentStep < questions.length) {
            question.textContent = questions[currentStep].question;
            inputField.placeholder = questions[currentStep].placeholder;
            inputField.value = "";
          } else {
            showCongratulations();
          }
        } else {
          alert("Jawaban salah! Coba lagi.");
          inputField.value = "";
        }
      }
    });

    function showCongratulations() {
      notification.innerHTML = "<h1>Congratulation 🎉</h1>";
      createConfetti();
      setTimeout(() => {
        notification.remove();
        showAnimation();
      }, 2000);
    }

    function createConfetti() {
      for (let i = 0; i < 100; i++) {
        const confetti = document.createElement("div");
        confetti.classList.add("confetti");
        confetti.style.backgroundColor = getRandomColor();
        confetti.style.left = `${Math.random() * 100}vw`;
        confetti.style.animationDelay = `${Math.random() * 2}s`;
        document.body.appendChild(confetti);
        setTimeout(() => confetti.remove(), 2000);
      }
    }

    function getRandomColor() {
      const colors = ["red", "yellow", "green", "blue", "pink", "purple"];
      return colors[Math.floor(Math.random() * colors.length)];
    }

    function showAnimation() {
      const canvas = document.createElement("canvas");
      canvas.width = 600;
      canvas.height = 500;
      canvas.style.display = "block";
      canvas.style.margin = "0 auto";
      document.body.appendChild(canvas);

      const ctx = canvas.getContext("2d");

      function drawCake() {
        ctx.fillStyle = "brown";
        ctx.fillRect(200, 300, 200, 80);
        ctx.fillStyle = "pink";
        ctx.fillRect(200, 240, 200, 60);
        ctx.fillStyle = "white";
        ctx.fillRect(200, 210, 200, 30);

        ctx.fillStyle = "blue";
        for (let i = 0; i < 5; i++) {
          ctx.beginPath();
          ctx.arc(240 + i * 40, 225, 8, 0, Math.PI * 2);
          ctx.fill();
        }

        for (let i = 0; i < 3; i++) {
          ctx.fillStyle = "white";
          ctx.fillRect(250 + i * 50, 180, 10, 30);
          ctx.fillStyle = "yellow";
          ctx.beginPath();
          ctx.moveTo(255 + i * 50, 180);
          ctx.lineTo(250 + i * 50, 160);
          ctx.lineTo(260 + i * 50, 160);
          ctx.closePath();
          ctx.fill();
        }
      }

      function animateBackground() {
        const colors = ["#FFB6C1", "#ADD8E6", "#FFFFE0", "#98FB98", "#FFD700"];
        let frame = 0;
        setInterval(() => {
          ctx.fillStyle = colors[frame % colors.length];
          ctx.fillRect(0, 0, canvas.width, canvas.height);
          drawCake();
          frame++;
        }, 200);
      }

      animateBackground();
    }
  </script>
</body>
</html>
