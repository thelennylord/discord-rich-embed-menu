# Discord Rich Embed Menu
A simple-to-use framework for creating responsive user interfaces using Discord's rich embed.

## Installation
`npm install discord-rich-embed-menu --save`

## Example
```js
const Discord = require(`discord.js`);
const DiscordRichEmbedMenu = require(`discord-rich-embed-menu`);
const bot = new Discord.Client();

const menuTemplate = {
    title: "Main menu",
    description: "Main menu",
    color: "BLUE",
    footer: {
        type: "timestamp",
        value: Date.now()
    },
    children: [
        {
            title: "GitHub repository",
            description: "Gives you the link of this tool's repository.",
            function: (outputMessage, senderMessage) => {
                return outputMessage.edit("Link to repository: https://github.com/thelennylord/discord-rich-embed-menu");
            }
        },
        {
            title: "About",
            description: "Get information about this framework.",
            function: (outputMessage, senderMessage) => {
                return outputMessage.edit("It's a simple framework for creating responsive user user interfaces using Discord's rich embed!");
            }
        }
    ]
};

bot.on(`message`, async message => {
    if (message.content === `!menu`) {
        let response = await message.channel.send(`Loading menu...`);
        const menu = new DiscordRichEmbedMenu(menuTemplate, response, message, {
                dataPersistance: true,
                backButton: true
        });
        return menu.start();
    };
});

bot.login(`token`);
```

## Tags
Discord Rich Embed Menu is defined using objects in Javascript.

- Root tag: (object)  
    - title: Title of the menu (string)  
    - description: Description of the menu (string)  
    - color: Colour of the rich embed in hex or colour name (string)  
    - thumbnail: Thumbnail of the rich embed (string)  
    - footer: Footer of the rich embed (object)  
        - type: Type of the footer. Currently, two types are available "timestamp" and "footer" (string)  
        - value: Sets the value of the footer (string or Date)  
    - children: Submenus are contained here in an array. Inside the array, another root menu object is stored inside which acts as the submenu. This tag is mandatory for the main root menu. (array)  
    - function: Fires a function stored here upon the submenu being selected. Cannot be used in the main root menu. Provides two arguments, outputMessage and sendersMessage. (function)

