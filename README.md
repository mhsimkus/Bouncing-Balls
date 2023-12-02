# Bouncing-Balls
code for bouncing balls
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        canvas {
            border: 1px solid #000;
        }
    </style>
    <title>Bouncing Balls</title>
</head>
<body>
    <canvas id="bouncingBallsCanvas" width="800" height="600"></canvas>

    <script>
        const canvas = document.getElementById('bouncingBallsCanvas');
        const ctx = canvas.getContext('2d');

        // Ball class
        class Ball {
            constructor(x, y, radius, color, speedX, speedY) {
                this.x = x;
                this.y = y;
                this.radius = radius;
                this.color = color;
                this.speedX = speedX;
                this.speedY = speedY;
            }

            move() {
                this.x += this.speedX;
                this.y += this.speedY;

                // Bounce off walls
                if (this.x - this.radius < 0 || this.x + this.radius > canvas.width) {
                    this.speedX *= -1;
                }

                if (this.y - this.radius < 0 || this.y + this.radius > canvas.height) {
                    this.speedY *= -1;
                }
            }

            draw() {
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2);
                ctx.fillStyle = this.color;
                ctx.fill();
                ctx.closePath();
            }
        }

        // Create balls
        const numBalls = 5;
        const balls = [];

        for (let i = 0; i < numBalls; i++) {
            const ball = new Ball(
                Math.random() * (canvas.width - 2 * 30) + 30,
                Math.random() * (canvas.height - 2 * 30) + 30,
                Math.random() * (20 - 10) + 10,
                `rgb(${Math.random() * 255},${Math.random() * 255},${Math.random() * 255})`,
                (Math.random() - 0.5) * 5,
                (Math.random() - 0.5) * 5
            );
            balls.push(ball);
        }

        // Animation loop
        function animate() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);

            for (const ball of balls) {
                ball.move();
                ball.draw();
            }

            requestAnimationFrame(animate);
        }

        animate();
    </script>
</body>
</html>
