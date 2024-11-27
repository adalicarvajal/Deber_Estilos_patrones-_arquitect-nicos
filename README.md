# Arquitectura y Patrones de Software

## Estilos de Arquitectura de Software

### Client-Server (Ejemplo práctico)
- **Escenario**: Una aplicación web para gestionar inventarios.
  - **Cliente**: Un navegador web (Chrome, Firefox) donde los usuarios visualizan y gestionan productos.
  - **Servidor**: Un backend desarrollado en Node.js que gestiona las solicitudes HTTP, interactúa con la base de datos y responde al cliente.
  - **Comunicación**:
    - El cliente envía una solicitud `GET` al servidor para listar productos.
    - El servidor consulta la base de datos y responde con los datos en formato JSON.

**Código Ejemplo:**
```javascript
// Backend con Node.js
const express = require('express');
const app = express();

app.get('/products', (req, res) => {
    const products = [
        { id: 1, name: 'Laptop', price: 1200 },
        { id: 2, name: 'Mouse', price: 20 }
    ];
    res.json(products);
});

app.listen(3000, () => console.log('Servidor ejecutándose en http://localhost:3000'));
