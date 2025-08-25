# FutureQuest Telegram Bot

A lightweight, text-based adventure game bot for Telegram, built on **Apache NiFi** and **Groovy**. The bot's content is easily generated and updated by replacing a single JSON configuration file, which can be created using Large Language Models (LLMs).

## 🚀 Key Features

- **Low-Code Backend:** Core orchestration and data flow handled by Apache NiFi.
    
- **Dynamic Content:** The entire game logic is defined in a single JSON file (`tasks.json`). Update the game by simply replacing this file.
    
- **LLM-Powered:** Game content (quests, dialogues, storylines) is perfectly suited for generation by LLMs (like GPT-4, Claude, or DeepSeek).
    
- **Stateless & Lightweight:** No user progress is stored on the server, making it incredibly simple and scalable.
    
- **Rich Formatting:** Supports MarkdownV2 for text formatting in messages.
    
- **Flexible Architecture:** Uses Groovy scripts within NiFi for complex business logic, combining the power of code with the simplicity of visual pipelines.
    

## 📋 Prerequisites

Before you begin, ensure you have the following installed and configured:

- **Apache NiFi** (Version 1.23+ recommended)
    
- **Java** (JDK 8 or 11, as required by your NiFi version)
    
- A **Telegram Bot Token** from [@BotFather](https://t.me/BotFather)
    

## 🛠️ Installation & Setup

1. **Clone the Repository**
    
    bash
    
    git clone https://github.com/your_username/futurequest-bot.git
    cd futurequest-bot
    
2. **Import the NiFi Template**
    
    - Open your Apache NiFi UI.
        
    - Drag the new `ProcessGroup` to the canvas.
        
    - Click **Browse...** and upload the provided `telegram-game.json` template file.
        
    - Click **Add** button.
        
3. **Configure Telegram Bot Token**
    
    - In the NiFi canvas, find the **GlobalSettings** `UpdateAttribute` processor.
        
    - Open its configuration.
        
    - In the **Properties** tab, set the value for the `telegrambot_token` attribute to your actual Telegram Bot Token (e.g., `123456:ABC-DEF1234ghIkl-zyx57W2v1u123ew11`).
        
4. **Deploy the Game Configuration**
    
    - Place your `tasks.json` file on the server where NiFi is running.
        
    - Update the **GlobalSettings** `UpdateAttribute` processor to point `configFile` to the correct path of your `tasks.json` 
    
5. **Start the Processors**
    
    - Enable all processors in the template (right-click -> Start).
        

## 🎮 How to Play

1. Start a chat with your bot on Telegram.
    
2. Send the `/start` command.
    
3. Follow the story, make choices using the inline buttons, and complete quests!
    

## 📁 Project Structure

text

futurequest-bot/
├── tasks.json           # Main game configuration (EXAMPLE)
├── telegram-game.json   # NiFi template to import
└── README.md

## 🤖 Generating Content with LLMs

The power of this project is its seamless integration with LLMs. To create a new game or update an existing one:

1. **Craft a Prompt:** Provide a detailed prompt to your LLM of choice. Example:
    
    > "Generate a JSON structure for a text-based Telegram quest game for children about space exploration. The structure should be compatible with the following Groovy code... Include 3 main quests with 2-3 choices each. Each choice should lead to a different outcome. Use the following schema as a guide: [paste a snippet of your tasks.json schema here]."
    
2. **Validate and Deploy:** Copy the LLM's output into your `tasks.json` file, deploy it, and restart your NiFi flow. Your new game is ready!
    

## 🔧 Customization

- **Adding New Commands:** Modify the `CommandProcessor.groovy` script.
    
- **Creating New Game Mechanics:** Extend the `processCallback()` function in the `GameLogicProcessor.groovy` script.
    
- **Changing the UI:** Modify the `buildQuestResponse()` function to change how messages and buttons are displayed.
    

## 🗺️ Architecture

The bot is built using a **polling mechanism** (`getUpdates`) for reliability and ease of setup. The logic is split into clear stages within NiFi:

1. **Polling:** Fetch updates from the Telegram API.
    
2. **Routing:** Determine the type of incoming event (command, callback, etc.).
    
3. **Processing:** Execute game logic based on the user's input and current state.
    
4. **Response Preparation:** Format the response for the Telegram API.
    
5. **Sending:** Send the message back to the user.

## 📝 Roadmap (To-Be)

- **Automated Content Pipeline:** Schedule NiFi to generate new game JSONs using Ollama/local LLMs based on a CSV list of prompts.
    
- **Database Integration:** Add optional persistence for user progress (e.g., SQLite, Redis).
    
- **Media Hosting:** Serve images/audio/video from a dedicated storage (e.g., MinIO).
    
- **Advanced Features:** Support for payments (TON blockchain), leaderboards, and mini-games.
    

## 👨‍💻 Author

Anatoly Smirnov

- LinkedIn: [Anatoliy Smirnov](https://www.linkedin.com/in/anatoliy-smirnov-586631155)
    

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](https://license/) file for details.

## 🙏 Acknowledgments

- The Apache NiFi community.
    
- Telegram for their powerful Bot API.
    

---

**⭐ If this project inspired you or helped you learn something new, please give it a star on GitHub!**
