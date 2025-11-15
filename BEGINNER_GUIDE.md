# Discord MCP Bridge - Complete Beginner's Guide

This guide will walk you through connecting Claude (the AI assistant) to Discord so it can read and send messages in your Discord server. **No prior technical knowledge required.**

## What You'll Be Able To Do

Once you complete this setup, Claude will be able to:
- Read messages in your Discord channels
- Send messages to Discord channels
- Reply to specific messages
- React to messages with emojis

**Important:** This is a "free tier" solution. It can do basic reading and writing, but NOT advanced features like managing forums, webhooks, or complex server management.

---

## Part 1: Understanding What You're Installing

Before we start, let's quickly explain what these tools are:

**Node.js** - A program that lets your computer run JavaScript code. The Discord connector is written in JavaScript, so you need Node.js installed to run it.

**Git** - A tool for downloading code from the internet. We'll use it to download the Discord connector code.

**Discord Bot** - A special Discord account that programs can control. This is what Claude will use to connect to your Discord server.

**MCP Server** - "Model Context Protocol" - this is the technology that lets Claude connect to external services like Discord.

**Terminal/Command Prompt** - A text-based way to give your computer commands. Don't worry, we'll tell you exactly what to type.

---

## Part 2: Installing Required Programs

### Step 1: Install Node.js

Node.js is the foundation that everything else runs on.

1. Go to https://nodejs.org/ in your web browser
2. You'll see two green download buttons. Click the one that says **"LTS"** (Long Term Support)
3. Once downloaded, open the installer file
4. Click "Next" through all the prompts (the default settings are fine)
5. Click "Install" and wait for it to finish
6. Click "Finish" when done

**How to check it worked:**
1. On Windows: Press the Windows key, type `cmd`, and press Enter
2. On Mac: Press Cmd+Space, type `terminal`, and press Enter
3. In the window that opens, type: `node --version`
4. Press Enter
5. You should see something like `v20.11.0` (the numbers might be different)

If you see a version number, Node.js is installed correctly!

### Step 2: Install Git

Git lets us download the Discord connector code.

1. Go to https://git-scm.com/downloads
2. Click the download link for your operating system (Windows, Mac, or Linux)
3. Open the installer
4. Click "Next" through all the prompts (default settings are fine)
5. Click "Install" and wait
6. Click "Finish"

**How to check it worked:**
1. Open Command Prompt (Windows) or Terminal (Mac) again
2. Type: `git --version`
3. Press Enter
4. You should see something like `git version 2.43.0`

If you see a version number, Git is installed correctly!

---

## Part 3: Creating Your Discord Bot

Now we need to create a special Discord account that Claude can control.

### Step 1: Access Discord Developer Portal

1. Go to https://discord.com/developers/applications
2. Log in with your Discord account
3. Click the blue **"New Application"** button in the top right
4. Give it a name (e.g., "Claude Bot" or "My AI Assistant")
5. Check the box agreeing to Discord's terms
6. Click **"Create"**

### Step 2: Configure Your Bot

1. In the left sidebar, click **"Bot"**
2. Click the **"Add Bot"** button
3. Click **"Yes, do it!"** to confirm
4. You'll see your bot's settings page

Now we need to give the bot the right permissions:

1. Scroll down to **"Privileged Gateway Intents"**
2. Turn ON these three switches:
   - **Presence Intent**
   - **Server Members Intent**
   - **Message Content Intent**
3. Click **"Save Changes"** at the bottom

### Step 3: Get Your Bot Token

**IMPORTANT:** Your bot token is like a password. Never share it with anyone or post it publicly!

1. Scroll back up to the top of the Bot page
2. Under the bot's username, find the **"Token"** section
3. Click **"Reset Token"**
4. Click **"Yes, do it!"**
5. Click **"Copy"** to copy the token
6. **IMMEDIATELY paste it somewhere safe** - like a text file on your computer
7. You'll need this token later and can't view it again without resetting

### Step 4: Invite Your Bot to Your Server

1. In the left sidebar, click **"OAuth2"**
2. Click **"URL Generator"**
3. Under **"Scopes"**, check the box for **"bot"**
4. A new section called **"Bot Permissions"** will appear below
5. Check these permissions:
   - **View Channels**
   - **Send Messages**
   - **Read Message History**
   - **Add Reactions** (optional, but helpful)
6. Scroll down and copy the **"Generated URL"**
7. Paste this URL in your browser and press Enter
8. Select which Discord server you want to add the bot to
9. Click **"Authorize"**
10. Complete the CAPTCHA if prompted

Your bot should now appear in your Discord server's member list (it will be offline for now).

---

## Part 4: Installing the Discord Connector

Now we need to download and set up the code that connects Claude to Discord.

### Step 1: Download the Code

1. Open Command Prompt (Windows) or Terminal (Mac)
2. Navigate to where you want to store the files. For example:
   - Windows: Type `cd Documents` and press Enter
   - Mac: Type `cd ~/Documents` and press Enter
3. Now type this exact command and press Enter:
   ```
   git clone https://github.com/codependent-ai/mcp-discord.git
   ```
4. Wait for it to finish downloading (you'll see text scrolling)
5. Type `cd mcp-discord` and press Enter

### Step 2: Install Dependencies

"Dependencies" are other pieces of code that the Discord connector needs to work.

1. Type this command and press Enter:
   ```
   npm install
   ```
2. Wait for it to finish (this might take a minute or two)
3. You'll see a lot of text scrolling - that's normal!

### Step 3: Build the Server

"Building" means converting the code into a format your computer can run.

1. Type this command and press Enter:
   ```
   npm run build
   ```
2. Wait for it to finish (should be quick)
3. When it's done, you should see a new folder called `build` inside the `mcp-discord` folder

### Step 4: Get the Full Path

We need to know the exact location of the file we just built.

**On Windows:**
1. Type `cd` and press Enter
2. The full path will be shown
3. Copy this path
4. Add `\mcp-discord\build\index.js` to the end
5. Save this complete path somewhere - you'll need it in a moment
6. **IMPORTANT:** In the path, change all single backslashes `\` to double backslashes `\\`
   - Example: `C:\Users\YourName\Documents` becomes `C:\\Users\\YourName\\Documents`

**On Mac:**
1. Type `pwd` and press Enter
2. Copy the path shown
3. Add `/mcp-discord/build/index.js` to the end
4. Save this complete path - you'll need it in a moment

---

## Part 5: Connecting to Claude Desktop

Now we'll tell Claude Desktop how to connect to your Discord bot.

### Step 1: Find the Configuration File

**On Windows:**
1. Press Windows key + R
2. Type `%APPDATA%\Claude` and press Enter
3. Look for a file called `claude_desktop_config.json`
4. Right-click it and open with Notepad

**On Mac:**
1. Open Finder
2. Press Cmd+Shift+G
3. Type `~/Library/Application Support/Claude` and press Enter
4. Look for a file called `claude_desktop_config.json`
5. Right-click and open with TextEdit

**On Linux:**
1. Open your file manager
2. Press Ctrl+H to show hidden files
3. Navigate to `.config/Claude`
4. Open `claude_desktop_config.json` in a text editor

### Step 2: Edit the Configuration

You'll see either an empty file with just `{}`, or existing configuration.

**If the file is empty or just has `{}`:**

Replace everything with this:

```json
{
  "mcpServers": {
    "discord": {
      "command": "node",
      "args": [
        "YOUR_FULL_PATH_HERE",
        "--config"
      ],
      "env": {
        "DISCORD_TOKEN": "YOUR_BOT_TOKEN_HERE"
      }
    }
  }
}
```

**If the file already has other content:**

Add a comma after the last `}` before the final closing bracket, then add:

```json
    "discord": {
      "command": "node",
      "args": [
        "YOUR_FULL_PATH_HERE",
        "--config"
      ],
      "env": {
        "DISCORD_TOKEN": "YOUR_BOT_TOKEN_HERE"
      }
    }
```

**Now replace the placeholders:**

1. Replace `YOUR_FULL_PATH_HERE` with the full path you saved earlier
   - Remember: On Windows, use double backslashes `\\`
   - Example: `"C:\\Users\\Mary\\Documents\\mcp-discord\\build\\index.js"`
2. Replace `YOUR_BOT_TOKEN_HERE` with your Discord bot token
3. Make sure you keep the quotation marks around both!

### Step 3: Save and Restart

1. Save the file (Ctrl+S or Cmd+S)
2. Close Claude Desktop completely (not just minimize - actually quit the application)
3. Reopen Claude Desktop

---

## Part 6: Testing It Works

### Step 1: Check the Connection

1. Open Claude Desktop
2. Start a new conversation
3. Type: "Can you list the Discord servers you have access to?"
4. Claude should respond with the name of your Discord server

### Step 2: Test Sending a Message

1. Ask Claude: "Can you send a test message to [channel name]?"
2. Replace [channel name] with an actual channel in your server
3. Check Discord - you should see a message from your bot!

---

## Troubleshooting

### "The bot is offline in Discord"

This is normal! The bot only appears online when Claude is actively connected. It doesn't stay online 24/7.

### "Claude says it can't find Discord tools"

1. Make sure you saved the config file
2. Make sure you completely closed and reopened Claude Desktop
3. Check that the path in your config file is correct (no typos)
4. Make sure the path uses double backslashes on Windows

### "Error: Invalid token"

Your Discord bot token might be incorrect. Go back to the Discord Developer Portal, reset your token, copy the new one, and update it in your config file.

### "npm: command not found"

Node.js didn't install correctly. Try reinstalling it, making sure to restart your terminal/command prompt after installation.

### "Permission denied" errors

On Mac/Linux, you might need to add `sudo` before commands:
```
sudo npm install
```
You'll need to enter your computer's password.

---

## What Can You Do Now?

Your Claude can now:
- Read messages from any channel the bot can see
- Send messages to any channel
- Reply to specific messages
- React to messages with emojis
- Create threads
- Edit its own messages

**What It CANNOT Do (Free Tier Limitations):**
- Manage webhooks
- Handle forum channels
- Advanced server administration
- Stay online 24/7 (only connects when Claude is actively being used)

---

## Need Help?

If you're stuck and these instructions aren't helping:

1. Check that you followed every step exactly as written
2. Try restarting your computer and Claude Desktop
3. Ask for help in your community Discord - others may have solved the same issue
4. Double-check that your bot has the right permissions in Discord

---

## Security Reminder

**NEVER share your Discord bot token with anyone.** If someone gets your token, they can control your bot and send messages in your server. If you think your token was leaked, immediately go to the Discord Developer Portal and reset it.

---

You're done! Enjoy using Claude in Discord.
