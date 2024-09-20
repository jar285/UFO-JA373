# Twelve‐Factor App

The Twelve-Factor App methodology is a set of best practices for building modern, cloud-native applications. Created by Adam Wiggins, it is widely regarded as a standard for developing scalable, reliable, and maintainable software applications. In this article, I will introduce you to the twelve factors that are essential for building an effective cloud-native application. Additionally, this methodology is specifically designed for SaaS applications and utilizes declarative formats for configuration automation, which minimizes the time and cost associated with onboarding new developers to the project.

![image](https://github.com/user-attachments/assets/b6368f23-64ec-4e26-96e5-ea1b8b4b17d6)

1. **Codebase:** An application should have a single codebase that is tracked in a version control system, and can be deployed to multiple environments. The codebase is unique for each application, but can have multiple deployments.

2. **Dependencies:** The application should explicitly declare its dependencies and run in an isolated environment. This ensures that the application is portable and does not depend on the configuration of the system it runs on.

3. **Config:** Application configuration should be separated from code. Configuration, such as database credentials and external service URLs, should be managed through environment variables.

4. **Backing Services**: Backing services (such as databases, message queues, and caches) should be treated as resources connected through a network interface. These services should be able to be swapped out without changing the application code.

5. **Build, Release, Run:** The application lifecycle should be clearly separated into three stages: build, release, and run. This allows for controlled and predictable deployment.

6. **Processes:** The application should run as one or more stateless processes. This means that the application should be able to handle storing sessions and other temporary data outside of the process.

7. **Port Binding:** The application should export services through ports and not rely on a web server or external infrastructure to handle requests. The application should self-manage the routing of requests.

8. **Concurrency:** The application should be able to scale by running multiple instances of concurrent processes. This allows it to handle larger workloads and improve availability.

9. **Disposability:** Processes should be disposable, meaning they should start quickly and shut down in an orderly manner. This makes deployment and fault management easier.

10. **Dev/Prod Parity:** The development environment and production environment should be as similar as possible to avoid problems when deploying the application. This includes using similar data and configurations.

11. **Logs:** The application should generate event logs and not worry about how they are stored. Logs should be sent to a log management system that handles retention and analysis.

12. **Admin Processes:** Administrative processes, such as database migrations or maintenance scripts, should be executed on an ad-hoc basis and be part of the application lifecycle.