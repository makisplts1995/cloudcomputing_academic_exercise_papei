<div align="center">

  <h1>Cloud-Native Microservices Architecture</h1>
  <h3>Cloud Computing and Advanced Application Architectures</h3>
  <p><em>Rick and Morty Themed Implementation</em></p>
  
  <br />

![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)
![Nginx](https://img.shields.io/badge/nginx-%23009639.svg?style=for-the-badge&logo=nginx&logoColor=white)
![Redis](https://img.shields.io/badge/redis-%23DD0031.svg?style=for-the-badge&logo=redis&logoColor=white)
![CouchDB](https://img.shields.io/badge/CouchDB-E42528?style=for-the-badge&logo=Apache%20CouchDB&logoColor=white)
![Budibase](https://img.shields.io/badge/Budibase-%23000000.svg?style=for-the-badge&logo=budibase&logoColor=white)
![PowerShell](https://img.shields.io/badge/PowerShell-%235391FE.svg?style=for-the-badge&logo=powershell&logoColor=white)
![Curl](https://img.shields.io/badge/curl-%23073555.svg?style=for-the-badge&logo=curl&logoColor=white)

</div>

<br />

A scalable, microservices-based web application for exploring the Rick and Morty multiverse and managing favorite characters. This project demonstrates a cloud-native architecture using **Docker Compose**, **Nginx**, **Budibase**, **CouchDB**, and **Redis**.

## 📂 Project Structure

The application is organized into distinct subdirectories for optimal resource management:

- **`Infrastructure/`**: Contains infrastructure configuration files (`compose.yaml`, `.env`, `.env.example`, `nginx.conf`).
- **`Data Context/`**: Includes subfolders `mock-api` & `mock-api-2` with character data (`db.json`) and corresponding Dockerfiles.
- **`App Export/`**: Contains the `.tar.gz` file for importing the pre-built application into the Budibase environment.
- **`Persistent Storage/`**: Folders for persistent data storage for CouchDB and Budibase.
- **`Documentation/`**: Contains the detailed project report (`ΑΝΑΦΟΡΑ_ΕΡΓΑΣΙΑΣ.pdf`).

## 🚀 Features

- **Character Explorer**: Browse the full cast using the API.
- **Family Interactions**: Dynamic interaction with characters using Groq AI.
- **Favorites Collection**: Persist your favorite characters locally via CouchDB.
- **Microservices**: Decoupled architecture (Budibase, CouchDB, Redis, Nginx).
- **Mock Context**: Custom mock server data for application context.

## 🏗️ Architecture

| Service       | Technology  | Description                   |
| :------------ | :---------- | :---------------------------- |
| **Gateway**   | Nginx       | Single entry point (Port 80). |
| **UI/Logic**  | Budibase    | Frontend and business logic.  |
| **Database**  | CouchDB     | NoSQL database for favorites. |
| **Cache**     | Redis       | Session state management.     |
| **Mock APIs** | JSON Server | Static data providers.        |
| **Ops**       | Portainer   | Container management.         |

## ⚡ Quick Start

### 1. Prerequisites

- Docker Desktop installed and running.

### 2. Execution

Open a terminal in the project root directory and run the following command to build and start the services:

```bash
docker compose -f ./Infrastructure/compose.yaml up --build -d
```

- The `-f` parameter specifies the orchestration file location.
- The `--build` parameter ensures local images are built correctly.

### 3. Service Access

Once the containers are running, you can access the services via the following URLs:

- **Budibase UI**: [http://localhost/](http://localhost/)
- **CouchDB Fauxton GUI**: [http://localhost:5984/\_utils/](http://localhost:5984/_utils/)
- **Nginx Proxy**: [http://localhost/](http://localhost/)
- **Portainer**: [http://localhost/portainer/](http://localhost/portainer/)
- **Mock APIs**:
  - [http://localhost/mock-api/v1/](http://localhost/mock-api/v1/)
  - [http://localhost/mock-api/v2/](http://localhost/mock-api/v2/)

## ⚙️ Configuration & Setup

### Database Setup

The `favourites` database is automatically created during container startup via the `couchdb-init` service. No manual action is required in Fauxton.

### Application Import (Budibase)

1.  **Access Budibase**: Go to [http://localhost/](http://localhost/).
2.  **Create Account**: Create an admin account if prompted.
3.  **Import App**:
    - Select **"Create New App"** -> **"Import"**.
    - Upload the `.tar.gz` file located in the `App Export/` folder.
    - The app will automatically connect to CouchDB using credentials from the `.env` file.

### Groq API Setup (AI Functionality)

To enable the interactive AI features (powered by Llama 3.3-70b-versatile), you need to configure the Groq API key manually.

**Step 1: Get a Groq API Key**

1.  Visit [https://console.groq.com/keys](https://console.groq.com/keys).
2.  Login or Sign up.
3.  Click **"Create API Key"**.
4.  Name it (e.g., "Budibase App") and click "Submit".
5.  **Copy the key** (starting with `gsk_`). _Note: You won't see it again._

**Step 2: Configure in Budibase**

1.  Open your imported Budibase App and go to the **"Design"** tab.
2.  Navigate to **"Data Sources"** and select the REST Connector named **"Groq"**.
3.  In the **Authentication** section, find the Token field.
4.  Replace the placeholder text `YOUR_API_KEY_HERE` with your actual API Key.
5.  Click **Update** and **Save**.
6.  (Optional) Click **Publish** to apply changes to the live app.

> **Note**: Environment variables for the API Token were intentionally avoided because the Open Source version of Budibase has limited/paid access to environment variables via the UI. The Manual Auth Token method ensures reliable portability.

## 🔒 Security Notes

- **Credentials**: Default credentials (`admin`/`admin`) are used in the `.env` file for demonstration purposes. In a production environment, these should be replaced and managed via Docker Secrets.

## 📄 License

Academic exercise for the "Cloud Computing and Advanced Application Architectures" course.
