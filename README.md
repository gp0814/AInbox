# AInbox - AI Email Writer

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![GitHub issues](https://img.shields.io/github/issues/gp0814/AInbox)](https://github.com/gp0814/AInbox/issues)
[![GitHub stars](https://img.shields.io/github/stars/gp0814/AInbox)](https://github.com/gp0814/AInbox/stargazers)

An intelligent AI-powered email writing assistant that helps you craft perfect email replies with different tones and styles using Google's Gemini API.

## 🚀 Features

- **AI-Powered Email Generation**: Generate contextual email replies using Google Gemini API
- **Multiple Tone Options**: Choose from various tones (Professional, Friendly, Formal, Casual, etc.)
- **Smart Context Understanding**: AI analyzes the original email to provide relevant responses
- **Real-time Generation**: Fast email reply generation with instant preview
- **Responsive Design**: Works seamlessly across desktop and mobile devices
- **Clean Interface**: Intuitive and user-friendly design built with React

## 🛠️ Tech Stack

### Frontend
- **Vite + React**: Modern, fast development environment
- **JavaScript/JSX**: Component-based architecture
- **CSS3**: Responsive styling
- **Axios**: HTTP client for API communication

### Backend
- **Spring Boot**: Robust Java-based backend framework
- **Spring Web**: RESTful API development
- **Maven**: Dependency management
- **Google Gemini API**: AI-powered text generation

## 📋 Table of Contents

- [Demo](#demo)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [API Endpoints](#api-endpoints)
- [Contributing](#contributing)
- [License](#license)

## 🌐 Demo

**Live Application**: [Add your deployment link here]

## 🛠️ Installation

### Prerequisites

- **Frontend**: Node.js (v16.0 or higher), npm/yarn
- **Backend**: Java 17+, Maven 3.6+
- **API**: Google Gemini API key

### Clone the Repository

```bash
git clone https://github.com/gp0814/AInbox.git
cd AInbox
```

### Backend Setup (Spring Boot)

```bash
# Navigate to backend directory
cd backend

# Configure application properties (create your own application.properties file)
# Add your Gemini API key to src/main/resources/application.properties
# See Configuration section below for required properties

# Build and run the application
mvn clean install
mvn spring-boot:run
```

The backend server will start on `http://localhost:8080`

### Frontend Setup (Vite + React)

```bash
# Navigate to frontend directory
cd frontend

# Install dependencies
npm install

# Create your own .env file and configure the backend API URL
# See Configuration section below for required environment variables

# Start the development server
npm run dev
```

The frontend application will start on `http://localhost:5173`

## ⚙️ Configuration

### Backend Configuration (`application.properties`)

Create `src/main/resources/application.properties` file with the following configuration:

```properties
# Server Configuration
server.port=8080

# Gemini API Configuration (REQUIRED - Get your own API key)
gemini.api.key=YOUR_GEMINI_API_KEY_HERE
gemini.api.url=https://generativelanguage.googleapis.com/v1/models/gemini-pro:generateContent

# CORS Configuration
cors.allowed.origins=http://localhost:5173

# Application Configuration
app.name=AInbox AI Email Writer
app.version=1.0.0
```

⚠️ **Important**: Never commit your actual API key to version control. Keep your `application.properties` file in `.gitignore`.

### Frontend Configuration (`.env`)

Create a `.env` file in the frontend directory:

```env
# API Configuration
VITE_API_BASE_URL=http://localhost:8080
VITE_APP_NAME=AInbox
VITE_APP_VERSION=1.0.0
```

⚠️ **Important**: Add `.env` to your `.gitignore` file to prevent committing environment variables.

### Getting Gemini API Key

1. Visit [Google AI Studio](https://makersuite.google.com/app/apikey)
2. Sign in with your Google account
3. Create a new API key
4. **Important**: Keep your API key secure and never share it publicly
5. Add the API key to your backend `application.properties` file
6. Ensure your `application.properties` file is added to `.gitignore`

## 🔒 Security Best Practices

- **Never commit API keys**: Always add configuration files containing sensitive data to `.gitignore`
- **Use environment variables**: For production deployments, use environment variables instead of configuration files
- **Rotate API keys**: Regularly rotate your API keys for better security
- **Monitor usage**: Keep track of your API usage to detect any unauthorized access

## 🚀 Usage

1. **Start the Application**:
   - Run the Spring Boot backend
   - Start the Vite React frontend
   - Open your browser to `http://localhost:5173`

2. **Generate Email Replies**:
   - Paste or type the original email you want to reply to
   - Select your preferred tone from the dropdown menu:
     - **Professional**: Formal business communication
     - **Friendly**: Warm and approachable tone
     - **Formal**: Very formal and structured
     - **Casual**: Relaxed and informal
     - **Apologetic**: When you need to apologize
     - **Enthusiastic**: Positive and energetic
     - **Concise**: Brief and to the point

3. **Review and Use**:
   - Click "Generate Reply" to create the AI response
   - Review the generated email
   - Copy the response to use in your email client

## 📖 API Endpoints

### Generate Email Reply

```http
POST /api/email/generate-reply
Content-Type: application/json

{
  "originalEmail": "Thank you for your interest in our product...",
  "tone": "professional",
  "context": "business inquiry"
}
```

**Response:**
```json
{
  "success": true,
  "generatedReply": "Dear [Name],\n\nThank you for reaching out...",
  "tone": "professional",
  "timestamp": "2024-01-15T10:30:00Z"
}
```

### Available Tones

```http
GET /api/email/tones
```

**Response:**
```json
{
  "tones": [
    {
      "id": "professional",
      "name": "Professional",
      "description": "Formal business communication"
    },
    {
      "id": "friendly",
      "name": "Friendly",
      "description": "Warm and approachable tone"
    }
  ]
}
```

## 🏗️ Project Structure

```
AInbox/
├── frontend/                    # Vite + React frontend
│   ├── src/
│   │   ├── components/         # React components
│   │   │   ├── EmailWriter.jsx
│   │   │   ├── ToneSelector.jsx
│   │   │   └── ReplyPreview.jsx
│   │   ├── services/          # API service functions
│   │   ├── styles/            # CSS stylesheets
│   │   ├── utils/             # Utility functions
│   │   └── App.jsx            # Main application component
│   ├── public/                # Static assets
│   ├── package.json
│   └── vite.config.js         # Vite configuration
└── backend/                    # Spring Boot backend
    ├── src/main/java/
    │   └── com/ainbox/
    │       ├── controller/     # REST controllers
    │       │   └── EmailController.java
    │       ├── service/        # Business logic
    │       │   ├── EmailService.java
    │       │   └── GeminiService.java
    │       ├── model/          # Data models
    │       │   └── EmailRequest.java
    │       ├── config/         # Configuration classes
    │       └── AInboxApplication.java
    ├── src/main/resources/
    │   └── application.properties
    └── pom.xml                 # Maven dependencies
```

## 🤝 Contributing

We welcome contributions! Please follow these steps:

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/new-feature`
3. Make your changes
4. Test your changes thoroughly
5. Commit with descriptive messages: `git commit -m 'Add new tone option'`
6. Push to your branch: `git push origin feature/new-feature`
7. Create a Pull Request

### Development Guidelines

- **Frontend**: Follow React best practices and maintain component structure
- **Backend**: Follow Spring Boot conventions and maintain clean architecture
- **Code Style**: Use consistent formatting and meaningful variable names
- **Testing**: Add tests for new features

## 🧪 Testing

### Frontend Testing
```bash
cd frontend
npm run test
```

### Backend Testing
```bash
cd backend
mvn test
```

## 🔒 Security

- **API Key Protection**: Gemini API keys are stored securely in backend configuration (never committed to repository)
- **Environment Variables**: Sensitive configuration is managed through environment variables
- **CORS Configuration**: Properly configured cross-origin resource sharing
- **Input Validation**: All user inputs are validated before processing
- **Error Handling**: Comprehensive error handling to prevent information leakage
- **Git Security**: Configuration files with sensitive data are excluded from version control

## 🚀 Deployment

The application is deployed and available at: **[Add your deployment link here]**

### Deployment Steps

1. **Backend**: Deploy Spring Boot application to your preferred platform (Heroku, AWS, etc.)
2. **Frontend**: Build and deploy React application (`npm run build`)
3. **Environment Variables**: Configure production API keys and URLs using environment variables (never hardcode in source)
4. **Security**: Ensure all sensitive configuration is properly secured in your deployment environment

### Environment Variables for Production

Set these environment variables in your production environment:

```bash
# Backend Environment Variables
GEMINI_API_KEY=your_production_gemini_api_key
CORS_ALLOWED_ORIGINS=https://yourdomain.com

# Frontend Environment Variables  
VITE_API_BASE_URL=https://your-backend-api-url.com
```

## 🎯 Future Enhancements

- [ ] Email template library
- [ ] Multiple language support
- [ ] Email signature integration
- [ ] Conversation thread analysis
- [ ] Custom tone creation
- [ ] Email scheduling suggestions
- [ ] Integration with popular email clients

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👥 Author

- **gp0814** - *Developer* - [GitHub Profile](https://github.com/gp0814)

## 🙏 Acknowledgments

- Google Gemini API for AI-powered text generation
- React and Vite communities for excellent development tools
- Spring Boot team for the robust backend framework

## 📞 Support

- **Issues**: [GitHub Issues](https://github.com/gp0814/AInbox/issues)
- **Email**: [Add your contact email]

---

**Built with ❤️ using React, Spring Boot, and Google Gemini API**
