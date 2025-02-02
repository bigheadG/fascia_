# fascia_
# How to build up own web page

Step-by-Step Guide to Set Up GitHub Pages
Create a GitHub Repository:

(1) Go to GitHub and sign in to your account.
Click the "+" icon in the top right corner and select "New repository".
Name your repository (e.g., alert-program), set it to "Public", and click "Create repository".
Upload Your Files:

(2) On your repository page, click "Add file" and select "Upload files".
Drag and drop your index.html and cricket.wav files into the upload area.
Click "Commit changes" to upload the files to the repository.
Enable GitHub Pages:

(3) Go to the repository settings by clicking the "Settings" tab.
Scroll down to the "GitHub Pages" section.
Under "Source", select the branch (usually main) and the root directory.
Click "Save" or "Save changes".
GitHub Pages will provide a URL where your webpage is hosted. 

(4) This usually looks like https://bigheadG.github.io/fascia_/













# vesion 2.0
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Self Myofascial Release Program</title>
    <style>
        body {
            display: flex;
            flex-direction: column;
            justify-content: flex-start;
            align-items: center;
            height: 100vh;
            margin: 0;
            padding-top: 20px; /* Adjust this value to move the content further up or down */
            font-family: 'Consolas', monospace;
        }
        #startButton {
            padding: 20px 40px;
            font-size: 24px;
            cursor: pointer;
            margin-top: 20px;
        }
        h1 {
            margin-bottom: 20px;
        }
        .status-line {
            display: flex;
            width: 100%;
            justify-content: flex-start;
            margin-bottom: 5px;
        }
        .status-label {
            min-width: 120px;
            display: inline-block;
        }
        #waitSecValue {
            font-size: 100px;
            color: red;
            position: fixed;
            bottom: 20px;
            text-align: center;
            width: 100%;
        }
    </style>
</head>
<body>
    <h1>FASCIA</h1>
    <div id="status">Self Myofascial Release</div>
    <div id="waitSecValue"></div>
    <button id="startButton">CLICK STARTING</button>
    <audio id="cricketSound" src="cricket.wav"></audio>
    <script>
        let loopCount = 0;
        const cricketSound = document.getElementById('cricketSound');
        let endTime;

        function playCricketSound(times = 1, interval = 500) {
            let count = 0;
            const playSound = () => {
                if (count < times) {
                    cricketSound.currentTime = 0;
                    cricketSound.play().then(() => {
                        console.log('Cricket sound played');
                    }).catch(error => {
                        console.error('Error playing sound:', error);
                    });
                    count++;
                    setTimeout(playSound, interval);
                }
            };
            playSound();
        }

        function startCountdown(duration, loopCount, display) {
            let timer = duration;
            const countdown = setInterval(() => {
                const seconds = parseInt(timer % 60, 10);
                const currentTime = new Date().toTimeString().split(' ')[0];
                document.getElementById('waitSecValue').textContent = `${seconds}`;

                display.innerHTML = `
                    <div class="status-line"><span class="status-label">Step:</span> <span>${loopCount}/60</span></div>
                    <div class="status-line"><span class="status-label">Current_time:</span> <span>${currentTime}</span></div>
                    <div class="status-line"><span class="status-label">End_time:</span> <span>${endTime}</span></div>
                `;

                if (--timer < 0) {
                    clearInterval(countdown);
                    if (loopCount < 59) {
                        showAlert();
                    } else {
                        document.getElementById('status').innerHTML = '<div class="status-line"><span class="status-label">Total time out:</span> <span>Alerting Finished</span></div>';
                    }
                }
            }, 1000);
        }

        function showAlert() {
            playCricketSound();
            loopCount++;
            startCountdown(59, loopCount, document.getElementById('status'));
        }

        function calculateEndTime() {
            const now = new Date();
            now.setMinutes(now.getMinutes() + 60);
            endTime = now.toTimeString().split(' ')[0]; // Get HH:MM:SS format
        }

        document.getElementById('startButton').addEventListener('click', () => {
            calculateEndTime();
            playCricketSound(1, 1000); // Play cricket sound 1 time, 1 second apart
            setTimeout(() => {
                showAlert();
                document.getElementById('startButton').style.display = 'none';
            }, 1000); // Delay to ensure the first sound is heard
        });
    </script>
</body>
</html>











# version 1.0
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Self Myofascial Release Program V1.0</title>
    <style>
        body {
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            height: 50vh;
            margin: 0;
            font-family: 'Consolas', monospace;
        }
        #startButton {
            padding: 20px 40px;
            font-size: 24px;
            cursor: pointer;
            margin-top: 20px;
        }
        h1 {
            margin-bottom: 20px;
        }
        .status-line {
            display: flex;
            width: 100%;
            justify-content: flex-start;
            margin-bottom: 5px;
        }
        .status-label {
            min-width: 120px;
            display: inline-block;
        }
        #stepValue {
            font-size: 48px;
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <h1>FASCIA</h1>
    <p id="status">Self Myofascial Release</p>
    <button id="startButton">CLICK STARTING</button>
    <audio id="cricketSound" src="cricket.wav"></audio>
    <script>
        let loopCount = 0;
        const cricketSound = document.getElementById('cricketSound');
        let endTime;

        function playCricketSound(times = 1, interval = 500) {
            let count = 0;
            const playSound = () => {
                if (count < times) {
                    cricketSound.currentTime = 0;
                    cricketSound.play().then(() => {
                        console.log('Cricket sound played');
                    }).catch(error => {
                        console.error('Error playing sound:', error);
                    });
                    count++;
                    setTimeout(playSound, interval);
                }
            };
            playSound();
        }

        function startCountdown(duration, loopCount, display) {
            let timer = duration;
            const countdown = setInterval(() => {
                const seconds = parseInt(timer % 60, 10);
                const currentTime = new Date().toTimeString().split(' ')[0];
                display.innerHTML = `Step: ${loopCount}/60<br>Wait_sec: ${seconds}<br>Current_time: ${currentTime}<br>End_time: ${endTime}`;

                if (--timer < 0) {
                    clearInterval(countdown);
                    if (loopCount < 59) {
                        showAlert();
                    } else {
                        document.getElementById('status').textContent = 'Total time out: Alerting Finished';
                    }
                }
            }, 1000);
        }

        function showAlert() {
            playCricketSound();
            loopCount++;
            startCountdown(59, loopCount, document.getElementById('status'));
        }

        function calculateEndTime() {
            const now = new Date();
            now.setMinutes(now.getMinutes() + 60);
            endTime = now.toTimeString().split(' ')[0]; // Get HH:MM:SS format
        }

        document.getElementById('startButton').addEventListener('click', () => {
            calculateEndTime();
            playCricketSound(1, 1000); // Play cricket sound 1 time, 1 second apart
            setTimeout(() => {
                showAlert();
                document.getElementById('startButton').style.display = 'none';
            }, 1000); // Delay to ensure the first sound is heard
        });
    </script>
</body>
</html>
