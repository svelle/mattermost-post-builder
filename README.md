# Mattermost Webhook Tester

A standalone HTML webapp for testing and building Mattermost webhook posts and API posts with live preview.

Live on gh-pages here: https://svelle.github.io/mattermost-post-builder/

## Features

### 🎨 Live Preview
- Real-time rendering of posts as they would appear in Mattermost
- Markdown support (bold, italic, links, lists)
- Message attachments with full styling
- Interactive action buttons and dropdowns (visual preview)

### 🔄 Dual Format Support
- **Webhook Posts**: Standard incoming webhook format (`text`, `username`, `icon_url`, `attachments[]`)
- **API Posts**: Direct API post format (`channel_id`, `message`, `root_id`, `props.attachments[]`)
- Easy toggle between formats
- Format-specific examples and builder buttons

### 🛠️ Visual Builder
Build complex posts without memorizing JSON structure:

**Post Properties:**
- Username/Icon (webhook only)
- Message Text
- Channel ID (API only)
- Root ID for replies (API only)
- Custom Post Type (API only)

**Attachment Components:**
- New Attachment with color
- Author Info (name, icon, link)
- Title with optional link
- Pretext
- Text content
- Fields (supports `short: true` for 2-column layout)
- Images (full-size and thumbnail)
- Action Buttons
- Action Select dropdowns
- Footer with icon

### 📋 Example Templates
Pre-built examples for quick testing:
- Simple Post
- Post with Attachment
- Post with Fields
- Post with Actions
- Complete Example (all features)

## Usage

### Getting Started

1. **Open the file**: Simply open `index.html` in a web browser
2. **Choose format**: Toggle between "Webhook" or "API Post" format
3. **Build or paste**: Use builder buttons or paste your JSON
4. **Preview**: See live preview on the right panel

### Building a Post from Scratch

1. Click **"Clear"** to start fresh
2. Choose your format (Webhook or API Post)
3. Click builder buttons to add components:
   - Start with **"💬 Message Text"** for the main post message
   - Click **"📎 New Attachment"** to add an attachment
   - Add attachment components (title, text, fields, etc.)
   - Components are added to the most recent attachment
4. Edit placeholder values in the JSON editor
5. See your post render in real-time

### Testing Existing Webhooks

1. Copy your webhook JSON
2. Select the correct format (Webhook or API Post)
3. Paste into the JSON editor
4. Preview instantly updates

## JSON Structure

### Webhook Post Format

```json
{
  "username": "Bot Name",
  "icon_url": "https://example.com/icon.png",
  "text": "Main message text with **markdown**",
  "attachments": [
    {
      "color": "#0066cc",
      "pretext": "Text above attachment",
      "author_name": "Author Name",
      "author_icon": "https://example.com/author.png",
      "author_link": "https://example.com",
      "title": "Attachment Title",
      "title_link": "https://example.com",
      "text": "Attachment text with **markdown**",
      "fields": [
        {
          "title": "Field Title",
          "value": "Field Value",
          "short": true
        }
      ],
      "image_url": "https://example.com/image.png",
      "thumb_url": "https://example.com/thumb.png",
      "actions": [
        {
          "name": "Button Name",
          "integration": {
            "url": "https://example.com/action"
          }
        }
      ],
      "footer": "Footer text",
      "footer_icon": "https://example.com/footer-icon.png"
    }
  ]
}
```

### API Post Format

```json
{
  "channel_id": "channel-id-here",
  "message": "Main message text with **markdown**",
  "root_id": "",
  "type": "custom_post_type",
  "props": {
    "attachments": [
      {
        "color": "#0066cc",
        "title": "Attachment Title",
        "text": "Attachment text",
        "fields": [
          {
            "title": "Field Title",
            "value": "Field Value",
            "short": true
          }
        ]
      }
    ]
  }
}
```

## Attachment Properties Reference

| Property | Type | Description |
|----------|------|-------------|
| `color` | string | Hex color for left border (e.g., `#0066cc`) |
| `pretext` | string | Text displayed above the attachment |
| `author_name` | string | Author name displayed in attachment header |
| `author_icon` | string | URL to author avatar image |
| `author_link` | string | URL when clicking author name |
| `title` | string | Attachment title |
| `title_link` | string | URL when clicking title |
| `text` | string | Main attachment text (supports markdown) |
| `fields` | array | Array of field objects with `title`, `value`, `short` |
| `image_url` | string | URL to full-width image |
| `thumb_url` | string | URL to thumbnail image (floats right) |
| `actions` | array | Interactive buttons and selects |
| `footer` | string | Footer text |
| `footer_icon` | string | URL to footer icon |
| `fallback` | string | Fallback text if attachment can't render |

## Field Properties

Fields support a 2-column layout when `short: true`:

```json
{
  "title": "Field Title",
  "value": "Field Value",
  "short": true
}
```

- `short: true` - Display in 2-column layout
- `short: false` - Display full-width

## Action Types

### Button

```json
{
  "name": "Button Name",
  "integration": {
    "url": "https://example.com/action"
  }
}
```

### Select Dropdown

```json
{
  "name": "Select Option",
  "type": "select",
  "integration": {
    "url": "https://example.com/action"
  },
  "options": [
    { "text": "Option 1", "value": "option1" },
    { "text": "Option 2", "value": "option2" }
  ]
}
```

## Tips

- **Markdown Support**: Use markdown in `text`, `message`, `pretext`, and field `value` properties
- **Colors**: Use hex colors (e.g., `#ff0000`) for the attachment color border
- **Multiple Attachments**: Both formats support multiple attachments in the array
- **Builder Workflow**: Add "New Attachment" first, then add components to it
- **Validation**: Builder alerts you if you try to add attachment components without an attachment
- **Live Updates**: Type in the JSON editor to see instant preview updates

## Technical Details

- **Rendering Engine**: Based on Mattermost webapp post rendering architecture
- **Markdown Library**: Uses marked.js (v11.1.1) for markdown parsing
- **Styling**: Mimics Mattermost's official design system
- **No Backend Required**: Completely client-side, works offline
- **Browser Support**: Works in all modern browsers

## Files

- `index.html` - Complete standalone webapp (no dependencies needed except marked.js CDN)

## Implementation Notes

This tester is based on the actual Mattermost webapp rendering components:
- `/webapp/platform/types/src/message_attachments.ts` - Type definitions
- `/webapp/channels/src/components/post_view/message_attachments/` - Rendering components
- `/webapp/channels/src/components/markdown/` - Markdown processing

## License

Based on Mattermost codebase structure and documentation.
