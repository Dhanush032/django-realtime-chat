# 💬 Real-Time Chat Application

<div align="center">

![Python](https://img.shields.io/badge/Python-3.12-blue?style=for-the-badge&logo=python)
![Django](https://img.shields.io/badge/Django-5.2-green?style=for-the-badge&logo=django)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Database-blue?style=for-the-badge&logo=postgresql)
![WebSocket](https://img.shields.io/badge/WebSocket-Real--Time-orange?style=for-the-badge)

</div>
---

## 🎯 Project Overview

A full-stack real-time chat application demonstrating modern web development practices with Django, WebSockets, and PostgreSQL. Built as a portfolio project to showcase backend development skills and production deployment experience.

### ✨ Why This Project?

As a Python/Django developer seeking opportunities in backend development, I wanted to build something that goes beyond basic CRUD applications. This project demonstrates my ability to:

- Implement real-time communication using WebSocket protocol
- Design and optimize database architecture
- Deploy applications to production environments
- Write clean, maintainable code following industry best practices
- Solve complex technical challenges independently

---

## 🚀 Key Features

<table>
<tr>
<td width="50%">

### 💬 Real-Time Messaging
- Instant message delivery using WebSocket
- No page refresh required
- Near real-time message delivery
- Bi-directional communication

### 👥 Group Chat Rooms
- Create unlimited chat groups
- Admin controls for group management
- Member management system
- Public and private room options

</td>
<td width="50%">

### 🔒 User Authentication
- Secure signup and login
- Password encryption
- Session management
- Profile customization with avatars

### 📊 Live User Tracking
- Real-time online/offline status
- See who's in each chat room
- Activity monitoring
- Last seen timestamps

</td>
</tr>
</table>

### 🎨 Additional Features
- **Private Messaging** - One-on-one conversations between users
- **Responsive Design** - Optimized for mobile, tablet, and desktop
- **User Profiles** - Customizable profiles with bio and avatar uploads
- **Message History** - Persistent storage of all conversations
- **Admin Dashboard** - Full Django admin panel for management

---

## 🛠️ Technology Stack

### Backend
```
Python 3.12          • Core programming language
Django 5.0+           • Web framework
Django Channels      • WebSocket support
Daphne              • ASGI server
PostgreSQL          • Production database
Django Allauth      • Authentication system
```

### Frontend
```
HTML5 & CSS3        • Markup and styling
TailwindCSS         • Utility-first CSS framework
JavaScript (ES6+)   • Client-side logic
Alpine.js           • Lightweight reactivity
```



## 🎓 Technical Highlights

### Real-Time Communication Architecture
```python
# WebSocket Consumer handling instant message delivery
class ChatConsumer(AsyncWebsocketConsumer):
    async def connect(self):
        # Establish WebSocket connection
        self.chatroom_name = self.scope['url_route']['kwargs']['chatroom_name']
        await self.channel_layer.group_add(self.chatroom_name, self.channel_name)
        await self.accept()
    
    async def receive(self, text_data):
        # Process incoming messages
        data = json.loads(text_data)
        # Save to database and broadcast to all users
        await self.channel_layer.group_send(...)
```

### Database Design
```
Users ──────┐
            │
Profiles ───┤
            │
ChatGroups ─┼──── Messages
            │
            │
UserOnlineStatus
```

**Optimized with:**
- Foreign key relationships for data integrity
- Indexed fields for faster queries
- `select_related()` and `prefetch_related()` for query optimization
- Efficient schema design minimizing database hits

### Security Implementation

✅ CSRF protection on all forms  
✅ SQL injection prevention via Django ORM  
✅ XSS protection with template escaping  
✅ Secure password hashing (PBKDF2)  
✅ Environment-based secret management  
✅ HTTPS in production  
✅ Secure session cookies  

---

## 🚀 Live Demo

### Try it yourself!

**🔗 [https://realtime-chat-r818.onrender.com](https://realtime-chat-r818.onrender.com)**

**Test Features:**
1. Create a new account or login
2. Join the Public Chat room
3. Send messages and see them appear in real-time
4. Open in another browser tab to simulate multiple users
5. Check the Online Tracker to see live user activity

> **Note:** First load may take 30-60 seconds (free tier cold start)

---

## 💻 Local Installation

### Prerequisites
- Python 3.12 or higher
- Git
- PostgreSQL (optional - SQLite works for local development)

### Quick Start
```bash
# 1. Clone the repository
git clone https://github.com/yourusername/django-realtime-chat.git
cd django-realtime-chat

# 2. Create virtual environment
python -m venv venv

# Activate virtual environment
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Run migrations
python manage.py migrate

# 5. Create superuser (for admin access)
python manage.py createsuperuser

# 6. Collect static files
python manage.py collectstatic

# 7. Run development server
python manage.py runserver
```

**Open your browser:** `http://localhost:8000`

---

## 📁 Project Structure
```
realtime-chat/
│
├── a_core/                 # Main project settings
│   ├── settings.py         # Django configuration
│   ├── urls.py             # URL routing
│   ├── asgi.py             # ASGI config for WebSocket
│   └── routing.py          # WebSocket URL routing
│
├── a_rtchat/               # Chat application
│   ├── models.py           # Database models (ChatGroup, Message)
│   ├── views.py            # View logic for chat pages
│   ├── consumers.py        # WebSocket consumers
│   ├── urls.py             # App-specific URLs
│   └── templates/          # HTML templates
│
├── a_users/                # User management
│   ├── models.py           # User Profile model
│   ├── views.py            # Profile views
│   ├── forms.py            # User forms
│   └── templates/          # User templates
│
├── static/                 # Static files (CSS, JS, images)
│   ├── css/
│   ├── js/
│   └── images/
│
├── media/                  # User uploaded files
│
├── templates/              # Global templates
│   └── layouts/
│
├── requirements.txt        # Python dependencies
├── runtime.txt             # Python version
├── build.sh                # Render build script
└── manage.py               # Django CLI
```

---

## 🔧 Configuration

### Environment Variables

Create a `.env` file in the root directory:
```env
# Security
SECRET_KEY=your-secret-key-here
DEBUG=True

# Database
DATABASE_URL=postgresql://user:password@host:port/database

# Allowed Hosts
ALLOWED_HOSTS=localhost,127.0.0.1
```

### Database Configuration

The application automatically detects the environment:

- **Development:** Uses SQLite (no setup needed)
- **Production:** Uses PostgreSQL (configure `DATABASE_URL`)

---




## 🔮 Future Enhancements

**Planned Features:**
- [ ] File and image sharing in chats
- [ ] Message search functionality
- [ ] Typing indicators
- [ ] Read receipts and delivery status
- [ ] Push notifications
- [ ] Voice messages
- [ ] Message reactions (emoji)
- [ ] Dark mode theme
- [ ] End-to-end encryption
- [ ] Group video calls
- [ ] Message editing and deletion
- [ ] User blocking and reporting

---


## 📚 Resources & Learning

**Key resources that helped me build this:**

- [Django Documentation](https://docs.djangoproject.com/)
- [Django Channels Documentation](https://channels.readthedocs.io/)
- [WebSocket Protocol Specification](https://tools.ietf.org/html/rfc6455)
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)
- [TailwindCSS Documentation](https://tailwindcss.com/docs)

---



