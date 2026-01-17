# Guía de Deploy en Coolify

## Pre-requisitos completados
- [x] Base de datos `dify` creada en Supabase
- [x] Base de datos `dify_plugin` creada en Supabase
- [x] Archivos de configuración modificados

## Paso 1: Subir cambios a Git

```bash
cd /Users/carlosmachin/Documents/GitHub/dify
git add docker/docker-compose.yaml docker/.env.example
git commit -m "Configure Dify for Coolify deployment"
git push origin main
```

## Paso 2: Crear proyecto en Coolify

1. Ve a Coolify → **Projects** → **Add New**
2. Selecciona **Docker Compose**
3. Conecta tu repositorio de GitHub (fork de Dify)
4. **Build Pack**: Docker Compose
5. **Docker Compose Location**: `docker/docker-compose.yaml`

## Paso 3: Configurar Environment Variables

En Coolify, ve a **Environment Variables** y añade el contenido de `.env.example`:

```env
CONSOLE_API_URL=https://dify.console.api.pitchdb.agency
CONSOLE_WEB_URL=https://dify.console.pitchdb.agency
SERVICE_API_URL=https://dify.api.pitchdb.agency
TRIGGER_URL=https://api.dify.pitchdb.agency
APP_API_URL=https://dify.api.app.pitchdb.agency
APP_WEB_URL=https://dify.pitchdb.agency

DB_HOST=supabase-db
DB_PASSWORD=QqipHLlRg5Xslef0Nc6XRvWci69Ljb33
```

> **Importante**: Coolify cargará las variables desde el archivo `.env.example` que está en el repositorio. Puedes sobreescribirlas desde la UI de Coolify.

## Paso 4: Configurar Dominios

En Coolify, configura los dominios para el servicio **nginx**:
- `dify.pitchdb.agency` → nginx:8089

## Paso 5: Deploy

1. Click en **Deploy**
2. Espera a que todos los contenedores estén running
3. Verifica los logs de cada servicio

## Puertos expuestos

| Servicio | Puerto |
|----------|--------|
| Nginx HTTP | 8089 |
| Nginx HTTPS | 8443 |
| Weaviate | 8090 |
| Plugin Debug | 5003 |

## Troubleshooting

**Si hay error de conexión a la base de datos:**
- Verifica que `supabase-db` es accesible desde la red `coolify`
- Verifica las credenciales de Postgres

**Si Weaviate no inicia:**
- Verifica que el puerto 8090 está libre
