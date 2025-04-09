# Solutions for the Tasks from Journey 2

In this document you will find the solutions for the Tasks from Journey 2.

Let's have a look at the data of our search index and try to think how users might ask questions - and with which search query type the relevant chunks would be retrieved best!

1. Review content of the PerksPlus.pdf
2. Formulate two questions that users might ask about this content
3. Make assumptions about which search method will perform better (focus on keyword search vs. vector search)
4. Test the assumption by executing both searches and comparing the retrieved results.
___

## :question: Question Example 1

<details>
  <summary>:white_check_mark: See Example Question 1!</summary>

    "Can I get reimbursed for soccer?"

    🔍 Assumption:
    - Keyword Search: May miss it unless "soccer" is explicitly mentioned (it's not).
    - Vector Search: Likely to succeed, since "sports team fees" is listed.

    Expected Outcome:
    ✅ Vector search performs better
    ❌ Keyword search misses or ranks irrelevant results

    
</details>

<details>
  <summary>:white_check_mark: See Code!</summary>

    question = "Can I get reimbursed for soccer?"
    results_keyword = search_client.search(search_text=question, top=5, select=["title", "chunk"])

    print("Key word search results")
    display_results(results_keyword)

    results_vector = search_client.search(vector_queries=[VectorizableTextQuery(text=question, k_nearest_neighbors=50, fields="text_vector")], top=5, select=["title", "chunk"])

    print("Vector search results")
    display_results(results_vector)
    
</details>

<details>
  <summary>:white_check_mark: See Expected Answer!</summary>
  
  Key word search results:

    | Title                                         | Chunk                                                                                                                                                                                                                       | @search.score |
    |-----------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|
    | PerksPlus.pdf                                 | PerksPlus Health and Wellness Reimbursement Program for Contoso Electronics Employees This document contains information generated using a language model (Azure OpenAI). The information contained in this document is only for demonstration purposes and does not reflect the ... | 11.965925     |
    | PerksPlus.pdf                                 | equipment purchases • Sports team fees • Health retreats and spas • Outdoor adventure activities (such as rock climbing, hiking, and kayaking) • Group fitness classes (such as dance, martial arts, and cycling) • Virtual fitness programs (such as online yoga and workout classes) In additi... | 9.303395      |
    | Northwind_Standard_Benefits_Details.pdf       | the risks and benefits of the treatment with your provider before beginning treatment. Massage Therapy COVERED SERVICES: Massage Therapy At Contoso, we understand the importance of taking time to care for yourself and to reduce stress. That is why Northwind Health offers massage therapy co... | 8.995705      |
    | Northwind_Health_Plus_Benefits_Details.pdf    | necessary. It also does not cover services provided by non-network providers. Tips for Employees If you or someone you care about is struggling with SUD, there are a few things you can do to get the most out of your Northwind Health Plus plan: • Talk to your doctor or a mental health prof... | 7.397019      |
    | Northwind_Health_Plus_Benefits_Details.pdf    | accurate and complete information to the review team. • If your coverage is denied, talk to your doctor about appealing the decision. • If you are considering a service or medication that is not covered by Northwind Health Plus, ask your doctor about other options that may be available. Pe... | 5.692018      |

    Vector search results:


</details>

___

## :question: Question Example 2

<details>
  <summary>:white_check_mark: See Example Question 2!</summary>

    "Is horseback riding considered eligible under PerksPlus?"

    🔍 Assumption:
    - Keyword Search: Strong — “horseback riding lessons” is explicitly listed.
    - Vector Search: Also strong, maybe even more flexible.

    Expected Outcome:
    🟡 Both work

    
</details>

<details>
  <summary>:white_check_mark: See Code!</summary>

    question = "Is horseback riding considered eligible under PerksPlus?"
    results_keyword = search_client.search(search_text=question, top=5, select=["title", "chunk"])

    print("Key word search results")
    display_results(results_keyword)

    results_vector = search_client.search(vector_queries=[VectorizableTextQuery(text=question, k_nearest_neighbors=50, fields="text_vector")], top=5, select=["title", "chunk"])

    print("Vector search results")
    display_results(results_vector)
    
</details>

<details>
  <summary>:white_check_mark: See Expected Answer!</summary>
  
    Key word search results:

    | Title                                      | Chunk                                                                                                                                                                                                                       | @search.score |
    |--------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|
    | PerksPlus.pdf                              | equipment purchases • Sports team fees • Health retreats and spas • Outdoor adventure activities (such as rock climbing, hiking, and kayaking) • Group fitness classes (such as dance, martial arts, and cycling) • Virtual fitness programs (such as online yoga and workout classes) In additi... | 12.768233     |
    | Northwind_Standard_Benefits_Details.pdf    | Northwind Standard plan offers a right of recovery for any services that were already paid for by the insured. This is a great feature for employees to be aware of, as it can help to save time and money. This right of recovery means that if the insured has already paid for a service that is co... | 7.433744      |
    | PerksPlus.pdf                              | PerksPlus Health and Wellness Reimbursement Program for Contoso Electronics Employees This document contains information generated using a language model (Azure OpenAI). The information contained in this document is only for demonstration purposes and does not reflect the ... | 6.615756      |
    | Northwind_Health_Plus_Benefits_Details.pdf | procedures that are typically done in a surgical center. All services must be medically necessary, and prior authorization may be required for some services. Exceptions There are some exceptions to coverage for surgical center care. The plan does not cover cosmetic or elective procedures, e... | 5.446031      |
    | Northwind_Health_Plus_Benefits_Details.pdf | questions or concerns about your coverage, it is important to contact Northwind Health Plus directly to ensure that you have the coverage you need. In addition to understanding the coverage you have, it is also important to understand the risks associated with surgery. It is important to discu... | 4.855504      |

    Vector search results:


</details>
