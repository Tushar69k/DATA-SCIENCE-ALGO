# DATA-SCIENCE-ALGO


---

# **K-Nearest Neighbors (KNN) Algorithm Using Euclidean Distance**

The **K-Nearest Neighbors (KNN)** algorithm is a very simple method used in **classification** and **regression**.
It works by looking at the **closest points** in the training data and deciding the class based on them.

---

## **Goal**

To find the class of a new data point by checking the classes of its **K nearest (closest)** points.

---

## **Step-by-Step KNN Algorithm**

### **Step 1: Choose the Value of K**

* Choose a number **K** (1, 3, 5, 7, etc.).
* K means how many neighbors we will check.
* K is usually an **odd number** so that voting is easy (no tie).

---

### **Step 2: Calculate Euclidean Distance**

We have a new point:

[
Q = (q_1, q_2, …, q_n)
]

And a training point:

[
P = (p_1, p_2, …, p_n)
]

To find how close they are, we use the **Euclidean Distance** formula:

[
\text{Distance} = \sqrt{(q_1 - p_1)^2 + (q_2 - p_2)^2 + … + (q_n - p_n)^2}
]

This gives a number.
**Smaller distance = closer point.**

---

### **Step 3: Find K Nearest Neighbors**

* Calculate the distance of **every** training point from Q.
* Put the distances in a list.
* Sort the list from **smallest to largest**.
* Pick the **top K points** → these are the **K nearest neighbors** of Q.

---

### **Step 4: Decide the Output (Voting / Average)**

#### **For Classification**

* Look at the classes of the K neighbors.
* Count how many neighbors belong to each class.
* The class with the **highest count (majority)** becomes the class of Q.

This is called **majority voting**.

#### **For Regression**

* Take the **average or median** of the values of the K neighbors.

---

### **Step 5: Final Prediction**

Assign the chosen class/value to the new query point Q.

---

## **Example (K = 3)**

Suppose the 3 nearest neighbors have these classes:

* Neighbor 1 → **Class A**
* Neighbor 2 → **Class B**
* Neighbor 3 → **Class A**

Count:

* Class A → 2
* Class B → 1

So the final class is:

### ✔ **Class A** (majority)

---


