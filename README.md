Rayeva AI – Structured Product Categorization System
Project Overview

Modern e-commerce platforms require structured product categorization for:

Search optimization

SEO metadata generation

Sustainability filtering

Analytics and reporting

However, Large Language Models (LLMs) typically produce unstructured and unpredictable outputs.

This project demonstrates a controlled AI integration architecture where:

AI outputs are strictly structured

Business logic validates AI responses

Only verified data is stored in the database

AI is treated as a suggestion engine, not a decision authority

Architecture Overview
User Input
    ↓
Business Logic Layer (process_product)
    ↓
AI Layer (ai_generate_product_category)
    ↓
Structured Output Validation
    ↓
Whitelist Enforcement
    ↓
Database Storage (SQLite)
    ↓
Logging
Design Principle

The system follows separation of concerns:

Layer	Responsibility
AI Layer	Generates structured product metadata
Validation Layer	Ensures schema correctness
Business Logic Layer	Enforces deterministic rules
Database Layer	Stores validated data
Logging Layer	Tracks system interactions
Structured AI Output Enforcement

All AI outputs must follow this JSON schema:

{
  "primary_category": "string",
  "sub_category": "string",
  "seo_tags": ["list of strings"],
  "sustainability_filters": ["list of strings"]
}

Validation ensures:

Required keys are present

Data types are correct

Hallucinated outputs are rejected

Only structured data enters the database

Business Logic Grounding

AI outputs are constrained using a whitelist:

ALLOWED_CATEGORIES = ["Personal Care", "Home", "Electronics"]

If the AI generates an invalid category, the system raises an error and blocks insertion.

This ensures deterministic control over probabilistic AI outputs.

Error Handling Strategy

The system includes:

Structured output validation

Category whitelist enforcement

Controlled exception handling

Runtime restart validation to ensure reproducibility

Database Integration

Validated product data is stored in SQLite with:

Product name

Primary category

Sub-category

SEO tags

Sustainability filters

Only validated outputs are inserted into the database.

How to Run

Restart runtime

Run all notebook cells

Execute:

process_product("Bamboo Toothbrush", "Eco friendly oral care product")

View stored records:

cursor.execute("SELECT * FROM products")
cursor.fetchall()
Engineering Highlights

Clear separation of AI and business logic

Strict structured output enforcement

Deterministic validation layer

Database persistence

Enterprise-style architecture thinking

Conclusion

This project demonstrates responsible AI integration by:

Treating AI as probabilistic

Enforcing structured contracts

Applying deterministic validation

Maintaining architectural separation

The result is a controlled, scalable, enterprise-ready AI pipeline.
