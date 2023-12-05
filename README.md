# breakout-game
<!DOCTYPE html>
<html>
<head>
<style>
 canvas {
    border: 1px solid black;
 }
</style>
</head>
<body>

<canvas id="myCanvas" width="480" height="320"></canvas>

<script>
var canvas = document.getElementById("myCanvas");
var ctx = canvas.getContext("2d");
var ballRadius = 7;
var x = canvas.width/2;
var y = canvas.height-30;
var dx = 2;
var dy = -2;
var paddleHeight = 10;
var paddleWidth = 75;
var paddleX = (canvas.width-paddleWidth) / 2;
var rightPressed = false;
var leftPressed = false;

document.addEventListener("keydown", keyDownHandler, false);
document.addEventListener("keyup", keyUpHandler, false);

function keyDownHandler(e) {
 if(e.key == "Right" || e.key == "ArrowRight") {
    rightPressed = true;
 }
 else if(e.key == "Left" || e.key == "ArrowLeft") {
    leftPressed = true;
 }
}

function keyUpHandler(e) {
 if(e.key == "Right" || e.key == "ArrowRight") {
    rightPressed = false;
 }
 else if(e.key == "Left" || e.key == "ArrowLeft") {
    leftPressed = false;
 }
}

function drawBall() {
 ctx.beginPath();
 ctx.arc(x, y, ballRadius, 0, Math.PI*2);
 ctx.fillStyle = "black";
 ctx.fill();
 ctx.closePath();
}

function drawPaddle() {
 ctx.beginPath();
 ctx.rect(paddleX, canvas.height-paddleHeight, paddleWidth, paddleHeight);
 ctx.fillStyle = "black";
 ctx.fill();
 ctx.closePath();
}

function draw() {
 ctx.clearRect(0, 0, canvas.width, canvas.height);
 drawBall();
 drawPaddle();
 x += dx;
 y += dy;
  
 if(x - ballRadius < 0) {
    dx = -dx;
 }
  
 if(x + ballRadius > canvas.width) {
    dx = -dx;
 }
  
 if(y - ballRadius < 0) {
    dy = -dy;
 }
  
 if(y + ballRadius > canvas.height-paddleHeight) {
    if(x > paddleX && x < paddleX + paddleWidth) {
      dy = -dy;
    }
    else {
      alert("GAME OVER");
      document.location.reload();
    }
 }
  
 if(rightPressed && paddleX < canvas.width-paddleWidth) {
    paddleX += 7;
 }
  
 if(leftPressed && paddleX > 0) {
    paddleX -= 7;
 }
  
 requestAnimationFrame(draw);
}

draw();
</script>

</body>
</html>
