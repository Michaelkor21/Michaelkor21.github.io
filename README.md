

<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Calculadora Simple</title>
</head>
<body>

    <h2>Calculadora de Beca y Financiamiento</h2>

    <form id="formulario">
        <label>Promedio (0-100):</label>
        <input type="number" id="promedio" min="0" max="100" required><br><br>

        <label>Costo Colegiatura:</label>
        <input type="number" id="colegiatura" min="0" required><br><br>

        <label>Meses a financiar:</label>
        <input type="number" id="meses" min="1" value="1" required><br><br>

        <button type="button" onclick="calcular()">Calcular</button>
    </form>

    <div id="resultado" style="margin-top: 20px;"></div>

    <script>
    function calcular() {
        // 1. Obtener los valores ingresados por el usuario
        const promedio = parseFloat(document.getElementById('promedio').value);
        const colegiatura = parseFloat(document.getElementById('colegiatura').value);
        const meses = parseInt(document.getElementById('meses').value);
        const divResultado = document.getElementById('resultado');

        let porcentajeBeca = 0;

        // 2. Determinar porcentaje de beca según los rangos
        if (promedio >= 95 && promedio <= 100) porcentajeBeca = 100;
        else if (promedio >= 90 && promedio < 95) porcentajeBeca = 80;
        else if (promedio >= 86 && promedio < 90) porcentajeBeca = 60;

        // 3. Evaluar si es apto para beca (>85) y si entró en un rango válido
        if (promedio > 85 && porcentajeBeca > 0) {
            const descuento = colegiatura * (porcentajeBeca / 100);
            const total = colegiatura - descuento;
            
            divResultado.innerHTML = `
                <h3>¡Apto para Beca!</h3>
                <p>Porcentaje: ${porcentajeBeca}%</p>
                <p>Total a pagar: $${total}</p>
            `;
        } else {
            // Si no tiene beca, calculamos financiamiento (1.5% de interés mensual de ejemplo)
            const costoSinInteres = colegiatura;
            const costoConInteres = colegiatura * (1 + (0.015 * meses));

            divResultado.innerHTML = `
                <h3>No apto para beca. Opciones de Financiamiento:</h3>
                <p><strong>Sin interés:</strong> Total $${costoSinInteres} (${meses} pagos de $${(costoSinInteres / meses).toFixed(2)})</p>
                <p><strong>Con interés:</strong> Total $${costoConInteres.toFixed(2)} (${meses} pagos de $${(costoConInteres / meses).toFixed(2)})</p>
            `;
        }
    }
    </script>

</body>
</html>
