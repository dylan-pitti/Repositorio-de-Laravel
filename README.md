<img width="975" height="770" alt="image" src="https://github.com/user-attachments/assets/e4af921c-fc3c-4f10-965c-4c4a04ae25d2" /># GUÍA TÉCNICA Y REPORTE DE LABORATORIO #2
> **Módulo:** Implementación de Login y Configuración Inicial en Laravel  
> **Asignatura:** Desarrollo Web 2  
> **Institución:** Universidad Tecnológica de Panamá — Facultad de Ingeniería de Sistemas Computacionales  

---

## 📌 Datos Generales del Proyecto

* **Estudiante:** Gabriel Mendoza
* **Correo Institucional:** gabriel.mendoza5@utp.ac.pa
* **Docente:** Irina Fong
* **Sede:** Campus Víctor Levis Sasso
* **Fecha de Ejecución:** 22 de octubre de 2026

---

## 📜 ÍNDICE DE CONTENIDOS

1. [Objetivos y Arquitectura MVC](#1-objetivos-y-arquitectura-mvc)
2. [Entorno de Desarrollo y Requisitos](#2-entorno-de-desarrollo-y-requisitos)
3. [Flujo Metodológico de Instalación](#3-flujo-metodologico-de-instalacion)
4. [Gestión y Respaldo de Base de Datos](#4-gestion-y-respaldo-de-base-de-datos)
5. [Resultados Obtenidos](#5-resultados-obtenidos)
6. [Bitácora de Errores y Soluciones](#6-bitacora-de-errores-y-soluciones)
7. [Fuentes y Referencias](#7-fuentes-y-referencias)

---

## 1. Objetivos y Arquitectura MVC

### 🎯 Objetivo Principal
Configurar un entorno local de desarrollo basado en **WampServer** para el despliegue del framework **Laravel**, estableciendo la integración con una base de datos **MySQL**, migración de esquemas y la preparación estructural para un sistema de autenticación de usuarios.

---

### 🏛️ Modelo–Vista–Controlador (MVC) en Laravel

El proyecto se estructura bajo la arquitectura MVC dividida en las siguientes capas dentro del árbol del proyecto:

* **`app/Models/` (Modelo):** Administra la lógica de negocio y la interacción con las tablas (ejemplo: `User.php`).
* **`resources/views/` (Vista):** Interfaz visual procesada mediante el motor de plantillas Blade (HTML dinamizado).
* **`app/Http/Controllers/` (Controlador):** Intermediario que procesa peticiones HTTP, consulta modelos y retorna respuestas o vistas.
* **`routes/web.php` (Rutas):** Mapeo global de URLs hacia sus respectivos controladores o vistas.

#### Componentes Complementarios:
* `database/migrations/`: Definición y control de versiones del esquema de la base de datos.
* `config/` y `.env`: Parámetros globales de entorno y credenciales de servicios.
* `app/Providers/`: Proveedores del ciclo de vida de la aplicación (`AppServiceProvider.php`).
* `public/`: Directorio público y punto de entrada raíz (`index.php`).

---

## 2. Entorno de Desarrollo y Requisitos

A continuación se detallan las versiones específicas y componentes del entorno local:

* **Sistema Operativo:** Microsoft Windows
* **Servidor Web:** Apache 2.4.65 (Integrado en WampServer)
* **Entorno Servidor:** WampServer (Ruta de trabajo: `C:\wamp64\www`)
* **Lenguaje:** PHP 8.3.28
* **Gestor de Dependencias PHP:** Composer 2.10.3
* **Framework:** Laravel Installer 5.32.0 / Laravel Framework 13.37.0
* **Base de Datos:** MySQL 8.4.7 (Administrado con phpMyAdmin 5.2.3, usuario `root`)
* **Compilador de Frontend:** Node / NPM con Vite 8.3.4
* **IDE:** Visual Studio Code

---

## 3. Flujo Metodológico de Instalación

### Paso 1: Creación del Proyecto
Navegar al directorio raíz del servidor local y ejecutar el comando de inicialización:

```bash
cd C:\wamp64\www
laravel new lab_laravel
```
<img width="975" height="701" alt="Image" src="https://github.com/user-attachments/assets/eebe71be-9451-4eec-beb9-9da5b0bf12df" />

> **Nota de instalación:** Durante el asistente interactivo se seleccionó **none** para el *starter kit* y **Blade** para el *frontend stack*.

---

### Paso 2: Parametrización del Entorno (`.env`)

Ajuste de variables globales y conexión a la base de datos MySQL:

```env
APP_NAME=Laravel
APP_ENV=local
APP_DEBUG=true
APP_URL=http://lab_laravel

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=laravel
DB_USERNAME=root
DB_PASSWORD=
```
<img width="533" height="204" alt="Image" src="https://github.com/user-attachments/assets/f430f730-ca21-44f5-8819-71f5cc3dffde" />

<img width="426" height="209" alt="Image" src="https://github.com/user-attachments/assets/e117432c-f95b-48d5-aaae-17cfc3c5e2fa" />

---

### Paso 3: Compatibilidad de Índices en MySQL
Para prevenir excepciones de longitud de llave primaria/índice en MySQL, se modificó el archivo `app/Providers/AppServiceProvider.php`:

```php
use Illuminate\Support\Facades\Schema;

public function boot(): void
{
    Schema::defaultStringLength(191);
}
```
<img width="975" height="770" alt="Image" src="https://github.com/user-attachments/assets/060a7589-805b-45fe-af45-e90b30d73d74" />

---

### Paso 4: Mantenimiento de Caché y Depuración

```bash
php artisan config:clear
php artisan config:cache
composer update
```
<img width="545" height="182" alt="Image" src="https://github.com/user-attachments/assets/38d1a64d-5bc6-48c3-9751-ecd3b132c58d" />

<img width="550" height="151" alt="Image" src="https://github.com/user-attachments/assets/ba835021-b4a3-4ab3-b38b-b8b50e3ca43d" />


---

### Paso 5: Ejecución de Migraciones

```bash
php artisan migrate
```
> **Nota:** Laravel identifica la ausencia de la base de datos `laravel` y consulta si se desea crear automáticamente; se confirmó mediante la opción `yes`.

---
<img width="819" height="239" alt="Image" src="https://github.com/user-attachments/assets/8de5dcab-d3f3-4497-aaf4-04024030e251" />
### Paso 6: Compilación de Assets Frontend

```bash
npm install
npm run dev
```
Servidor de desarrollo activo localmente en: `http://localhost:5173/`

---

### Paso 7: Implementación del Módulo de Autenticación
Integración del paquete de autenticación mediante el kit Bootstrap:

```bash
composer require laravel/ui
php artisan ui bootstrap --auth
npm install && npm run dev
```

---

### 📋 Secuencia Consolidada de Comandos

```bash
cd C:\wamp64\www
laravel new lab_laravel
cd lab_laravel
# Ajuste manual del archivo .env
php artisan config:clear
composer update
php artisan migrate
php artisan migrate:fresh
npm install
npm run dev
```

---

## 4. Gestión y Respaldo de Base de Datos

* **Gestor:** MySQL / phpMyAdmin
* **Base de Datos:** `laravel`
* **Credencial de Acceso:** Usuario `root` sin clave predeterminada.

### Tablas Generadas por el Framework

| Tabla | Propósito |
| :--- | :--- |
| `users` | Registros de usuarios autenticados. |
| `password_reset_tokens` | Tokens de recuperación de contraseñas. |
| `sessions` | Almacenamiento de sesiones activas. |
| `cache` / `cache_locks` | Gestión de memoria temporal de la app. |
| `jobs` / `job_batches` / `failed_jobs` | Cola y procesamiento de tareas en segundo plano. |
| `migrations` | Historial de versiones del esquema SQL. |

#### Comandos Útiles de Migración:
```bash
php artisan migrate          # Ejecuta migraciones pendientes
php artisan migrate:fresh    # Regenera la estructura completa desde cero
```

### 💾 Procedimiento de Backup
1. Acceso a phpMyAdmin e ingreso a la base de datos `laravel`.
2. Selección de la pestaña **Exportar** → Método **Rápido** → Formato **SQL**.
3. El archivo generado se adjunta en la raíz del proyecto como: `backup_laravel.sql`.
4. **Para restaurar:** Crear la BD `laravel` y ejecutar la importación del archivo `.sql`.

---

## 5. Resultados Obtenidos

1. **Instalación Base:** Despliegue exitoso del motor Laravel v13.37.0.
2. **Autenticación:** Formulario de registro e inicio de sesión funcional utilizando la ruta `/register` (`http://127.0.0.1:8000/register`).
3. **Persistencia:** Almacenamiento correcto de usuarios en la tabla `users` con contraseñas encriptadas bajo el algoritmo **bcrypt**.

---

## 6. Bitácora de Errores y Soluciones

### ⚠️ Dificultad 1: Excepción de Base de Datos (`Illuminate\Database\QueryException`)
* **Síntoma:** Mensaje `Base table or view already exists: 1050 Table 'users' already exists` al intentar correr las migraciones.
* **Causa:** Intentos previos de migración que dejaron tablas creadas a medias.
* **Solución:** Reiniciar el esquema completo e incluir el ajuste en `AppServiceProvider`:
  ```bash
  php artisan migrate:fresh
  ```

---

### ⚠️ Dificultad 2: Error de Ejecución en Entorno de Node (`vite no se reconoce...`)
* **Síntoma:** Falla al ejecutar `npm run dev`.
* **Causa:** Módulos de Node.js no instalados o desactualizados en el proyecto.
* **Solución:** Reinstalación explícita de paquetes de depuración web:
  ```bash
  npm install
  npm run dev
  ```

---

### ⚠️ Dificultad 3: Error de Sintaxis en Terminal (Typo)
* **Síntoma:** Error de comando no reconocido al intentar limpiar la configuración (`php artisian config::clear`).
* **Causa:** Error tipográfico en el binario y los delimitadores del comando.
* **Solución:** Corrección a la sintaxis nativa de Artisan:
  ```bash
  php artisan config:clear
  ```

---

## 7. Fuentes y Referencias

1. Laravel Documentation – *Database Migrations:* https://laravel.com/docs/migrations
2. Laravel Documentation – *Configuration & Database:* https://laravel.com/docs/database
3. Laravel Documentation – *Starter Kits:* https://laravel.com/docs/starter-kits
4. Composer Documentación Oficial: https://getcomposer.org/doc/
5. Vite Core Guide: https://vite.dev/guide/
6. WampServer Environment: https://www.wampserver.com/en/
