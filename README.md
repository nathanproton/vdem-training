# VDEM Training Events Manager

A self-contained, offline-capable training events management system for Virginia Department of Emergency Management (VDEM).

## Features

- 📋 **Add & Manage Events** - Complete event tracking with dates, times, locations, and details
- 💾 **Auto-Save** - Automatic browser localStorage persistence
- 📥 **Export/Import** - Download HTML file with embedded data for backups
- 📊 **View Data** - Export events as JSON with one-click copy
- 🌐 **API Publishing** - Publish events to external API endpoints
- 📄 **Pagination** - Display 20 events per page for easy browsing
- 🎨 **Classic UI** - Clean, professional 2000s business app aesthetic

## Usage

### Online (GitHub Pages)
Visit: `https://YOUR-USERNAME.github.io/vdem-training/`

### Offline
1. Download `index.html`
2. Open in any modern web browser
3. Works without internet connection

## How It Works

### Data Storage
- **Browser Storage**: Changes auto-save to localStorage
- **File Export**: Download HTML file with all data embedded
- **Embedded Data**: Fallback data stored in the HTML file itself

### Workflow
1. **Add events** using the form
2. **View events** in paginated table
3. **Save to File** to create a backup with current data
4. **Publish to API** to sync with external systems (optional)

### Settings
- Configure API endpoint for publishing
- Choose between CORS and No-CORS modes
- Set request method (POST/PUT)
- Optional API key authentication

## Data Schema

Events include:
- Event ID (auto-generated)
- Start/End dates and times
- Title (required)
- Course code and name
- Type (ICS, G-series, L-series, HazMat, Other)
- Location (city, state, details)
- Delivery mode (In-Person, Virtual, Hybrid)
- Application and admin notes
- Timestamps (created, updated)

## Browser Compatibility

Works in all modern browsers:
- Chrome/Edge
- Firefox
- Safari
- Opera

## Development

This is a single-file application. The entire app is contained in `index.html`:
- HTML structure
- CSS styling
- JavaScript logic
- Embedded data (JSON)

To modify, simply edit `index.html` and refresh your browser.

## License

Open source - feel free to use and modify for your needs.
