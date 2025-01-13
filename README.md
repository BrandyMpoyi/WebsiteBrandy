<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Brandy's Website</title>
  <style>
    * { box-sizing: border-box; }
    body { 
      font-family: 'Lato', Arial, sans-serif; 
      padding: 10px; 
      background: linear-gradient(135deg, #000, #333); 
      color: #fff;
    }
    .header { 
      padding: 40px; 
      text-align: center; 
      background: linear-gradient(135deg, #1c1c1c, #4a4a4a); 
      color: #fff; 
      border-radius: 8px;
    }
    .header h1 { font-size: 50px; margin-bottom: 10px; }
    .header p { font-size: 20px; }
    .topnav { 
      overflow: hidden; 
      background-color: #2c3e50; 
      border-radius: 8px;
    }
    .topnav a { 
      float: left; 
      display: block; 
      color: #f2f2f2; 
      text-align: center; 
      padding: 14px 16px; 
      text-decoration: none;
    }
    .topnav a:hover { background-color: #ddd; color: black; }
    .leftcolumn { float: left; width: 75%; }
    .rightcolumn { float: left; width: 25%; background-color: #f9f9f9; padding-left: 20px; border-radius: 8px; }
    .card { 
      background-color: #2b2b2b; 
      color: #f1f1f1; 
      padding: 20px; 
      margin-top: 20px; 
      border-radius: 8px;
    }
    .card h2 { color: #e6e6e6; }
    .about-img img { width: 100%; border-radius: 8px; }
    .footer { padding: 20px; text-align: center; background: #2c3e50; color: white; margin-top: 20px; border-radius: 8px; }
    input { padding: 10px; width: 100%; margin: 10px 0; border-radius: 5px; border: 1px solid #ccc; }
    .password-checker { margin-top: 20px; }
    canvas { background-color: #f1f1f1; display: block; margin: 0 auto; border: 1px solid #ddd; }
    @media screen and (max-width: 800px) { .leftcolumn, .rightcolumn { width: 100%; padding: 0; } }
    @media screen and (max-width: 400px) { .topnav a { float: none; width: 100%; } }
  </style>
</head>
<body>

<div class="header">
  <h1>Welcome to Brandy's World</h1>
  <p>Professional, Creative, and Passionate</p>
</div>

<div class="topnav">
  <a href="#">Home</a>
  <a href="#">About Me</a>
  <a href="#">Experience</a>
  <a href="#" style="float:right">Contact</a>
</div>

<div class="row">
  <!-- Left Column -->
  <div class="leftcolumn">
    <div class="card">
      <h2>Professional Journey</h2>
      <h5>My story, latest update Sep 2023</h5>
      <!-- Embed professional video -->
      <iframe width="100%" height="315" src="https://www.youtube.com/embed/oD5mKfO_4dY?autoplay=1" title="YouTube video" frameborder="0" allowfullscreen></iframe>
      <p>Discover how I navigate the professional world, bringing innovation and passion to my work. Watch the video to learn more about my journey.</p>
    </div>

    <div class="card">
      <h2>Skills and Expertise</h2>
      <p>Brandy's top skills:</p>
      <ul>
        <li>Team Leadership</li>
        <li>Strategic Planning</li>
        <li>Client Relationship Management</li>
        <li>Creative Problem Solving</li>
        <li>Project Management</li>
      </ul>
    </div>

    <div class="card">
      <h2>Snake Game</h2>
      <p>Play the Snake Game below:</p>
      <canvas id="gameArea" width="400" height="400"></canvas>
    </div>

    <div class="card">
      <h2>Password Security Checker</h2>
      <p>I developed a password strength checker to ensure secure, strong passwords. Test your password below:</p>
      <div class="password-checker">
        <input type="password" id="password" placeholder="Enter your password">
        <p id="password-feedback"></p>
      </div>
    </div>
  </div>

  <!-- Right Column -->
  <div class="rightcolumn">
    <div class="card">
      <h2>About Me</h2>
      <div class="about-img">
        <img src="https://imgur.com/iHSlXHO.jpg" alt="Brandy Image">
      </div>
      <p>Hello! I'm Brandy, a passionate professional with a flair for creative problem-solving and leadership. I have experience as a Twitch Live Streamer and started gaming content creation at 11. I also played piano in Year 7. My goal is to innovate and make a difference in every project I undertake.</p>
    </div>

    <div class="card">
      <h3>Contact Me</h3>
      <p>Phone: 07903255678</p>
      <p>Email: mpoyibrandy@gmail.com</p>
      <p>LinkedIn: <a href="https://www.linkedin.com/in/brandy-mpoyi-696a182a1/" target="_blank">LinkedIn Profile</a></p>
    </div>
  </div>
</div>

<div class="footer">
  <h2>Let's Connect!</h2>
  <p>Follow me on social media or get in touch through email for any collaborations or opportunities.</p>
</div>

<script>
  // Snake Game
  let canvas = document.getElementById("gameArea");
  let ctx = canvas.getContext("2d");

  const box = 20;
  let snake = [];
  snake[0] = {x: 9 * box, y: 10 * box};

  let food = {
    x: Math.floor(Math.random() * 19 + 1) * box,
    y: Math.floor(Math.random() * 19 + 1) * box
  };

  let d;
  document.addEventListener("keydown", direction);

  function direction(event) {
    if(event.keyCode == 37 && d != "RIGHT") d = "LEFT";
    else if(event.keyCode == 38 && d != "DOWN") d = "UP";
    else if(event.keyCode == 39 && d != "LEFT") d = "RIGHT";
    else if(event.keyCode == 40 && d != "UP") d = "DOWN";
    // Prevent page from scrolling when playing the game
    event.preventDefault();
  }

  function collision(newHead, snake) {
    for(let i = 0; i < snake.length; i++) {
      if(newHead.x == snake[i].x && newHead.y == snake[i].y) {
        return true;
      }
    }
    return false;
  }

  function draw() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    for(let i = 0; i < snake.length; i++) {
      ctx.fillStyle = i == 0 ? "green" : "white";
      ctx.fillRect(snake[i].x, snake[i].y, box, box);
      ctx.strokeStyle = "red";
      ctx.strokeRect(snake[i].x, snake[i].y, box, box);
    }

    ctx.fillStyle = "red";
    ctx.fillRect(food.x, food.y, box, box);

    let snakeX = snake[0].x;
    let snakeY = snake[0].y;

    if(d == "LEFT") snakeX -= box;
    if(d == "UP") snakeY -= box;
    if(d == "RIGHT") snakeX += box;
    if(d == "DOWN") snakeY += box;

    if(snakeX == food.x && snakeY == food.y) {
      food = {
        x: Math.floor(Math.random() * 19 + 1) * box,
        y: Math.floor(Math.random() * 19 + 1) * box
      };
    } else {
      snake.pop();
    }

    let newHead = {x: snakeX, y: snakeY};

    if(snakeX < 0 || snakeY < 0 || snakeX >= canvas.width || snakeY >= canvas.height || collision(newHead, snake)) {
      alert('Game Over!');
      clearInterval(game);
    }

    snake.unshift(newHead);
  }

  let game = setInterval(draw, 100);
</script>

</body>
</html>
