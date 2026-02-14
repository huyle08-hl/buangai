<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Happy Valentine ❤️ - Huy Yêu Em</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Arial', sans-serif;
            background: #000;
            min-height: 100vh;
            overflow: hidden;
            position: relative;
            touch-action: none;
        }

        canvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            cursor: grab;
        }

        canvas:active {
            cursor: grabbing;
        }

        .content-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 10;
        }

        .slide {
            position: absolute;
            right: 5%;
            top: 50%;
            transform: translateY(-50%) translateX(100px);
            display: flex;
            flex-direction: column;
            align-items: flex-start;
            opacity: 0;
            transition: all 1s ease;
        }

        .slide.active {
            opacity: 1;
            transform: translateY(-50%) translateX(0);
        }

        .slide-title {
            font-size: 2em;
            font-weight: bold;
            color: #fff;
            text-shadow: 0 0 20px rgba(255, 105, 180, 0.8),
                         0 0 40px rgba(255, 105, 180, 0.6);
            margin-bottom: 20px;
            text-align: left;
        }

        .slide-message {
            font-size: 1.2em;
            color: #fff;
            text-shadow: 0 2px 10px rgba(0, 0, 0, 0.8);
            text-align: left;
            margin-bottom: 30px;
            line-height: 1.8;
            max-width: 400px;
        }

        .slide-photo {
            width: 280px;
            height: 320px;
            object-fit: cover;
            border-radius: 15px;
            border: 4px solid rgba(255, 105, 180, 0.6);
            box-shadow: 0 0 30px rgba(255, 105, 180, 0.8),
                        0 0 60px rgba(255, 105, 180, 0.4);
        }

        .replay-btn {
            position: fixed;
            bottom: 30px;
            left: 50%;
            transform: translateX(-50%);
            padding: 12px 40px;
            font-size: 1.2em;
            font-weight: bold;
            color: white;
            background: rgba(139, 0, 139, 0.7);
            border: 2px solid rgba(255, 105, 180, 0.8);
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.3s;
            letter-spacing: 2px;
            box-shadow: 0 0 20px rgba(255, 105, 180, 0.5);
            z-index: 20;
            pointer-events: all;
        }

        .replay-btn:hover {
            background: rgba(255, 105, 180, 0.8);
            transform: translateX(-50%) scale(1.05);
        }

        .instruction {
            position: fixed;
            bottom: 90px;
            left: 50%;
            transform: translateX(-50%);
            color: rgba(255, 255, 255, 0.6);
            font-size: 0.9em;
            text-align: center;
            z-index: 20;
            pointer-events: none;
        }

        .progress-dots {
            position: fixed;
            top: 30px;
            left: 50%;
            transform: translateX(-50%);
            display: flex;
            gap: 10px;
            z-index: 20;
        }

        .dot {
            width: 12px;
            height: 12px;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.3);
            transition: all 0.3s;
        }

        .dot.active {
            background: rgba(255, 105, 180, 1);
            box-shadow: 0 0 10px rgba(255, 105, 180, 0.8);
        }

        @media (max-width: 768px) {
            .slide {
                right: 50%;
                transform: translateY(-50%) translateX(50%) scale(0.9);
                align-items: center;
            }
            .slide.active {
                transform: translateY(-50%) translateX(50%) scale(1);
            }
            .slide-title { 
                font-size: 1.5em;
                text-align: center;
            }
            .slide-message { 
                font-size: 1em;
                text-align: center;
                max-width: 280px;
            }
            .slide-photo { 
                width: 180px;
                height: 240px;
            }
        }
    </style>
</head>
<body>
    <canvas id="canvas"></canvas>

    <div class="progress-dots" id="progressDots">
        <div class="dot"></div>
        <div class="dot"></div>
        <div class="dot"></div>
        <div class="dot"></div>
        <div class="dot"></div>
    </div>

    <div class="content-overlay" id="contentOverlay">
        <!-- Slide 1 -->
        <div class="slide" id="slide1">
            <div class="slide-title">Happy Valentine ❤️</div>
            <div class="slide-message">Em bé An Quỳnh của tôi ❤️</div>
            <img src="vlt1.jpg" 
                 alt="Photo 1" class="slide-photo">
        </div>

        <!-- Slide 2 -->
        <div class="slide" id="slide2">
            <div class="slide-title">Cảm ơn em ✨</div>
            <div class="slide-message">Vì đã đến bên anh<br>và làm cuộc đời anh trọn vẹn hơn</div>
            <img src="vlt2.jpg" 
                 alt="Photo 2" class="slide-photo">
        </div>

        <!-- Slide 3 -->
        <div class="slide" id="slide3">
            <div class="slide-title">Mỗi ngày bên em 💕</div>
            <div class="slide-message">Là một món quà quý giá<br>mà anh không bao giờ ngừng trân trọng</div>
            <img src="vlt3.jpg" 
                 alt="Photo 3" class="slide-photo">
        </div>

        <!-- Slide 4 -->
        <div class="slide" id="slide4">
            <div class="slide-title">Em là tất cả 🌟</div>
            <div class="slide-message">Anh yêu em không chỉ vì em xinh<br>Mà vì em là ánh sáng trong đời anh</div>
            <img src="vlt4.jpg" 
                 alt="Photo 4" class="slide-photo">
        </div>

        <!-- Slide 5 -->
        <div class="slide" id="slide5">
            <div class="slide-title">Mãi mãi yêu em 💖</div>
            <div class="slide-message">Từ hôm nay đến mãi về sau<br>Anh sẽ luôn ở đây, bên em</div>
            <img src="vlt6.jpg" 
                 alt="Photo 5" class="slide-photo">
        </div>
    </div>

    <div class="instruction">Kéo chuột để xoay trái tim 💕</div>
    <button class="replay-btn" onclick="replaySequence()">REPLAY</button>

    <script>
        const canvas = document.getElementById('canvas');
        const ctx = canvas.getContext('2d');

        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;

        // Mouse/Touch interaction
        let mouseX = 0;
        let mouseY = 0;
        let isDragging = false;
        let rotationX = 0;
        let rotationY = 0;
        let targetRotationX = 0;
        let targetRotationY = 0;

        // Particles for the 3D heart
        const heartParticles = [];
        const floatingHearts = [];
        const backgroundParticles = [];

        // Slide management
        let currentSlide = 0;
        let slideInterval;
        const totalSlides = 5;
        const slideDuration = 4000; // 4 seconds per slide

        class BackgroundParticle {
            constructor() {
                this.x = Math.random() * canvas.width;
                this.y = Math.random() * canvas.height;
                this.size = Math.random() * 2 + 1;
                this.speedY = Math.random() * 0.3 - 0.15;
                this.speedX = Math.random() * 0.3 - 0.15;
                this.opacity = Math.random() * 0.5 + 0.3;
            }

            update() {
                this.y += this.speedY;
                this.x += this.speedX;
                if (this.y > canvas.height) this.y = 0;
                if (this.y < 0) this.y = canvas.height;
                if (this.x > canvas.width) this.x = 0;
                if (this.x < 0) this.x = canvas.width;
            }

            draw() {
                ctx.fillStyle = `rgba(255, 255, 255, ${this.opacity})`;
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
                ctx.fill();
            }
        }

        class FloatingHeart {
            constructor() {
                this.x = Math.random() * canvas.width;
                this.y = Math.random() * canvas.height;
                this.size = Math.random() * 30 + 20;
                this.speedY = Math.random() * 0.5 - 0.25;
                this.speedX = Math.random() * 0.5 - 0.25;
                this.opacity = Math.random() * 0.4 + 0.2;
            }

            update() {
                this.y += this.speedY;
                this.x += this.speedX;
                if (this.y > canvas.height + 50) this.y = -50;
                if (this.y < -50) this.y = canvas.height + 50;
                if (this.x > canvas.width + 50) this.x = -50;
                if (this.x < -50) this.x = canvas.width + 50;
            }

            draw() {
                ctx.save();
                ctx.globalAlpha = this.opacity;
                ctx.font = `${this.size}px Arial`;
                ctx.fillText('❤', this.x, this.y);
                ctx.restore();
            }
        }

        class Particle3D {
            constructor(x, y, z) {
                this.x = x;
                this.y = y;
                this.z = z;
                this.size = Math.random() * 3 + 2;
                this.color = Math.random() > 0.3 ? 
                    `rgb(255, ${105 + Math.random() * 50}, ${180 + Math.random() * 50})` :
                    `rgb(255, ${182 + Math.random() * 30}, ${193 + Math.random() * 30})`;
            }

            project() {
                // Rotate around Y axis
                const cosY = Math.cos(rotationY);
                const sinY = Math.sin(rotationY);
                const x1 = this.x * cosY - this.z * sinY;
                const z1 = this.x * sinY + this.z * cosY;

                // Rotate around X axis
                const cosX = Math.cos(rotationX);
                const sinX = Math.sin(rotationX);
                const y1 = this.y * cosX - z1 * sinX;
                const z2 = this.y * sinX + z1 * cosX;

                // Perspective projection
                const scale = 300 / (300 + z2);
                const x2D = x1 * scale + canvas.width / 2;
                const y2D = y1 * scale + canvas.height / 2;

                return { x: x2D, y: y2D, scale: scale, z: z2 };
            }

            draw() {
                const projected = this.project();
                if (projected.z < -200) return;

                ctx.fillStyle = this.color;
                ctx.globalAlpha = Math.max(0.3, Math.min(1, projected.scale));
                ctx.beginPath();
                ctx.arc(projected.x, projected.y, this.size * projected.scale, 0, Math.PI * 2);
                ctx.fill();
                ctx.globalAlpha = 1;
            }
        }

        // Create 3D heart shape
        function createHeart3D() {
            heartParticles.length = 0;
            const scale = 8;
            const density = 0.08;

            for (let t = 0; t < Math.PI * 2; t += density) {
                const x = scale * 16 * Math.pow(Math.sin(t), 3);
                const y = -scale * (13 * Math.cos(t) - 5 * Math.cos(2 * t) - 2 * Math.cos(3 * t) - Math.cos(4 * t));
                
                for (let z = -30; z <= 30; z += 8) {
                    for (let i = 0; i < 3; i++) {
                        const px = x + (Math.random() - 0.5) * 10;
                        const py = y + (Math.random() - 0.5) * 10;
                        const pz = z + (Math.random() - 0.5) * 10;
                        heartParticles.push(new Particle3D(px, py, pz));
                    }
                }
            }
        }

        // Initialize
        function init() {
            backgroundParticles.length = 0;
            floatingHearts.length = 0;

            for (let i = 0; i < 150; i++) {
                backgroundParticles.push(new BackgroundParticle());
            }

            for (let i = 0; i < 15; i++) {
                floatingHearts.push(new FloatingHeart());
            }

            createHeart3D();
        }

        // Slide management
        function showSlide(index) {
            // Hide all slides
            document.querySelectorAll('.slide').forEach(slide => {
                slide.classList.remove('active');
            });

            // Update progress dots
            document.querySelectorAll('.dot').forEach((dot, i) => {
                if (i === index) {
                    dot.classList.add('active');
                } else {
                    dot.classList.remove('active');
                }
            });

            // Show current slide
            const slideElement = document.getElementById(`slide${index + 1}`);
            if (slideElement) {
                slideElement.classList.add('active');
            }
        }

        function nextSlide() {
            currentSlide++;
            if (currentSlide >= totalSlides) {
                currentSlide = 0;
            }
            showSlide(currentSlide);
        }

        function startSlideShow() {
            currentSlide = 0;
            showSlide(currentSlide);
            
            if (slideInterval) {
                clearInterval(slideInterval);
            }
            
            slideInterval = setInterval(nextSlide, slideDuration);
        }

        function replaySequence() {
            startSlideShow();
        }

        // Mouse/Touch events
        canvas.addEventListener('mousedown', (e) => {
            isDragging = true;
            mouseX = e.clientX;
            mouseY = e.clientY;
        });

        canvas.addEventListener('mousemove', (e) => {
            if (isDragging) {
                const deltaX = e.clientX - mouseX;
                const deltaY = e.clientY - mouseY;
                targetRotationY += deltaX * 0.01;
                targetRotationX += deltaY * 0.01;
                mouseX = e.clientX;
                mouseY = e.clientY;
            }
        });

        canvas.addEventListener('mouseup', () => {
            isDragging = false;
        });

        canvas.addEventListener('mouseleave', () => {
            isDragging = false;
        });

        // Touch events
        canvas.addEventListener('touchstart', (e) => {
            isDragging = true;
            mouseX = e.touches[0].clientX;
            mouseY = e.touches[0].clientY;
        });

        canvas.addEventListener('touchmove', (e) => {
            if (isDragging) {
                const deltaX = e.touches[0].clientX - mouseX;
                const deltaY = e.touches[0].clientY - mouseY;
                targetRotationY += deltaX * 0.01;
                targetRotationX += deltaY * 0.01;
                mouseX = e.touches[0].clientX;
                mouseY = e.touches[0].clientY;
            }
        });

        canvas.addEventListener('touchend', () => {
            isDragging = false;
        });

        // Animation loop
        function animate() {
            ctx.fillStyle = 'rgba(0, 0, 0, 0.1)';
            ctx.fillRect(0, 0, canvas.width, canvas.height);

            // Smooth rotation
            rotationX += (targetRotationX - rotationX) * 0.1;
            rotationY += (targetRotationY - rotationY) * 0.1;

            // Auto-rotate if not dragging
            if (!isDragging) {
                targetRotationY += 0.003;
            }

            // Draw background particles
            backgroundParticles.forEach(p => {
                p.update();
                p.draw();
            });

            // Draw floating hearts
            floatingHearts.forEach(h => {
                h.update();
                h.draw();
            });

            // Sort particles by depth for correct rendering
            heartParticles.sort((a, b) => {
                const projA = a.project();
                const projB = b.project();
                return projB.z - projA.z;
            });

            // Draw 3D heart
            heartParticles.forEach(p => {
                p.draw();
            });

            requestAnimationFrame(animate);
        }

        // Resize handler
        window.addEventListener('resize', () => {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        });

        // Start
        init();
        animate();
        startSlideShow();
    </script>
</body>
</html>


