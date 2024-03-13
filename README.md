<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Facturación de Productos</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
        }

        h1, h2 {
            text-align: center;
        }

        form {
            max-width: 600px;
            margin: 0 auto;
            padding: 20px;
            border: 1px solid #ccc;
            border-radius: 5px;
            background-color: #f9f9f9;
        }

        label, input, button {
            display: block;
            margin-bottom: 10px;
        }

        input[type="number"], input[type="text"] {
            width: 100%;
            padding: 8px;
            border: 1px solid #ccc;
            border-radius: 5px;
            box-sizing: border-box;
        }

        table {
            width: 100%;
            border-collapse: collapse;
        }

        table, th, td {
            border: 1px solid #ccc;
            padding: 8px;
            text-align: left;
        }

        button {
            background-color: #4CAF50;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
            width: 100%;
        }

        button:hover {
            background-color: #45a049;
        }

        @media (max-width: 768px) {
            form {
                padding: 10px;
            }

            table {
                font-size: 12px;
            }
        }
    </style>
</head>
<body>
    <h1>Facturación de Productos</h1>
    <form id="facturaForm">
        <h2>Datos del Cliente</h2>
        <label for="nombreCliente">Nombre del Cliente:</label>
        <input type="text" id="nombreCliente" name="nombreCliente">

        <label for="direccion">Dirección:</label>
        <input type="text" id="direccion" name="direccion">

        <label for="telefono">Teléfono:</label>
        <input type="text" id="telefono" name="telefono">

        <h2>Productos</h2>
        <table id="productosTable">
            <tr>
                <th>Producto</th>
                <th>Precio</th>
            </tr>
            <!-- Aquí se agregarán las filas de productos dinámicamente -->
        </table>

        <button type="button" onclick="agregarProducto()">Agregar Producto</button>

        <label for="costoEnvio">Costo de Envío:</label>
        <input type="number" id="costoEnvio" name="costoEnvio">

        <label for="total">Total:</label>
        <input type="number" id="total" name="total" readonly>

        <button type="submit">Generar Factura</button>
    </form>

    <script>
        let productosCount = 0;

        function agregarProducto() {
            if (productosCount >= 10) {
                alert("No puedes agregar más de 10 productos.");
                return;
            }

            productosCount++;

            const productosTable = document.getElementById("productosTable");
            const newRow = productosTable.insertRow();
            const cell1 = newRow.insertCell(0);
            const cell2 = newRow.insertCell(1);

            cell1.innerHTML = `<input type="text" name="producto${productosCount}" placeholder="Nombre del Producto">`;
            cell2.innerHTML = `<input type="number" name="precio${productosCount}" placeholder="Precio del Producto">`;
        }

        document.getElementById("facturaForm").addEventListener("submit", function(event) {
            event.preventDefault();
            let total = parseFloat(document.getElementById("costoEnvio").value) || 0;

            for (let i = 1; i <= productosCount; i++) {
                const precio = parseFloat(document.getElementsByName(`precio${i}`)[0].value) || 0;
                total += precio;
            }

            document.getElementById("total").value = total.toFixed(2);
        });
    </script>
</body>
</html>
