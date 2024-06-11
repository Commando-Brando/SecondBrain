
- 5 Whys, keep asking why 5 times until you know something for sure


# Chapter 2
- Code represents knowledge and logic
- Just because two functions are exactly the same does not mean they violate dry since they represent different knowledge p35
- Orthognality 
# Chapter 3
- **Shell** Need to get better with shells, I think exploring PowerShell for me and improve one of the TDS scripts
- **Power Editing** Learn more about Visual Studio become fluent with my editor/IDE pg81
- **Version Control** learn more about azure devops and its settings/emails
- **Debugging** 
	- If you find a bug think about how it could have been prevented and maybe update a unit test to do so
	- If you find a bug is it a symptom or the root cause? Do not fix symptoms fix the route cause
	- Assume the bug is caused by your code and not a libraries because probability states it is
	- • Do the conditions that caused this bug exist anywhere else in the system? Are there other bugs still in the larval stage, just waiting to hatch?

# Chapter 4
**Design by contract (DBC)**
- Design by contract (DBC) is a design technique emphasizing a contract for what say a function or component will do give data in a specific way. For example, your rest endpoint may require data in a very specific format. Given the correct format your endpoint can guarantee a "contract" on what will have. This reminds me of at Microsoft how I recently worked on a project where another team had to stand up an endpoint for us and we had to in some way negotiate a contact for what we pass and what we expect.
- DBC crashing early. The idea of asserting things early in business logic so your stack trace and things are closer to where the bug occurred. I agree with this practice although you may not want the program to crash, but in imperative languages using validation as DBC suggests could achieve the same effect.
- In general validating data to be passed to a class/function is the responsibility of the caller. Although I think that the functions being called should have guard rails on if it is widely shared and should handle errors gracefully. Where is the border line of this? Should every function in a class do data input validation? That would lead to possibly a lot of duplicated code as the same inputs are passed around. I think the line should be drawn at the class level since it is generally the smallest cohesive component in a system. I think if a class calls something outside of its class then that thing should have guard rails. Or any publicly exposed function should have the guard rails, this makes the most sense to me
**Dead Programs Tell No Lies**
- Essentially simply your error handling and do not handle every case necessarily which is interesting because across the board I have heard people recommend always be specific with types of exception when handling but that may just be counter productive and you cannot possibly predict every situation or later on more exception types could be introduced so definitely capture Exceptions but also specific ones when specific handling is necessary.
**Assertive programming**
- Aka using assert statements in actual code, not just in tests
- I have never seen this at Microsoft so curious where it is being used there if at all but I think we basically accomplish the same thing but doing validation and then throwing errors 
**How to Balance Resources**
- Finish what you start section shows how to nicely refactor multiple functions that operate on the same file. It shows a nice solution which provides leans towards having one function call multiple functions and passing the object to those functions, kind of how I wanted to refactor the apply access plugin
- Balancing exceptions section is nice, I like how he talks about how they point out that when using finally to deallocate a resource ensure the allocation is not in the try part otherwise you may attempt deallocating something that was never allocated
- _Exercise 18 (__possible answer on page 299__)_
	- Some Java developers make a point of setting an object variable to_ _NULL_ _after they have finished using the object. Why is this a good idea?

**Don't Outrun Your Headlights**
- Take small steps always falls into the don't outrun your headlights saying, you can only see so far ahead of your software's life and cannot predict what will come soon so take small steps

# Chapter 5

