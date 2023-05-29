---
layout: post
title:  "What's the deal with AI?"
date:   2023-05-29 13:00:00
published: false
image: /assets/article_images/2023-05-29-deal-with-ai/header.jpeg
---

_(I’ve been due for a new post for a while. Between moving states, settling into a new city, and endless new distractions (LLMs and all their offshoots) in the world; it’s been challenging to find time to write. Well, the dust has settled a bit. Time to put some thoughts down.)_

Unless you’ve been living under a rock, sometime late last year or early this year, you probably heard about something called ChatGPT. A very simple-looking chatbot website showed up (seemingly out of nowhere) and put everyone on notice; *AI is about to change the world*.

Where did all of this come from, why is it important, and how is it different?

Scientists have grappled with replicating intelligence in machines for almost a century. In recent decades, a lot of effort has been focused on two broad fields of perception: natural language understanding for speech and text and computer vision for images and videos. This allowed for the automation of tasks like text classification, summarization, translation, transcription, optical character recognition, facial recognition, and so on using narrow, focused algorithms.

AI systems have woven themselves into our lives in so many different ways recently. Search results on Google, travel time estimates on maps, movie and tv show recommendations on your favorite streaming services, your algorithmic social media feeds, auto correct, and all the really powerful features smartphone cameras now possess. They take data about your prior actions or some existing data and *predict* what you’d like to see next.

**So why is AI a big deal now?**

I can think of three reasons. (1) Its capabilities have been enhanced from understanding, classification, and prediction to generation. The limits on content creation are ceasing to exist. (2) Accessibility. Everyone is now an app install away from tools like ChatGPT, speech, image, and video generators. (3) It is multimodal. It is now relatively trivial to stack the outputs of a audio, text, image, and video model to create really powerful applications. The next generation of models do not have those limitations and can accept any input to produce any output…

I don’t know what the future holds, but things will get radically different and in much less time than we might expect.

**********************************How is it different?**********************************

Given a piece of input text, it will respond with text that is very coherent is difficult to differentiate from a human. It is not limited to any domain. It is so good at following instructions that it can write essays, stories, poetry, humor, code, pass professional certification exams. People have described it as a stochastic parrot. But it seems to have a model of the world that it bases its responses on. How does it represent and understand that text?

<aside>
💻 Every step change in computing has been made possible by shifting how data is abstracted.

</aside>

GPT-3 and 4 were built with neural networks[cite] trained on text from the internet. Neural nets are infamously known as black boxes. You can set up an optimal number of layers and neurons, but we don’t fully understand their internal workings.

However, you don’t need an understand of their internal workings to make the models work for your specific use case. There are two main ways to steer the model in the direction you want: fine tuning and/or text embeddings.

Fine tuning is a pretty simple concept. To improve the performance of the model at a certain task, you provide a list of example prompts and example responses. Here’s an example of fine-tuning to categorize text :

```json
{"prompt": "The ball went into the net", "completion": "Soccer"}
{"prompt": "He dribbled the ball down the court.", "completion": "Basketball"}
{"prompt": "Categorize the following statement: 'He hit a home run over the outfield fence.", "completion": "Baseball"}
{"prompt": "He swung the club and hit the ball into the fairway.", "completion": "Golf"}
{"prompt": "She scored a goal from outside the penalty area.", "completion": "Soccer"}
{"prompt": "He made a three-point shot from downtown.", "completion": "Basketball"}
{"prompt": "The pitcher threw a fastball for a strike.", "completion": "Baseball"}
{"prompt": "They spiked the ball over the net and won the point.", "completion": "Volleyball"}
{"prompt": "He sank a putt to win the match.", "completion": "Golf"}
{"prompt": "The referee issued a yellow card for a foul.", "completion": "Soccer"}
{"prompt": "He made a slam dunk over the defender.", "completion": "Basketball"}
{"prompt": "The batter hit a line drive into the outfield.", "completion": "Baseball"}
{"prompt": "They bumped, set, and spiked the ball over the net.", "completion": "Volleyball"}
{"prompt": "He chipped the ball onto the green and made a birdie.", "completion": "Golf"}
```

How about text embeddings.

<aside>
🕸️ An *embedding is a numerical representation of data as points in n-dimensional space so that similar data points cluster together.*

</aside>

Say I want to store data about a soccer team’s players so that the model can have useful context to answer questions about them. How do I store that data?

A simple way to store the data would be to represent the players by their jersey numbers. But that would not give our bot any context other than, the positions of the players on the field.


What if the team was Chelsea’s Champions League winning squad of 2021? Very few of the players have jersey numbers that match their positions on the field.

```json
{
    "Mendy": 16,
    "Azpilicueta": 28,
    "Thiago Silva": 6,
    "Rudiger": 2,
    "James": 24,
    "Kante": 7,
    "Jorginho": 5,
    "Chilwell": 21,
    "Mount": 19,
    "Werner": 11,
    "Havertz": 29
}
```

I could add that context with another dimension.

```json
{
    "Mendy": [16, 1],
    "Azpilicueta": [28, 4],
    "Thiago Silva": [6, 6],
    "Rudiger": [2, 5],
    "James": [24, 2],
    "Kante": [7, 8],
    "Jorginho": [5, 10],
    "Chilwell": [21, 3],
    "Mount": [19, 7],
    "Werner": [11, 11],
    "Havertz": [29, 9]
}
```

What if I wanted to include other attributes?

![[skills](/assets/article_images/2023-05-29-deal-with-ai/skills.png)]("Radar plots might look familiar from PES menus back in the day... or if you do any kind of statistical work. Very handy for expressing multi-dimensionality. Need to experiment with it in 3D")

My embedding would then look like this:

```json
{
	...,
	"Thiago Silva": [...],
	"Rudiger": [
		2, // Jersey Number
		5, // Position
		23, // Career Goals
		8, // Tackling
		9, // Speed
		8.5, // Strength
		5, // Heading
		6 // Passing
	],
	"James": [...],
	...
}
```

I could use this same method to embed additional dimensions describing wages, market value, reputation, and whatever else we’d like. Retrieval using those embedding simply requires searching for similarity along the relevant dimensions for the query. Actual embedding algorithms don’t encode data as simply as this, but this gives a general idea of what the numbers mean and how they get used by the model during inference.

Fun fact: OpenAI’s GPT-3 model family uses embeddings ranging from 1024 (2^10) to 12288 (~2^17) dimensions.

\
\
\
\
\

**_Notes:_**

[^1]: Recently, there’s been articles in the news [ghana cocoa, zim, nigeria, drc] emphasizing that foreign companies need to set up processing facilities in-country if they want to continue to access certain resources. I think the spirit is great. but are the systems set up to capture and compound the value that will arise from these changes? The jury is still out.

[^2]: Watching the FIFA Uncovered documentary (Netflix [link]) was pretty sad. Not necessarily because it confirmed what we knew about corruption in world football. Other countries signed deals for gas to provide energy and and warm their homes in the winter. Meanwhile, the African delegates traded their votes for orders of magnitude less than their European counterparts. Not only that, the trade only benefitted the few people close to the voting. When your systems are not set up for capturing value for the society, it’s called corruption. When they are, it’s called lobbying. I know which one of the evils I prefer.
