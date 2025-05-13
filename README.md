# Prompt Engineering Cheatsheet (17 Techniques for 1B LLMs)

This cheatsheet summarizes 17 prompt engineering techniques, from beginner to advanced, to help you get more accurate, creative, or reliable responses from Large Language Models (LLMs), even smaller ones like a 1B parameter model.

---

## 1. Zero-Shot Prompting

*   **Core Idea:** Ask the model to perform a task or answer a question directly, without any examples.
*   **Key Benefit/When to Use:**
    *   Simple questions and answers.
    *   Basic text summarization.
    *   Quick brainstorming.
    *   When the LLM likely has enough general understanding.
*   **How to Implement:** Directly state your request. Can be improved by adding context like the target audience.
*   **Example:**
    *   **Before:** `What is photosynthesis?`
    *   **After:** `Explain photosynthesis to a 5-year-old child.`
    *   **Improvement:** The "After" prompt guides the model to produce a simpler, more engaging, and age-appropriate response.

---

## 2. Few-Shot Prompting

*   **Core Idea:** Provide a few examples (input/output pairs) to show the model the desired task and format. (One-Shot is a special case with one example).
*   **Key Benefit/When to Use:**
    *   Sentiment analysis (for specific labels).
    *   Simple code generation.
    *   Data extraction or reformatting.
    *   Generating text in a highly specific, non-standard style.
*   **How to Implement:** Include examples of `user` input and desired `assistant` output before your actual query.
*   **Example (Sentiment Classification):**
    *   **Before (Zero-Shot):** `Classify the sentiment of this movie review: 'The movie was okay, not great but not terrible.'` (Might be chatty)
    *   **After (Few-Shot):**
        ```
        User: Classify: 'This is the best movie I have ever seen!'
        Assistant: Positive
        User: Classify: 'I hated this film, it was a waste of time.'
        Assistant: Negative
        User: Classify: 'The movie was okay, not great but not terrible.'
        ```
    *   **Improvement:** The model learns the desired single-word output format.

---

## 3. Role Prompting

*   **Core Idea:** Instruct the LLM to adopt a specific persona or character (e.g., "Act as a seasoned travel guide").
*   **Key Benefit/When to Use:**
    *   Making interactions more engaging.
    *   Explanations for specific audiences.
    *   Generating creative content in a particular voice.
    *   Simulating dialogues or expert perspectives.
*   **How to Implement:** Typically in the system prompt or at the start of a user prompt: `You are [Role]...`
*   **Example:**
    *   **Before:** `Tell me about black holes.` (System: `You are a helpful assistant.`)
    *   **After:** `Professor Astra, I'm curious! Can you tell me all about those mysterious black holes?` (System: `You are Professor Astra, a friendly and slightly eccentric astronomer...`)
    *   **Improvement:** Response becomes more engaging, vivid, and uses analogies fitting the persona.

---

## 4. Style Prompting

*   **Core Idea:** Guide the LLM to write in a particular literary, artistic, formal, or informal style (e.g., "Write in the style of Ernest Hemingway").
*   **Key Benefit/When to Use:**
    *   Creative writing (stories, poems in specific styles).
    *   Content adaptation for different audiences.
    *   Matching a specific brand voice.
*   **How to Implement:** Specify the desired style in the prompt: `Write ... in the style of [style].`
*   **Example:**
    *   **Before:** `Write a short description of a sunset.`
    *   **After:** `Write a short description of a sunset in the style of a haiku.`
    *   **Improvement:** Output adheres to the specific stylistic constraints (e.g., 5-7-5 syllables for haiku).

---

## 5. Emotion Prompting

*   **Core Idea:** Instruct the LLM to generate a response conveying a specific emotion or from an emotional perspective.
*   **Key Benefit/When to Use:**
    *   Adding emotional depth to creative writing.
    *   Crafting messages with specific sentiment (thank you notes, apologies).
    *   Generating empathetic customer service responses.
*   **How to Implement:** Explicitly state the desired emotion: `Write this ... make it sound [emotion].`
*   **Example (Thank You Note):**
    *   **Before:** `Write a thank you note for a gift I received.`
    *   **After:** `Write a thank you note for a gift I received. Make it sound very excited and deeply grateful. The gift was a book I've wanted for ages...`
    *   **Improvement:** The note becomes warmer, more personal, and emotionally expressive.

---

## 6. Contextual Prompting

*   **Core Idea:** Provide the LLM with sufficient background information relevant to the request.
*   **Key Benefit/When to Use:**
    *   Personalized recommendations.
    *   Problem-solving with specific data.
    *   Content generation about specific topics.
    *   Multi-turn conversations.
*   **How to Implement:** Include all necessary details, history, preferences, or constraints in your prompt.
*   **Example (Gift Suggestion):**
    *   **Before:** `Suggest a gift.`
    *   **After:** `I need a gift suggestion. Recipient: My sister, 30. Occasion: Birthday. Interests: Fantasy novels, gardening, tea. Budget: Around $50.`
    *   **Improvement:** Suggestions become specific, relevant, and tailored.

---

## 7. Chain-of-Thought (CoT) Prompting

*   **Core Idea:** Encourage the LLM to "think step by step" or show its work, especially for tasks requiring multi-step reasoning.
*   **Key Benefit/When to Use:**
    *   Mathematical word problems.
    *   Logical reasoning puzzles.
    *   Commonsense reasoning.
    *   Debugging LLM responses by making the thought process visible.
*   **How to Implement:**
    *   **Zero-Shot CoT:** Add "Let's think step by step."
    *   **Few-Shot CoT:** Provide examples showing intermediate reasoning steps.
*   **Example (Math Word Problem):**
    *   **Before:** `Roger has 5 tennis balls. He buys 2 more cans of tennis balls. Each can has 3 tennis balls. How many tennis balls does he have now?` (Gives only final answer)
    *   **After:** `Roger has 5 tennis balls... How many tennis balls does he have now? Let's think step by step.`
    *   **Improvement:** The LLM includes its reasoning process, leading to more reliable answers for complex problems.

---

## 8. System Prompting

*   **Core Idea:** Provide high-level instructions, context, or persona guidelines in the "system message" to apply across an entire conversation.
*   **Key Benefit/When to Use:**
    *   Ensuring consistent LLM behavior or persona.
    *   Defining overall goals or constraints for a session.
    *   Simplifying user prompts by offloading standing instructions.
*   **How to Implement:** Use the `system` role in the message list for persistent instructions.
*   **Example (Concise Summarization):**
    *   **Before (User Prompt):** `Summarize the following text in one sentence: '[text]'` (System: Default)
    *   **After (System Prompt):**
        System: `You are a 'Concise Summarizer'. Your primary goal is to provide the shortest possible, grammatically correct summary... aim for just one clear sentence.`
        User: `[text_to_summarize]`
    *   **Improvement:** Method is more robust and scalable for multiple summarization tasks needing the same constraint.

---

## 9. Explicit Instructions Prompting

*   **Core Idea:** Be crystal clear, direct, and unambiguous in your requests, leaving little room for misinterpretation.
*   **Key Benefit/When to Use:**
    *   Specific output structure or content requirements.
    *   Avoiding certain topics.
    *   When length or conciseness is important.
    *   Complex tasks that could be interpreted in multiple ways.
*   **How to Implement:** Detail exactly what you want: format, length, content to include/exclude, specific points to address.
*   **Example (Writing about Apples):**
    *   **Before:** `Write about apples.`
    *   **After:** `Write a short paragraph about apples focusing on their nutritional benefits and common varieties. The paragraph should be exactly 3 sentences long. Mention at least two specific varieties. Do not discuss apple cultivation or history.`
    *   **Improvement:** Output is significantly more targeted and useful according to stated requirements.

---

## 10. Output Priming

*   **Core Idea:** Provide the LLM with the beginning of its desired response, nudging it towards a specific structure, format, or tone.
*   **Key Benefit/When to Use:**
    *   Guiding output format (e.g., lists, JSON).
    *   Ensuring a specific tone or starting phrase.
*   **How to Implement:** End the user's last message to naturally lead into the desired output format (e.g., `Here is the list:\n-`).
*   **Example (Listing Ingredients):**
    *   **Before:** `What are the ingredients for a simple vanilla cake?` (Might output a paragraph)
    *   **After:** `What are the ingredients for a simple vanilla cake? Please list them out.\nHere are the ingredients for a simple vanilla cake:\n-`
    *   **Improvement:** LLM generates a bulleted list as cued by the priming.

---

## 11. Rephrase and Respond (RaR)

*   **Core Idea:** Ask the LLM to first rephrase your request or explain its understanding of the task before generating the main response.
*   **Key Benefit/When to Use:**
    *   Complex, multi-faceted, or potentially ambiguous requests.
    *   When the cost of an incorrect response is high.
    *   To ensure the LLM has grasped all key constraints.
*   **How to Implement:** `First, briefly describe what kind of [task] you are planning to write about... Then, write [the task].`
*   **Example (Story Writing):**
    *   **Before:** `Write a story about a journey.`
    *   **After:** `I'd like a story about a journey. First, briefly describe what kind of journey you are planning to write about... Then, write a short story based on your description.`
    *   **Improvement:** Forces the LLM to commit to an interpretation, leading to a more focused story.

---

## 12. Step-Back Prompting

*   **Core Idea:** Guide the LLM to first consider broader concepts, principles, or general knowledge related to a specific question before answering it.
*   **Key Benefit/When to Use:**
    *   Questions involving nuanced distinctions or definitions (e.g., "Is a virus alive?").
    *   Complex or debated topics.
    *   Problem-solving that benefits from first-principles thinking.
*   **How to Implement:** Ask the LLM to explain general principles first, then apply them to the specific query.
*   **Example (Tomato Classification):**
    *   **Before:** `Is a tomato a fruit or a vegetable?`
    *   **After:** `I have a question about tomatoes. But first, please explain: 1. What is the botanical definition of a fruit? 2. What is the general culinary understanding of a vegetable? Now, using those definitions, explain whether a tomato is considered a fruit or a vegetable...`
    *   **Improvement:** Response is more comprehensive and educational, explaining the "why" behind the classification.

---

## 13. Self-Critique & Refinement

*   **Core Idea:** Instruct the LLM to: 1. Generate an initial response. 2. Critically evaluate its own response based on criteria. 3. Generate a revised version.
*   **Key Benefit/When to Use:**
    *   Improving creative tasks (slogans, story ideas).
    *   Ensuring clarity and accuracy in complex explanations.
    *   Refining summaries.
    *   Reviewing generated code.
*   **How to Implement:** Provide explicit steps for generation, critique (with criteria), and refinement.
*   **Example (Slogan Generation):**
    *   **Before:** `Write a short, catchy slogan for a new eco-friendly water bottle.`
    *   **After:** `I need a slogan... Please follow these steps: 1. Generate one initial slogan. 2. Critically evaluate your slogan: Is it catchy? Does it communicate "eco-friendly"? ...What are its weaknesses? 3. Based on your critique, provide an improved slogan.`
    *   **Improvement:** Encourages a more deliberative and refined generation process through structured self-reflection.

---

## 14. Goal Decomposition Prompting

*   **Core Idea:** Break down a large, complex task into smaller, manageable sub-goals or steps within the prompt itself.
*   **Key Benefit/When to Use:**
    *   Outputs with several distinct parts (e.g., planning an event, report with sections).
    *   Ensuring all necessary components are addressed.
    *   Guiding the LLM through a specific workflow.
*   **How to Implement:** List the components or stages of the desired output for the LLM to address sequentially.
*   **Example (Planning a Trip):**
    *   **Before:** `Plan a simple weekend trip to a nearby nature spot.`
    *   **After:** `I want to plan a trip. Please help by creating a plan that includes: 1. Suggest one specific type of nature spot. 2. List 3-4 essential items to pack... 3. Suggest one main activity for Saturday and Sunday. 4. Provide one important safety tip.`
    *   **Improvement:** Output is far more structured, comprehensive, and actionable.

---

## 15. Meta-Prompting

*   **Core Idea:** Use the LLM to help you create better prompts for another (or the same) LLM. "How should I ask you to do task X effectively?"
*   **Key Benefit/When to Use:**
    *   Unsure how to best phrase a complex request.
    *   Discovering more effective ways to prompt for specific outputs.
    *   Optimizing prompts for quality, specificity, or creativity.
*   **How to Implement:** Describe the task you want an LLM to do and the desired characteristics of the output, then ask the current LLM to write the prompt you should use.
*   **Example (Generating Fantasy Story Ideas):**
    *   **Before (User's thought):** `Give me some fantasy story ideas.` (Too basic)
    *   **After (Meta-Prompt):** `I want to use an LLM to generate 3 distinct fantasy story ideas. For each idea, I need: a) A unique main character. b) A compelling conflict. c) A unique magical element. Please write out the actual, detailed prompt I should use.`
    *   **Improvement:** The LLM generates a much more detailed and structured prompt for the user to then use for their original task.

---

## 16. ReAct (Reason + Act)

*   **Core Idea:** Enable LLMs to solve complex tasks by interleaving reasoning (breaking down the problem) with acting (simulating information gathering or tool use).
*   **Key Benefit/When to Use:**
    *   Multi-hop question answering.
    *   Fact verification.
    *   Complex problem solving requiring decomposition and information synthesis.
    *   Making the LLM's problem-solving process explicit.
*   **How to Implement:** Instruct the LLM to follow a "Thought, Action, Observation" cycle until it can answer the main question.
*   **Example (Multi-part Question):**
    *   **Before:** `Who was the U.S. president when the first person walked on the moon, and what was the name of that astronaut?`
    *   **After:** `Answer: "[Question]". To answer this, please follow a ReAct-like process. For each step, state: Thought: [reasoning] Action: [info needed] Observation: [hypothetical result] ... Then, provide the final answer.`
    *   **Improvement:** Forces the LLM to break down the question and make its "knowledge lookup" process more explicit.

---

## 17. Thread-of-Thought (ThoT)

*   **Core Idea:** Encourage the LLM to maintain a coherent and connected line of reasoning or narrative across multiple turns or a long piece of generated text.
*   **Key Benefit/When to Use:**
    *   Long-form content generation (essays, articles).
    *   Complex explanations requiring logical flow.
    *   Multi-turn problem solving.
    *   Extended conversations to maintain focus.
*   **How to Implement:** Provide a structured outline and explicitly ask the LLM to ensure logical flow, use transition phrases, and connect each part to the previous one.
*   **Example (Explaining a Complex Process):**
    *   **Before:** `Explain how a bill becomes a law in the US.` (Might be disjointed)
    *   **After:** `I need an explanation of how a bill becomes a law... Please structure your explanation as follows: 1. Introduction... 2. Bill Introduction... [etc.] ... Throughout your explanation, ensure each stage logically follows the previous one, maintaining a clear "thread".`
    *   **Improvement:** The resulting explanation is much more coherent, structured, and easier to follow.

---

Experiment with these techniques to significantly improve the quality and relevance of responses from your LLM interactions!
