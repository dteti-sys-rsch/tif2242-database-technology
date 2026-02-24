# Homework 1: Conceptual Data Modeling

**Course:** TIF2242 \- Database Systems \
**Instructor:** Dr. Guntur D Putra \
**Due Date:** \[Monday, 2 March 2026 at **07.59**\]

## Part 1: Basic Entity-Relationship Modeling (40 Points)
Suppose you are buidling a new **social media app** from the ground up, namely *UGM-Fezz*. Draw a Peter Chen ER Diagram for it based on the following business rules. Focus on capturing the conceptual logic of how users interact.

**Business Rules:**
* **Users** are identified by a User\_ID and have a Username and Email.  
* **Posts** are identified by a Post\_ID and have a Content (text) and a Timestamp.  
* A **User** can *create* multiple **Posts**, but each **Post** is created by exactly one **User**.  
* **Communities** (Groups) are identified by a Comm\_ID and have a Description.  
* **Users** can *join* multiple **Communities**, and each **Community** can have many **Users**.  
* We must record the Join\_Date of when a User joined a specific Community.

**Requirements:**

* Use **Rectangles** for Entities and **Diamonds** for Relationships.  
* Use **Ovals** for Attributes and underline the **Primary Keys**.  
* Clearly label the **Cardinality** (e.g., 1:N, M:N) on the relationship lines.

You are also free to add more data or entities if you think they are necessary.

## Part 2: Advanced Attributes & Relationships (30 Points)
Building on the social media model, apply the following conceptual constraints:

1. **Multivalued Attributes:** A **User** may have multiple Social\_Links (e.g., links to their GitHub, LinkedIn, or Portfolio). Refer to your lecture notes on how to represent an attribute that can have multiple values.  
2. **Composite Attributes:** The User's Account\_Settings should be broken down into Privacy\_Level, Notification\_Pref, and Theme\_Color.  
3. **Derived Attributes:** A **Post** has a Total\_Likes count. Since this number is calculated based on the likes relationship, represent it as a derived attribute. (Recall the specific dashed oval style for derived data).

## Part 3: Identifying Existence Dependency (30 Points)
*The concept of "Weak Entities" is fundamental for handling data that cannot exist on its own (Existence Dependency).*

**Scenario:**
* **Post** is a Strong Entity with attributes Post\_ID (PK) and Content.  
* **Comment** is a Weak Entity with attributes Comment\_No (discriminator), Text, and Post\_Time.  
* **Logic:** A Comment is "weak" because it belongs to a specific Post. You cannot have "Comment \#5" floating in the database without knowing which Post it belongs to.

**Questions:**

1. **The Discriminator:** In this scenario, why is Comment\_No called a "Partial Key" (Discriminator) instead of a Primary Key?  
2. **Drawing (Chen Notation):** Draw the relationship between Post and Comment. Refer to **Slide 34** and ensure you use:  
   * **Double Rectangles** for the Weak Entity (Comment).  
   * **Double Diamonds** for the Identifying Relationship.  
   * **Double Lines** to show Total Participation of the Comment in the relationship.

## Submission Instructions

* You may use tools like **Draw.io** (select the "Entity Relation" library) or draw clearly by hand and scan your work.  
* Ensure all symbols follow the standard Peter Chen notation as shown in the lecture slides.  
* Submit your answers in PDF format via eLOK. Remember to include your name and student id in your PDF file.