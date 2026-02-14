# Project Development & Architecture Documentation

## 1. Project Creation
This project was initialized as a **Spring Boot** application using standard tools (like Spring Initializr or IDE wizards).

**Steps taken:**
1.  **Initialization**: We selected 'Maven' as the build tool, 'Java' as the language, and 'Spring Boot 3.x' as the framework version.
2.  **Dependencies**: We added `spring-boot-starter-web` to enable web capabilities (Tomcat server, REST support) and `spring-boot-devtools` for faster development.
3.  **Structure**: The project follows the standard Maven directory structure:
    *   `src/main/java`: Backend Java code.
    *   `src/main/resources`: Configuration and static assets.
    *   `src/test`: Unit tests.

## 2. Technology Stack & Justification

### Backend: Java & Spring Boot
*   **Why**: Spring Boot is the industry standard for enterprise-grade Java applications. It provides "opinionated defaults," meaning it sets up a production-ready server (Tomcat) with minimal configuration.
*   **Use**: functionality.
    *   **Auto-Configuration**: Spring Boot automatically scans our project and configures the web server, ensuring `steps` like handling HTTP requests are managed without writing boilerplate code.
    *   **Scalability**: While currently serving a portfolio, this stack allows for easy expansion (e.g., adding a database or complex business logic) without rewriting the core architecture.

### Build Tool: Maven
*   **Why**: Dependency management.
*   **Use**: It handles downloading all the libraries we need (like Spring Web) and manages the build lifecycle (compiling, packaging into JAR).

### Frontend: HTML5, CSS3, JavaScript (Vanilla)
*   **Why**: Performance and Control.
*   **Use**:
    *   **HTML**: Semantic structure of the pages (`index.html`, `projects.html`).
    *   **CSS**: Custom variables (`:root`) and flexbox/grid layouts allow for a unique "Neon Dark Mode" aesthetic that would be harder to customize with a rigid framework like Bootstrap.
    *   **JavaScript**: Validates user interactions (like contact forms) and handles dynamic UI effects (custom cursor, scroll animations) without the overhead of a heavy Single Page Application (SPA) framework like React/Angular for this specific use case.

## 3. API & Architecture Building

### How the "API" Works
In this specific project context, we are using Spring Boot's **Static Resource Handling** capabilities rather than writing custom REST Controllers (like `@RestController`).

1.  **Request Handling**:
    *   When a user requests `http://localhost:8080/`, the request hits the embedded **Tomcat Web Server**.
    *   Spring Boot's `DispatcherServlet` receives this request.
    *   Since we placed our HTML files in `src/main/resources/static`, Spring Boot automatically maps the root URL `/` to `index.html`.
    *   Similarly, `/projects.html` serves the projects page.

2.  **Extensibility (Building Custom APIs)**:
    *   If we wanted to verify form data or fetch real-time data, we would create a **Controller Class**:
        ```java
        @RestController
        @RequestMapping("/api")
        public class PortfolioController {
            @GetMapping("/projects")
            public List<Project> getProjects() {
                // Return JSON data
            }
        }
        ```
    *   This separation allows the frontend to be decoupled from the backend logic.

## 4. Deployment Pipeline
1.  **Version Control**: We use **Git** to track changes.
2.  **Hosting**: The static content is pushed to **GitHub Pages** (or a cloud provider like Render via Dockerfile if using the full Java backend). The current setup is optimized for standard web server deployment.
