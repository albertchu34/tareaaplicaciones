# 🌟 **Sistema de Gestión de Carnets Universitarios** 🌟

<p align="center">
  <img src="https://imagen.upla.edu.pe/wp-content/uploads/2023/02/cropped-LOGOUPLA-removebg-preview-300x115.png.webp" alt="Logo UPLA" width="200">
</p>

---

## 🏫 **Universidad Peruana Los Andes**
### 👨‍🎓 **Facultad de Ingeniería de Sistemas**  
### 👩‍🏫 **Escuela Profesional de Ingeniería de Sistemas e Informática**

---

## ✨ **Información del Proyecto**

**Realizado por:**  
[Chuquiyauri Lagunas Albert Jeankarlo]  

**Asignatura:**  
Taller VI Aplicaciones  

**Docente a Cargo:**  
[Mg. Fernandez Bejarano Raul]  

**Año Académico:**  
2025

---

# 🎓 Sistema de Gestión de Carnets Universitarios

Este proyecto es una aplicación de escritorio en Java Swing que permite **gestionar carnets universitarios**. Se construyó siguiendo el patrón de diseño **MVC (Modelo - Vista - Controlador)**, y permite realizar operaciones básicas de **crear, listar, actualizar y eliminar** carnets, así como vincularlos a una **facultad y carrera profesional**.

---

## 📷 Capturas de Pantalla

### Interfaz principal:

![Interfaz principal](./ui_formulario.png)

### Componentes del formulario:

![Componentes del formulario](./screenshots/componentes_ui.png)

---

## 🧠 Objetivo del Proyecto

El sistema busca facilitar la administración de carnets universitarios, con una interfaz simple que interactúa con una base de datos MySQL. Cada carnet se relaciona con una **facultad** y una **carrera profesional**, cumpliendo las siguientes reglas:

- Una **facultad** puede tener muchas **carreras profesionales**.
- Una **carrera profesional** pertenece a **una sola facultad**.

---

## 🧱 Arquitectura MVC

Este proyecto fue dividido en tres capas:

### 📄 Modelo (`modelo`)

Contiene las clases que representan las entidades:

- `Carnet.java`: Modelo de los estudiantes.
- `Facultad.java`: Modelo para facultades.
- `Carrera.java`: Modelo para carreras profesionales.
- `ConexionBD.java`: Encapsula la conexión a la base de datos.

### ⚙️ Controlador (`controlador`)

Lógica de negocio y consultas SQL:

- `ControladorCarnet.java`: Contiene métodos para registrar, actualizar, eliminar y listar carnets, así como cargar facultades y carreras.

### 🎨 Vista (`vista`)

Formulario Swing ya diseñado gráficamente (NetBeans, etc.):

- `Inicio.java`: Pantalla principal con tabla, campos de entrada, combo box, y botones para CRUD.

---

## 🗃️ Base de Datos (MySQL)

````sql
CREATE TABLE IF NOT EXISTS facultades (
    id_facultad INT AUTO_INCREMENT PRIMARY KEY,
    nombre_facultad VARCHAR(100) NOT NULL UNIQUE
);

CREATE TABLE IF NOT EXISTS carreras (
    id_carrera INT AUTO_INCREMENT PRIMARY KEY,
    nombre_carrera VARCHAR(100) NOT NULL UNIQUE,
    id_facultad INT NOT NULL,
    FOREIGN KEY (id_facultad) REFERENCES facultades(id_facultad)
);

CREATE TABLE IF NOT EXISTS estudiantes (
    id_estudiante INT AUTO_INCREMENT PRIMARY KEY,
    codigo VARCHAR(50) NOT NULL UNIQUE,
    dni VARCHAR(8) UNIQUE,
    apellidos VARCHAR(100) NOT NULL,
    nombres VARCHAR(100) NOT NULL,
    id_carrera INT NOT NULL,
    FOREIGN KEY (id_carrera) REFERENCES carreras(id_carrera)
);

## 🔧 Funcionalidades

- ✅ Crear nuevo carnet con datos como DNI, nombres, apellidos, código, facultad y carrera.
- ✅ Actualizar información de un carnet seleccionado desde la tabla.
- ✅ Eliminar carnet existente previa confirmación.
- ✅ Listar todos los carnets con su información completa en una tabla.
- ✅ Cargar dinámicamente la lista de **facultades** desde la base de datos.
- ✅ Mostrar solo las **carreras** que pertenecen a la **facultad seleccionada**.
- ✅ Validación de campos vacíos antes de registrar o actualizar.

---

## ⚙️ Ejecución del Proyecto

1. Asegúrate de tener **MySQL** funcionando y una base de datos llamada `carnet`.
2. Ejecuta los scripts SQL para crear las tablas `facultades`, `carreras`, y `estudiantes`.
3. Llena las tablas de facultades y carreras con datos de prueba.
4. Modifica `ConexionBD.java` con tu configuración local:

   ```java
   private static final String URL = "jdbc:mysql://localhost:3306/carnet";
   private static final String USER = "root";
   private static final String PASSWORD = "root123";

## ⚙️ Ejecución del Proyecto

1. **Base de Datos**:
   - Asegúrate de tener **MySQL** funcionando y una base de datos llamada `carnet`.
   - Ejecuta los siguientes scripts SQL para crear las tablas necesarias:

     ```sql
     CREATE TABLE IF NOT EXISTS facultades (
         id_facultad INT AUTO_INCREMENT PRIMARY KEY,
         nombre_facultad VARCHAR(100) NOT NULL UNIQUE
     );

     CREATE TABLE IF NOT EXISTS carreras (
         id_carrera INT AUTO_INCREMENT PRIMARY KEY,
         nombre_carrera VARCHAR(100) NOT NULL UNIQUE,
         id_facultad INT NOT NULL,
         FOREIGN KEY (id_facultad) REFERENCES facultades(id_facultad)
     );

     CREATE TABLE IF NOT EXISTS estudiantes (
         id_estudiante INT AUTO_INCREMENT PRIMARY KEY,
         codigo VARCHAR(50) NOT NULL UNIQUE,
         dni VARCHAR(8) UNIQUE,
         apellidos VARCHAR(100) NOT NULL,
         nombres VARCHAR(100) NOT NULL,
         id_carrera INT NOT NULL,
         FOREIGN KEY (id_carrera) REFERENCES carreras(id_carrera)
     );
     ```

   - Llena las tablas de **facultades** y **carreras** con datos de prueba.

2. **Configuración de la Conexión a la Base de Datos**:
   - Abre el archivo `ConexionBD.java` y modifica los siguientes parámetros con tus credenciales de MySQL locales:

     ```java
     private static final String URL = "jdbc:mysql://localhost:3306/carnet";
     private static final String USER = "root";
     private static final String PASSWORD = "root123";  // Cambia por tu contraseña real
     ```

3. **Abrir en NetBeans (o tu IDE preferido)**:
   - Si estás usando **NetBeans**:
     - Abre **NetBeans** y selecciona **File → Open Project**.
     - Navega a la carpeta de tu proyecto y selecciona el directorio principal donde está el archivo `.java` principal.
   - Si usas otro IDE, simplemente abre el proyecto normalmente.

4. **Ejecución del Proyecto**:
   - En NetBeans, haz clic derecho sobre el archivo `Inicio.java` (o el archivo principal que contiene la función `main`) y selecciona **Run**.
   - El formulario debería abrirse y podrás interactuar con la base de datos para agregar, actualizar, eliminar y listar los carnets universitarios.

---

## 🔎 Explicación de Código Clave

### `ControladorCarnet.java`

- **`listarCarnets(JTable tabla)`**: Este método consulta la base de datos para obtener los carnets existentes y los carga en la tabla con información adicional sobre la carrera y la facultad.
- **`registrarCarnet(Carnet carnet)`**: Inserta un nuevo carnet en la base de datos, utilizando los datos proporcionados en el formulario.
- **`actualizarCarnet(Carnet carnet)`**: Permite modificar un carnet ya registrado en la base de datos mediante su ID.
- **`eliminarCarnet(int id)`**: Elimina un carnet específico de la base de datos utilizando su ID.
- **`obtenerFacultades()`**: Recupera todas las facultades desde la base de datos.
- **`obtenerCarrerasPorFacultad(int idFacultad)`**: Recupera todas las carreras asociadas a una facultad específica desde la base de datos.

---

## 🧠 ¿Por qué se creó este proyecto?

Este proyecto se desarrolló como parte de una práctica de programación con Java y MySQL, con los siguientes objetivos:

- Aplicar el patrón de diseño **MVC (Modelo - Vista - Controlador)** en una aplicación real.
- Integrar **Java Swing** con **MySQL** utilizando **JDBC** para la manipulación de datos.
- Desarrollar un sistema de gestión de carnets universitarios.
- Crear una interfaz de usuario simple y funcional para interactuar con la base de datos de forma eficiente.

---

## 👤 Autor

- **Nombre del Autor**: [Tu Nombre Aquí]
- **Correo Electrónico**: [tu.email@dominio.com]
- **Año de Creación**: 2025

---

## 📜 Licencia

Este proyecto es de libre uso y distribución bajo fines educativos y académicos.
````
