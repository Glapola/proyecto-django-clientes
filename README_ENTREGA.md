# Proyecto Django - autenticación y clientes

Basado en README-DJANGO-PRACTICA-1.md de la clase. Incluye registro, login, logout, recuperación por consola y alta/listado de clientes.

## Windows / XAMPP (Python 3.12+)

1. Iniciar MySQL en XAMPP; crear `django_db` en phpMyAdmin (SQL: `CREATE DATABASE django_db CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;`).
2. Abrir PowerShell en esta carpeta y ejecutar:

```powershell
py -m venv venv
.\venv\Scripts\Activate.ps1
pip install -r requirements.txt
python manage.py migrate
python manage.py runserver
```

3. Abrir http://127.0.0.1:8000/registro/ y crear usuario; probar /login/, /clientes/, /recuperar/ y logout.
4. Si MySQL tiene contraseña, definir `MYSQL_PASSWORD` en PowerShell antes de migrar: `$env:MYSQL_PASSWORD='tu-clave'`.

## Publicación en Railway (requiere cuenta, GitHub y base MySQL accesible)

1. Subir este proyecto a un repositorio privado GitHub, sin subir `venv`, contraseñas ni `.env`.
2. Crear proyecto Railway, agregar servicio MySQL y servicio web desde GitHub.
3. En el servicio web configurar variables `DJANGO_SECRET_KEY`, `DJANGO_DEBUG=False`, `DJANGO_ALLOWED_HOSTS`, `DJANGO_CSRF_TRUSTED_ORIGINS`, `MYSQL_DATABASE`, `MYSQL_USER`, `MYSQL_PASSWORD`, `MYSQL_HOST`, `MYSQL_PORT` según la conexión MySQL del servicio (no copiar valores ficticios de `.env.example`).
4. Configurar build `pip install -r requirements.txt && python manage.py collectstatic --noinput`; start `gunicorn config.wsgi:application --bind 0.0.0.0:$PORT`.
5. Ejecutar `python manage.py migrate` en una consola del servicio con las variables configuradas. Generar dominio público y ajustar hosts y CSRF con el dominio definitivo.
6. Probar registro/login/clientes en el dominio público. Capturar pantallas reales y pegar la URL final en el PDF.

**Nota:** La recuperación de contraseña imprime el correo en logs de servidor; no envía email real. Para producción se necesita un proveedor SMTP. No habilitar DEBUG en público. La disponibilidad y precios de Railway pueden cambiar.
