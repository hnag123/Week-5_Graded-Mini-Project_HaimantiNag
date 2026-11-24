# ADR-001: Architecture for Ecommerce Discovery Agent — From Shopping to Checkout

- **Status:** Proposed
- **Date:** 24 November 2026
- **Decision Type:** Application Architecture and Technology Selection
- **Project:** Ecommerce Discovery Agent: From Shopping to Checkout

---

## 1. Context

Traditional ecommerce platforms often require customers to search through multiple product listings, apply filters, compare specifications, and navigate several pages before making a purchase decision.

Customers may also struggle to describe their requirements using exact product names or technical specifications. Keyword-based search systems may fail to understand natural-language queries such as:

- "Find me a lightweight laptop for programming under ₹60,000."
- "I need wireless headphones with good noise cancellation for travelling."
- "Compare smartphones with good cameras and long battery life."

The proposed Ecommerce Discovery Agent aims to simplify this shopping journey by using AI and Retrieval-Augmented Generation (RAG) to understand customer intent, retrieve relevant products, compare alternatives, and guide customers toward checkout.

The architecture must prioritize accurate product discovery, relevant recommendations, reliable information retrieval, affordability, scalability, and a user-friendly shopping experience.

## 2. Decision Drivers

The architecture will be evaluated based on the following requirements:

1. **Natural-language understanding:** Interpret customer queries and identify product preferences, constraints, and requirements.
2. **Accurate product discovery:** Retrieve relevant products from a structured product catalogue.
3. **Personalized recommendations:** Rank products according to customer preferences, budget, and requirements.
4. **Product comparison:** Present important product attributes, specifications, prices, and differences.
5. **Reliable responses:** Ground AI-generated answers in retrieved product information to reduce hallucinations.
6. **Checkout integration:** Guide customers through cart management and the checkout process.
7. **Cost efficiency:** Minimize unnecessary LLM calls and optimize response time.
8. **Scalability:** Support future expansion to larger product catalogues and additional ecommerce categories.

## 3. Considered Options

### Option 1: Traditional keyword-based search

Use keyword matching and conventional database queries to retrieve products.

**Advantages:**
- Simple to implement.
- Fast retrieval for exact product searches.
- Low operational cost.

**Disadvantages:**
- Limited understanding of natural-language queries.
- Difficult to interpret complex customer preferences.
- Less effective when customers do not know exact product names.

### Option 2: LLM-only conversational shopping agent

Use a Large Language Model to interpret customer queries and generate product recommendations.

**Advantages:**
- Strong natural-language interaction.
- Flexible conversational experience.
- Can interpret complex customer requirements.

**Disadvantages:**
- May generate inaccurate or fabricated product information.
- Product recommendations may not reflect current prices or availability.
- Can become expensive with frequent model calls.

### Option 3: RAG-based ecommerce discovery agent

Combine an LLM with product catalogue retrieval, semantic search, structured filtering, and recommendation ranking.

**Advantages:**
- Retrieves relevant product information from a controlled catalogue.
- Supports natural-language product discovery.
- Reduces hallucinations through grounded responses.
- Enables product comparison and personalized recommendations.
- Can integrate with cart and checkout services.

**Disadvantages:**
- Requires product catalogue preparation and indexing.
- Needs additional retrieval and ranking logic.
- Requires careful handling of changing prices and inventory.

## 4. Decision

We will adopt a **RAG-based conversational ecommerce discovery architecture**.

The system will combine an LLM, product catalogue, retrieval mechanism, recommendation logic, and ecommerce checkout integration.

The agent will follow this workflow:

1. Accept a natural-language shopping query.
2. Identify customer intent, budget, product category, and preferences.
3. Convert the query into structured search filters and semantic search queries.
4. Retrieve relevant products from the product catalogue.
5. Rank and compare products based on relevance and customer preferences.
6. Generate grounded recommendations using retrieved product information.
7. Allow customers to ask follow-up questions and refine their choices.
8. Add selected products to the shopping cart.
9. Redirect or connect the customer to a secure checkout process.

## 5. Proposed Architecture

The application will contain the following logical components:

| Component | Responsibility |
|---|---|
| User Interface | Accept shopping queries and display recommendations |
| Conversation Manager | Maintain conversation context and manage follow-up queries |
| LLM / Prompt Layer | Understand customer intent and generate responses |
| Query Processing | Extract product category, budget, and preferences |
| Retrieval Engine | Retrieve relevant products using semantic and structured search |
| Product Catalogue | Store product names, descriptions, specifications, prices, and availability |
| Recommendation Engine | Rank products based on relevance and customer preferences |
| Comparison Module | Compare product attributes and highlight differences |
| Cart Service | Manage selected products and quantities |
| Checkout Integration | Connect customers to a secure checkout process |

### High-Level Workflow

```text
Customer
   |
   v
User Interface
   |
   v
Conversation Manager
   |
   v
LLM / Intent Extraction
   |
   v
Query Processing
   |
   v
Product Retrieval (RAG)
   |
   v
Product Catalogue
   |
   v
Recommendation and Ranking
   |
   v
Product Comparison
   |
   v
Customer Selection
   |
   v
Shopping Cart
   |
   v
Secure Checkout
```

## 6. Technology Considerations

The following technologies are proposed for implementation. Final selection may depend on project requirements and available resources.

| Layer | Proposed Technology |
|---|---|
| Programming Language | Python |
| LLM Integration | OpenAI-compatible API |
| Prompt Engineering | Zero-shot, Few-shot, and Structured Prompts |
| Embeddings | Embedding model for semantic search |
| Vector Database | FAISS or ChromaDB |
| Product Storage | JSON/CSV initially; relational database for future expansion |
| Backend | FastAPI |
| Frontend | Streamlit |
| Data Processing | Pandas |
| Checkout | Ecommerce platform or payment gateway sandbox |

## 7. Consequences

### Positive Consequences

- Customers can search using natural language instead of exact keywords.
- Recommendations are grounded in retrieved product catalogue information.
- Product comparisons become easier and more transparent.
- The architecture supports personalized shopping experiences.
- The system can be extended to additional product categories.
- Checkout integration creates a more complete shopping journey.

### Negative Consequences

- Maintaining accurate product information requires regular catalogue updates.
- Retrieval quality depends on product descriptions and embedding quality.
- LLM responses introduce latency and API costs.
- Additional safeguards are needed to prevent incorrect recommendations.
- Checkout integration introduces security and transaction-handling requirements.

## 8. Risks and Mitigation

| Risk | Mitigation |
|---|---|
| Hallucinated product details | Ground responses in retrieved catalogue records |
| Outdated prices | Retrieve current prices from the product source |
| Irrelevant recommendations | Combine semantic retrieval with structured filters and ranking |
| Slow responses | Optimize retrieval and limit unnecessary LLM calls |
| Poor product data quality | Validate and normalize catalogue information |
| Checkout errors | Use secure payment gateway integrations and transaction validation |
| Privacy concerns | Minimize collection of personal customer information |

## 9. Security Considerations

- Customer information should be handled securely.
- API keys and credentials must be stored in environment variables.
- Payment card details should be handled by a trusted payment gateway rather than stored directly by the agent.
- Checkout operations must require appropriate user confirmation.
- Product information and external data must be validated before being used.
- The system should protect against prompt injection and malicious product descriptions.

## 10. Success Criteria

The architecture will be evaluated using the following metrics:

- Product retrieval relevance and accuracy.
- Recommendation quality.
- Accuracy of product specifications and price information.
- Response latency.
- LLM API cost per shopping interaction.
- Customer query understanding.
- Successful cart operations.
- Successful checkout handoff or transaction completion in a sandbox environment.

## 11. Future Enhancements

Potential future improvements include:

- Personalized recommendations based on shopping history and explicit preferences.
- Multi-agent architecture for product discovery, comparison, and checkout assistance.
- Real-time inventory and price synchronization.
- Voice-based shopping assistance.
- Support for multiple ecommerce platforms.
- Recommendation evaluation using customer feedback and interaction data.

## 12. Conclusion

A RAG-based conversational architecture is selected for the Ecommerce Discovery Agent because it combines the flexibility of LLM-powered natural-language interaction with the reliability of product catalogue retrieval.

This architecture provides a foundation for transforming the traditional ecommerce experience into an intelligent shopping journey, helping customers move from product discovery and comparison to informed purchasing decisions and checkout.

## Project Structure Planned

Ecommerce-Discovery-Agent/
│
├── README.md
├── docs/
│   └── ADR-001-ecommerce-discovery-agent.md
├── data/
├── notebooks/
├── src/
│   ├── retrieval/
│   ├── recommendation/
│   ├── conversation/
│   └── checkout/
└── requirements.txt