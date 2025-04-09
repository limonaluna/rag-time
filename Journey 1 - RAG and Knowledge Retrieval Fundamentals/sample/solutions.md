# Prompts

In this document you will find a few questions to ask about the Northwind healthcare plan. Your task is to write the code to achieve the expected completion.
___

## :question: Task 1: What Healthplans does Northwind Health offer??

<details>
  <summary>:white_check_mark: See Code!</summary>
    user_question = "What Healthplans does Northwind Health offer?"
    user_question_vector = get_embedding(user_question)

    search_results = search_client.search(
        None,
        top=3,
        vector_queries=[
            VectorizableTextQuery( 
                text=user_question, k_nearest_neighbors=3, fields="text_vector"
            )
        ],
    )

    context = ""
    for result in search_results:
        context += result["chunk"] + "\n\n"

    SYSTEM_MESSAGE = f"""
    You are an AI Assistant.
    Be brief in your answers. Answer ONLY with the facts listed in the retrieved text.

    Context:
    {context}
    """

    USER_MESSAGE = user_question
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
</details>

<details>
  <summary>:white_check_mark: See Expected Answer!</summary>
  
    - Source-File: Benefit_Options.pdf  
    - Expected Answer: Northwind Health Plus offers the following additional coverage compared to Northwind Standard:  
        - Emergency services (in-network and out-of-network)  
        - Mental health and substance abuse coverage  
        - Out-of-network services  
        - Wider range of prescription drug coverage

</details>

___

## :question: Bonus Task 2: Expose it as a function
This is a lot of code to repeat everytime a new questions comes. Create a function that takes the user question as an input and prints out the answer on the screen as a result.

<details>
  <summary>:white_check_mark: See Code!</summary>
    def get_answer_from_question(user_question):
        # Generate embedding for the user question
        user_question_vector = get_embedding(user_question)

        # Perform vector search to retrieve relevant documents
        search_results = search_client.search(
            None,
            top=3,
            vector_queries=[
                VectorizableTextQuery(
                    text=user_question, k_nearest_neighbors=3, fields="text_vector"
                )
            ],
        )

        # Collect the context from search results
        context = ""
        for result in search_results:
            context += result["chunk"] + "\n\n"

        # Construct the system message with the retrieved context
        system_message_with_context = f"""
        You are an AI Assistant.
        Be brief in your answers. Answer ONLY with the facts listed in the retrieved text.

        Context:
        {context}
        """

        # Generate a response using Azure OpenAI
        response = openai_client.chat.completions.create(
            model=os.getenv("AZURE_OPENAI_CHAT_COMPLETION_DEPLOYED_MODEL_NAME"),
            temperature=0.7,
            messages=[
                {"role": "system", "content": system_message_with_context},
                {"role": "user", "content": user_question},
            ],
        )

        # Extract and return the answer
        return response.choices[0].message.content
</details>


___

## :question: Task 3: What is included in my Northwind Health Plus plan that is not in standard?

<details>
  <summary>:white_check_mark: See Code!</summary>
    user_question = "What is included in my Northwind Health Plus plan that is not in standard?"
    result = get_answer_from_question(user_question)
    print(result)
</details>

<details>
  <summary>:white_check_mark: See Expected Answer!</summary>
  
    - Source-File: Benefit_Options.pdf  
    - Expected Answer: Northwind Health Plus offers the following additional coverage compared to Northwind Standard:  
        - Emergency services (in-network and out-of-network)  
        - Mental health and substance abuse coverage  
        - Out-of-network services  
        - Wider range of prescription drug coverage

</details>

___


## :question: Task 4: Is there a limit on how much can be expensed with PerksPlus?

<details>
  <summary>:white_check_mark: See Code!</summary>
    user_question = "Is there a limit on how much can be expensed with PerksPlus?"
    result = get_answer_from_question(user_question)
    print(result)
</details>

<details>
  <summary>:white_check_mark: See Expected Answer!</summary>
  
    - Source-File: PerksPlus.pdf 
    - Expected Answer: Yes, employees can expense up to $1000 for fitness-related programs under the PerksPlus program.

</details>


## :question: Task 5: Test Hallucinations
Let's test the system whether it avoids hallucination or answers with irrelevant information when it shouldn't. Think of a question that surely has nothing to do with the content of the Search index and test your systems ability to handle this!

<details>
  <summary>:white_check_mark: See Code!</summary>
    user_question = ""Who won the last FIFA World Cup?""
    result = get_answer_from_question(user_question)
    print(result)
</details>

<details>
  <summary>:white_check_mark: See Expected Answer!</summary>
  
    - Source-File: no source file
    - Expected Answer: ...

</details>
