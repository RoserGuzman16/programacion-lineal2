<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Programación Lineal - Simplex y Gráfico</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjs/11.11.0/math.min.js"></script>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 40px;
      background-color: #f4f4f4;
    }
    h1 {
      color: #333;
    }
    textarea, input {
      width: 100%;
      margin: 10px 0;
      padding: 8px;
      font-family: monospace;
    }
    button {
      background-color: #007BFF;
      color: white;
      padding: 10px;
      border: none;
      cursor: pointer;
      font-weight: bold;
    }
    button:hover {
      background-color: #0056b3;
    }
    #grafico {
      margin-top: 20px;
    }
    pre {
      background-color: #fff;
      padding: 10px;
      border: 1px solid #ccc;
      overflow: auto;
    }
  </style>
</head>
<body>
  <h1>🧮 Programación Lineal: Simplex y Método Gráfico</h1>

  <label>Función objetivo (ej: 3x + 5y):</label>
  <input id="objetivo" value="3x + 5y">

  <label>Restricciones (una por línea, ejemplo: x + 2y <= 10):</label>
  <textarea id="restricciones" rows="4">x + 2y <= 10
3x + y <= 15</textarea>

  <button onclick="resolver()">Resolver</button>

  <div id="resultados">
    <h3>📊 Resultados:</h3>
    <pre id="output">---</pre>
  </div>

  <canvas id="grafico" width="600" height="400"></canvas>

  <script>
    function parseFuncion(funcionStr) {
      const vars = ['x', 'y'];
      let coef = vars.map(v => {
        const regex = new RegExp("([+-]?\\d*\\.?\\d*)\\s*" + v);
        const match = funcionStr.match(regex);
        if (match) return parseFloat(match[1] || '1');
        return 0;
      });
      return coef;
    }

    function parseRestricciones(texto) {
      const lineas = texto.trim().split("\n");
      let A = [], b = [];

      lineas.forEach(linea => {
        const match = linea.match(/(.+)(<=|>=|=)(.+)/);
        if (match) {
          const [_, lhs, op, rhs] = match;
          const coef = parseFuncion(lhs);
          A.push(coef);
          b.push(Number(rhs.trim()));
        }
      });

      return { A, b };
    }

    function resolver() {
      const c = parseFuncion(document.getElementById("objetivo").value);
      const { A, b } = parseRestricciones(document.getElementById("restricciones").value);

      let texto = `🔹 Función objetivo: Max Z = ${c.join(" , ")}\n`;
      texto += `🔹 Restricciones:\n`;

      A.forEach((row, i) => {
        texto += `   ${row.join(" , ")} <= ${b[i]}\n`;
      });

      const vertices = calcularVertices(A, b);
      let maxZ = -Infinity;
      let solucion = null;

      vertices.forEach(v => {
        const z = math.dot(c, v);
        if (z > maxZ) {
          maxZ = z;
          solucion = v;
        }
      });

      if (solucion) {
        texto += `\n✅ Solución óptima:\n`;
        texto += `   Variables: x = ${solucion[0].toFixed(2)}, y = ${solucion[1].toFixed(2)}\n`;
        texto += `   Valor óptimo Z = ${maxZ.toFixed(2)}\n`;
      } else {
        texto += "\n❌ No se encontró solución válida.\n";
      }

      document.getElementById("output").textContent = texto;
      dibujarGrafico(A, b, solucion);
    }

    function calcularVertices(A, b) {
      const puntos = [];
      for (let i = 0; i < A.length; i++) {
        for (let j = i + 1; j < A.length; j++) {
          const mat = [A[i], A[j]];
          const vector_b = [b[i], b[j]];
          try {
            const sol = math.lusolve(mat, vector_b).map(row => row[0]);
            if (sol.every(val => val >= 0)) {
              let cumple = true;
              for (let k = 0; k < A.length; k++) {
                if (math.dot(A[k], sol) > b[k] + 1e-6) {
                  cumple = false;
                  break;
                }
              }
              if (cumple) puntos.push(sol);
            }
          } catch (e) { }
        }
      }
      puntos.push([0, 0]);
      return puntos;
    }

    function dibujarGrafico(A, b, punto) {
      const canvas = document.getElementById("grafico");
      const ctx = canvas.getContext("2d");
      ctx.clearRect(0, 0, canvas.width, canvas.height);

      const escala = 40;

      // Ejes
      ctx.beginPath();
      ctx.moveTo(0, canvas.height);
      ctx.lineTo(canvas.width, canvas.height);
      ctx.moveTo(0, 0);
      ctx.lineTo(0, canvas.height);
      ctx.stroke();

      // Restricciones
      A.forEach((a, i) => {
        const x = canvas.width / escala;
        const y = (b[i] - a[0] * 0) / a[1];
        const y2 = (b[i] - a[0] * x) / a[1];

        ctx.beginPath();
        ctx.moveTo(0, canvas.height - y * escala);
        ctx.lineTo(x * escala, canvas.height - y2 * escala);
        ctx.strokeStyle = `hsl(${i * 90}, 100%, 40%)`;
        ctx.stroke();
      });

      // Punto óptimo
      if (punto) {
        ctx.beginPath();
        ctx.arc(punto[0] * escala, canvas.height - punto[1] * escala, 5, 0, 2 * Math.PI);
        ctx.fillStyle = "red";
        ctx.fill();
        ctx.fillText("Óptimo", punto[0] * escala + 5, canvas.height - punto[1] * escala - 5);
      }
    }
  </script>
</body>
</html>
