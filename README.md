# 🛸 Rick and Morty Cloud-Native Explorer

![Docker](https://img.shields.io/badge/Docker-2CA5E0?style=for-the-badge&logo=docker&logoColor=white)
![Nginx](https://img.shields.io/badge/nginx-009639?style=for-the-badge&logo=nginx&logoColor=white)
![Budibase](https://img.shields.io/badge/Budibase-000000?style=for-the-badge&logo=budibase&logoColor=white)
![Redis](https://img.shields.io/badge/redis-%23DD0031.svg?style=for-the-badge&logo=redis&logoColor=white)
![CouchDB](https://img.shields.io/badge/CouchDB-CW?style=for-the-badge&logo=apachecouchdb&logoColor=red)

A scalable, containerized web application that allows users to explore the Rick and Morty multiverse, manage their favorite characters, and interact with them using Generative AI.

## 🌟 Key Features

- **Character Explorer**: Browse the full cast of the show using the [Rick and Morty API](https://rickandmortyapi.com/).
- **AI "Family Judge"**: Interaction with characters where Rick, Morty, or other family members "judge" your choices using the **Groq LLM**.
- **Favorites Collection**: Persist your favorite characters in a local **CouchDB** database.
- **Microservices Architecture**: Fully decoupled services for UI, Data, Caching, and Logic.
- **Mock APIs**: Custom mock servers for landing page content and AI context.

## 🏗️ Architecture

The project is built on a **Microservices Architecture** orchestrated by **Docker Compose**:

| Service        | Technology  | Description                                                        |
| :------------- | :---------- | :----------------------------------------------------------------- |
| **Gateway**    | Nginx       | Single entry point (Port 80) routing traffic to internal services. |
| **UI/Logic**   | Budibase    | Low-code platform handling the frontend and business logic.        |
| **Database**   | CouchDB     | NoSQL database for storing user favorites.                         |
| **Cache**      | Redis       | In-memory store for session management and performance.            |
| **Mock APIs**  | JSON Server | Provides static context (Family config, Landing page data).        |
| **Management** | Portainer   | Container management GUI.                                          |

## 📂 Project Structure

```
├── App Export/           # Application export archives (.tar.gz)
├── Data Context/         # Static data for Mock APIs (JSON files)
├── Documentation/        # Academic reports and manuals
├── Infrastructure/       # Docker configuration (compose.yaml, nginx.conf)
└── Persistent Storage/   # Persisted data volumes (Database, Redis)
```

## 🚀 Getting Started

### Prerequisites

- **Docker Desktop** (running)
- **Git**

### Installation

1.  **Clone the repository:**

    ```bash
    git clone <repository-url>
    cd <repository-folder>
    ```

2.  **Navigate to the Infrastructure setup:**

    ```bash
    cd Infrastructure
    ```

3.  **Start the services:**

    ```bash
    docker compose up -d --build
    ```

4.  **Access the Application:**
    - **Main App:** [http://localhost](http://localhost)
    - **Portainer (Manager):** [http://localhost:9000](http://localhost:9000)
    - **Budibase Builder:** [http://localhost:10000](http://localhost:10000)

## 🔧 Configuration

The application is pre-configured with default credentials for development:

- **CouchDB**: `admin` / `admin`
- **Ports**: Exposed in `Infrastructure/compose.yaml` (80, 5984, 6379, 10000).

## 📄 License

This project is an academic exercise for the "Cloud Computing and Advanced Application Architectures" course at the University of Piraeus.
