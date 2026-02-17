# Mini-RAG Implementation 

This project is a comprehensive implementation of the **"Mini-RAG"** course by **Eng. Abu Bakr Soliman**.

The goal of this project is to move beyond simple Jupyter Notebooks and build a **production-ready Retrieval-Augmented Generation (RAG) application** using software engineering best practices. It covers the full pipeline from file uploading to generating answers based on documents.

**Course Source:** [Abu Bakr Soliman YouTube Channel]

---

##  Architecture & Tech Stack

This project is built using a modern Python stack designed for scalability and maintainability:

*   **Core Framework:** [FastAPI](https://fastapi.tiangolo.com/) (High-performance web framework).
*   **Database:** 
    *   **PostgreSQL (PGVector):** For storing application data and vector embeddings [1].
    *   *Previously supported MongoDB & Qdrant*.
*   **Asynchronous Tasks:** [Celery](https://docs.celeryq.dev/) with **RabbitMQ** (Broker) and **Redis** (Result Backend) to handle heavy processing tasks like file chunking and embedding [2].
*   **Containerization:** **Docker** & **Docker Compose** for orchestrating all services [3].
*   **LLM Integration:** Flexible factory pattern supporting **OpenAI**, **Cohere**, and local LLMs via **Ollama** [4, 5].
*   **Monitoring:** Prometheus & Grafana for observability [6].

---

##  Key Features

1.  **File Management:** Upload documents and manage project-based assets [7].
2.  **Data Processing Pipeline:** 
    *   Text extraction and chunking.
    *   Asynchronous processing using Celery workflows [8].
3.  **Vector Store Integration:** 
    *   Embeds text using OpenAI or Cohere models.
    *   Stores vectors in PGVector for semantic search [9].
4.  **RAG Query Engine:** 
    *   Semantic search against stored documents.
    *   LLM answer generation based on retrieved context [10].
5.  **Robust Architecture:**
    *   **MVC Pattern:** Separation of concerns (Models, Views, Controllers) [11].
    *   **Alembic:** Database migration management [1].
    *   **Factory Pattern:** Easily switch between different LLM providers and Vector DBs [4, 12].

---

##  Getting Started

### Prerequisites

*   **Docker & Docker Compose** installed on your machine [3].
*   **Python 3.8+** (if running locally without Docker) [6].
*   **Git** installed [13].

### Installation

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/YOUR_USERNAME/mini-rag-implementation.git
    cd mini-rag-implementation
    ```

2.  **Environment Setup:**
    *   Copy the example environment files to create your local configurations.
    ```bash
    cp .env.example .env
    cp .env.app.example .env.app
    # Repeat for other .env files in the /env directory
    ```
    *   *Important:* Edit the `.env` files to add your API Keys (OpenAI/Cohere) and database credentials [14].

3.  **Run with Docker:**
    To spin up the entire stack (App, DB, Broker, Redis):
    ```bash
    docker-compose up --build
    ```

### Accessing the Application

Once the containers are running, you can access the services:

*   **FastAPI Docs (Swagger UI):** `http://localhost:8000/docs` (or configured port) [15].
*   **RabbitMQ Management:** `http://localhost:15672` (Default User/Pass in env).
*   **Flower (Celery Monitor):** `http://localhost:5555`.

---

## 🛠️ Project Structure

The project follows a clean structure to ensure scalability:

*   `src/`: Main application source code.
    *   `controllers/`: Logic for handling requests (Data, NLP processing) [7].
    *   `models/`: Database schemas (SQLAlchemy & Pydantic) [1].
    *   `routes/`: API endpoints definitions [16].
    *   `stores/`: Factories for LLM and Vector DB providers [4].
    *   `tasks/`: Celery tasks for background processing [2].
*   `docker/`: Docker configuration files and environment variables [3].

---

##  Contribution

This project is open for contribution! If you are following the course and want to improve the code, feel free to submit a Pull Request.

---
