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

## Project Abstract

This project introduces an innovative Rocket.Chat application that allows communication between users through AI Generated GIFs. This empowers users to generate entirely original GIFs based on descriptive prompts, this app transcends the traditional GIF features of Rocket.Chat. It's integration into Rocket.Chat ensures a seamless experience allowing users to generate and send GIFs directly from Rocket.Chat. Users can either provide their own prompt or rely on an LLM generated prompt based on user query.

## Deliverables

1. **OnInstallation Message**: When user installs the `AI.GIF` app from the marketplace, they are introduced to the app via our bot. The welcome message explains the basics about the app what are the basic setup requirements and how to get started.
2. **Helper Message**: Users can access the command `/gen-gif help` to get instructions on how to utilize the app and what all commands & features are available.
3. **Generate GIF using prompt**: Users can utilize the command `/gen-gif p "prompthere"` to generate a GIF based on the prompt provided. The GIF generated is shown as preview first and the user can then decide to send the GIF in the channel.
4. **Generate GIF using query**: Users can uitilize the command `/gen-gif q "queryhere"` to firstly get a set(4) of prompt suggestions based on query. The user can then shortlist the best prompt and utilize it to generate the GIF. Once generated, the GIF is only visible to the user who generates it. The user is provided with action buttons to either regenerate or send the generated GIF.
5. **View Generations**: Users can utilize the command `/gen-gif history <pagenumber>` to view the past generations. As RC only allows showing 10 items at a time, the app provides a workaround in the form of pagination. The user can pass page numbers (0, 1, 2, 3 ...) to get the expected page of history.
6. **Webhook based App**: To ensure a non-blocking experience, the app utilized webhooks to automatically update the client about the GIF generation process. As the GIF generation is a time taking process, client awaiting for the response is not the suggested approach.
7. **Profanity Filtering**: The app utilizes LLM as for a robust NSFW content filter safeguarding the platform by preventing the generation of inappropriate GIFs.
8. **Storage Solutions**: The app takes cares of storing the generated GIFs safely on the Rocket.Chat server, ensuring no foreign dependency and complete availability.

   





