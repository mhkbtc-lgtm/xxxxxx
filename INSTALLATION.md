# YouTube Shorts Pipeline - Installation Complete

## Installation Summary

The YouTube Shorts Pipeline v2.1.0 has been successfully installed in `/home/user/webapp`.

### What Was Installed

1. **Project Files**: Cloned from GitHub repository
2. **Python Dependencies**: All required packages installed including:
   - anthropic (Claude API)
   - google-api-python-client (YouTube API)
   - google-auth & google-auth-oauthlib (Authentication)
   - openai-whisper (Speech transcription)
   - PyTorch (Deep learning backend)
   - feedparser (RSS feeds)
   - Pillow (Image processing)
   - And all their dependencies

3. **System Requirements Verified**:
   - Python 3.12.11 ✓
   - ffmpeg 5.1.7 ✓

4. **Test Dependencies**: pytest and pytest-mock installed

### Project Structure

```
/home/user/webapp/
├── README.md              # Full documentation
├── CHANGELOG.md           # Version history
├── SKILL.md              # Quick reference guide
├── requirements.txt       # Python dependencies
├── pyproject.toml        # Project metadata
├── pipeline/             # Main application code
│   ├── __main__.py       # CLI entry point
│   ├── config.py         # Configuration and setup wizard
│   ├── draft.py          # Script generation
│   ├── broll.py          # AI video generation
│   ├── voiceover.py      # Text-to-speech
│   ├── captions.py       # Subtitle generation
│   ├── music.py          # Background music
│   ├── assemble.py       # Video assembly
│   ├── thumbnail.py      # Thumbnail generation
│   ├── upload.py         # YouTube upload
│   └── topics/           # Topic discovery engine
├── scripts/              # Utility scripts
│   └── setup_youtube_oauth.py
├── tests/                # Test suite (78 tests)
└── references/           # Additional documentation

```

## Next Steps

### 1. First Run Setup

The pipeline will automatically run a setup wizard on first use:

```bash
cd /home/user/webapp
python -m pipeline run --news "your topic" --dry-run
```

The wizard will prompt for:
- **ANTHROPIC_API_KEY** (required) - Get from https://console.anthropic.com/settings/keys
- **GEMINI_API_KEY** (required) - Get from Google AI Studio
- **ELEVENLABS_API_KEY** (optional) - Get from ElevenLabs (or use macOS `say` fallback)

Configuration is saved to: `~/.youtube-shorts-pipeline/config.json`

### 2. YouTube OAuth Setup (When Ready to Upload)

When you're ready to upload videos:

```bash
python scripts/setup_youtube_oauth.py
```

This will guide you through OAuth authentication with YouTube.

## Usage Examples

### Draft a Script (No Production)
```bash
python -m pipeline draft --news "AI breakthrough in medicine"
```

### Discover Trending Topics
```bash
python -m pipeline topics --limit 10
```

### Draft from Trending Topic
```bash
python -m pipeline draft --discover --auto-pick
```

### Full Pipeline (Draft + Produce + Upload)
```bash
python -m pipeline run --news "your topic here"
```

### Produce Video from Existing Draft
```bash
python -m pipeline produce --draft ~/.youtube-shorts-pipeline/drafts/<id>.json
```

### Upload Pre-produced Video
```bash
python -m pipeline upload --draft ~/.youtube-shorts-pipeline/drafts/<id>.json
```

## Options

- `--lang en|hi` - Language for voiceover and captions (English or Hindi)
- `--verbose` - Enable debug logging
- `--force` - Redo completed stages
- `--dry-run` - Draft only, skip production and upload
- `--context "..."` - Add channel context for script generation

## Running Tests

```bash
python -m pytest tests/ -v
```

## Key Features

- ✅ **Fully Automated**: Topic → Research → Script → Video → Upload
- ✅ **AI-Generated Visuals**: Gemini Imagen with Ken Burns effect
- ✅ **Professional Voiceover**: ElevenLabs TTS with multiple voices
- ✅ **Word-by-Word Captions**: Whisper transcription with ASS subtitles
- ✅ **Background Music**: Royalty-free tracks with auto voice-ducking
- ✅ **AI Thumbnails**: Auto-generated and uploaded
- ✅ **Resume Capability**: Re-runs skip completed work
- ✅ **Trending Topics**: Discover from Reddit, RSS, Google Trends, Twitter, TikTok
- ✅ **Retry Logic**: Exponential backoff on all API calls
- ✅ **Structured Logging**: File and console logging

## Cost Estimate

Per video (approximate):
- Claude (script generation): ~$0.02
- Gemini Imagen (b-roll + thumbnail): ~$0.04
- ElevenLabs (60-90 sec voiceover): ~$0.05
- **Total**: ~$0.11 per video

## Troubleshooting

See `references/troubleshooting.md` for detailed troubleshooting guide.

## Security Notes

- API keys stored in `~/.youtube-shorts-pipeline/config.json` with 0600 permissions
- YouTube OAuth tokens in `~/.youtube-shorts-pipeline/youtube_token.json`
- Videos uploaded as **private** by default
- Never commit config files (covered by .gitignore)

## Documentation

- **README.md** - Complete documentation
- **SKILL.md** - Quick reference for AI assistants
- **CHANGELOG.md** - Version history
- **references/setup.md** - Detailed setup guide
- **references/troubleshooting.md** - Common issues and solutions

---

## Installation Date
March 2, 2026

## Version
v2.1.0

## License
MIT
