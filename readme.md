
With this project you can use "Chatbot-UI" as user interface for your Rivet projects!
This allows you to create complex LLM based processes (e.g. a teachable assistant) in a visual programming interface and interact with it via a beautiful chat UI. Chatbot-UI also keeps all the conversation history, so we do not need to care about that!

Features:
- Creates an OpenAI SDK compatible API for any rivet project
- Captures streaming output from a configured node
- Streams the output
- Transforms messages, before sending them to the rivet graph
- Beautiful Chat-UI (provided by Chatbot-UI)
- Chatbot-UI features: Multiple chats with conversation history, Integrated RAG etc.

![Chat UI for Rivet!](/chat_ui.png "Chat UI for Rivet!")

# Last updates 14. Feb 2024
- Fully revamped how most of the parts are working; you do not need to touch a configuration file anymore
- You only need to drop files into /rivet folder to be able to work with them (but make sure to properly prepare the files; see "Use your own files")
- Files are references now as models and no more via different ports

# Project setup
For simplicity all is explained for Visual Studio Code. You can of course run it in other IDEs.

## Software installation (prerequisites)
1. Install **Visual Studio Code**: https://code.visualstudio.com/download
1. Install **node.js + node package manager**: https://nodejs.org/en/download/ (in the install process, make sure you also install npm package manager!)
1. Install **Github**: https://desktop.github.com/

## Clone the repo
1. Open terminal or command line
1. Enter ```git clone https://github.com/ai-made-approachable/rivet-chat-api.git```

## Configure the project
1. Open the folder in Visual Studio Code (File -> Open Folder)
1. Open "Terminal -> New Terminal" and enter ```npm install```
1. Go to /.vscode/ folder
1. Rename "launch_sample.json" to "launch.json"
1. Open "launch.json" and replace the value for OPEN_API_KEY with your OpenAI Key

## Running the project
Just press "Run -> Start Debugging" in Visual Studio Code.
Continue with the "Chat setup". The URLs displayed are the endpoints to connect the chat to rivet-chat-api.

## Use your own project files
- Make sure your project file has an input of type "chat-message" and array checked (Type: chat-message[])
- Rename all "Chat" nodes you want to have streaming output to "output"
- Select a main graph in "Project" settings
- Add your file into the /rivet folder and remember the filename

## Using plugins
If you want to use plugins, you need to import and register them first in graphManager.ts

Example for mongoDB Plugin
```
import rivetMongoDbPlugin from 'rivet-plugin-mongodb';
import * as Rivet from '@ironclad/rivet-node';
Rivet.globalRivetNodeRegistry.registerPlugin(rivetMongoDbPlugin(Rivet));
```

---
# Chat setup
We are using "Chatbot-UI" as it is a very user friendly UI (similiar to ChatGPTs UI): https://github.com/mckaywrigley/chatbot-ui

## Software installation (prerequisites)
1. Install **Docker**: https://docs.docker.com/engine/install/

## Install Chatbot-UI
Note: This installation is a bit long, but it is a one time thing!

1. Open terminal (MacOs) or command line (Windows)
1. ```git clone https://github.com/mckaywrigley/chatbot-ui.git```
1. Navigate into the folder of the repository ```cd chatbot-ui```
1. Install dependencies ```npm install```
1. Install superbase: ```npm install supabase```
1. Make sure Docker is running
1. Start Supabase ```supabase start```
1. Create file .env.local ```cp .env.local.example .env.local```
1. Open ".env.local" in Visual Studio Code (in chatbot-ui root folder)
1. Get the required values by running ```supabase status```
1. Copy "API URL" value and insert it into "NEXT_PUBLIC_SUPABASE_URL"
1. Copy "anon key" and insert it into "NEXT_PUBLIC_SUPABASE_ANON_KEY"
1. Open ```supabase/migrations/20240108234540_setup.sql``` file
1. Replace "service_role_key" with the value from ```supabase status``` and save

Note: Also see instructions on: https://github.com/mckaywrigley/chatbot-ui

## Starting the Chat-UI
1. Make sure Docker is running
1. Navigate to your "chatbot-ui" folder
1. Enter ```npm run chat```
1. Navigate to the URL shown to you, usually: http://localhost:3000

## Configure the Chat-UI
1. When you start "chatbot-ui" for the first time enter e-mail + password (don't worry, all stays locally on your pc)
1. In the sidebar press on "Models" (Stars-Icon) and on "New Model"
1. Enter any name
1. Add the name of your graph e.g. "example.rivet-project" as model
1. Enter ```http://localhost:3100/``` as Base URL
1. Enter anything as API key
1. Open the model selection in the top-right corner and select your custom model
1. Have fun chatting
