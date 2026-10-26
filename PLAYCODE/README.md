# PLAYVERSE — Quiz Quest + Code Arena

Java Spring Boot application with solo quizzes, shared-question quiz duels, Java/Python coding missions, coding duels, player lobby, and leaderboard.

## Important multiplayer setup

Both players must open the same deployed service URL and use different usernames. The lobby refreshes automatically. The invited player accepts the challenge; the sender chooses the topic and starts the match; the invited player is then moved into the same match automatically. Both players get the same question set/problem and start timestamp.

Active online players, invitations, and matches are stored in server memory. Keep this Render service at one instance; restarting/redeploying clears active matches and online status. Quiz score history is stored in MySQL.

## Deploy to Render (recommended: Docker)

1. Push the contents of the `PLAYCODE` folder to a GitHub repository.
2. In Render choose **New + → Blueprint** or **New + → Web Service** and select the repository. Set runtime to **Docker** and Dockerfile path to `./Dockerfile`.
3. Configure the MySQL database environment variables in Render: `DB_HOST`, `DB_PORT` (usually `3306`), `DB_NAME`, `DB_USER`, and `DB_PASSWORD`. Use a reachable MySQL provider; do not use localhost for a cloud database.
4. Deploy. The Docker image installs JDK 17 and Python 3, so the coding runner can find `javac`, `java`, and `python3`.
5. Open the generated Render URL in two separate browsers/devices and log in with two different usernames to test duels.

## Run locally (Windows)

Install JDK 17+, Maven 3.9+, Python 3, and MySQL 8+. Create database `playcode`, configure credentials in `src/main/resources/application.properties`, then run `mvn spring-boot:run` from this folder and open `http://localhost:8080`.

## Coding execution security warning

This project runs submitted code as child processes on the application server. The Dockerfile provides the required runtimes but is **not a security sandbox**. For a public production service, use a properly isolated code execution service/container with CPU, memory, network, and time limits.
