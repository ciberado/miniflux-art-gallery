# Art Viewer

A beautiful, full-screen art viewer that displays images from your Miniflux RSS feed with an elegant blurred background effect.

## Features

- **Elegant Display**: Images are shown with a blurred background version and sharp foreground
- **Smart Rotation**: Automatically cycles through your art feed, prioritizing images you've seen least
- **Interactive Overlay**: Click anywhere to show/hide image details and controls
- **Smooth Transitions**: Fade effects between images for a polished experience
- **Responsive Design**: Works on desktop and mobile devices

## Setup

### 1. Prerequisites

You need:
- A Miniflux RSS reader instance
- A category in Miniflux dedicated to art/image feeds
- A Miniflux API key

### 2. Configuration

Open the HTML file and update these constants at the top of the `<script>` section:

```javascript
const MINIFLUX_URL = 'https://miniflux.mininube.com'; // Your Miniflux URL
const CATEGORY_ID = 3; // Your art category ID
```

### 3. API Key

You can provide your Miniflux API key in two ways:

**Option A: URL Parameter (Recommended)**
```
art-viewer.html?key=YOUR_API_KEY_HERE
```

**Option B: Edit the HTML file**
Replace `YOUR_API_KEY_HERE` in the code:
```javascript
const API_KEY = urlParams.get('key') || 'YOUR_API_KEY_HERE';
```

## Usage

### Basic Controls

- **Click anywhere**: Toggle the information overlay on/off
- **Next Image button**: Skip to the next image
- **View Original button**: Open the source article in a new tab

### How It Works

1. The viewer fetches the 50 most recent entries from your specified Miniflux category
2. It filters entries to only show those with images
3. Images are displayed with a smart rotation algorithm that prioritizes unseen or rarely-shown images
4. View counts are stored in your browser's localStorage to persist across sessions

### Display Logic

- All images use a "contain" strategy - the full image is always visible
- A heavily blurred version of the same image fills the background
- This creates an attractive, immersive effect for both portrait and landscape images

## Finding Your Category ID

1. Log into your Miniflux instance
2. Navigate to your art category
3. Look at the URL - it will be something like: `https://your-miniflux.com/category/3`
4. The number at the end is your category ID

## Optional Features

### Auto-Advance

Uncomment these lines at the bottom of the script to automatically advance to the next image every 30 seconds:

```javascript
setInterval(() => {
    const nextEntry = selectNextEntry();
    showEntry(nextEntry);
}, 30000);
```

## Troubleshooting

### "Unable to load art" error

Check that:
- Your Miniflux URL is correct
- Your API key is valid
- The category ID exists and contains entries with images
- Your Miniflux instance is accessible from your browser

### Images not displaying

- Ensure your RSS feeds actually contain image enclosures or images in their content
- Check the browser console (F12) for specific error messages
- Verify that image URLs are accessible (not blocked by CORS or authentication)

## Privacy & Storage

The app stores image appearance counts in your browser's localStorage to track which images you've seen. This data:
- Never leaves your browser
- Is specific to each device/browser
- Can be cleared by clearing your browser data

## Technical Details

- Pure HTML/CSS/JavaScript - no build process required
- Uses the Miniflux API v1
- Responsive design with modern CSS effects
- Graceful error handling and fallbacks

## License

Free to use and modify as needed.
