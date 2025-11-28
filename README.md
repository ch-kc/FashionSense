# Fashion Sense - AI Style Advisor

An intelligent fashion recommendation system that analyzes your clothing items and provides personalized style suggestions based on context using Computer Vision and Large Language Models.

## Features

- **Image Upload**: Upload photos of your clothing items via drag-and-drop or file selection
- **Vision Analysis**: Automatically detects clothing attributes (type, color, texture, style)
- **AI Recommendations**: Get personalized outfit suggestions from Gemini AI based on your occasion
- **Context-Aware**: Choose from preset contexts (Office, Formal, Casual, Athletic, Evening) or describe your own
- **Wardrobe Management**: Save items to your personal wardrobe library with drag-and-drop reordering
- **History**: Save and access past analyses for future reference
- **UI**: Modern, responsive design with smooth animations and toast notifications

## Architecture

The system uses a three-tier architecture:

1. **Frontend** (HTML/CSS/JavaScript)
   - User interface for uploading images and viewing recommendations
   - IndexedDB for wardrobe storage, localStorage for history
   - Responsive design for all devices

2. **Backend** (Node.js/Express)
   - REST API for handling image uploads
   - Integration with Gemini API for vision and language models
   - Image preprocessing and data handling

3. **AI Models**
   - **Gemini 2.5 Flash**: Analyzes clothing attributes from images and generates personalized fashion recommendations

## Prerequisites

- Node.js (v14 or higher)
- npm or yarn
- Gemini API key - **Optional for demo mode**

### Getting a Gemini API Key

1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create a new project (or select an existing one)
3. Search for "Generative Language API" and enable it
4. Go to **APIs & Services → Credentials**
5. Click **Create Credentials → API Key**
6. Copy the generated key

## Installation

1. **Clone or navigate to the project directory**
   ```bash
   cd FashionSense
   ```

2. **Install server dependencies**
   ```bash
   cd server
   npm install
   ```

3. **Set up environment variables (Optional - runs in demo mode without this)**
   ```bash
   # For full AI functionality, add your API key
   echo "GEMINI_API_KEY=your_actual_api_key_here" > ../.env
   echo "PORT=3000" >> ../.env
   ```
   
   **Note:** Without an API key, the app runs in DEMO MODE with mock data for testing.

4. **Start the server**
   ```bash
   npm start
   ```

   For development with auto-reload:
   ```bash
   npm run dev
   ```

5. **Open your browser**
   Navigate to: `http://localhost:3000`

## Usage

### Step 1: Upload Clothing Items
- Click the upload area or drag and drop images of your clothing items
- You can upload multiple images at once
- Supported formats: JPG, PNG, WEBP

### Step 2: Select Context
- Choose from preset occasions (Office, Formal, Casual, Athletic, Evening)
- Or type your own custom occasion (e.g., "casual dinner date")

### Step 3: Get Recommendations
- Click "Get Style Recommendation"
- Wait for AI analysis (typically 5-10 seconds)
- View your personalized style assessment and outfit suggestions

### Step 4: Save to History (Optional)
- Click "Save to History" to store the analysis
- Access past analyses from the History tab

## API Endpoints

### `POST /api/analyze-images`
Analyzes uploaded clothing images using Gemini Vision.

**Request:**
- Content-Type: `multipart/form-data`
- Body: `images` (file array)

**Response:**
```json
{
  "success": true,
  "attributes": [
    {
      "name": "Blue Denim Shirt",
      "color": "Blue",
      "texture": "Denim",
      "category": "Casual",
      "confidence": 0.95
    }
  ],
  "count": 1
}
```

### `POST /api/get-recommendation`
Gets fashion recommendations from Gemini based on clothing attributes and context.

**Request:**
- Content-Type: `application/json`
- Body:
```json
{
  "attributes": [...],
  "context": "Office"
}
```

**Response:**
```json
{
  "success": true,
  "recommendation": "Your style assessment and outfit suggestions..."
}
```

## Project Structure

```
CVProject/
├── frontend/
│   ├── index.html          # Main HTML file
│   ├── styles.css          # Styles and animations
│   └── js/
│       ├── app.js          # Main application entry point
│       ├── analysis.js     # Image analysis logic
│       ├── db.js           # IndexedDB storage for wardrobe
│       ├── history.js      # History management
│       ├── navigation.js   # Tab navigation
│       ├── results.js      # Results display
│       ├── state.js        # Application state management
│       ├── toast.js        # Toast notifications
│       ├── upload.js       # Image upload handling
│       ├── utils.js        # Utility functions
│       └── wardrobe.js     # Wardrobe management
├── server/
│   ├── server.js           # Express server & API routes
│   ├── gemini.js           # Gemini AI integration
│   ├── mock.js             # Mock data for demo mode
│   └── package.json        # Server dependencies
├── .gitignore              # Git ignore rules
├── COPYRIGHT               # License information
└── README.md               # This file
```

## Privacy & Security

- Images are processed in-memory and not permanently stored on the server
- All data transmission occurs securely
- Local history is stored only in your browser's localStorage

## Troubleshooting

### Server won't start
- Ensure Node.js is installed: `node --version`
- Check if port 3000 is available
- Verify all dependencies are installed: `npm install`

### API key errors
- Make sure your `.env` file exists in the project root
- Verify your Gemini API key is valid
- Check that the environment variable is correctly named: `GEMINI_API_KEY`

### Images not uploading
- Check file size (max 10MB per image)
- Ensure images are in supported formats (JPG, PNG, WEBP)
- Check browser console for errors

### Poor recommendations
- Upload clearer, well-lit photos of clothing items
- Try uploading multiple angles of the same item
- Provide more specific context descriptions

## Future Enhancements

- Side-by-side comparison mode for outfit evaluation
- Integration with custom-trained vision models for better accuracy
- Weather-based recommendations
- Color palette analysis
- Shopping suggestions for complementary items
- EXIF metadata removal before processing for enhanced privacy

## Technical Details

### Vision Model
- Uses Gemini 2.5 Flash for clothing detection
- Extracts attributes: garment type, color, texture, style category
- Returns confidence scores for each detection

### Language Model
- Uses Gemini 2.5 Flash for natural language recommendations
- Considers clothing attributes and user context
- Provides style assessments and practical outfit combinations

## Acknowledgments

- Google Gemini API for AI capabilities