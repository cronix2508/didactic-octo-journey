<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Cumpleaños Profesora Fedra</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background: linear-gradient(45deg, #000000, #FFD700, #FFFFFF);
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            perspective: 1000px;
            overflow: hidden;
        }
        .birthday-card {
            width: 500px;
            background: rgba(255, 255, 255, 0.2);
            border-radius: 20px;
            backdrop-filter: blur(10px);
            box-shadow: 0 15px 25px rgba(0, 0, 0, 0.1);
            padding: 30px;
            transform-style: preserve-3d;
            transition: all 1s ease;
        }
        .birthday-card:hover {
            transform: rotateY(20deg) scale(1.05);
        }
        .image-container {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-bottom: 20px;
        }
        .profile-image {
            width: 150px;
            height: 150px;
            border-radius: 50%;
            object-fit: cover;
            border: 5px solid gold;
            transition: all 0.6s ease;
        }
        .profile-image:hover {
            transform: scale(1.1) rotate(360deg);
        }
        .birthday-message {
            text-align: center;
            color: #333;
            font-size: 1.2em; /* Aumentar tamaño de fuente */
            line-height: 1.6;
            text-shadow: 2px 2px 4px rgba(255,215,0,0.5);
        }
        #confetti-canvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            pointer-events: none;
        }
        #reset-confetti {
            margin-top: 20px; 
            padding: 10px 20px; 
            font-size: 1em; 
            background-color: #FFD700; 
            border: none; 
            border-radius: 5px; 
            cursor: pointer;
            transition: background-color 0.3s; /* Agregar transición */
        }
        #reset-confetti:hover {
            background-color: #FFC300; /* Cambiar color al pasar el mouse */
        }
    </style>
</head>
<body>
    <div class="birthday-card">
        <div class="birthday-message bold-black">
            ¡ 🎉Feliz CUMPLEAÑOS PROFESORA FEDRA 🎉! <br><br>
        </div>
        <div class="image-container">
            <img src="image1.png" alt="Imagen de la profesora 1" class="profile-image">
            <img src="image2.png" alt="Imagen de la profesora 2" class="profile-image">
        </div>
        <div class="birthday-message">
            En este día tan especial, queremos expresarte nuestra más profunda gratitud. 
            Eres más que una profesora, eres un faro de inspiración y sabiduría. 
            Tu dedicación, pasión y compromiso han transformado nuestras vidas. 
            Cada lección que nos has enseñado va mucho más allá de los libros. 
            Eres un ejemplo de excelencia, humanidad y amor por la educación. 
            Gracias por creer en nosotros cuando ni nosotros mismos lo hacíamos. 
            Eres la mejor profesora de nuestra promoción y un regalo para la educación. 
             ¡Feliz cumpleaños, Profesora Fedra! Que este día sea tan especial como tú! 🎂 🎉
        </div>
        <button id="reset-confetti">Reiniciar Confetti</button>
    </div>
    <canvas id="confetti-canvas"></canvas>

    <script>
        // Funcionalidad para cargar imágenes
        document.addEventListener('DOMContentLoaded', () => {
            const images = [
                document.querySelector('.profile-image:nth-of-type(1)'),
                document.querySelector('.profile-image:nth-of-type(2)')
            ];

            images.forEach(img => {
                img.addEventListener('click', () => {
                    const input = document.createElement('input');
                    input.type = 'file';
                    input.accept = 'image/*';
                    input.onchange = (e) => {
                        const file = e.target.files[0];
                        const reader = new FileReader();
                        reader.onload = (event) => {
                            img.src = event.target.result;
                        };
                        reader.readAsDataURL(file);
                    };
                    input.click();
                });
            });
        });

        // Confetti Animation
        let confettiAnimation;

        function createConfetti() {
            const canvas = document.getElementById('confetti-canvas');
            const ctx = canvas.getContext('2d');
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;

            const confetti = [];
            const colors = ['#FFD700', '#000000', '#FFFFFF'];

            function createConfettiPiece() {
                return {
                    x: Math.random() * canvas.width,
                    y: -10,
                    size: Math.random() * 10 + 5,
                    speedY: Math.random() * 5 + 2,
                    speedX: Math.random() * 4 - 2,
                    color: colors[Math.floor(Math.random() * colors.length)]
                };
            }

            function drawConfetti() {
                ctx.clearRect(0, 0, canvas.width, canvas.height);

                for (let i = 0; i < confetti.length; i++) {
                    const piece = confetti[i];
                    ctx.fillStyle = piece.color;
                    ctx.fillRect(piece.x, piece.y, piece.size, piece.size);
                    
                    piece.y += piece.speedY;
                    piece.x += piece.speedX;

                    if (piece.y > canvas.height) {
                        confetti.splice(i, 1);
                        i--;
                    }
                }

                if (confetti.length < 100) {
                    confetti.push(createConfettiPiece());
                }

                requestAnimationFrame(drawConfetti);
            }

            drawConfetti();
        }

        createConfetti();
    </script>
</body>
</html>
