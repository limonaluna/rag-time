# Prompts

In this document you will find a few questions to ask about the Northwind healthcare plan. Your task is to write the code to achieve the expected completion.
___

## :question: Question 1: Is there a limit on how much can be expensed with PerksPlus?

<details>
  <summary>:white_check_mark: See solution!</summary>
  ```
    USER_MESSAGE = "Is there a limit on how much I can expense through PerksPlus?"
    response = openai_client.chat.completions.create(
        model=os.getenv("AZURE_OPENAI_CHAT_COMPLETION_DEPLOYED_MODEL_NAME"),
        temperature=0.7,
        messages=[
            {"role": "system", "content": SYSTEM_MESSAGE},
            {"role": "user", "content": USER_MESSAGE},
        ],
    )

    answer = response.choices[0].message.content
    print(answer)
  ```
    Expected Answer:
    Source-File: PerksPlus.pdf
    Text-Chunk: With PerksPlus, employees have the opportunity to expense up to $1000 for fitness-related programs, making it easier and more affordable to maintain a healthy lifestyle.

</details>


