 Telegram Bot Automation Framework

A powerful automation framework for building scalable Telegram bots with advanced features like DM automation, campaign orchestration, and third-party service integrations.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)
[![Python 3.11+](https://img.shields.io/badge/python-3.11+-blue.svg)](https://www.python.org/downloads/)

## 🚀 Features

- **Modular DM Automation**: Sophisticated system for handling direct messages
- **Human-in-the-Loop Control**: Manual oversight and intervention capabilities
- **Campaign Orchestration**: Command-based campaign management with keyword routing
- **Third-Party Integrations**: Built-in support for Notion, Zapier, and more
- **Rate Limiting**: Token bucket implementation with FloodWait recovery
- **Error Handling**: Comprehensive error management with optional Sentry integration

## 🛠️ Technical Stack

- Python 3.11+
- python-telegram-bot library
- aioratelimit for rate limiting
- Docker containerization
- Async/await architecture
- Type hints throughout

## 📦 Installation

### Using Docker (Recommended)
```bash
docker-compose up -d
```

### Manual Installation
```bash
# Clone the repository
git clone https://github.com/Algo-aKairos/telegram-bot-automation.git
cd telegram-bot-automation

# Create and activate virtual environment
python -m venv venv
source venv/bin/activate  # Linux/Mac
# or
venv\\Scripts\\activate  # Windows

# Install dependencies
pip install -r requirements.txt

# Configure environment
cp .env.example .env
# Edit .env with your settings

# Run the bot
python src/main.py
```

## 🔧 Configuration

The framework uses environment variables for configuration. Key settings:

```env
BOT_TOKEN=your_telegram_bot_token
LOG_LEVEL=INFO
RATE_LIMIT_TOKENS=10
RATE_LIMIT_INTERVAL=1.0
NOTION_API_KEY=optional_notion_integration
SENTRY_DSN=optional_sentry_monitoring
```

## 💡 Usage Example

```python
from telegram_bot_automation import Bot, RateLimiter
from telegram_bot_automation.decorators import admin_only, rate_limited

# Initialize bot with advanced features
bot = Bot(
    token="YOUR_BOT_TOKEN",
    rate_limiter=RateLimiter(tokens=10, interval=1.0),
    integrations=["notion", "zapier"]
)

@admin_only
@rate_limited
async def start_campaign(update, context):
    """Start an automated outreach campaign"""
    campaign = await bot.campaigns.create(
        name="welcome_sequence",
        messages=["Hello!", "Welcome aboard!"],
        interval=timedelta(hours=24)
    )
    await campaign.start()

# Add handlers
bot.add_handler(CommandHandler("start_campaign", start_campaign))
```

## 🏗️ Architecture

![Architecture Diagram](docs/images/architecture.png)

The framework follows an async event-driven architecture:
1. Updates flow through middleware pipeline
2. Matched with appropriate handlers
3. Processed with error handling and rate limiting
4. Results post-processed and logged

## 🧪 Testing

```bash
# Run tests
pytest

# Run with coverage
pytest --cov=src tests/
```

## 📈 Scaling

The framework is designed for production use with:
- Horizontal scaling via Docker
- Rate limiting to respect Telegram's limits
- Error recovery with exponential backoff
- Monitoring via Sentry integration

## 👥 Contributing

Contributions welcome! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👤 Author

Daniel Kairos Clinton
- GitHub: [@Algo-aKairos](https://github.com/Algo-aKairos)
- Email: maddenvincent22@gmail.com

## 🙏 Acknowledgments

- Built on python-telegram-bot
- Inspired by real-world automation needs
- Community contributions and feedback 
