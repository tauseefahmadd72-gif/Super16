# Super16
zangetsu
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>FRIDAY Voice Assistant – Stark Mode</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />

  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: system-ui, -apple-system, BlinkMacSystemFont,
        "Segoe UI", sans-serif;
    }

    body {
      min-height: 100vh;
      background:
        radial-gradient(circle at top, #1f2933, #020617 55%, #000 100%);
      color: #e5e7eb;
      display: flex;
      align-items: center;
      justify-content: center;
      position: relative;
      overflow: hidden;
    }

    .screen {
      width: 100%;
      max-width: 480px;
      padding: 32px 20px;
      display: flex;
      flex-direction: column;
      align-items: center;
      text-align: center;
    }

    /* FRIDAY brand – Stark style */
    .brand {
      font-size: 1.4rem;
      letter-spacing: 0.3em;
      text-transform: uppercase;
      color: #f9fafb;
      margin-bottom: 48px;
      text-shadow:
        0 0 12px rgba(248, 250, 252, 0.9),
        0 0 24px rgba(248, 113, 113, 0.7);
    }

    .brand span {
      color: #f97316; /* orange highlight on F */
      text-shadow:
        0 0 10px rgba(249, 115, 22, 0.9),
        0 0 22px rgba(248, 113, 113, 0.9);
    }

    .circle-wrapper {
      position: relative;
      width: 230px;
      height: 230px;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    /* Outer arc / ring */
    .ring {
      position: absolute;
      inset: 0;
      border-radius: 50%;
      border: 2px solid rgba(248, 113, 113, 0.6);
      box-shadow:
        0 0 35px rgba(248, 113, 113, 0.8),
        0 0 80px rgba(249, 115, 22, 0.5);
      opacity: 0.85;
      transition: 0.25s ease;
    }

    .circle-button {
      position: relative;
      width: 170px;
      height: 170px;
      border-radius: 50%;
      border: 1px solid rgba(248, 250, 252, 0.2);
      background:
        radial-gradient(circle at 30% 20%, #7f1d1d, #020617 70%);
      display: flex;
      align-items: center;
      justify-content: center;
      cursor: pointer;
      box-shadow:
        0 22px 60px rgba(0, 0, 0, 0.9),
        inset 0 0 26px rgba(0, 0, 0, 0.9);
      transition: transform 0.18s ease, box-shadow 0.18s ease,
        border-color 0.18s ease;
    }

    .circle-button:hover {
      transform: translateY(-3px) scale(1.04);
      border-color: rgba(252, 165, 165, 0.9);
      box-shadow:
        0 26px 70px rgba(0, 0, 0, 1),
        0 0 32px rgba(248, 113, 113, 0.7);
    }

    .circle-button:active {
      transform: scale(0.97);
    }

    .circle-inner {
      width: 120px;
      height: 120px;
      border-radius: 50%;
      background:
        radial-gradient(circle at 30% 20%, #b91c1c, #111827 75%);
      display: flex;
      align-items: center;
      justify-content: center;
      box-shadow:
        0 0 26px rgba(248, 113, 113, 1),
        inset 0 0 20px rgba(0, 0, 0, 0.9);
    }

    .mic-icon {
      font-size: 2.8rem;
      filter: drop-shadow(0 0 10px rgba(252, 165, 165, 0.9));
    }

    /* Listening animation – arc reactor style */
    .listening .ring {
      animation: arcPulse 1.4s infinite ease-out;
      border-color: rgba(248, 113, 113, 0.9);
      box-shadow:
        0 0 65px rgba(248, 113, 113, 1),
        0 0 120px rgba(250, 204, 21, 0.6);
    }

    .listening .circle-inner {
      animation: corePulse 1s infinite alternate ease-in-out;
      background:
        radial-gradient(circle at 30% 20%, #ef4444, #111827 75%);
    }

    .listening .mic-icon {
      text-shadow:
        0 0 16px rgba(252, 165, 165, 1),
        0 0 28px rgba(250, 204, 21, 0.8);
    }

    @keyframes arcPulse {
      0% {
        transform: scale(1);
        opacity: 0.9;
      }
      100% {
        transform: scale(1.17);
        opacity: 0.25;
      }
    }

    @keyframes corePulse {
      0% {
        transform: scale(1);
        box-shadow:
          0 0 20px rgba(248, 113, 113, 1),
          inset 0 0 18px rgba(0, 0, 0, 0.95);
      }
      100% {
        transform: scale(1.07);
        box-shadow:
          0 0 32px rgba(250, 204, 21, 1),
          inset 0 0 12px rgba(0, 0, 0, 0.95);
      }
    }

    /* IRON MAN STYLE ANIMATED WATERMARK */
    .watermark {
      position: absolute;
      bottom: 20px;
      right: 24px;
      font-size: 0.95rem;
      letter-spacing: 0.25em;
      text-transform: uppercase;
      color: #f97316;
      opacity: 0.55;
      user-select: none;
      pointer-events: none;
      text-shadow:
        0 0 10px rgba(248, 113, 113, 0.9),
        0 0 22px rgba(250, 204, 21, 0.8);
      animation:
        wmGlow 2.4s infinite ease-in-out,
        wmDrift 7s infinite ease-in-out,
        wmFlicker 5.2s infinite steps(2, end);
    }

    @keyframes wmGlow {
      0% {
        opacity: 0.35;
        text-shadow:
          0 0 6px rgba(248, 113, 113, 0.6),
          0 0 12px rgba(250, 204, 21, 0.4);
      }
      50% {
        opacity: 0.8;
        text-shadow:
          0 0 16px rgba(248, 113, 113, 1),
          0 0 30px rgba(250, 204, 21, 0.9);
      }
      100% {
        opacity: 0.45;
        text-shadow:
          0 0 8px rgba(248, 113, 113, 0.7),
          0 0 16px rgba(250, 204, 21, 0.6);
      }
    }

    @keyframes wmDrift {
      0%   { transform: translateX(0); }
      50%  { transform: translateX(-14px); }
      100% { transform: translateX(0); }
    }

    /* occasional tiny flicker like HUD glitch */
    @keyframes wmFlicker {
      0%, 96%, 100% {
        filter: none;
      }
      97% {
        filter: brightness(1.2);
      }
      98% {
        filter: brightness(0.75);
      }
      99% {
        filter: brightness(1.4);
      }
    }

    @media (max-width: 480px) {
      .circle-wrapper {
        width: 200px;
        height: 200px;
      }
      .circle-button {
        width: 150px;
        height: 150px;
      }
      .circle-inner {
        width: 110px;
        height: 110px;
      }
      .mic-icon {
        font-size: 2.4rem;
      }
      .brand {
        margin-bottom: 36px;
        font-size: 1.2rem;
      }
      .watermark {
        right: 16px;
        bottom: 16px;
        font-size: 0.8rem;
        letter-spacing: 0.2em;
      }
    }
  </style>
</head>
<body>
  <div class="screen">
    <div class="brand">
      <span>F</span>RIDAY
    </div>

    <div class="circle-wrapper" id="circleWrapper">
      <div class="ring"></div>
      <button class="circle-button" id="assistantButton" aria-label="Activate FRIDAY">
        <div class="circle-inner">
          <div class="mic-icon">🎙️</div>
        </div>
      </button>
    </div>
  </div>

  <!-- Iron Man style animated watermark -->
  <div class="watermark">Tauseef Ahmad</div>

  <script>
    const circleWrapper = document.getElementById("circleWrapper");
    const button = document.getElementById("assistantButton");

    // FRIDAY voice output
    function fridaySpeak(text) {
      if (!("speechSynthesis" in window)) return;
      const utter = new SpeechSynthesisUtterance(text);
      utter.rate = 1;
      utter.pitch = 1;
      utter.volume = 1;
      window.speechSynthesis.cancel();
      window.speechSynthesis.speak(utter);
    }

    // Handle spoken commands
    function handleCommand(raw) {
      const cmd = raw.toLowerCase().trim();
      console.log("You:", cmd);
      if (!cmd) return;

      if (cmd.startsWith("open ")) {
        const site = cmd.replace("open ", "").trim();
        openSite(site);
      } else if (cmd.startsWith("search ") || cmd.startsWith("google ")) {
        const q = cmd.replace(/^search|^google/, "").trim();
        doSearch(q);
      } else if (cmd.includes("time")) {
        const now = new Date();
        fridaySpeak("The time is " + now.toLocaleTimeString());
      } else if (cmd.includes("date")) {
        const now = new Date();
        fridaySpeak("Today is " + now.toLocaleDateString());
      } else if (cmd.includes("who are you")) {
        fridaySpeak("I am F.R.I.D.A.Y, your personal assistant. Online and ready.");
      } else if (
        cmd.includes("hello") ||
        cmd.includes("hi") ||
        cmd.includes("hey")
      ) {
        fridaySpeak("Hello, Tauseef. How can I assist you?");
      } else if (cmd.includes("joke")) {
        tellJoke();
      } else if (cmd.includes("stop") || cmd.includes("mute")) {
        window.speechSynthesis.cancel();
      } else {
        fridaySpeak("Command not recognized. Try open YouTube, search something, or ask for the time.");
      }
    }

    function openSite(site) {
      const map = {
        youtube: "https://www.youtube.com",
        google: "https://www.google.com",
        github: "https://github.com",
        instagram: "https://www.instagram.com",
        whatsapp: "https://web.whatsapp.com",
        twitter: "https://x.com",
        x: "https://x.com"
      };

      let url = map[site];

      if (!url && site.includes(".")) {
        url = "https://" + site;
      } else if (!url) {
        url = "https://www.google.com/search?q=" + encodeURIComponent(site + " website");
      }

      fridaySpeak("Opening " + site + ".");
      window.open(url, "_blank");
    }

    function doSearch(query) {
      if (!query) {
        fridaySpeak("What should I search for?");
        return;
      }
      fridaySpeak('Searching for "' + query + '".');
      const url = "https://www.google.com/search?q=" + encodeURIComponent(query);
      window.open(url, "_blank");
    }

    function tellJoke() {
      const jokes = [
        "Why do programmers prefer dark mode? Because light attracts bugs.",
        "There are only 10 types of people in the world: those who understand binary, and those who do not.",
        "I had a bug, so I added logging. Now I have two problems."
      ];
      const joke = jokes[Math.floor(Math.random() * jokes.length)];
      fridaySpeak(joke);
    }

    // Speech recognition
    let recognition;
    let listening = false;

    if ("webkitSpeechRecognition" in window || "SpeechRecognition" in window) {
      const SR = window.SpeechRecognition || window.webkitSpeechRecognition;
      recognition = new SR();
      recognition.lang = "en-US";
      recognition.continuous = false;
      recognition.interimResults = false;

      recognition.onstart = () => {
        listening = true;
        circleWrapper.classList.add("listening");
      };

      recognition.onend = () => {
        listening = false;
        circleWrapper.classList.remove("listening");
      };

      recognition.onerror = (e) => {
        listening = false;
        circleWrapper.classList.remove("listening");
        console.error("Speech error:", e.error);
      };

      recognition.onresult = (e) => {git add 
        const transcript = e.results[0][0].transcript;
        handleCommand(transcript);
      };
    } else {
      fridaySpeak("Voice recognition is not supported in this browser.");
    }

    function toggleListening() {
      if (!recognition) return;
      if (listening) recognition.stop();
      else recognition.start();
    }

    button.addEventListener("click", toggleListening);

    // Intro line
    fridaySpeak("F.R.I.D.A.Y online. Tap the core and speak your command, Tauseef.");
  </script>
</body>
</html>
