# Hospital Triage Recommendation System

A FastAPI service that automatically suggests the most relevant specialist department based on patient symptoms using Google's Gemini AI.

## Features

- 🤖 AI-powered department recommendation using Google Gemini
- ⚡ FastAPI for high-performance API
- 🏥 Automatic triage based on symptoms, age, and gender
- 📝 Easy-to-use REST API with interactive documentation
- 🔍 Built-in API testing interface

## Tech Stack

- **Framework**: FastAPI
- **AI Model**: Google Gemini Pro
- **Language**: Python 3.8+
- **Environment Management**: python-dotenv

## Prerequisites

- Python 3.8 or higher
- Google AI Studio API key

## Installation

1. **Clone or download the project files**

2. **Create a virtual environment (recommended)**
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. **Install dependencies**
```bash
pip install -r requirements.txt
```

4. **Set up environment variables**

   Create a `.env` file in the project root:
```env
GEMINI_API_KEY=your_google_gemini_api_key_here
```

## Getting Your API Key

1. Go to [Google AI Studio](https://aistudio.google.com/)
2. Sign in with your Google account
3. Create a new API key
4. Copy the key and add it to your `.env` file

## Running the Application

### Development Mode
```bash
uvicorn main:app --reload --port 8000
```

The application will be available at: `http://127.0.0.1:8000`

## API Usage

### 1. Using Interactive API Documentation

Once the server is running, visit `http://127.0.0.1:8000/docs` to access the interactive Swagger UI:

![API Documentation](Screenshot%202025-11-26%20210501.png)

**Steps to test:**
1. Click on `POST /recommend`
2. Click "Try it out"
3. Modify the request body with your data:
```json
{
  "gender": "female",
  "age": 62,
  "symptoms": ["pusing", "mual", "sulit berjalan"]
}
```
4. Click "Execute" to send the request

### 2. Using cURL Command

**Example Request:**
```bash
curl -X POST "http://127.0.0.1:8000/recommend" \
     -H "Content-Type: application/json" \
     -d '{
       "gender": "female",
       "age": 62,
       "symptoms": ["pusing", "mual", "sulit berjalan"]
     }'
```

**Example Response:**
```json
{
  "recommended_department": "Neurology"
}
```

![API Response](Screenshot%202025-11-26%20210622.png)

### 3. Request Format

**POST** `/recommend`

**Request Body:**
```json
{
  "gender": "female",  // "male" or "female"
  "age": 62,           // patient age in years
  "symptoms": [        // list of symptoms
    "pusing",
    "mual", 
    "sulit berjalan"
  ]
}
```

**Response:**
```json
{
  "recommended_department": "string"  // Recommended department name
}
```

## Available Departments

The system can recommend various departments including:
- **Neurology**: headaches, dizziness, balance issues, neurological symptoms
- **Cardiology**: chest pain, breathing difficulties, heart-related issues  
- **Gastroenterology**: nausea, stomach pain, digestive issues
- **Psychiatry/Mental Health**: sleep disorders, anxiety, depression
- **Dentistry**: gum bleeding, dental issues
- **General Practice**: general symptoms, fever, cough
- **Orthopedics**: bruises, injuries, musculoskeletal issues

## Project Structure

```
submission bithealth/case_3/
├── main.py                 
├── requirements.txt        
├── .env                   
├── Screenshot 2025-11-26 210501.png 
├── Screenshot 2025-11-26 210622.png 
└── README.md             
```

## Example Use Cases

```bash
# Example 1: Neurological symptoms
curl -X POST "http://127.0.0.1:8000/recommend" \
     -H "Content-Type: application/json" \
     -d '{"gender": "male", "age": 45, "symptoms": ["pusing", "sakit kepala", "mual"]}'

# Example 2: Digestive issues  
curl -X POST "http://127.0.0.1:8000/recommend" \
     -H "Content-Type: application/json" \
     -d '{"gender": "female", "age": 35, "symptoms": ["mual", "sakit perut", "diare"]}'

# Example 3: Respiratory problems
curl -X POST "http://127.0.0.1:8000/recommend" \
     -H "Content-Type: application/json" \
     -d '{"gender": "male", "age": 68, "symptoms": ["sesak nafas", "batuk", "demam"]}'
```

## Troubleshooting

### Common Issues

1. **API Key Error**
   - Ensure `GEMINI_API_KEY` is set in `.env` file
   - Verify the API key is valid and has sufficient quota

2. **Port Already in Use**
   - Change the port: `uvicorn main:app --port 8081`
   - Or kill the process using the port

3. **Module Not Found**
   - Ensure all dependencies are installed: `pip install -r requirements.txt`
   - Check your virtual environment is activated

### Testing the API

1. Start the server: `cd case 3` -> `uvicorn main:app --reload --port 8000`
2. Open browser to: `http://127.0.0.1:8000/docs`
3. Use the interactive interface to test the `/recommend` endpoint
4. Verify you get a response like: `{"recommended_department":"Neurology"}`

