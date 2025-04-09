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

    "Does PerksPlus support reducing anxiety or stress?"

    🔍 Assumption:
    - Keyword Search: Will likely fail or underperform, as the exact phrase "anxiety" isn’t in the document.
    - Vector Search: Should perform well — the document mentions “reduce stress,” “improve mood,” and “mental health.”

    Expected Outcome:
    ✅ Vector search performs better
    ❌ Keyword search misses or ranks irrelevant results

    
</details>

<details>
  <summary>:white_check_mark: See Code!</summary>

    question = "Does PerksPlus support reducing anxiety or stress?"
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

