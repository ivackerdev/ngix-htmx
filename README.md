# NGINX Coniguracion para HTMX con soporte CORS

Este repositorio contiene un ejemplo de configuración de NGINX diseñado para trabajar con HTMX, incluyendo la configuración necesaria para soportar CORS (Cross-Origin Resource Sharing). Esta configuración permite a los desarrolladores integrar servicios backend con frontends HTMX, habilitando solicitudes entre dominios de manera segura y eficiente.

## Requisitos Previos

Antes de implementar esta configuración, asegúrate de tener:

- NGINX instalado en tu servidor.
- Un dominio configurado y apuntando a tu servidor NGINX.
- Certificados SSL (por ejemplo, de Let's Encrypt) para el dominio, asegurando una conexión HTTPS segura.

## Configuración

La configuración de NGINX incluida en este repositorio está diseñada para ser implementada en un bloque de servidor NGINX. Sigue estos pasos para configurar tu servidor:

1. **Editar Archivo de Configuración NGINX**: Abre tu archivo de configuración de NGINX para el dominio específico. Este archivo suele encontrarse en `/etc/nginx/sites-available/tu-dominio.conf`.

2. **Añadir la Configuración**: Copia y pega la configuración proporcionada en este repositorio dentro del bloque `server` de tu archivo de configuración.

3. **Ajustar los Valores de Configuración**:
   - Cambia `go.api.evolpos.cloud` por tu dominio.
   - Asegúrate de que las rutas a los certificados SSL (`ssl_certificate` y `ssl_certificate_key`) correspondan a las ubicaciones y nombres de tus archivos de certificado.

4. **Configurar CORS**: Ajusta el valor `'https://DOMINIO'` en las directivas `Access-Control-Allow-Origin` con el dominio desde el cual permitirás las solicitudes. Si necesitas permitir múltiples dominios, considera ajustar esta configuración según tus necesidades específicas.

5. **Recargar NGINX**: Guarda los cambios y recarga la configuración de NGINX para aplicar los cambios:
   ```
   sudo nginx -t
   sudo systemctl reload nginx
   ```

## Ejemplo de Configuración

El siguiente es un extracto de la configuración incluida en este repositorio, ajustada para trabajar con HTMX y soportar correctamente CORS:

```nginx
server {
    listen 443 ssl;
    server_name tu-dominio.com;

    location /solicitud {
        proxy_pass http://localhost:8888;
        # ...resto de la configuración...
    }

    ssl_certificate /etc/letsencrypt/live/tu-dominio.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/tu-dominio.com/privkey.pem;
}
```

## Contribuciones

Las contribuciones a este proyecto son bienvenidas. Si encuentras una manera de mejorar la configuración o deseas añadir soporte para más escenarios, por favor, considera abrir un Pull Request.

## Licencia

Este proyecto está licenciado bajo la [Licencia MIT](LICENSE).

---

Este README proporciona una guía básica para configurar NGINX para trabajar con HTMX, incluyendo la gestión de CORS. Asegúrate de ajustar los valores de configuración según tus necesidades específicas y el entorno de tu servidor.
