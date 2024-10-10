<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Corazones y Mensaje Final</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f4f4f4;
      margin: 0;
      padding: 0;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      height: 100vh;
      overflow: hidden;
    }
    .heart {
      font-size: 100px;
      cursor: pointer;
      color: red;
      transition: color 0.3s ease, transform 0.3s ease;
    }
    .message {
      font-size: 24px;
      margin-top: 20px;
      color: red;
      opacity: 1;
      transition: color 0.3s ease, opacity 0.3s ease;
    }
    .explosion {
      position: absolute;
      font-size: 30px;
      opacity: 0;
      animation: rise 3s ease-out forwards;
    }
    .final-message {
      display: none;
      font-size: 50px;
      color: pink;
      margin-top: 20px;
      text-align: center;
      animation: fadeIn 2s ease-in forwards;
    }
    @keyframes rise {
      0% {
        opacity: 1;
        transform: translateY(100vh) scale(1);
      }
      100% {
        opacity: 1;
        transform: translateY(-100vh) scale(1.5);
      }
    }
    @keyframes fadeIn {
      0% {
        opacity: 0;
      }
      100% {
        opacity: 1;
      }
    }
  </style>
</head>
<body>

  <div class="heart" id="heart">&#10084;</div> <!-- Corazón -->
  <div class="message" id="message">Me gustas</div> <!-- Mensaje -->
  <div class="final-message" id="finalMessage">Me Gustas Cachetes de Algodón</div> <!-- Mensaje final -->

  <script>
    // Colores del corazón y texto
    const colors = ['red', 'blue', 'green', 'turquoise', 'yellow'];
    let currentColorIndex = 0;
    let clickCount = 0;

    // Selección de los elementos
    const heart = document.getElementById('heart');
    const message = document.getElementById('message');
    const finalMessage = document.getElementById('finalMessage');

    // Función para generar corazones pequeños (explosión)
    function createHeartsExplosion() {
      for (let i = 0; i < 50; i++) {
        const smallHeart = document.createElement('div');
        smallHeart.classList.add('explosion');
        smallHeart.innerHTML = '&#10084;';
        smallHeart.style.left = `${Math.random() * 100}vw`;
        smallHeart.style.animationDelay = `${i * 0.1}s`; // Diferente tiempo de inicio para cada corazón
        document.body.appendChild(smallHeart);
      }

      // Mostrar el mensaje final después de que los corazones suban
      setTimeout(() => {
        finalMessage.style.display = 'block';
      }, 3000); // Aparece después de 3 segundos
    }

    // Evento de clic en el corazón
    heart.addEventListener('click', () => {
      // Cambiar el color del corazón y del texto
      currentColorIndex = (currentColorIndex + 1) % colors.length;
      heart.style.color = colors[currentColorIndex];
      message.style.color = colors[currentColorIndex];

      // Hacer que el mensaje aparezca/desaparezca de manera intermitente
      message.style.opacity = message.style.opacity == '1' ? '0' : '1';

      // Contar los clics
      clickCount++;

      // Si se ha clicado 10 veces, hacer que los corazones suban y mostrar el mensaje final
      if (clickCount >= 10) {
        heart.style.transform = 'scale(2)'; // Crecer el corazón

        setTimeout(() => {
          heart.style.display = 'none'; // Desaparecer el corazón
          createHeartsExplosion(); // Generar la explosión de corazones subiendo
        }, 500); // Después de 500 ms
      }
    });
  </script>

</body>
</html>
