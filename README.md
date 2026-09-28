# ClassConnect

**ClassConnect** is a web application for CUNY students that automatically creates group chats for every course. It solves the problem of inconsistent, student-made WhatsApp groups by ensuring every course has a dedicated chat, accessible only to verified CUNY students.

## 🎯 Problem

CUNY students often rely on student-made WhatsApp group chats for communication, class updates, and collaboration. However, these chats are created inconsistently. If no student takes initiative, then no group chat exists, leaving students disconnected and without an easy way to share resources or support each other.

## ✨ Solution

ClassConnect automatically generates a class group chat for each course. When students enroll in a class, they can join the chat for their courses. Students can choose whether to join, ensuring that every course has a consistent communication option without depending on individuals to create it.

## 🚀 Features

### Core Functionality
- **Automatic Course Chats**: Every CUNY course has a dedicated group chat
- **CUNY Email Authentication**: Only verified CUNY students can register and access chats
- **Email Verification**: Required before accessing protected pages
- **Course Browser**: Browse and search courses from all CUNY colleges
- **Real Course Data**: Displays actual courses scraped from CUNY Global Search
- **Secure Access**: Only enrolled and verified students can access course chats

### Chat Features
- **Real-time Messaging**: Send and receive messages in course group chats
- **Course Resources**: Share helpful links, study materials, and resources
- **Polls**: Create polls to get quick feedback from classmates
- **Persistent Storage**: All messages and data are stored securely

## 🛠️ Tech Stack

- **Frontend**: Next.js 16 (App Router), React 19, TypeScript
- **Styling**: Tailwind CSS
- **Backend**: Firebase (Authentication, Firestore)
- **Data Scraping**: Python, Selenium
- **Deployment**: Vercel-ready

## 📋 Prerequisites

- Node.js 18+ and npm
- Firebase project with Authentication and Firestore enabled
- Python 3.8+ (for course scraping)

## 🔧 Setup

### 1. Clone the Repository

```bash
git clone <repository-url>
cd Class-Connect
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Configure Firebase

1. Create a Firebase project at [Firebase Console](https://console.firebase.google.com/)
2. Enable **Authentication** (Email/Password)
3. Enable **Cloud Firestore**
4. Get your Firebase configuration from Project Settings
5. Create a `.env.local` file in the root directory:

```env
NEXT_PUBLIC_FIREBASE_API_KEY=your_api_key
NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN=your_auth_domain
NEXT_PUBLIC_FIREBASE_PROJECT_ID=your_project_id
NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET=your_storage_bucket
NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID=your_messaging_sender_id
NEXT_PUBLIC_FIREBASE_APP_ID=your_app_id
```

6. Download your Firebase service account key:
   - Go to Project Settings → Service Accounts
   - Click "Generate New Private Key"
   - Save as `scripts/serviceAccountKey.json`

### 4. Import Course Data

1. Scrape courses (optional - if you need to update course data):
   ```bash
   python scripts/scrape_course.py
   ```

2. Import courses to Firestore:
   ```bash
   npm run import:courses
   ```

### 5. Run the Development Server

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

## 📁 Project Structure

```
Class-Connect/
├── app/                    # Next.js App Router pages
│   ├── chat/              # Course chat pages
│   ├── courses/           # Course browser
│   ├── dashboard/         # User dashboard
│   └── verify-email/      # Email verification
├── components/            # React components
├── lib/                   # Utility functions
│   ├── firebase.ts       # Firebase initialization
│   ├── firebaseHelpers.ts # Firestore helper functions
│   ├── data.ts           # Data fetching functions
│   └── AuthContext.tsx   # Authentication context
├── pages/api/            # API routes
├── scripts/              # Utility scripts
│   ├── scrape_course.py  # Course scraper
│   └── import_courses_to_firestore.cjs # Firestore import
├── types/                # TypeScript type definitions
└── public/               # Static assets
```

## 🔐 Security

- **CUNY Email Validation**: Only `@*.cuny.edu` email addresses can register
- **Email Verification**: Required before accessing protected routes
- **Firestore Security Rules**: Configured to ensure only authenticated users can read/write data
- **Protected Routes**: Dashboard, courses, and chat pages require authentication

### Environment Variables

Make sure to add all `NEXT_PUBLIC_FIREBASE_*` variables to your deployment platform.

## 📝 Available Scripts

- `npm run dev` - Start development server
- `npm run build` - Build for production
- `npm run start` - Start production server
- `npm run lint` - Run ESLint
- `npm run import:courses` - Import courses from JSON to Firestore
