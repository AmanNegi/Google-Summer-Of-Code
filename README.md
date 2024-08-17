# Documentation of Work done under GSoC'24
![banner-ai-gif](https://github.com/user-attachments/assets/91cd3518-4a84-4064-b56a-00789f650dd1)

<p align="center"> 
    <h1 align="center">
      <a href="https://summerofcode.withgoogle.com/programs/2024/projects/41d12z0y">✨ AI in-channel GIF Image Generator ✨</a>
    </h1>
</p>

```
           Generate GIF's directly from Rocket.Chat
```

## Project Abstract 📑

This project introduces an innovative Rocket.Chat application that allows communication between users through AI Generated GIFs. This empowers users to generate entirely original GIFs based on descriptive prompts, this app transcends the traditional GIF features of Rocket.Chat. It's integration into Rocket.Chat ensures a seamless experience allowing users to generate and send GIFs directly from Rocket.Chat. Users can either provide their own prompt or rely on an LLM generated prompt based on user query.

## Deliverables 🛒

1. **OnInstallation Message**: When user installs the `AI.GIF` app from the marketplace, they are introduced to the app via our bot. The welcome message explains the basics about the app what are the basic setup requirements and how to get started.
2. **Helper Message**: Users can access the command `/gen-gif help` to get instructions on how to utilize the app and what all commands & features are available.
3. **Generate GIF using prompt**: Users can utilize the command `/gen-gif p "prompthere"` to generate a GIF based on the prompt provided. The GIF generated is shown as preview first and the user can then decide to send the GIF in the channel.
4. **Generate GIF using query**: Users can uitilize the command `/gen-gif q "queryhere"` to firstly get a set(4) of prompt suggestions based on query. The user can then shortlist the best prompt and utilize it to generate the GIF. Once generated, the GIF is only visible to the user who generates it. The user is provided with action buttons to either regenerate or send the generated GIF.
5. **View Generations**: Users can utilize the command `/gen-gif history <pagenumber>` to view the past generations. As RC only allows showing 10 items at a time, the app provides a workaround in the form of pagination. The user can pass page numbers (0, 1, 2, 3 ...) to get the expected page of history.
6. **Webhook based App**: To ensure a non-blocking experience, the app utilized webhooks to automatically update the client about the GIF generation process. As the GIF generation is a time taking process, client awaiting for the response is not the suggested approach.
7. **Profanity Filtering**: The app utilizes LLM as for a robust NSFW content filter safeguarding the platform by preventing the generation of inappropriate GIFs.
8. **Storage Solutions**: The app takes cares of storing the generated GIFs safely on the Rocket.Chat server, ensuring no foreign dependency and complete availability.

   

## Demo 📹

### 1. OnInstallation Message:

Once the user installs our app, they are introduced to our application with an introductory message. It entails the features of the applications and basic information to get started with our app. 

https://github.com/user-attachments/assets/bbc428f5-ca11-4200-8bd8-2e0619a709fd

### 2. Helper Message:

The user can use the `/gen-gif help` command to get quick info about all the commands available in our app. This command assists users by providing the commands and a line explaining what does each command do.

https://github.com/user-attachments/assets/24ca62cf-cc0b-40a9-b220-8da2c8a4d4a8

### 3. Generate GIF from prompt:

The user can use the `/gen-gif p <yourprompthere>` to generate GIF's directly from the provided prompt. This feature empowers **power users** who have knowledge about prompts, and are specific about the input that goes into the generation process. This command entails three major processes:

1. The _prompt_ passed by the user firstly goes through a profanity filter to ensure that user entered a safe prompt. To identify profanity we use a prompt-tuned text-to-text LLM.
2. Once, we are sure that the _prompt_ is safe, we pass the prompt to the GIF generation model through an API call.
3. When the generation is complete we are notified via Webhooks, and we get notified via a message that our generation is complete. At this step we provide two action buttons(**send** & **regenerate**), we can choose to either regenerate the GIF or send the GIF.

https://github.com/user-attachments/assets/b2e67786-20c9-4c74-809b-0a98225447ba


### 4. Generate GIF from query:

The user can use the `/gen-gif q <yourqueryhere` to generate GIF's using a query, the query in turn provides the user with a set of 4 prompts which the user can use to generate GIFs. This feature is for normal users, who don't have much prompting knowledge or don't wish to write a detailed prompt. This command entails 4 major processes:

1. The _query_ passed by the user firstly goes through a profanity filter to ensure that the user entered a safe prompt.
2. Once, we are sure that the _query_ is safe, we pass the query to the Prompt Generation LLM(another prompt-tuned text-to-text LLM). Which provides us a set of 4 prompts, which are optimized for GIF generation.
3. The user can then select any of the 4 _prompts_ and then continue with the GIF generation process.
4. When the generation is complete, we get a similar message as discussed in above command, the user can decide to either send the GIF or regenerate using the same command.

https://github.com/user-attachments/assets/7cf327c2-0d4d-41a4-900e-5b6d4b6a6a10

### 5. View Past Generations

The user can use the `/gen-gif history <pagenumber>` to view the past generations. As we know, the generation of a GIF is time-consuming and takes up resources. It’s a good idea to store the generations locally so that the GIFs can be reused.

#### Pagination in History:

One issue we faced was that RC atmost shows 10 items in preview, meanwhile we wanted to show all the past generations. To resolve this issue, we went ahead and implemented pagination in history. The user can simply pass the `<pagenumber>` in the command and get the specific page of history.

```
> /gen-gif history 0/1 # return latest 10 items or the 1st page

> /gen-gif history 2 # return the 2nd page

> /gen-gif history <pagenumber> # pagenumber should be a number & pagenumber >= 0
```

https://github.com/user-attachments/assets/8a4ed577-d093-4397-9c21-b3da0fa734e4

## Contributions 📈

### Pull Requests

<div align="center">

| PR Link   | Description  | Status | 
| :-----------: | :------------------------------------:| :------:|
| [PR #6](https://github.com/RocketChat/apps.ai.gif/pull/6) | <b> [CHORE] Initialise RC App</b>  | <img src="https://i.imgur.com/tskv8MM.png" width=55 height=40> |
| [PR #7](https://github.com/RocketChat/apps.ai.gif/pull/7) | <b> [Feat] Generate GIF from chat directly </b>  | <img src="https://i.imgur.com/tskv8MM.png" width=55 height=40> |
| [PR #8](https://github.com/RocketChat/apps.ai.gif/pull/8) | <b> [Feat] Enhance user query using LLM </b>  | <img src="https://i.imgur.com/tskv8MM.png" width=55 height=40> |
| [PR #11](https://github.com/RocketChat/apps.ai.gif/pull/11) | <b> [Feat] Enable user to enter custom prompt </b>  | <img src="https://i.imgur.com/tskv8MM.png" width=55 height=40> |
| [PR #12](https://github.com/RocketChat/apps.ai.gif/pull/12) | <b> [Feat] Allow users to view past generations </b>  | <img src="https://i.imgur.com/tskv8MM.png" width=55 height=40> |
| [PR #13](https://github.com/RocketChat/apps.ai.gif/pull/13) | <b> [Feat] Add Profanity Filter </b>  | <img src="https://i.imgur.com/tskv8MM.png" width=55 height=40> |
| [PR #16](https://github.com/RocketChat/apps.ai.gif/pull/16) | <b> [Feat] Enable GIF preview and add action buttons </b>  | <img src="https://i.imgur.com/tskv8MM.png" width=55 height=40> |
| [PR #18](https://github.com/RocketChat/apps.ai.gif/pull/18) | <b> [Feat] Add Pagination in history </b>  | <img src="https://i.imgur.com/tskv8MM.png" width=55 height=40> |
| [PR #22](https://github.com/RocketChat/apps.ai.gif/pull/22) | <b> [Feat] Support upload GIF to RC Channel </b>  | <img src="https://i.imgur.com/tskv8MM.png" width=55 height=40> |
| [PR #23](https://github.com/RocketChat/apps.ai.gif/pull/23) | <b> [Feat] Add Help Command </b>  | <img src="https://i.imgur.com/tskv8MM.png" width=55 height=40> |
| [PR #24](https://github.com/RocketChat/apps.ai.gif/pull/24) | <b> [Feat] Implement bot and add onInstall message </b>  | <img src="https://i.imgur.com/tskv8MM.png" width=55 height=40> |
| [PR #26](https://github.com/RocketChat/apps.ai.gif/pull/26) | <b> [Bug] Fix app size too large to upload issue </b>  | <img src="https://i.imgur.com/tskv8MM.png" width=55 height=40> |

</div>

### Issues

   
<div align="center">
    
| Issue Link   | Description  | Status | 
| :-----------: | :------------------------------------:| :------:|
| [ISSUE #1](https://github.com/RocketChat/apps.ai.gif/issues/1) | <b>[CHORE] Initialize basic RC App Template</b> | <img src="https://i.imgur.com/ihaDyZS.png" width=55 height=40>
| [ISSUE #2](https://github.com/RocketChat/apps.ai.gif/issues/2) | <b>[Feat] Generate GIF directly from RC Chat </b> | <img src="https://i.imgur.com/ihaDyZS.png" width=55 height=40>
| [ISSUE #3](https://github.com/RocketChat/apps.ai.gif/issues/3) | <b>[Feat] Allow users to view past generations </b> | <img src="https://i.imgur.com/ihaDyZS.png" width=55 height=40>
| [ISSUE #4](https://github.com/RocketChat/apps.ai.gif/issues/4) | <b>[Feat] Enhance user query using LLM as NLP </b> | <img src="https://i.imgur.com/ihaDyZS.png" width=55 height=40>
| [ISSUE #9](https://github.com/RocketChat/apps.ai.gif/issues/9) | <b>[Feat] Add profanity filter to prompt and query </b> | <img src="https://i.imgur.com/ihaDyZS.png" width=55 height=40>
| [ISSUE #10](https://github.com/RocketChat/apps.ai.gif/issues/10) | <b>[Feat] Allow users to pass custom prompt </b> | <img src="https://i.imgur.com/ihaDyZS.png" width=55 height=40>
| [ISSUE #14](https://github.com/RocketChat/apps.ai.gif/issues/14) | <b>[Feat] Create a help command helping users to understand the app </b> | <img src="https://i.imgur.com/ihaDyZS.png" width=55 height=40>
| [ISSUE #15](https://github.com/RocketChat/apps.ai.gif/issues/15) | <b>[Feat] Enable user to view GIF preview and provide options to regenerate/approve the generation </b> | <img src="https://i.imgur.com/ihaDyZS.png" width=55 height=40>
| [ISSUE #17](https://github.com/RocketChat/apps.ai.gif/issues/17) | <b>[Feat] Allow pagination in history to support viewing more than 10 generations </b> | <img src="https://i.imgur.com/ihaDyZS.png" width=55 height=40>
| [ISSUE #19](https://github.com/RocketChat/apps.ai.gif/issues/19) | <b>[Bug] Upload GIF's to RC as the provider may decide to remove the generated GIF after some specific amount of time </b> | <img src="https://i.imgur.com/ihaDyZS.png" width=55 height=40>
| [ISSUE #20](https://github.com/RocketChat/apps.ai.gif/issues/20) | <b>[Feat] Send helper messages from app bot and add onInstall Message </b> | <img src="https://i.imgur.com/ihaDyZS.png" width=55 height=40>
| [ISSUE #28](https://github.com/RocketChat/apps.ai.gif/issues/28) | <b>[Bug] Options block message not sent via bot user </b> | <img src="https://user-images.githubusercontent.com/70485812/189489748-ed27630f-36e7-4eb9-a9a4-e082d6894490.png" width=55 height=40>

</div>

## Challenges we ran into 🔻

Building this app has been quite challenging as I was introduced to the Apps Framework and the RC UI Kit(Fuselage). I learned how these could be utilized and how the Apps Framework worked with the main Rocket Chat server. Some specific issues that I remember are:

1. **Repetitive requests issue**: This issue is quite common in most text based apps, where the frontend tries to call the backend for each request present. A common solution for this is debouncing and throttling. However, in my case the requirement was quite unique. Firstly, I needed to return a response and secondly I also needed to await it. By common convention, debouncing does not care about the cancelled request however I needed to care about them as well. Also, commonly any debounced function is not expected to be awaited however I required that as well. To resolve this issue, I created my own tailored implementation of debounced with Generics and Promises. You can learn more about it [here](https://medium.com/@asterjoules/resolving-repetitive-requests-issue-in-my-gsoc24-project-49eabd42c51b).
2. **App not notified of all keystrokes**: This issue also involves text input, and the issue was that my app was not notified of all the keystrokes that the user made. Due to which after a point anything that user entered I couldn't get it. You can find more details about the issue [here](https://github.com/RocketChat/Rocket.Chat/issues/32650). To resovle this I thought maybe there was a issue in Apps Framework, however later I found the issue was that the frontend was trying to make too many requests to the backend. Due to this, all the upcoming requests were denied. I easily solved this issue in the main Rocket.Chat Framework using debouncing(the same function I implemented above). I have raised the PR([#32952](https://github.com/RocketChat/Rocket.Chat/pull/32952)) for this issue with necessary changes and hopefully it will get merged soon. 
3. **Preview Title not showing up in preview component**: The issue here is that the preview title is taken in as a parameter for preview section, however it is not displayed. Currently, this is under consideration by the design team, and this will also be hopefully fixed soon! Learn more about it [here](https://github.com/RocketChat/Rocket.Chat/issues/32733).


## Thanking Mentors 🤝✨

I would like to express my sincere gratitude to my amazing mentor, [Nabhag Motivaras](https://www.linkedin.com/in/nabhag-motivaras-460b3b1aa/), for their invaluable guidance and support throughout this GSoC'24 journey. Their constant encouragement, technical expertise, and willingness to help have been instrumental in the success of this project. I am incredibly fortunate to have had the opportunity to learn from such a talented individual.

A big thank you to the entire Rocket.Chat developer community for their openness and support throughout the development process.

## Connect With Me 💬
<div align="center">

| **Student** | Aman Negi |
|:--------------------|:-------------------|
| **Organization** | [Rocket.Chat](https://rocket.chat/) |
| **Project** | [AI in-channel GIF Image Generator](https://summerofcode.withgoogle.com/programs/2024/projects/41d12z0y) |
| **GitHub** | [@amannegi](https://github.com/amannegi) |
| **LinkedIn** | [Aman Negi](https://www.linkedin.com/in/aman-negi-3a1a221a9/) |
| **Email** | <a href="mailto:asterjoules@gmail.com">asterjoules@gmail.com</a> |
| **Rocket.Chat** | [aman.negi](https://open.rocket.chat/direct/aman.negi) |
| **Project Github Repository** | [Apps.AI.GIF](https://github.com/RocketChat/Apps.AI.GIF) |
       
</div>

