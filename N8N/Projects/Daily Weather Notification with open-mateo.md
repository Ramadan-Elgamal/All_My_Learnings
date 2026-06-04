## Description
A workflow that runs every morning, checks the weather for your city, and sends a summary to you telegram.

## Nodes used
- Schedule Trigger
- HTTP Request
- Set
- Telegram ( action: send a message )

## Tutorials & Notes
### How to use open-mateo free weather api:
1 - Go to the api website [open-mateo](https://open-meteo.com/en/docs)
2 - Choose what fields you want to extract from the api by checking on fields in Current Weather section.
3- make a `HTTP` node and make the `method` to `Get`, and add the params which shows in the url after you choose the fields. ( change the latitude and longitude based on your location )
![[Pasted image 20260529221835.png]]4 - Execute the node by clicking the `Execute step`.

### How to use the `Telegram` node:
1. Start a chat with the [BotFather](https://telegram.me/BotFather) by searching for his name in your telegram account.
2. Enter the `/newbot` command to create a new bot.
3. The BotFather will ask you for a name and username for your new bot:
    - The **name** is the bot's name displayed in contact details and elsewhere. You can change the bot name later.
    - The **username** is a short name used in search, mentions, and t.me links. Use these guidelines when creating your username:
        - Must be between 5 and 32 characters long.
        - Not case sensitive.
        - May only include Latin characters, numbers, and underscores.
        - Must end in `bot`, like `tetris_bot` or `TetrisBot`.
        - You can't change the username later.
4. Copy the bot **token** the BotFather generates and add it as the **Access Token** in n8n and leave the `Base Url` field in the credentials as it is.

### How to remove the automated message from n8n when sending an email:
 1- Open the Telegram node.
 2- Click on the plus icon next the `Additional Field` section.
 3- Choose `Append n8n Attribution`
 4- Disable the toggle