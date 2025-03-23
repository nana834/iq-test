# iq-test
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Welcome Page 
        <font> white 
            
        </font>
    </title>
    <style>
       
        body {
            font-family: Arial, sans-serif;
            
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
           background-color: #ccc;
           background-image: url('	https://img.freepik.com/premium-photo/math-equation_1134901-221786.jpg?semt=ais_hybrid');
        }
        .container {
            background-color: #314da8;
            padding: 20px;
            border-radius: 15px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            text-align: center;
        }

        h1 {
            margin-bottom: 20px;
        }

        input[type="text"] {
            padding: 10px;
            font-size: 16px;
            width: 80%;
            margin-bottom: 20px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }

        button {
            padding: 10px 20px;
            font-size: 16px;
            cursor: pointer;
            background-color: #5387d6;
            color:black;
            border: none;
            border-radius: 5px;
            font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
            font-size: 20px;
        }

        button:hover {
            background-color: #218838;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Welcome to the IQ Test Game!</h1>
        <input type="text" id="nameInput" placeholder="Enter your name...">
        <button id="submitButton">Start Game</button>
    </div>

    <script>
       
        const nameInput = document.getElementById('nameInput');
        const submitButton = document.getElementById('submitButton');

        submitButton.addEventListener('click', () => {
            const userName = nameInput.value.trim();

            if (userName) {
             
                localStorage.setItem('userName', userName);
                
                window.location.href = 'iq.html';
            } else {
                alert('Please enter your name!');
            }
        });
        
    </script>
</body>
game
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>IQ Test Game</title>
    <style>
       
        body {
        background-image: url('	https://img.freepik.com/free-vector/mathematical-g…or-gradient-blue-education-remix_53876-114100.jpg') ;
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }

        .container {
            background-color: #4752ec;
            padding: 60px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(182, 7, 7, 0.1);
            text-align: center;
        }

        h1 {
            margin-bottom: 30px;
        }

        #welcomeMessage {
            font-size: 24px;
            margin-bottom: 20px;
        }

        #question {
            font-size: 24px;
            margin-bottom: 20px;
        }

        #answer {
            padding: 10px;
            font-size: 18px;
            width: 100%;
            margin-bottom: 20px;
        }

        #Next {
            padding: 20px 40px;
            font-size: 18px;
            cursor: pointer;
            border-radius: 30px;
            font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
            font-style: unset;
            forced-color-adjust: red;
             
             background-color: rgb(134, 134, 224);
             font-size: 30px;
        }

        #result, #score {
            margin-top: 20px;
            font-size: 18px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>IQ Test Game</h1>
        <div id="welcomeMessage"></div>
        <div id="question"></div>
        <input type="text" id="answer" placeholder="Your answer...">
        <button id="Next">Next</button>
        <div id="result"></div>
        <div id="score"></div>
    </div>

    <script>
        
        
        const welcomeMessage = document.getElementById('welcomeMessage');
        const questionElement = document.getElementById('question');
        const answerElement = document.getElementById('answer');
        const submitButton = document.getElementById('Next');
        const resultElement = document.getElementById('result');
        const scoreElement = document.getElementById('score');

       
        const userName = localStorage.getItem('userName');
        welcomeMessage.textContent = `Hello, ${userName}! Let's test your IQ.`;

        let score = 0;
        let totalQuestions = 10;
        let currentQuestion = 0;
        let level = 1; 

        function generateMathQuestion() {
            const operations = ['+', '-', '*', '/'];
            const operation = operations[Math.floor(Math.random() * operations.length)];
            let num1, num2;

            if (operation === '/') {
                num2 = Math.floor(Math.random() * 10) + 1; // Ensure no division by zero
                num1 = num2 * (Math.floor(Math.random() * 10) + 1);
            } else {
                num1 = Math.floor(Math.random() * 100) + 1;
                num2 = Math.floor(Math.random() * 100) + 1;
            }

            const question = `${num1} ${operation} ${num2} = ?`;
            const correctAnswer = eval(`${num1} ${operation} ${num2}`);

            return { question, correctAnswer };
        }

        function generateGeometryQuestion() {
            const questionTypes = ['triangleAngle', 'countTriangles'];
            const type = questionTypes[Math.floor(Math.random() * questionTypes.length)];

            if (type === 'triangleAngle') {
                const angle1 = Math.floor(Math.random() * 100) + 1;
                const angle2 = Math.floor(Math.random() * (180 - angle1)) + 1;
                const angle3 = 180 - angle1 - angle2; // Sum of angles in a triangle is 180 degrees
                const question = `In a triangle, two angles are ${angle1}° and ${angle2}°. What is the third angle?`;
                const correctAnswer = angle3;
                return { question, correctAnswer };
            } else if (type === 'countTriangles') {
                const figure = `
                    ▲
                   ▲ ▲
                  ▲ ▲ ▲
                `;
                const question = `How many triangles are in the following figure?\n${figure}`;
                const correctAnswer = 9; 
                return { question, correctAnswer };
            }
        }

        function displayQuestion() {
            if (currentQuestion < totalQuestions) {
                let questionData;
                if (level === 1) {
                    questionData = generateMathQuestion();
                } else if (level === 2) {
                    questionData = generateGeometryQuestion();
                }

                questionElement.textContent = questionData.question;
                answerElement.value = '';
                resultElement.textContent = '';

                submitButton.onclick = () => {
                    const userAnswer = parseFloat(answerElement.value);
                    if (userAnswer === questionData.correctAnswer) {
                        score++;
                        resultElement.textContent = 'Correct!';
                    } else {
                        resultElement.textContent = `Wrong! The correct answer was ${questionData.correctAnswer}.`;
                    }
                    currentQuestion++;
                    displayQuestion();
                };
            } else {
                if (level === 1) {
                    
                    level = 2;
                    currentQuestion = 0;
                    totalQuestions = 5; 
                    scoreElement.textContent = `Math Level Complete! Your score is ${score}/${totalQuestions}. Moving to Geometry Level...`;
                    setTimeout(() => {
                        displayQuestion();
                    }, 3000); 
                } else if (level === 2) {
                   
                    const totalScore = score + (level - 1) * totalQuestions; 
                    scoreElement.textContent = `Game Complete! Your total score is ${totalScore}/${totalQuestions * 2}.`;
                    questionElement.textContent = 'Thank you for playing!';
                    answerElement.style.display = 'none';
                    submitButton.style.display = 'none';
                }
            }
        }

        displayQuestion();
    </script>

     
</body>
</html>
