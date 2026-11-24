## Step 6 — Reflection
## 1. Which strategy won, and on what dimension?
Based on my experiment, Few-shot prompting was the best-performing strategy in terms of accuracy, achieving a mean accuracy of 3.0 out of 3, meaning all three target fields were correctly extracted on average. COT, Structured/Role-based, and Zero-shot prompting each achieved a mean accuracy of 2.9 out of 3.
All four strategies achieved a 100% parse success rate and a mean LLM judge score of 25 out of 25, indicating that every strategy produced consistently parseable responses and received the maximum average judge rating.
However, Zero-shot prompting performed best in terms of efficiency. It had the lowest estimated total cost ($0.000464) and the fastest median latency (2.358 seconds). Therefore, Few-shot was the winner for accuracy, while Zero-shot was the winner for cost and speed.

## 2. What surprised you?
One result that surprised me was that Zero-shot prompting performed almost as well as Few-shot prompting, achieving 2.9 accuracy compared with Few-shot's 3.0. I initially expected that providing examples through Few-shot prompting would create a much larger improvement in extraction accuracy.
Another surprising result was that all four strategies achieved 100% parse success and the maximum average judge score of 25. This suggests that all the strategies generated well-formatted and relevant responses, although their field-level accuracy differed slightly. I also noticed that Zero-shot prompting was significantly faster and cheaper than the other strategies.

## 3. Which strategy would I choose first for my capstone project?
For my capstone project, "Ecommerce Discovery Agent: From Shopping to Checkout," I would choose Few-shot prompting as my starting strategy. An ecommerce agent needs to understand customer requirements and extract product information such as product names, brands, prices, features, and specifications accurately. Since Few-shot prompting achieved the highest accuracy in my experiment, I would use examples to guide the model toward more consistent and reliable product discovery results.

## 4. What would I try next with another day?
If I had another day, I would test the strategies using a larger and more diverse dataset containing complex job descriptions and ambiguous experience requirements. I would also experiment with different models and refine the prompts by combining Few-shot examples with structured output instructions. For my capstone project, I would additionally test the prompts on real-world ecommerce product descriptions and customer queries to evaluate how accurately the agent identifies relevant products and compares their features.

## Conclusion
This experiment helped me understand that different prompting strategies offer different advantages. Few-shot prompting provided the highest accuracy, whereas Zero-shot prompting offered the best cost and latency performance. I learned that choosing a prompting strategy depends on the application's priorities, and that accuracy, response consistency, cost, and speed must all be considered when developing a practical AI application.
