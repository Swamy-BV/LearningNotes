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
