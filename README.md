# Notes App Backend with Hapi.js

This project is a simple **Notes App Backend** built using the **Hapi.js framework**. It provides a CRUD (Create, Read, Update, Delete) API for managing notes. The project is part of the [Dicoding Course: Belajar Membuat Aplikasi Back-End untuk Pemula dengan Google Cloud](https://www.dicoding.com/academies/342).

## Features
- **Add Notes**: Add new notes with a title, tags, and body.
- **View Notes**: Retrieve all notes or a specific note by its ID.
- **Edit Notes**: Update the details of an existing note.
- **Delete Notes**: Remove a note by its ID.

## Tech Stack
- **Runtime**: [Node.js](https://nodejs.org/)
- **Framework**: [Hapi.js](https://hapi.dev/)
- **Database**: In-memory storage (for simplicity)
- **Hosting**: Google Compute Engine VM (GCP)

---

## Getting Started

### Prerequisites
- **Local Development**:
  - Node.js (version 18 or above recommended)
  - npm (comes with Node.js)
- **VM Deployment**:
  - Google Cloud Platform account
  - Google Compute Engine VM instance set up with SSH access

---

### Installation (Local)
1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/notes-app-backend.git
   cd notes-app-backend
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Start the server:
   ```bash
   npm run start-dev
   ```

4. Test the API using tools like Postman or curl.

---

### Running on Google Compute Engine VM
1. SSH into your VM instance:
   ```bash
   gcloud compute ssh <vm-instance-name>
   ```

2. Clone the repository on the VM:
   ```bash
   git clone https://github.com/your-username/notes-app-backend.git
   cd notes-app-backend
   ```

3. Install Node.js and npm on the VM:
   ```bash
   sudo apt update
   sudo apt install -y nodejs npm
   ```

4. Install dependencies:
   ```bash
   npm install
   ```

5. Start the server (binding to all interfaces for external access):
   ```bash
   HOST=0.0.0.0 PORT=5000 npm start
   ```

6. Configure your firewall rules to allow traffic on the server port (e.g., `5000`).

---

## API Documentation

### Add Note
```http
/POST /notes
```
| Parameter | Type     | Description                          |
| :-------- | :------- | :----------------------------------- |
| `title`   | `string` | **Required**. Title of the note      |
| `tags`    | `array`  | **Optional**. Tags for the note      |
| `body`    | `string` | **Required**. Content of the note    |

**Response**:
```json
{
  "status": "success",
  "message": "Catatan berhasil ditambahkan",
  "data": {
    "noteId": "note-12345"
  }
}
```

---

### Get All Notes
```http
/GET /notes
```
No parameters required.

**Response**:
```json
{
  "status": "success",
  "data": {
    "notes": [
      {
        "id": "note-12345",
        "title": "Sample Note",
        "tags": ["tag1", "tag2"],
        "body": "This is the content of the note.",
        "createdAt": "2024-11-28T12:00:00.000Z",
        "updatedAt": "2024-11-28T12:00:00.000Z"
      }
    ]
  }
}
```

---

### Get Note by ID
```http
/GET /notes/{id}
```
| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `id`      | `string` | **Required**. ID of the note      |

**Response (Success)**:
```json
{
  "status": "success",
  "data": {
    "note": {
      "id": "note-12345",
      "title": "Sample Note",
      "tags": ["tag1", "tag2"],
      "body": "This is the content of the note.",
      "createdAt": "2024-11-28T12:00:00.000Z",
      "updatedAt": "2024-11-28T12:00:00.000Z"
    }
  }
}
```

**Response (Not Found)**:
```json
{
  "status": "fail",
  "message": "Catatan tidak ditemukan"
}
```

---

### Edit Note
```http
/PUT /notes/{id}
```
| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `id`      | `string` | **Required**. ID of the note      |
| `title`   | `string` | **Required**. Updated title       |
| `tags`    | `array`  | **Optional**. Updated tags        |
| `body`    | `string` | **Required**. Updated content     |

**Response (Success)**:
```json
{
  "status": "success",
  "message": "Catatan berhasil diperbarui"
}
```

**Response (Not Found)**:
```json
{
  "status": "fail",
  "message": "Gagal memperbarui catatan. Id tidak ditemukan"
}
```

---

### Delete Note
```http
DELETE /notes/{id}
```
| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `id`      | `string` | **Required**. ID of the note      |

**Response (Success)**:
```json
{
  "status": "success",
  "message": "Catatan berhasil dihapus"
}
```

**Response (Not Found)**:
```json
{
  "status": "fail",
  "message": "Catatan gagal dihapus. Id tidak ditemukan"
}
```

---
