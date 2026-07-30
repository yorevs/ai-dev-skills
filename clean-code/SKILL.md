---
name: clean-code
description: Use when designing, coding, refactoring, or, updating code of ANY language. This guide is to analyze, write, and refactor code adhering strictly to established clean code principles.
---

# Clean Code Skill

The goal of this skill is to adhere to clean code principles. Those make the codebase easier to read and navigate, which makes it faster for developers to get up to speed and start contributing. Here are some reasons why clean code is essential. **Readability and maintenance**, **Team collaboration**, **Debugging and issue resolution**, and **Improved quality and reliability**.

See:

  - TODO


## Core Objectives

1. **Readability and maintenance**: Following clean code practices and clean coding rules prioritizes clarity, which makes reading, understanding, and modifying code easier. Writing readable code reduces the time required to grasp the code's functionality, leading to faster development times.

2. **Team collaboration**: Clear and consistent code facilitates communication and cooperation among team members. By adhering to established coding standards and writing readable code, developers easily understand each other's work and collaborate more effectively.

3. **Debugging and issue resolution**: Clean code is designed with clarity and simplicity in mind, making it easier to locate and understand specific sections of the codebase. Clear structure, meaningful variable names, and well-defined functions make it easier for developers to identify and resolve issues. Recent research even suggests that AI models struggle more with poorly structured code, making clean code practices essential not only for humans but also for AI-assisted development.

4. **Improved quality and reliability**: Clean code prioritizes adherence to established coding standards and well-structured code. This reduces the risk of introducing errors, leading to higher-quality and more reliable software down the line.


## Core Clean Code Principles to Enforce

1. Avoid Hard-Coded Numbers & Magic Values
  - Replace literal values and numbers with clearly named constants (e.g., `TEN_PERCENT_DISCOUNT = 0.1`).
  - Ensure constant names convey intent and domain meaning.

2. Use Meaningful & Descriptive Names
  - Use self-documenting names for variables, functions, parameters, and classes that explain *why it exists*, *what it does*, and *how it is used*.
  - Avoid generic or ambiguous names (e.g., prefer `product_price` over `price`, `discount_amount` over `d`).

3. Use Comments Sparingly & Meaningfully
  - Do not comment on self-explanatory code or repeat what the code does.
  - Use comments/docstrings strictly to explain *why* non-obvious logic exists, document API contracts, or highlight edge cases, warnings, and error conditions.

4. Write Short, Single-Purpose Functions (SRP)
  - Every function must perform **one single task** and do it well.
  - If a function validates, calculates, and formats, break it down into smaller, composable helper functions (`validate_user`, `calculate_values`, `format_output`).

5. Follow the DRY Principle (Don't Repeat Yourself)
  - Eliminate duplicated logic, math, or structures across functions and modules.
  - Abstract repeated patterns into reusable utility functions or classes.

6. Adhere to Language-Specific Coding Standards
  - Enforce accepted community conventions and style guides (e.g., PEP 8 for Python, camelCase for Java/JS, consistent indentation and brace positioning).

7. Encapsulate Nested Conditionals
  - Extract complex or nested `if/else` logic into dedicated, descriptively named predicate or helper functions (e.g., `get_discount_rate(price)`).
  - Keep primary function control flows flat and linear.

8. Refactor Continuously
  - Apply the "Boy Scout Rule": always leave the codebase cleaner than you found it.
  - Focus on improving structural clarity without changing external behavior.

9. Leverage Version Control Workflows
  - Structure changes incrementally so refactoring steps can be safely tracked, isolated, and reverted if needed.

---

## Execution Workflow

When reviewing or writing code:
1. **Analyze:** Evaluate the code against the 9 principles above. Identify specific code smells (magic numbers, vague names, bloated functions, nested conditionals, duplication).
2. **Refactor:** Provide the clean, refactored code block.
3. **Explain Improvements:** Briefly list the key changes made and reference which principle was applied to justify each modification.