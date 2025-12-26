# Todo List Application

A full-stack todo list application built with FastAPI backend and Docker containerization, featuring MongoDB for data persistence.

## 🚀 Features

- Create, read, update, and delete todo lists
- Add, remove, and check/uncheck todo items
- RESTful API architecture
- MongoDB database for persistent storage
- Docker Compose for easy deployment
- Nginx reverse proxy setup

## 🛠️ Technology Stack

### Backend
- **Python 3.12** - Programming language
- **FastAPI** - Modern web framework for building APIs
- **Motor** - Async MongoDB driver
- **Pydantic** - Data validation and settings management
- **Uvicorn** - ASGI server

### Database
- **MongoDB Atlas** - Cloud-hosted MongoDB database

### Infrastructure
- **Docker & Docker Compose** - Containerization
- **Nginx** - Reverse proxy server
- **Node.js 22** - Frontend runtime

## 📋 Prerequisites

Before running this application, ensure you have the following installed:

- [Docker](https://docs.docker.com/get-docker/) (version 20.10 or higher)
- [Docker Compose](https://docs.docker.com/compose/install/) (version 2.0 or higher)
- A MongoDB Atlas account or local MongoDB instance

## ⚙️ Setup

### 1. Clone the Repository

```bash
git clone https://github.com/iamthefamous/todo-list.git
cd todo-list
```

### 2. Configure Environment Variables

The `.env` file should contain your MongoDB connection string:

```env
MONGODB_URI=mongodb+srv://<username>:<password>@<cluster-url>/<database>?appName=<app-name>
```

**Note:** Update the MongoDB URI with your own credentials.

### 3. Build and Run with Docker Compose

```bash
docker-compose up --build
```

This will start three services:
- **Backend**: FastAPI server on port 3001
- **Frontend**: Node.js server on port 3000
- **Nginx**: Reverse proxy on port 8000

## 🌐 Accessing the Application

Once the containers are running:

- **Application**: http://localhost:8000
- **Backend API**: http://localhost:8000/api
- **Frontend** (direct): http://localhost:3000
- **Backend** (direct): http://localhost:3001

## 📚 API Documentation

### Todo Lists

#### Get All Lists
```http
GET /api/lists
```
Returns a list of all todo lists with summary information.

**Response:**
```json
[
  {
    "id": "string",
    "name": "string",
    "item_count": 0
  }
]
```

#### Create New List
```http
POST /api/lists
```

**Request Body:**
```json
{
  "name": "string"
}
```

**Response:**
```json
{
  "id": "string",
  "name": "string"
}
```

#### Get Single List
```http
GET /api/lists/{list_id}
```

**Response:**
```json
{
  "id": "string",
  "name": "string",
  "items": [
    {
      "id": "string",
      "label": "string",
      "checked": false
    }
  ]
}
```

#### Delete List
```http
DELETE /api/lists/{list_id}
```

**Response:** `true` or `false`

### Todo Items

#### Create Item
```http
POST /api/lists/{list_id}/items/
```

**Request Body:**
```json
{
  "label": "string"
}
```

**Response:** Returns the updated todo list object.

#### Delete Item
```http
DELETE /api/lists/{list_id}/items/{item_id}
```

**Response:** Returns the updated todo list object.

#### Update Item Checked State
```http
PATCH /api/lists/{list_id}/checked_state
```

**Request Body:**
```json
{
  "item_id": "string",
  "checked_state": true
}
```

**Response:** Returns the updated todo list object.

## 📁 Project Structure

```
todo-list/
├── backend/
│   ├── src/
│   │   ├── server.py       # FastAPI application and endpoints
│   │   └── dal.py          # Data Access Layer for MongoDB
│   ├── Dockerfile          # Backend container configuration
│   ├── requirements.txt    # Python dependencies
│   └── pyproject.toml      # Python project configuration
├── frontend/               # Frontend application files
├── nginx/
│   └── nginx.conf          # Nginx reverse proxy configuration
├── compose.yaml            # Docker Compose configuration
├── .env                    # Environment variables (not in git)
├── package.json            # Node.js dependencies
└── README.md               # This file
```

## 🔧 Development

### Running Backend Locally

```bash
cd backend
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt
export MONGODB_URI="your_mongodb_uri"
export DEBUG=true
python src/server.py
```

### Debugging

Set the `DEBUG` environment variable to `true` in the `.env` file or docker-compose configuration to enable:
- Auto-reload on code changes
- Detailed error messages
- FastAPI debug mode

## 🔒 Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `MONGODB_URI` | MongoDB connection string | Required |
| `DEBUG` | Enable debug mode | `false` |

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📝 License

This project is open source and available under the [MIT License](LICENSE).

## 👤 Author

**iamthefamous**

- GitHub: [@iamthefamous](https://github.com/iamthefamous)

## 🐛 Known Issues

- Frontend directory is currently empty and needs implementation
- MongoDB credentials should not be committed to version control (use `.env` file)

## 🚧 Future Enhancements

- [ ] Add frontend implementation (React/Vue/Angular)
- [ ] Add user authentication and authorization
- [ ] Add unit and integration tests
- [ ] Add CI/CD pipeline
- [ ] Add data validation and error handling improvements
- [ ] Add API rate limiting
- [ ] Add logging and monitoring
