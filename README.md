# Programación Distribuida

Repositorio para las prácticas y proyectos de la asignatura **Programación Distribuida**.
Incluye microservicios desarrollados con **Quarkus**, gestión de persistencia con **Hibernate ORM Panache**, base de datos **PostgreSQL** y contenedores orquestados con **Docker Compose**.

---

## 📁 Estructura del Proyecto

* **`app-authors`**: Microservicio para autores en Quarkus (Puerto `8070`).
* **`app-books`**: Microservicio para libros en Quarkus (Puerto `8080`).
* **`web01`**, **`web02`**, **`web03`**: Módulos y prácticas complementarias.
* **`docker-compose.yml`**: Servicios de infraestructura (Base de datos PostgreSQL y Adminer).

---

## 🐳 1. Infraestructura con Docker

La base de datos y herramientas de administración se gestionan mediante Docker Compose.

* **PostgreSQL**: `localhost:5433` (Base de datos: `books-db`, Usuario: `postgres`, Contraseña: `postgres`)
* **Adminer** (Gestor web de BD): [http://localhost:8088](http://localhost:8088)

### Comandos en Windows (Casa / PowerShell o CMD)
```powershell
# Iniciar contenedores en segundo plano
docker compose up -d

# Ver el estado de los contenedores
docker compose ps

# Ver logs de la base de datos
docker compose logs -f books-db

# Detener los contenedores
docker compose down

# Detener y borrar volúmenes (reiniciar la base de datos limpia)
docker compose down -v
```

### Comandos en Linux (Universidad / Terminal Bash)
> **Nota:** Si tu usuario en la universidad no está en el grupo `docker`, agrega `sudo` antes de cada comando.

```bash
# Iniciar contenedores en segundo plano
docker compose up -d
# (o si usas versión anterior de docker-compose: sudo docker-compose up -d)

# Ver el estado de los contenedores
docker compose ps

# Ver logs en tiempo real
docker compose logs -f

# Detener los contenedores
docker compose down
```

---

## ⚡ 2. Ejecutar Microservicios Quarkus

Cada microservicio se ejecuta de forma independiente usando el wrapper de Gradle (`gradlew`).

### Requisito previo en Linux (Universidad)
En Linux debes asegurarte de que el script wrapper tenga permisos de ejecución:
```bash
chmod +x gradlew
```

---

### Modo Desarrollo (Quarkus Dev Mode con Live Reload)

#### En Windows:
```powershell
# Levantar microservicio app-authors (Puerto 8070)
.\gradlew :app-authors:quarkusDev

# Levantar microservicio app-books (Puerto 8080)
.\gradlew :app-books:quarkusDev
```

#### En Linux:
```bash
# Levantar microservicio app-authors (Puerto 8070)
./gradlew :app-authors:quarkusDev

# Levantar microservicio app-books (Puerto 8080)
./gradlew :app-books:quarkusDev
```

---

### Consola Dev UI de Quarkus
Una vez levantado cada servicio en modo desarrollo, puedes ingresar a su panel interactivo:
* **app-authors Dev UI:** [http://localhost:8070/q/dev/](http://localhost:8070/q/dev/)
* **app-books Dev UI:** [http://localhost:8080/q/dev/](http://localhost:8080/q/dev/)

---

### Compilar y Empaquetar

```bash
# Windows
.\gradlew build

# Linux
./gradlew build
```

---

## 🔄 3. Flujo para clonar en otra máquina (Universidad o Casa)

Cuando clones el repositorio en otra computadora:

```bash
# 1. Clonar el repositorio
git clone https://github.com/Dennis290699/prog-distribuida.git
cd prog-distribuida

# 2. Levantar la base de datos
docker compose up -d

# 3. Levantar el microservicio deseado (ejemplo Linux)
chmod +x gradlew
./gradlew :app-books:quarkusDev
```
