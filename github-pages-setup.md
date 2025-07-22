# GitHub Pages Setup for Pydantic AI + Logfire Demo

## Files You Need to Create

### 1. `index.html`
Use the HTML file from the artifact above

### 2. `README.md`
```markdown
# Pydantic AI + Logfire Demo

Live demo showcasing the integration of Pydantic AI with Logfire for building type-safe AI applications with comprehensive observability.
**repo** https://github.com/w4ester/pydantic-ai-demo.git 

🚀 **[View Live Demo](https://w4ester.github.io/pydantic-ai-demo/)**

## Features

- **Live OpenAI Integration**: Real API calls to demonstrate actual functionality
- **Structured Data Extraction**: Shows how Pydantic validates AI outputs
- **Observability Tracking**: Simulated Logfire integration for monitoring
- **Multiple Models**: Support for GPT-3.5, GPT-4, and GPT-4 Turbo
- **Cost Tracking**: Real-time API cost calculation

## Setup Instructions

1. Fork this repository
2. Go to Settings → Pages
3. Set Source to "Deploy from a branch"
4. Select "main" branch and "/ (root)" folder
5. Save and wait for deployment
6. Visit `https://w4ester.github.io/pydantic-ai-demo/`
7. Enter your OpenAI API key when prompted

## Security Note

- API keys are stored locally in your browser
- Keys are never sent to GitHub or any third party
- All API calls are made directly from your browser to OpenAI

## Local Development

```bash
# Clone the repository
git clone https://github.com/w4ester/pydantic-ai-demo.git

# Navigate to the directory
cd pydantic-ai-demo

# Open in browser (Python)
python -m http.server 8000

# Or use any static server
npx serve .
```

## API Keys Required

1. **OpenAI API Key** (Required)
   - Get from: https://platform.openai.com/api-keys
   - Used for: AI chat and data extraction

2. **Logfire Token** (Optional)
   - Get from: https://logfire.pydantic.dev
   - Used for: Real observability (currently simulated in demo) change to actually use Logfire for observability ... 

## Backend Implementation

For production use, implement the backend with Pydantic AI:

```python
from pydantic import BaseModel
from pydantic_ai import Agent
import logfire

# Configure Logfire
logfire.configure(token="your-token")

# Define your model
class UserData(BaseModel):
    name: str
    email: str
    age: int | None = None

# Create agent
agent = Agent(
    'openai:gpt-4.1-mini',
    result_type=UserData,
    system_prompt="Extract user information"
)

# Instrument with Logfire
logfire.instrument_pydantic_ai(agent)

# Use the agent
result = await agent.run("Mo Jo, 34, john@example.com")
print(result.data)  # UserData(name='Mo Jo', email='john@example.com', age=34)
```

## License

MIT
```

### 3. `.gitignore`
```
# API Keys (though they're in localStorage, not files)
.env
.env.local

# OS files
.DS_Store
Thumbs.db

# Editor files
.vscode/
.idea/

# Logs
*.log
```

### 4. `SECURITY.md`
```markdown
# Security Policy

## API Key Handling

This demo requires API keys to function. Here's how we handle them securely:

1. **Client-Side Only**: All API keys are stored in your browser's localStorage
2. **Never Committed**: Keys are never stored in the repository
3. **Direct API Calls**: All calls go directly from your browser to the API providers
4. **No Backend**: This is a static site with no server-side processing

## Reporting Security Issues

If you discover a security vulnerability, please:
1. Do NOT create a public issue
2. Email security concerns to: [ailabs@mindgrub.com]
3. Include steps to reproduce the issue

## Best Practices for Users

1. **Use Restricted API Keys**: Create API keys with limited permissions
2. **Set Usage Limits**: Configure spending limits on your OpenAI account
3. **Monitor Usage**: Regularly check your API usage dashboard
4. **Rotate Keys**: Change your API keys periodically
5. **Private Browsing**: Use incognito mode for shared computers
```

### 5. `_config.yml` (for GitHub Pages)
```yaml
theme: minima
title: Pydantic AI + Logfire Demo
description: Interactive demo of type-safe AI agents with observability
```

## Deployment Steps

1. **Create a new GitHub repository** named `pydantic-ai-demo`

2. **Upload the files**:
   ```bash
   git init
   git add index.html README.md .gitignore SECURITY.md _config.yml
   git commit -m "Initial commit: Pydantic AI + Logfire demo"
   git branch -M main
   git remote add origin https://github.com/w4ester/pydantic-ai-demo.git
   git push -u origin main
   ```

3. **Enable GitHub Pages**:
   - Go to repository Settings → Pages
   - Source: Deploy from a branch
   - Branch: main / root
   - Save

4. **Access your demo** at:
   `https://w4ester.github.io/pydantic-ai-demo/`

## What This Demo Shows Your Team

### 🎯 **Key Demonstrations**:

1. **Real API Integration**: 
   - Actual OpenAI API calls (not simulated)
   - Multiple model options with different cost/performance tradeoffs
   - Live response streaming and error handling

2. **Structured Data Extraction**:
   - JSON mode for guaranteed structured outputs
   - Shows how Pydantic would validate on the backend
   - Demonstrates retry logic for failed validations

3. **Observability Features**:
   - Token usage tracking
   - Cost calculation in real-time
   - Response latency monitoring
   - Error tracking and debugging

4. **Production Patterns**:
   - Secure API key handling
   - Proper error boundaries
   - User-friendly loading states
   - Professional UI/UX

### 💰 **Cost Estimates for Demo**:
- **OpenAI GPT-4.1-mini**: ???

### 🔒 **Security Features**:
- API keys stored only in browser localStorage
- No backend server needed
- Direct browser-to-API communication
- Keys never exposed in code or logs

## Optional Enhancements

To make it even more impressive, you could add:

1. **Export conversation history** to JSON/CSV
2. **Token usage graphs** using Chart.js
3. **Streaming responses** for better UX
4. **Multiple extraction schemas** to demo
5. **Webhook integration** for Logfire (when available) setup now

This setup gives you a fully functional demo that your team can interact with using real API calls, demonstrating the actual capabilities of Pydantic AI rather than just simulations!