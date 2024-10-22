# Algorithm Cheat Sheet: Substitution, Master Method, and Recursion Trees

## 1. Substitution Method
The substitution method is used to prove that a recurrence relation is within a certain time complexity bound.

- **Steps:**
  1. **Guess** the form of the solution (usually based on patterns or intuition).
  2. **Substitute** the guess into the recurrence to verify if it works.
  3. **Adjust** the guess as necessary if the substitution doesn’t hold.

- **Example:**
  For the recurrence $T(n) = 2T(n/2) + O(n)$, guess that $T(n) = O(n \log n)$:
  
$$
T(n) = 2T(n/2) + O(n)
$$
  
  Substituting $T(n) = cn \log n$:
  
$$
cn \log n = 2 \left( c \frac{n}{2} \log \frac{n}{2} \right) + O(n)
$$

  Simplifying this should lead to confirming the guess.
  
---
### Substitution Method Examples
---

### $T(n) = T(n - 1) + n$ has solution $T(n) = O(n^2)$

**Guess**: $T(n) = O(n^2)$.

- Base case: $T(1) = 1$.

Now, assume $T(k) \leq ck^2$ for some constant $c$. For $n$:

$$
T(n) = T(n - 1) + n
$$

Substitute the inductive hypothesis $T(n - 1) \leq c(n - 1)^2$:

$$
T(n) \leq c(n - 1)^2 + n
$$

$$
= c(n^2 - 2n + 1) + n
$$

$$
= cn^2 - 2cn + c + n
$$

$$
= cn^2 + (-2c + 1)n + c
$$

For sufficiently large $n$, the quadratic term dominates, so $T(n) = O(n^2)$ is valid.

---

### $T(n) = T(n/2) + \Theta(1)$ has solution $T(n) = O(\log n)$

**Guess**: $T(n) = O(\log n)$.

- Base case: $T(1) = 1$.

Now, assume $T(k) \leq c \log k$. For $n$:

$$
T(n) = T(n/2) + O(1)
$$

Substitute the inductive hypothesis $T(n/2) \leq c \log(n/2))$:

$$
T(n) \leq c \log(n/2) + O(1)
$$

$$
= c(\log n - \log 2) + O(1)
$$

$$
= c\log n - c + O(1)
$$

For sufficiently large $n$, this simplifies to $T(n) = O(\log n)$.

---

### $T(n) = 2T(n/2) + n$ has solution $T(n) = \Theta(n \log n)$

**Guess**: $T(n) = O(n \log n)$.

- Base case: $T(1) = 1$.

Now, assume $T(k) \leq ck \log k$. For $n$:

$$
T(n) = 2T(n/2) + n
$$

Substitute the inductive hypothesis $T(n/2) \leq c(n/2) \log(n/2)$:

$$
T(n) \leq 2 \cdot c(n/2) \log(n/2) + n
$$

$$
= cn \log(n/2) + n
$$

$$
= cn(\log n - \log 2) + n
$$

$$
= cn\log n - cn + n
$$

For sufficiently large $n$, $T(n) = O(n \log n)$.

---

### $T(n) = 2T(n/2 + 17) + n$ has solution $T(n) = O(n \log n)$

This recurrence is similar to the previous one but with a slight change in the subproblem size $n/2 + 17$. The additive constant doesn't affect the asymptotic behavior significantly, so the same steps as in $T(n) = 2T(n/2) + n$ apply.

Thus, $T(n) = O(n \log n)$.

---

### $( T(n) = 2T(n/3) + \Theta(n) )$ has solution $( T(n) = \Theta(n) )$

**Guess**: $T(n) = O(n)$.

- Base case: $T(1) = 1$.

Now, assume $T(k) \leq ck$. For  $n$:

$$
T(n) = 2T(n/3) + O(n)
$$

Substitute the inductive hypothesis $T(n/3) \leq c(n/3)$:

$$
T(n) \leq 2 \cdot c(n/3) + O(n)
$$

$$
= \frac{2cn}{3} + O(n)
$$

This simplifies to $T(n) = O(n)$.

Thus, $T(n) = \Theta(n)$.

---

### $T(n) = 4T(n/2) + \Theta(n)$ has solution $T(n) = \Theta(n^2)$

**Guess**: $T(n) = O(n^2)$.

- Base case: $T(1) = 1$.

Now, assume $T(k) \leq ck^2$. For $n$:

$$
T(n) = 4T(n/2) + O(n)
$$

Substitute the inductive hypothesis $T(n/2) \leq c(n/2)^2$:

$$
T(n) \leq 4 \cdot c(n/2)^2 + O(n)
$$

$$
= 4c(n^2 / 4) + O(n)
$$

$$
= cn^2 + O(n)
$$

Thus, $( T(n) = O(n^2) )$ , which confirms that $( T(n) = \Theta(n^2) )$.



## 2. Master Method
Master Method provides a straightforward way to analyze recurrences of the form:

$$
T(n) = aT\left(\frac{n}{b}\right) + O(n^d)
$$

- **Steps:**
  1. Compare $n^d$ to $n^{\log_b a}$.
  2. Apply one of the following cases:
     - **Case 1:** If $d > \log_b a$, then $T(n) = O(n^d)$.
     - **Case 2:** If $d = \log_b a$, then $T(n) = O(n^d \log n)$.
     - **Case 3:** If $d < \log_b a$, then $T(n) = O(n^{\log_b a})$.

- **Example:**
  For $T(n) = 2T(n/2) + O(n)$:
  $$ a = 2, b = 2, d = 1 $$
  $$ \log_b a = \log_2 2 = 1 $$

  This matches **Case 2**, so $T(n) = O(n \log n)$.

---
  ### Master Method Examples with Steps
---

### $T(n) = 2T(n/4) + 1$

- Here, $a = 2$, $b = 4$, and $d = 0$ (since the constant 1 can be written as $O(1) = O(n^0)$).
- Now, calculate $\log_b a$:

$$
\log_4 2 = \frac{1}{2}
$$

- Now, compare $n^d$ (which is $n^0 = 1$) to $n^{\log_b a}$ (which is $n^{1/2}$):

  - Since $0 < \frac{1}{2}$, this fits **Case 3**.
  - Therefore, the solution is:

$$
T(n) = O(n^{1/2}) = O(\sqrt{n})
$$

---

### $T(n) = 2T(n/4) + \sqrt{n}$

- Here, $a = 2$, $b = 4$, and $d = \frac{1}{2}$ (since $\sqrt{n} = n^{1/2}$).
- Now, calculate $\log_b a$:

$$
\log_4 2 = \frac{1}{2}
$$

- Now, compare $n^d$ (which is $n^{1/2}$) to $n^{\log_b a}$ (which is also $n^{1/2}$):

  - Since $d = \log_b a$, this fits **Case 2**.
  - Therefore, the solution is:

$$
T(n) = O(n^{1/2} \log n) = O(\sqrt{n} \log n)
$$

---

### $T(n) = 2T(n/4) + \sqrt{n} \cdot \log^2 n$

- Here, $a = 2$, $b = 4$, and $d = \frac{1}{2}$ (since $\sqrt{n} = n^{1/2}$).
- Now, calculate $\log_b a$:

$$
\log_4 2 = \frac{1}{2}
$$

- Now, compare $n^d$ (which is $n^{1/2}$) to $n^{\log_b a}$ (which is also $n^{1/2}$):

  - Since $d = \log_b a$, this fits **Case 2** but the additive term has an extra $\log^2 n$, so we multiply by $\log n$:

$$
T(n) = O(n^{1/2} \log^3 n)
$$

---

### $T(n) = 2T(n/4) + n$

- Here, $a = 2$, $b = 4$, and $d = 1$ (since $n = n^1$).
- Now, calculate $\log_b a$:

$$
\log_4 2 = \frac{1}{2}
$$

- Now, compare $n^d$ (which is $n^1$) to $n^{\log_b a}$ (which is $n^{1/2}$):

  - Since $1 > \frac{1}{2}$, this fits **Case 1**.
  - Therefore, the solution is:

$$
T(n) = O(n)
$$

---

### $T(n) = 2T(n/4) + n^2$

- Here, $a = 2$, $b = 4$, and $d = 2$ (since $n^2 = n^2$).
- Now, calculate $\log_b a$:

$$
\log_4 2 = \frac{1}{2}
$$

- Now, compare $n^d$ (which is $n^2$) to $n^{\log_b a}$ (which is $n^{1/2}$):

  - Since $2 > \frac{1}{2}$, this fits **Case 1**.
  - Therefore, the solution is:

$$
T(n) = O(n^2)
$$


## 3. Recursion Trees
Recursion trees help visualize the cost of recursive algorithms by representing the recursive calls as a tree structure.

- **Steps:**
  1. Draw the recursion tree. Each node represents a recursive call, and the cost of the subproblems is at each level.
  2. **Sum the cost** at each level.
  3. **Determine the depth** of the tree.
  4. **Combine the costs** to get the total complexity.

- **Example:**
  For $T(n) = 2T(n/2) + O(n)$:
  - The root has cost $O(n)$, the next level has 2 subproblems with cost $O(n/2)$, etc.
  - Summing all the levels gives $O(n \log n)$.

---

## Asymptotic Notation:
- **Big O (O):** Upper bound (worst-case)
- **Omega (Ω):** Lower bound (best-case)
- **Theta (Θ):** Tight bound (both upper and lower bounds)

 ---
