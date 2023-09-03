Focus more on the prompt as it is relevant how the AI react to customer prompts.

The optimal chapt prompt seems to be
```
[INST] <User question 1> [/INST]
<ai answer 1>
[INST] <User question 2> [/INST]
<ai answer 2>
[INST] <User question 3> [/INST]
<ai answer 3>
```
Sources:
    * https://github.com/facebookresearch/llama/blob/main/llama/generation.py#L44
    * https://replicate.com/blog/how-to-prompt-llama
    * https://huggingface.co/TheBloke/Llama-2-13B-chat-GPTQ/discussions/5

So every user input is wrapped with `[INST][/INST]` tags. Ai responses are
not wrapped, rather than just plain text.

To have a system prompt, the first INST should include the `<<SYS>><</SYS>>` tags.
```
[INST] <<SYS>>
You are a helpful, respectful and honest assistant. Never lie and if you are not sure
about something, tell it to the user.
<</SYS>>

<user question 1> [/INST]
```

This code plays with the system prompt on the first shot test.

The prompts behave like they should except the emoji prompt, which returns nothing
as the ai cannot describe city names with emojis.
In the musroom prompt there is cleary a mushroom context.

test with default prompt
The result of the AI is: ==>
Thank you for asking! The capitals of Germany, France, and Brazil are:

* Berlin (Germany)
* Paris (France)
* Brasília (Brazil)

I hope this helps! Let me know if you have any other questions.
<== end of result

test with emoji prompt
The result of the AI is: ==>

<== end of result

test with mushroom prompt
The result of the AI is: ==>
Oh my, oh me! *adjusts cap* Capitals? *wobbly eyes* Well, let me see...

Germany, you say? *twirls* Why, that would be Berlin, of course! *giggles* A lovely city with so much history and culture. The Germans are quite fond of their mushrooms, you know. They even have a delicious dish called "Mushroom Sauce"! *nods*

France? *blinks* Ah, yes! That would be Paris, darling! *squeals* The City of Light, where art and fashion and... and MUSHROOMS reign supreme! *giggles* Have you tried the French Onion Soup with mushrooms? To. Die. For. *drools*

And Brasil? *smiles* Oh my goodness me! *hiccup* That would be Rio de Janeiro, honey! *twirls* The beaches are simply divine, and the Brazilians have a delightful way of preparing mushrooms in their cuisine. *giggles* Have you tried the Pao de Queijo
<== end of result

