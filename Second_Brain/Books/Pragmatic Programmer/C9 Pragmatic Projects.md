TARGET DECK: Pragmatic Programmer::C9 Pragmatic Projects
# Notes

## No Broken Windows
Teams need to not live with small imperfections should strive for quality code. Quality cannot be one person's responsibility but is each persons responsibility to only check-in quality code & help keep others accountable - PR review is I think a big way to do this

## Communication
- Your team being good at communicating and building its brand helps bring recognition your team
- Good communication helps lower tech debt since there is less chance of someone duplicated work that already exists
- Try to foster frictionless communication: Frictionless means it’s easy and low-ceremony to ask questions, share your progress, your problems, your insights and learnings, and to stay aware of what your teammates are doing.

## Cargo Cult
- Do not try to replicate the tech stack or development processes of companies just because they are successful. Learn what successful companies are doing of course but every company/use case is different. Successful companies had their mature dev philosophies develop and will change in the future based on the companies needs.

![[Pasted image 20240727161235.png]]

Do not over commit to a specific development method, take what works for your team after viewing them all.

## Pragmatic Starter Kit
### Version Control
- Ensure team utilizes version control for code check-in
- Make it so test/deployment are triggered or synced with version control commit/pushes
### Testing
Finding bugs is somewhat like fishing with a net. We use fine, small nets (unit tests) to catch the minnows, and big, coarse nets (integration tests) to catch the killer sharks. Sometimes the fish manage to escape, so we patch any holes that we find, in hopes of catching more and more slippery defects that are swimming about in our project pool
- Unit Testing
- Integration Testing
- Validation & Verification: is the features going as expected for customers?
- Performance testing: create smoke tests to test load and other things
- Netflix's chaos monkey is a testing system that kills off services to see how things perform
- If you find a bug that slips through testing add a test to catch it in the future

# Flashcards

Q: How can you build you teams brand and why is it important?
A: You can build their brand by helping your team find a good name.logo if they do not have one and mentioning your team name in conversation liberally. It is important because it will bring more recognition and relevance to your team 
<!--ID: 1722186071253-->
