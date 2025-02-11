# Basics of Probability

Probability is a way to measure how likely something is to happen. The probability of an event is always between 0 and 1:

- **0** means impossible (e.g., rolling a 7 on a standard die).
- **1** means certain (e.g., the sun rising tomorrow).
- A probability of **0.5** means a 50% chance (e.g., flipping a fair coin and getting heads).

## Example: Coin Flip

Imagine flipping a fair coin:

- There are two possible outcomes: Heads (H) or Tails (T).
- Since the coin is fair, both outcomes are equally likely.

The probability of getting heads is:

```math
P(H) = \frac{\text{Number of favorable outcomes}}{\text{Total outcomes}} = \frac{1}{2} = 0.5
```

The probability of getting tails is also 0.5.

## Example: Rolling a Die

If you roll a 6-sided die, each side has an equal chance of appearing:

- **Probability of rolling a 3:**

```math
P(3) = \frac{1}{6} \approx 0.1667
```

- **Probability of rolling an even number (2, 4, or 6):**

```math
P(\text{even}) = \frac{3}{6} = 0.5
```
---

### **Mutually Exclusive vs. Non-Mutually Exclusive Events**

#### **1. Mutually Exclusive Events**
Two events are **mutually exclusive** if they **cannot happen at the same time**.

##### **Example: Rolling a Die**
- When rolling a six-sided die, the events "rolling a **2**" and "rolling a **5**" are **mutually exclusive** because you can only get **one number at a time**.
- Mathematically:
    ```math
    P(2 \text{ or } 5) = P(2) + P(5) = \frac{1}{6} + \frac{1}{6} = \frac{2}{6}
    ```

##### **Example: Flipping a Coin**
- The events **"getting heads"** and **"getting tails"** are mutually exclusive because a coin can’t land on both sides at once.

**Rule**: If two events are mutually exclusive:
```math
P(A \text{ or } B) = P(A) + P(B)
```

---

### **2. Non-Mutually Exclusive Events**
Two events are **non-mutually exclusive** if they **can happen at the same time**.

##### **Example: Drawing a Card**
When drawing a card from a deck:
- Event A: "Getting a red card" (26/52 cards)
- Event B: "Getting a King" (4/52 cards)
- Both events overlap with red Kings (2 cards)

The probability calculation:
```math
P(\text{Red or King}) = P(\text{Red}) + P(\text{King}) - P(\text{Red and King})
```
```math
= \frac{26}{52} + \frac{4}{52} - \frac{2}{52} = \frac{28}{52}
```

##### **Example: Daily Activities**
Consider "Watching TV" and "Using Phone":
- These events can occur simultaneously
- A person can watch TV while using their phone
- They are non-mutually exclusive events

**Rule for Non-Mutually Exclusive Events:**
```math
P(A \text{ or } B) = P(A) + P(B) - P(A \text{ and } B)
```
---

### **Key Difference**

| Type | Can Happen Together? | Formula |
|------|---------------------|---------|
| **Mutually Exclusive** | ❌ No | P(A or B) = P(A) + P(B) |
| **Non-Mutually Exclusive** | ✅ Yes | P(A or B) = P(A) + P(B) - P(A and B) |

---
### Conditional Probability

Conditional probability measures the likelihood of an event happening given that another event has already occurred.

#### Basic Formula
```math
P(A|B) = \frac{P(A \text{ and } B)}{P(B)}
```
Where P(A|B) reads as "probability of A given B"

#### Real-World Examples

##### 1. Weather Example
- Suppose you want to know the probability of it being cold (A) given that it's raining (B)
- If:
    - P(cold and rain) = 0.15
    - P(rain) = 0.3
```math
P(\text{cold}|\text{rain}) = \frac{0.15}{0.3} = 0.5
```
This means there's a 50% chance it's cold when it's raining.

##### 2. Card Drawing Example
Consider drawing two cards in sequence:
- Probability of drawing second ace given first card was ace:
```math
P(\text{ace}_2|\text{ace}_1) = \frac{3}{51}
```
Because:
- Only 3 aces remain
- Only 51 cards left in deck

#### Key Points
- Conditional probability always depends on the occurrence of the first event
- The vertical bar | means "given that"
- The probability must be recalculated based on the new information
---
# Bayes' Theorem - Explanation with Examples

## What is Bayes' Theorem?
Bayes' Theorem is a fundamental concept in probability that helps us update our beliefs when we get new information. It is widely used in fields like **machine learning, statistics, decision-making, and Kalman filters**.

Mathematically, Bayes' Theorem is expressed as:

```math
P(A | B) = \frac{P(B | A) \cdot P(A)}{P(B)}
```

Where:
- `P(A | B)` → **Posterior Probability** (Probability of event `A` given that event `B` has occurred)
- `P(B | A)` → **Likelihood** (Probability of event `B` occurring given that event `A` is true)
- `P(A)` → **Prior Probability** (Initial probability of event `A` occurring before considering new evidence)
- `P(B)` → **Total Probability of event `B` occurring**

---

## Intuitive Explanation
Bayes' Theorem helps us answer: 
👉 **"If we already know something (prior), and get new evidence, how should we update our belief?"**

---

## Why is the Denominator Different in Bayes' Theorem?
The **denominator** in Bayes’ Theorem represents the **total probability of the evidence** (the event `B`, also called the "normalizing factor"). It ensures that probabilities are correctly adjusted across all cases.

The denominator is calculated as:

```math
P(B) = P(B | A) P(A) + P(B | \neg A) P(\neg A)
```

This accounts for **all ways** the evidence `B` (e.g., a positive test result) can occur:
- If `A` is true: This happens with probability `P(B | A) P(A)`.
- If `A` is false: This happens with probability `P(B | ¬A) P(¬A)`.

### Example Breakdown
Consider a medical test:
- `P(D) = 0.01` (1% of people have the disease)
- `P(¬D) = 0.99` (99% of people do not)
- `P(T | D) = 0.9` (90% true positive rate)
- `P(T | ¬D) = 0.05` (5% false positive rate)

To find `P(D | T)`, we use:

```math
P(D | T) = \frac{P(T | D) P(D)}{P(T | D) P(D) + P(T | \neg D) P(\neg D)}
```

Substituting values:

```math
P(T) = (0.9 \times 0.01) + (0.05 \times 0.99)
```

Why do we add both terms?
- The **first term** (`0.9 × 0.01`) accounts for true positives.
- The **second term** (`0.05 × 0.99`) accounts for false positives.

👉 This ensures we correctly normalize the probability so that all cases where `B` occurs are considered.

---

## Example 1: Medical Diagnosis
Imagine a disease that affects **1%** of a population, and a test that is **90% accurate** (true positive rate) but also has a **5% false positive rate**.

We define:
- `P(D) = 0.01` → Prior: **1% of people have the disease**
- `P(¬D) = 0.99` → **99% of people do not have the disease**
- `P(T | D) = 0.9` → **90% of sick people test positive** (True Positive)
- `P(T | ¬D) = 0.05` → **5% of healthy people test positive** (False Positive)

Now, if someone tests positive, what is the probability that they **actually** have the disease?

Using Bayes’ Theorem:

```math
P(D | T) = \frac{P(T | D) P(D)}{P(T | D) P(D) + P(T | ¬D) P(¬D)}
```

Substituting values:

```math
P(D | T) = \frac{(0.9 \times 0.01)}{(0.9 \times 0.01) + (0.05 \times 0.99)}
```

```math
P(D | T) = \frac{0.009}{0.009 + 0.0495} = \frac{0.009}{0.0585} \approx 0.154
```

👉 **Even if the test is 90% accurate, the chance of actually having the disease is only 15.4%!** This happens because the disease is rare, and false positives dominate.

---

## Example 2: Spam Email Filtering
An email is classified as **spam** based on words it contains. Suppose:
- **30% of all emails are spam** → `P(S) = 0.3`
- **Word "lottery" appears in 40% of spam emails** → `P(W | S) = 0.4`
- **Word "lottery" appears in 5% of non-spam emails** → `P(W | ¬S) = 0.05`

If we see "lottery" in an email, what’s the probability it's spam?

Using Bayes' Theorem:

```math
P(S | W) = \frac{P(W | S) P(S)}{P(W | S) P(S) + P(W | ¬S) P(¬S)}
```

Substituting values:

```math
P(S | W) = \frac{(0.4 \times 0.3)}{(0.4 \times 0.3) + (0.05 \times 0.7)}
```

```math
P(S | W) = \frac{0.12}{0.12 + 0.035} = \frac{0.12}{0.155} \approx 0.774
```

👉 **77.4% probability the email is spam if it contains the word "lottery".** This is how spam filters work!

---

## Key Takeaways
✅ **Bayes' Theorem helps update probabilities** based on new information.  
✅ **It is widely used** in **medical diagnosis, spam detection, machine learning, and Kalman filters**.  
✅ **Prior probability matters** – even a highly accurate test can give misleading results if the event is rare.  

---
