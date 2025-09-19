<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width,initial-scale=1.0">
  <title>Student Portfolio</title>
  <link rel="stylesheet" href="style.css">
  <script defer src="script.js"></script>

  <!-- EmailJS SDK -->
  <script type="text/javascript" src="https://cdn.emailjs.com/dist/email.min.js"></script>
  <script>
    (function(){
      emailjs.init("YOUR_PUBLIC_KEY"); // replace with your EmailJS Public Key
    })();
  </script>

  <style>
    /* General */
    body { font-family: Arial, sans-serif; margin:0; padding:0; }
    h2 { margin-bottom: 15px; }
    section { padding: 60px 20px; }

    /* Navbar */
    .navbar { display:flex; justify-content:space-between; align-items:center; padding:15px 30px; background:#333; color:#fff; }
    .navbar .logo { font-weight:bold; font-size:1.2rem; }
    .nav-links { list-style:none; display:flex; gap:20px; }
    .nav-links a { color:#fff; text-decoration:none; }
    .menu-toggle { display:none; cursor:pointer; }

    /* Hero */
    .hero { height:90vh; display:flex; align-items:center; justify-content:center; background:#f5f5f5; text-align:center; }
    .hero h1 span { color:#0077ff; }
    .btn { display:inline-block; margin-top:15px; padding:10px 20px; background:#0077ff; color:#fff; text-decoration:none; border-radius:5px; }

    /* About */
    .about-content { display:flex; align-items:center; gap:20px; max-width:800px; margin:auto; }
    .about-content img { width:150px; border-radius:50%; }

    /* Projects */
    .project-grid { display:grid; grid-template-columns:repeat(auto-fit,minmax(250px,1fr)); gap:20px; }
    .project-card { background:#fff; padding:20px; border-radius:10px; box-shadow:0 4px 8px rgba(0,0,0,0.1); text-align:center; }

    /* Quiz */
    .quiz-box {
      background: #fff; padding: 20px; border-radius: 10px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.1); max-width: 400px;
      margin:20px auto;
    }
    .quiz-box button {
      display:block; width:100%; margin:8px 0; padding:10px;
      border:none; border-radius:5px; background:#eee; cursor:pointer;
    }
    .quiz-box button.correct { background:#4caf50; color:#fff; }
    .quiz-box button.wrong { background:#e53935; color:#fff; }

    /* Blog */
    .container { max-width:800px; margin:20px auto; padding:10px; }
    .post {
      background:white; padding:15px; margin-bottom:20px;
      border-radius:8px; box-shadow:0 0 5px rgba(0,0,0,0.1);
    }
    .post h2 { margin:0 0 10px; }
    .post small { color:gray; font-size:12px; }

    /* Contact */
    form { display:flex; flex-direction:column; max-width:400px; margin:auto; gap:10px; }
    form input, form textarea { padding:10px; border-radius:5px; border:1px solid #ccc; }
    form button { padding:10px; background:#0077ff; color:#fff; border:none; border-radius:5px; cursor:pointer; }

    footer { text-align:center; padding:20px; background:#333; color:#fff; margin-top:40px; }
  </style>
</head>
<body>

  <!-- Navbar -->
  <header>
    <nav class="navbar">
      <div class="logo">MyPortfolio</div>
      <ul class="nav-links" id="nav-links">
        <li><a href="#home">Home</a></li>
        <li><a href="#about">About</a></li>
        <li><a href="#projects">Projects</a></li>
        <li><a href="#quiz">Quiz</a></li>
        <li><a href="#blog">Blog</a></li>
        <li><a href="#contact">Contact</a></li>
      </ul>
      <div class="menu-toggle" id="menu-toggle">&#9776;</div>
    </nav>
  </header>

  <!-- Hero -->
  <section id="home" class="hero">
    <div class="hero-content">
      <h1>Hello, I'm <span>MR SURYA PRAKASH</span></h1>
      <p>I am the student</p>
      <a href="#projects" class="btn">View My Work</a>
    </div>
  </section>

  <!-- About -->
  <section id="about" class="about">
    <h2>About Me</h2>
    <div class="about-content">
      <img src="IMG-20250919-WA0004.jpg" alt="Profile Photo">
      <p>
        I am a student enthusiastic about technology and design. I love building interactive,
        user-friendly web applications and exploring new tools in the tech world.
      </p>
    </div>
  </section>

  <!-- Projects -->
  <section id="projects" class="projects">
    <h2>My Projects</h2>
    <div class="project-grid">
      <div class="project-card">
        <h3>Project 1</h3>
        <p>A simple responsive website.</p>
      </div>
      <div class="project-card">
        <h3>Project 2</h3>
        <p>JavaScript-based quiz app.</p>
      </div>
      <div class="project-card">
        <h3>Project 3</h3>
        <p>Personal blog with CMS.</p>
      </div>
    </div>
  </section>

  <!-- Quiz -->
  <section id="quiz">
    <h2>Random Quiz</h2>
    <div class="quiz-box">
      <h2 id="question">Question will appear here</h2>
      <div id="options"></div>
      <p id="result"></p>
    </div>
  </section>

  <!-- Blog -->
  <section id="blog">
    <h2>My Blog</h2>
    <div class="container" id="postsContainer"></div>
  </section>

  <!-- Contact -->
  <section id="contact" class="contact">
    <h2>Contact Me</h2>
    <form id="contact-form">
      <input type="text" id="name" name="user_name" placeholder="Your Name" required>
      <input type="email" id="email" name="user_email" placeholder="Your Email" required>
      <textarea id="message" name="message" placeholder="Your Message" required></textarea>
      <button type="submit">Send</button>
    </form>
    <p id="form-status"></p>
  </section>

  <!-- Footer -->
  <footer>
    <p>&copy; 2025 MR SURYA PRAKASH | All rights reserved</p>
  </footer>

  <script>
    // Quiz Questions
    const questions = [
      {q:"What is the capital of India?", options:["Mumbai","Delhi","Chennai","Kolkata"], answer:"Delhi"},
      {q:"Which is the largest planet?", options:["Earth","Mars","Jupiter","Saturn"], answer:"Jupiter"},
      {q:"Who wrote Ramayana?", options:["Valmiki","Vyasa","Tulsidas","Kalidasa"], answer:"Valmiki"},
      {q:"Which gas do humans breathe in?", options:["Carbon Dioxide","Oxygen","Nitrogen","Helium"], answer:"Oxygen"},
      {q:"What is 5 × 6?", options:["25","30","35","20"], answer:"30"}
    ];
    const randomQuestion = questions[Math.floor(Math.random()*questions.length)];
    document.getElementById("question").textContent = randomQuestion.q;
    const optionsDiv = document.getElementById("options");
    randomQuestion.options.forEach(opt => {
      const btn = document.createElement("button");
      btn.textContent = opt;
      btn.onclick = () => {
        if(opt === randomQuestion.answer){
          btn.classList.add("correct");
          document.getElementById("result").textContent = "✅ Correct!";
        } else {
          btn.classList.add("wrong");
          document.getElementById("result").textContent = "❌ Wrong! Correct answer: " + randomQuestion.answer;
        }
        Array.from(optionsDiv.children).forEach(b => b.disabled = true);
      };
      optionsDiv.appendChild(btn);
    });

    // Blog Posts
    function loadPosts() {
      const postsContainer = document.getElementById("postsContainer");
      const posts = JSON.parse(localStorage.getItem("blogPosts")) || [
        {title:"Welcome Post", content:"This is my first blog post!", date:new Date()}
      ];
      postsContainer.innerHTML = "";
      posts.reverse().forEach(post => {
        const postEl = document.createElement("div");
        postEl.classList.add("post");
        postEl.innerHTML = `
          <h2>${post.title}</h2>
          <small>${new Date(post.date).toLocaleString()}</small>
          <p>${post.content}</p>
        `;
        postsContainer.appendChild(postEl);
      });
    }
    loadPosts();
  </script>
</body>
</html>
