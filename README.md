# Notion Typewriter

A typewriter effect that displays content from a Notion page, with full support for Notion's text colors, highlights, and formatting.

## Features

- ✨ Typewriter animation effect
- 🎨 Full Notion color support (text colors and backgrounds)
- 📝 Supports bold, italic, strikethrough, underline, code formatting
- 🔗 Link support
- 📱 Responsive design

## Quick Start

### Prerequisites

- Node.js installed
- A Notion API token ([get one here](https://www.notion.so/my-integrations))

### Local Development

1. **Install dependencies:**
   ```bash
   npm install
   ```

2. **Create a `.env` file:**
   ```env
   NOTION_TOKEN=your_notion_token_here
   NOTION_BLOCK_ID=your_block_id_here
   ```

3. **Get your Notion credentials:**
   - **Token**: Go to [Notion Integrations](https://www.notion.so/my-integrations) → Create integration → Copy "Internal Integration Token"
   - **Block ID**: Open your Notion page → Copy link → Extract the ID (part after last `/` and before any `?`)
     - Example: `https://notion.so/page/2297e0b5c63440f883ea65aedc7611d1` → Block ID is `2297e0b5c63440f883ea65aedc7611d1`

4. **Start the proxy server:**
   ```bash
   npm start
   # or
   node proxy-server.js
   ```

5. **Open `index.html` in your browser**

The typewriter will automatically fetch content from your Notion page.

## Configuration

Edit `script.js` to customize:

- `NOTION_BLOCK_ID`: The Notion block/page ID to fetch content from
- `TYPEWRITER_CONFIG`: Animation settings (delay, speed, etc.)
- `PROXY_URL`: Automatically detected (localhost for dev, current origin for production)

## Deployment

### Deploy to Vercel (Recommended)

Vercel hosts both the frontend and serverless function in one place.

1. **Install Vercel CLI:**
   ```bash
   npm install -g vercel
   ```

2. **Login and deploy:**
   ```bash
   vercel login
   vercel --prod
   ```

3. **Set environment variables in Vercel:**
   - Go to your project → Settings → Environment Variables
   - Add `NOTION_TOKEN` with your token value
   - Add `NOTION_BLOCK_ID` with your block ID
   - Redeploy

4. **Your app will be live at:**
   - `https://your-project.vercel.app`

### Embed in Notion

Once deployed, you can embed your typewriter in Notion:

1. In Notion, type `/embed` or click `+` → `Embed`
2. Paste your Vercel URL: `https://your-project.vercel.app`
3. Press Enter

The app is configured to allow iframe embedding with proper headers.

## How It Works

1. Browser loads `index.html` and `script.js`
2. `script.js` makes a request to the serverless function at `/api/notion/blocks/:blockId/children`
3. The serverless function (`api/notion.js`) makes the actual request to Notion API (avoiding CORS)
4. Content is returned and displayed with typewriter effect
5. Notion formatting (colors, highlights, etc.) is preserved

## Project Structure

```
typewriter_n/
├── index.html          # Main HTML file
├── script.js           # Client-side JavaScript
├── styles.css          # Styling
├── proxy-server.js     # Node.js proxy server (for local dev only)
├── api/
│   └── notion.js      # Vercel serverless function (for deployment)
├── vercel.json        # Vercel configuration
└── package.json       # Dependencies
```

## Notes

- **Local development**: Requires running `proxy-server.js` to avoid CORS issues
- **Production**: Uses Vercel serverless function automatically (no proxy needed)
- **Environment variables**: `.env` file is gitignored for security. Never commit your actual token.

## License

See repository license.
