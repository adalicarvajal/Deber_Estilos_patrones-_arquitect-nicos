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
### Microservicios (Ejemplo práctico)
- **Escenario**: Un sistema de streaming de música.
  - **Servicios independientes**:
    - **Servicio de autenticación**: Verifica las credenciales de los usuarios.
    - **Servicio de reproducción**: Gestiona la reproducción de canciones.
    - **Servicio de recomendaciones**: Ofrece listas de reproducción personalizadas basadas en los gustos del usuario.
  - **Comunicación**: Los microservicios se comunican utilizando un bus de mensajes como **RabbitMQ** o mediante **API REST**.

#### Arquitectura:
1. **Servicio de autenticación**:
   - Gestiona el inicio de sesión y tokens de usuario.
   - Provee información de autorización para los demás servicios.
2. **Servicio de reproducción**:
   - Recibe peticiones de reproducción de una canción o una lista.
   - Comunica errores si una canción no está disponible.
3. **Servicio de recomendaciones**:
   - Analiza el historial de canciones reproducidas.
   - Devuelve sugerencias personalizadas.

---

**Código Ejemplo:**

#### Servicio de autenticación
```python
# Servicio de autenticación (Flask)
from flask import Flask, request, jsonify

app = Flask(__name__)

@app.route('/login', methods=['POST'])
def login():
    data = request.json
    if data['username'] == 'user' and data['password'] == 'pass':
        return jsonify({'message': 'Autenticación exitosa', 'token': '12345'}), 200
    return jsonify({'message': 'Credenciales incorrectas'}), 401

if __name__ == '__main__':
    app.run(port=5000, debug=True)
