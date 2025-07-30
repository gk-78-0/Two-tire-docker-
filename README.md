# Quotes App – Flask + MySQL (Dockerized)

This project is a simple two-tier Quotes application that demonstrates networking between containers using Docker Compose. The backend is built with Flask (Python) and connects to a MySQL database. The app allows users to view and add quotes via a REST API.

## Features

- **RESTful API** to view and add quotes.
- **Flask** as the web application framework.
- **MySQL** as the database.
- **Docker Compose** for easy multi-container management.
- **Demonstrates container networking** (Flask + MySQL in separate containers).

## Project Structure

```
quotes-app/
├── app/
│   ├── app.py
│   ├── requirements.txt
│   └── config.py
├── db/
│   └── init.sql
├── Dockerfile
├── docker-compose.yml
└── README.md
```

## Getting Started

### Prerequisites

- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)

### Setup & Run

1. **Clone the repository**  
   ```bash
   git clone <repo-url>
   cd quotes-app
   ```

2. **Build and start the services**
   ```bash
   docker-compose up --build
   ```
   This will:
   - Build the Flask app image.
   - Start both the Flask app and MySQL database containers.
   - Initialize the database with sample data.

3. **Access the API**
   - Flask app: [http://localhost:5000](http://localhost:5000)

## API Endpoints

### Get all quotes

```
GET /quotes
```
Example:
```bash
curl http://localhost:5000/quotes
```

### Add a new quote

```
POST /quotes
```
JSON body:
```json
{
  "quote": "Networking rocks!"
}
```
Example:
```bash
curl -X POST -H "Content-Type: application/json" -d '{"quote":"Networking rocks!"}' http://localhost:5000/quotes
```

## How it Works

- **Flask app** connects to the MySQL database using environment variables for host, user, password, and database name.
- **MySQL container** is initialized with a script (`init.sql`) that creates the `quotes_db` database and a simple `quotes` table.
- **Docker Compose** creates a bridge network so the web app can access the database using the service name `db` as the host.

## Networking Showcase

This setup demonstrates Docker container networking. The Flask app (`web` service) communicates with the MySQL database (`db` service) over Docker's default bridge network using the service name.

## Stopping the App

To stop and remove containers, run:
```bash
docker-compose down
```

## Customization

- Update the `db/init.sql` file to add more initial quotes.
- Extend `app/app.py` to add, edit, or delete quotes.

## License

MIT

---

**Happy Coding!**