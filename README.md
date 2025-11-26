# DATA-SCIENCE-ALGO



# **K-Nearest Neighbors (KNN) Algorithm Using Euclidean Distance**

The **K-Nearest Neighbors (KNN)** algorithm is a very simple method used in **classification** and **regression**.
It works by looking at the **closest points** in the training data and deciding the class based on them.


To find the class of a new data point by checking the classes of its **K nearest (closest)** points.



## **Step-by-Step KNN Algorithm**

### **Step 1: Choose the Value of K**

* Choose a number **K** (1, 3, 5, 7, etc.).
* K means how many neighbors we will check.
* K is usually an **odd number** so that voting is easy (no tie).


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



### **Step 3: Find K Nearest Neighbors**

* Calculate the distance of **every** training point from Q.
* Put the distances in a list.
* Sort the list from **smallest to largest**.
* Pick the **top K points** → these are the **K nearest neighbors** of Q.



### **Step 4: Decide the Output (Voting / Average)**

#### **For Classification**

* Look at the classes of the K neighbors.
* Count how many neighbors belong to each class.
* The class with the **highest count (majority)** becomes the class of Q.

This is called **majority voting**.

#### **For Regression**

* Take the **average or median** of the values of the K neighbors.



### **Step 5: Final Prediction**

Assign the chosen class/value to the new query point Q.



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




# **K-Means Clustering Algorithm**

*(Easy Language, Full Exam Format)*


K-Means is an **unsupervised learning** algorithm used to group data into **K clusters**.
The goal is to place data points into clusters such that points in the same cluster are **similar**, and points in different clusters are **different**.


# **Algorithm: K-Means Clustering (Step-by-Step)**

### **Step 1: Choose the value of K**

* Decide how many clusters you want (K).
* Example: K = 3 means you want 3 clusters.

### **Step 2: Initialize centroids**

* Randomly select **K points** from the dataset as the initial **centroids**.
* A centroid is like the “center” of a cluster.

### **Step 3: Assign each data point to the nearest centroid**

* For each data point:

  * Calculate the **distance** to each centroid
  * Mostly **Euclidean distance** is used
  * Assign the point to the centroid with **minimum distance**
  * This forms clusters

### **Step 4: Update centroids**

* After assigning all points:

  * Take the **mean (average)** of all points in each cluster
  * This mean becomes the **new centroid**

### **Step 5: Repeat Step 3 and Step 4**

* Keep assigning points and updating centroids
* Stop when:

  * Centroids **do not change**, or
  * Maximum number of iterations is reached

### **Step 6: Final Clusters**

* The algorithm returns the final **K clusters** and their **centroids**.

---

# **Flow / Diagram (Text-Based)**

```
Start
  ↓
Choose K
  ↓
Select K initial centroids (random)
  ↓
Assign each point to nearest centroid
  ↓
Recalculate centroids (mean)
  ↓
Centroids changed?
    Yes → Repeat assignment step
    No  → Stop
  ↓
Output final clusters
```

---

# **How Initial Centroids Influence the Results**

Initial centroids play a **very important role** in K-Means because:

### **1. Different starting points → Different final clusters**

* K-Means can get stuck in **local minima**
* If the initial centroid positions are bad:

  * Clusters will be bad
* If the starting centroids are good:

  * Clusters will be more accurate

### **2. K-Means may give different results each time**

* Because centroids are chosen **randomly**
* Running the algorithm again may give **different clusters**

### **3. Poor initialization can create:**

* Wrong cluster shapes
* Uneven clusters
* Empty clusters
* Convergence to a bad solution

### **4. Good initialization improves:**

* Speed of convergence
* Stability of results
* Quality of clusters

### **5. K-Means++ initialization**

* A better method to choose initial centroids
* It spreads initial centroids apart
* Gives more stable and accurate clusters

---

# **Example of Impact (Simple)**

If you choose two centroids far away from natural groups, clusters become **wrong**.
But if initial centroids are placed near natural groups, clusters are **perfect**.

---

# **Short Summary**

* K-Means depends heavily on the **initial centroids**
* Poor initial centroids → poor clustering
* Good initial centroids → good clustering
* K-Means++ solves this issue

---



