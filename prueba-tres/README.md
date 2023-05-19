En este ejercicio se hace uso del workflow de github contenido en el directorio .github/workflows/main.yml
En el .yml se consideran cambios hechos en:
- prueba-tres/** (directorio del server)
- .github/workflows/main.yml (archivo que regula el flujo de build & deploy)

Se utilizo docker-compose para centralizar el buildeo y dar pie a la facil inclusion de nuevos servicios y herramientas.
> Nota: Quizas no era necesario para el caso pero me parece una buena práctica y facilita a un solo comando (docker-compose up -d --build) el buildeo y deploy de la app.