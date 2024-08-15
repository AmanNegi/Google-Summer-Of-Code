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

   

## Demo

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


