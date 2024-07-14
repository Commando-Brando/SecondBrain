TARGET DECK: Pragmatic Programmer::C8 Before the Project

# Notes
## Requirements
- Great section
As early machines were
fairly limited, the scope of problems they solved was constrained: it was
actually possible to understand the whole problem before you started.
But that is not the real world. The real world is messy, conflicted, and
unknown. In that world, exact specifications of anything are rare, if not
downright impossible.

Whenever you get a new requirement what should you do?
Avoid the pitfall of immediately coming up with a solution. Identify and edge cases and concerns and clarify them with the client.

For example, you receive the following requirement from someone:

"Shipping should be free on all orders costing $50 or more"

Stop for second and try to think of edge cases and clarifying questions. For the example:

• Does the $50 include tax?
• Does the $50 include current shipping charges?
• Does the $50 have to be for paper books, or can the order also include
ebooks?
• What kind of shipping is offered? Priority? Ground?
• What about international orders?
• How often will the $50 limit change in the future?


## Group Questions
- Does anyone pair program at work?

# Flashcards

START
Basic
How can you walk in a client's shoes to help understand their point of view when it comes to requirements?
Back: You can try to sit in with them for a week and understand how their tool will actually be used to try and create some mockups to get feedback
<!--ID: 1720551593865-->
END

------ 

START
Basic
How should approach requirement policies?
Back: Generalize them in a pragmatic way if possible. 

For example, if a requirement is to only let supervisors and HR access a feature there should not be explicit tests for those 2 cases but maybe a small generalized access control system for it.
Be careful not to over-engineer or prematurely optimize here.

Pragmatic Programmer Page 248
<!--ID: 1720551593878-->
END

----------

START
Basic
How can you stay up to date with acronyms or technical terms on a project?
Back: Create a glossary document containing them with their definitions
<!--ID: 1720551593880-->
END

---

START
Basic
When trying to figure out a solution for a hard problem what should you keep in mind?
Back:
 Challenge any constraints you initialize think
- Identify what are hard constraints and consider how to approach the problem with the most restrictive constraints in mind
- A lot of the time trying some paths that may seem unlikely should be explored as they may be better than the solution that seems more obvious

"When faced with an intractable problem, enumerate all the possible avenues you have before you. Don’t dismiss anything, no matter how unusable or stupid it sounds. Now go through the list and explain why a certain path cannot be taken. Are you sure? Can you prove it?"
- Pragmatic Programmer page 254
<!--ID: 1720551593884-->
END

---

START
Basic
What a flexibility standpoint what is a hallmark of a good design?
Back: A good design is one that is easy to change
<!--ID: 1720551593886-->
END

--- 
