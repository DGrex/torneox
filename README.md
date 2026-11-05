# TorneoX

Sistema integral de gestión de torneos de fútbol (fútbol 5 a 11), con roles
de **Administrador** y **Dirigente de equipo**, inscripciones, arbitrajes,
multas y reglas de bonificación por fase.

## Stack

- Python 3 + Django 5.2 (LTS)
- SQLite en desarrollo → PostgreSQL en producción
- Tailwind CSS (vía CDN por ahora)
- Variables de entorno con `django-environ`

## Primeros pasos (local)

```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt

cp .env.example .env             # y completa DJANGO_SECRET_KEY
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver
```

## Estructura de apps

| App | Responsabilidad |
|---|---|
| `usuarios` | Autenticación, modelo de usuario y roles |
| `equipos` | Equipos, jugadores, plantillas |
| `torneos` | Torneos, fases, calendario |
| `partidos` | Resultados, tarjetas, estadísticas |
| `finanzas` | Inscripciones, arbitrajes, multas |

## Seguridad

- `SECRET_KEY` y credenciales **solo** por variables de entorno (nunca en el código).
- `DEBUG=False` por defecto; se activa a propósito en `.env` local.
- Cookies de sesión y CSRF con `HttpOnly`; en producción además `Secure` y HSTS.
- Validadores de contraseña reforzados (mínimo 10 caracteres).

## Migración a PostgreSQL

Cuando se despliegue, basta con definir `DATABASE_URL` en el entorno de
producción (por ejemplo `postgres://usuario:password@host:5432/bd`); el
proyecto la detecta automáticamente sin cambiar código.

## Estado

Base del proyecto: configuración, apps vacías y modelo de usuario con roles.
Construcción paso a paso — sin modelos de negocio todavía.
