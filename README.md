# Seykoc - Corporate Social Network API

A production-ready, scalable RESTful backend API for a corporate social network built with Node.js, Express.js, and MySQL.

## 🏗️ Architecture

```
src/
├── config/           # Environment & app configuration
├── controllers/      # Request handlers (thin layer)
├── database/         # Connection pool, migrations, seeds
├── middleware/        # Auth, error handling, validation, upload
├── models/           # Database access layer (SQL queries)
├── routes/           # Route definitions & middleware wiring
├── services/         # Business logic layer
├── utils/            # ApiError, ApiResponse, helpers
├── validators/       # express-validator rules
├── app.js            # Express app setup
└── server.js         # Entry point
```

## 🚀 Quick Start

### Prerequisites
- Node.js 18+
- MySQL 8.0+

### Setup

1. **Configure environment:**
   ```bash
   # Edit .env with your MySQL credentials
   cp .env.example .env
   ```

2. **Install dependencies:**
   ```bash
   npm install
   ```

3. **Run migrations (auto-runs on start too):**
   ```bash
   npm run db:migrate
   ```

4. **Seed demo data (optional):**
   ```bash
   npm run db:seed
   ```

5. **Start the server:**
   ```bash
   # Development (with hot-reload)
   npm run dev

   # Production
   npm start
   ```

### Demo Credentials
| Role  | Email              | Password      |
|-------|--------------------|---------------|
| Admin | admin@seykoc.com   | Password123!  |
| User  | john@seykoc.com    | Password123!  |

## 📡 API Endpoints

### Auth
| Method | Endpoint                    | Auth | Description         |
|--------|-----------------------------|------|---------------------|
| POST   | `/api/auth/register`        | No   | Register new user   |
| POST   | `/api/auth/login`           | No   | Login               |
| POST   | `/api/auth/refresh`         | No   | Refresh token       |
| POST   | `/api/auth/logout`          | No   | Logout              |
| POST   | `/api/auth/change-password` | Yes  | Change password     |
| GET    | `/api/auth/me`              | Yes  | Get current user    |

### Users
| Method | Endpoint                       | Auth  | Description           |
|--------|--------------------------------|-------|-----------------------|
| GET    | `/api/users`                   | Yes   | List all users        |
| GET    | `/api/users/search?q=`         | Yes   | Search users          |
| GET    | `/api/users/:uuid`             | Yes   | Get user profile      |
| PUT    | `/api/users/profile`           | Yes   | Update own profile    |
| PUT    | `/api/users/avatar`            | Yes   | Upload avatar         |
| PUT    | `/api/users/:uuid/role`        | Admin | Change user role      |
| PUT    | `/api/users/:uuid/deactivate`  | Admin | Deactivate user       |
| PUT    | `/api/users/:uuid/activate`    | Admin | Activate user         |

### Posts
| Method | Endpoint                          | Auth | Description        |
|--------|-----------------------------------|------|--------------------|
| POST   | `/api/posts`                      | Yes  | Create post        |
| GET    | `/api/posts`                      | Yes  | Get feed           |
| GET    | `/api/posts/:uuid`                | Yes  | Get single post    |
| PUT    | `/api/posts/:uuid`                | Yes  | Update post        |
| DELETE | `/api/posts/:uuid`                | Yes  | Delete post        |
| POST   | `/api/posts/:uuid/like`           | Yes  | Like post          |
| DELETE | `/api/posts/:uuid/like`           | Yes  | Unlike post        |
| GET    | `/api/posts/:uuid/likes`          | Yes  | Get post likes     |
| POST   | `/api/posts/:uuid/comments`       | Yes  | Add comment        |
| GET    | `/api/posts/:uuid/comments`       | Yes  | Get comments       |
| DELETE | `/api/posts/comments/:commentId`  | Yes  | Delete comment     |

### Messages
| Method | Endpoint                                          | Auth | Description          |
|--------|---------------------------------------------------|------|----------------------|
| `POST` | `/api/messages/send`                              | Yes  | Send direct message  |
| `GET`  | `/api/messages/:userId`                           | Yes  | Get chat history     |
| `GET`  | `/api/messages/conversations`                     | Yes  | List conversations   |
| `POST` | `/api/messages/conversations/direct`              | Yes  | Start DM             |
| `POST` | `/api/messages/conversations/group`               | Yes  | Create group chat    |
| `GET`  | `/api/messages/conversations/:uuid/messages`      | Yes  | Get messages         |
| `POST` | `/api/messages/conversations/:uuid/messages`      | Yes  | Send message         |
| `GET`  | `/api/messages/conversations/:uuid/participants`  | Yes  | Get participants     |

### Notifications
| Method | Endpoint                            | Auth | Description        |
|--------|-------------------------------------|------|--------------------|
| GET    | `/api/notifications`                | Yes  | List notifications |
| GET    | `/api/notifications/unread-count`   | Yes  | Unread count       |
| PUT    | `/api/notifications/read-all`       | Yes  | Mark all read      |
| PUT    | `/api/notifications/:id/read`       | Yes  | Mark one read      |
| DELETE | `/api/notifications/:id`            | Yes  | Delete notification|

### Announcements
| Method | Endpoint                      | Auth  | Description           |
|--------|-------------------------------|-------|-----------------------|
| GET    | `/api/announcements`          | Yes   | List announcements    |
| GET    | `/api/announcements/:uuid`    | Yes   | Get one               |
| POST   | `/api/announcements`          | Admin | Create announcement   |
| PUT    | `/api/announcements/:uuid`    | Admin | Update announcement   |
| DELETE | `/api/announcements/:uuid`    | Admin | Delete announcement   |

## 🔒 Security Features
- **bcrypt** password hashing (12 salt rounds)
- **JWT** access + refresh token rotation
- **Helmet** HTTP security headers
- **CORS** configuration
- **Rate limiting** (100 req/15min general, 20 req/15min auth)
- **Input validation** via express-validator
- **SQL injection prevention** via parameterized queries

## License
MIT
