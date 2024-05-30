<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>ecuación</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 20px;
    }
    label, input {
      margin-bottom: 10px;
    }
  </style>
</head>
<body>
  <h1>Resolver Ecuación 3sen(0,5x)-0,5*x+2=0</h1>
  <form id="rootForm">
    <label for="initialGuess">Estimación Inicial:</label>
    <input type="number" id="initialGuess" name="initialGuess" value="1" step="0.01" required>
    <br>
    <label for="tolerance">Tolerancia:</label>
    <input type="number" id="tolerance" name="tolerance" value="1e-6" step="1e-7" required>
    <br>
    <button type="submit">resolver</button>
  </form>
  <div id="result"></div>

  <script>
    // Definir la función
    function f(x) {
      return 3 * Math.sin(0.5 * x) - 0.5 * x + 2;
    }

    // Definir la función derivada
    function df(x) {
      return 1.5 * Math.cos(0.5 * x) - 0.5;
    }

    // Usar el método de Newton-Raphson para encontrar la raíz
    function findRoot(initialGuess, tolerance) {
      let x = initialGuess;
      let iterations = 0;
      const maxIterations = 100;

      while (Math.abs(f(x)) > tolerance && iterations < maxIterations) {
        x = x - f(x) / df(x);
        iterations++;
      }

      if (iterations === maxIterations) {
        return "El método no convergió dentro del número especificado de iteraciones.";
      } else {
        return `La solución es: x = ${x.toFixed(4)}`;
      }
    }

    document.getElementById("rootForm").addEventListener("submit", function(event) {
      event.preventDefault();

      const initialGuess = parseFloat(document.getElementById("initialGuess").value);
      const tolerance = parseFloat(document.getElementById("tolerance").value);
      const result = findRoot(initialGuess, tolerance);
      document.getElementById("result").textContent = result;
    });
  </script>
</body>
</html>
