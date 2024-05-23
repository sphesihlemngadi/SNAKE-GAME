# SNAKE-GAME
A kids game
   // Function to draw food
    function drawFood() {
      ctx.fillStyle = "#f00";
      ctx.fillRect(food.x, food.y, 10, 10);
    }

    // Function to move the snake
    function moveSnake() {
      const head = { x: snake[0].x + dx, y: snake[0].y + dy };
      snake.unshift(head);

      if (head.x === food.x && head.y === food.y) {
        // If snake eats food, generate new food and do not remove snake tail
        generateFood();
      } else {
        // If snake does not eat food, remove tail segment
        snake.pop();
      }
    }

    // Function to generate new food
    function generateFood() {
      food.x = Math.floor(Math.random() * (canvas.width / 10)) * 10;
      food.y = Math.floor(Math.random() * (canvas.height / 10)) * 10;
    }

    // Function to handle key events
    function handleKey(e) {
      if (e.key === "ArrowUp" && dy === 0) {
        dx = 0;
        dy = -10;
      } else if (e.key === "ArrowDown" && dy === 0) {
        dx = 0;
        dy = 10;
      } else if (e.key === "ArrowLeft" && dx === 0) {
        dx = -10;
        dy = 0;
      } else if (e.key === "ArrowRight" && dx === 0) {
        dx = 10;
        dy = 0;
      }
    }

    // Function to check if the snake has collided with itself or the wall
    function checkCollision() {
      const head = snake[0];
      if (head.x < 0 || head.x >= canvas.width || head.y < 0 || head.y >= canvas.height) {
        return true;
      }
      for (let i = 1; i < snake.length; i++) {
        if (head.x === snake[i].x && head.y === snake[i].y) {
          return true;
        }
      }
      return false;
    }

    // Main game loop
    function gameLoop() {
      if (checkCollision()) {
        alert("Game Over! Your score: " + (snake.length - 1));
        window.location.reload();
      }

      ctx.clearRect(0, 0, canvas.width, canvas.height);
      moveSnake();
      drawSnake();
      drawFood();

      setTimeout(gameLoop, 100); // Repeat every 100ms
    }

    // Initialize game
    generateFood();
    gameLoop();

    // Event listener for keyboard input
    document.addEventListener("keydown", handleKey);
  </script>
</body>
</html>
