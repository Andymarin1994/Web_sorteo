# Web_sorteo
Codigo de html, css, java script, para realizar un sorteo, cuenta con un contador sobre registro de personas. version 1.0
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sorteo TV 55 Pulgadas - Droguería Daniand</title>
    <style>
        /* Estilos generales del cuerpo del documento */
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f0f0; /* Color de fondo */
            color: #333; /* Color de texto principal */
            margin: 0; /* Elimina márgenes */
            padding: 0; /* Elimina relleno */
            display: flex; /* Flexbox para centrar contenido vertical y horizontalmente */
            justify-content: center;
            align-items: center;
            height: 100vh; /* Tamaño completo de la pantalla */
        }

        /* Estilos del contenedor principal */
        .container {
            text-align: center; /* Texto centrado */
            background-color: #fff; /* Fondo blanco */
            padding: 30px; /* Relleno interno */
            border-radius: 10px; /* Bordes redondeados */
            box-shadow: 0 0 20px rgba(0, 0, 0, 0.1); /* Sombra */
            max-width: 600px; /* Ancho máximo */
            width: 90%; /* Ancho del contenedor */
        }

        /* Estilos del título principal */
        h1 {
            color: #e91e63; /* Color del título */
            font-size: 2.5em; /* Tamaño de fuente grande */
            margin-bottom: 20px; /* Margen inferior */
        }

        /* Estilos del párrafo */
        p {
            font-size: 1.2em; /* Tamaño de fuente */
            line-height: 1.6; /* Espaciado entre líneas */
            margin-bottom: 20px; /* Margen inferior */
        }

        /* Estilos del botón */
        .button {
            display: inline-block; /* Mostrar como bloque en línea */
            background-color: #e91e63; /* Color de fondo del botón */
            color: #fff; /* Color de texto del botón */
            font-size: 1.2em; /* Tamaño de fuente */
            padding: 10px 20px; /* Relleno interno */
            text-decoration: none; /* Sin subrayado */
            border-radius: 5px; /* Bordes redondeados */
            transition: background-color 0.3s ease; /* Transición suave */
        }

        /* Estilos del botón al pasar el mouse */
        .button:hover {
            background-color: #c2185b; /* Color de fondo al pasar el mouse */
        }
    </style>
</head>
<body>
    <!-- Contenedor principal de la página -->
    <div class="container">
        <!-- Título principal -->
        <h1>GRAN SORTEO TELEVISOR DE 55 PULGADAS</h1>
        <!-- Párrafo de introducción -->
        <p>Bienvenidos al sorteo del televisior de 55 pulgadas ofrecido por Droguería Daniand. Participa para tener la oportunidad de ganar este increíble premio.</p>
        <!-- Botón de participación -->
        <a href="inscripciones.html" class="button">¡Participa Ahora!</a>
    </div>
</body>
</html> 
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Registro de Participantes - Sorteo TV 55 Pulgadas</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f0f0;
            color: #333;
            margin: 0;
            padding: 20px;
        }

        .container {
            max-width: 600px;
            margin: 0 auto;
            background-color: #fff;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
        }

        h1 {
            color: #e91e63;
            text-align: center;
        }

        form {
            display: flex;
            flex-direction: column;
        }

        label {
            margin-bottom: 10px;
        }

        input[type="text"],
        input[type="email"],
        input[type="tel"] {
            padding: 10px;
            margin-bottom: 15px;
            border: 1px solid #ccc;
            border-radius: 5px;
            font-size: 1em;
        }

        .registrarse-btn {
            background-color: #e91e63;
            color: #fff;
            padding: 12px 20px;
            border: none;
            border-radius: 5px;
            font-size: 1.2em;
            text-align: center;
            cursor: pointer;
            transition: background-color 0.3s ease;
            margin-top: 20px;
        }

        .registrarse-btn:hover {
            background-color: #c2185b;
        }

        .counter {
            text-align: center;
            margin-top: 20px;
            font-size: 1.2em;
            color: #777;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Registro de Participantes</h1>
        <p>Completa el formulario para participar en el sorteo de una TV de 55 Pulgadas.</p>
        <form id="registration-form">
            <label for="nombre">Nombre:</label>
            <input type="text" id="nombre" name="nombre" required>

            <label for="email">Email:</label>
            <input type="email" id="email" name="email" required>

            <label for="telefono">Teléfono:</label>
            <input type="tel" id="telefono" name="telefono" required>

            <button type="submit" class="registrarse-btn">Registrarse</button>
        </form>

        <div class="counter" id="registration-counter">0 personas inscritas</div>
    </div>

    <script>
        // Contador de personas inscritas (obtenido de localStorage si existe)
        let registeredCount = localStorage.getItem('registeredCount') || 0;
        const counterElement = document.getElementById('registration-counter');
        updateCounterUI();

        function updateCounterUI() {
            counterElement.textContent = `${registeredCount} persona${registeredCount !== 1 ? 's' : ''} inscrita${registeredCount !== 1 ? 's' : ''}`;
        }

        function updateCounter() {
            registeredCount++;
            localStorage.setItem('registeredCount', registeredCount);
            updateCounterUI();
        }

        const form = document.getElementById('registration-form');
        form.addEventListener('submit', function(event) {
            event.preventDefault(); // Evita que se recargue la página al enviar el formulario
            
            // Obtener datos del formulario
            const nombre = form.querySelector('#nombre').value;
            const email = form.querySelector('#email').value;
            const telefono = form.querySelector('#telefono').value;

            // Guardar datos en localStorage (usando un identificador único)
            const participantKey = `participant_${registeredCount}`;
            const participantData = { nombre, email, telefono };
            localStorage.setItem(participantKey, JSON.stringify(participantData));

            // Incrementar el contador y actualizar la UI
            updateCounter();

            // Limpiar el formulario después de enviar
            form.reset();
        });
    </script>
</body>
</html>

