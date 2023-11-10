
Ideas for narrowing down project:

Can large language models generate quality Anki card decks?

Can large languages models be used to generate quality Anki card decks for courses at a low cost and be effective in a classroom?

2-3 combination study idea:
- Have LLM generate python 101 class cards based on course material and rate its quality
	- variation of producing cards for various classes across UTSA campus say 5 and rate the quality of the cards
- Generate python decks for python 101 class and quantify the effective of the cards for the classes. Either whole class uses cards and rate effectiveness against old class scores or half of sections get cards and others don't and compare the sections test score differences and survey how well the students who got anki cards thought they helped them on a score of 1-5. This study also can provide us a cost effectiveness analysis for institutions to implement LLM anki card generation for their classes. We can quantify the time/effort it takes to generate and curate the course anki and then also try to measure its effectiveness. We may be able to conclude from this that LLM generated anki decks are low cost but highly effective and therefore could be promoted to be adopted by learning institutions as part of their normal course curriculum.


Identify the following for the review:
- Trends/patterns
	- Anki flashcards efficient and help students learn better and perform better on tests
	- Anki cards are labor intensive to create and so third party decks or institution made decks are preferred and their availability increases the usage of cards
	- Spaced Repetition & Recall Testing effective in learning and learning retention
	- A lot of studies centered around medical school and language learning
- Themes
- Debates or contradictions
- Influential Studies
	- - 24 citation Enhanced learning and retention of medical knowledge using the mobile flash card application Anki
	- 24 citation Integrating a Computer-Based Flashcard Program into Academic Vocabulary Learning.
	- 11 Citations Novel spaced repetition flashcard system for the in-training examination for obstetrics and gynecology
- Gaps
	- no research done on the effectiveness/quality of LLM generated cards
	- none or little research done on anki cards in various non-medical science fields

Possible study ideas:
- effectiveness of anki cards in studying programming specifically python programming for beginners
- quality of LLM produced anki cards given various modes of producing the cards, from only questions, to questions with supplementary text such as books, pages from books, syllabi, and other educational materials.
- How a system can be designed to effectively facilitate LLM generated flash cards

[Anki Spaced algorithm](https://faqs.ankiweb.net/what-spaced-repetition-algorithm.html)

**Active recall** is the act of retrieving information from your brain.

A lot of help for chronological outline from [What is the evidence around spaced repetition](https://www.edapp.com/blog/evidence-around-spaced-repetition/)
**5 October 2006** anki birthdate
Review Outline (Chronological):

NEED TO INCLUDE OG 1880-1885 STUDIIES

1939 `Studies in Retention` - 150 citations - One of the first notable articles on spaced repetition of active recall being effective

1989 `Spacing effects and their implications for theory and practice` - 314 citations - talks about how much research has been done showing effective of spaced repetition in learning and how it is an agreeable form of learning by students

2016 `Spaced Repetition Promotes Efficient and Effective Learning: Policy Implications for Instruction` - 451 citations - Talks about effectiveness of spaced repetition learning and why institutions such as schools should adopt it instead of talking about total hours spent in school. He also argues it is cost-effective because implementing general practices for spaced repetition is not costly and also students will have to spend less time relearning older material due to better memory retention

2020 `Spaced Repetition: towards more effective learning in STEM` - 10 citations - made a react web app to use to study for spaced repetition, showed increase in mean score for all the students who used it

2021 `Enhanced Learning and Retention of Medical Knowledge Using the Mobile Flash card Application Anki` - 24 citations - showed effectiveness in increasing test scores of students and also showed that third party decks/institution made decks more popular than individual created - an assumption to be made could be that students are more likely to participate in spaced repetition if they don't have to make the cards themselves

2022 `Does the Use of Pre‐made Digital Flashcards Aid in Medical Students Learning of Anatomy` - 0 citations - showed effectiveness in increasing test scores of students and also showed that third party decks/institution made decks more popular than individual created - an assumption to be made could be that students are more likely to participate in spaced repetition if they don't have to make the cards themselves

2023 `The Ultimate Study Partner: Using A Custom Chatbot To Optimize Student Studying During Law School` - 0 citations - author describes using LLM to make law school anki cards for studying and that he found it effective

2023 `Anki Tagger: A Generative AI Tool for Aligning Third-Party Resources to Preclinical Curriculum` - 0 citations - author shows that LLM is effective at tagging (categorizing) third party anki decks to fit education course material
#### Consideration

The 2020 study was using a custom built webapp it probably is worth noting the convenience of anki in comparison to a custom made web app and because anki is cross platform which may cause an increase in the amount of students who participate in the spaced repetition learning.'


Introduction:
- Jaap M. J. Murre Replication and Analysis of Ebbinghaus’ Forgetting Curve
- Herbert F. Spitzer 1939
- 1989
- 1880 by Hermann Ebbinghaus


## Anki

Towards the end of the twentieth century paper flash cards being used for active recall testing started to become popular but it wouldn’t take long for computer and the internet to innovate. Anki is an open-source project that was first started in 2006 by Damien Elmes with the goal of helping to make things easier to remember. The project boasts that " you can either greatly decrease your time spent studying, or greatly increase the amount you learn” by utilizing virtual flashcards combined with active recall testing over spaced intervals. Anki has seen most of its success with those that want an edge when learning and language or help in medical school but is far from limited to just those topics. The Anki website supports a portal where users can share their decks with topics ranging anywhere from programming, to history, or even music. The primary developers of Anki develop and maintain a free cross-platform application on Windows, Linux, MacOS, and Android while a paid third-party iOS mobile application exists. Once a user installs and downloads the software, they can build virtual decks just like regular flash cards and sync them across devices. Users can then study their decks and for each Anki card they can select from four buttons how easy the card was for them. Using Free Spaced Repetition Scheduler (FSRS) combined with user feedback when studying a calculation is made to determine when to next show the card to the user to optimally assist their information retained. Anki has made such an impact on many medical students test scores and success that a significant number of papers have been written illustrating that Anki is a highly effective learning tool.

Improving education often comes down to a conversation about how many hours students spend in the classroom but ”incorporating spaced practice into education can be a cost-effective approach—learning becomes more durable in the same amount of time (relative to massed practice), and this can lead to future savings because less time needs to be spent on relearning content that has been forgotten, leaving more time for other productive learning activities (e.g., higher order analysis, application of knowledge). Despite over a century of research findings demonstrating the spacing effect, however, it does not have widespread application in the classroom. The spacing effect is “a case study in the failure to apply the results of psychological research”” (Sean H. K. Kang). While there are multiple factors behind educators enhancing their classroom’s modalities of learning to include spaced repetition recall testing one common theme across Anki studies is that students are more likely to use pre-made Anki decks over creating their own which speaks to the labor cost required to build effective decks. Sean A Harrington wrote a study about how large language models can help law students amplify their learning and one notable aspect to it was using OpenAI’s ChatGPT LLM model to produce Anki cards. There are also a handful of early-stage projects working to try and automate Anki card creation using large language models. One challenge people face is that they sometimes want to study a small amount of a shared Anki deck that is relevant to their course curriculum but find themselves having to sift through massive decks. Tricia Pendergrast’s Anki Tagger study found that they could effectively use an LLM to tag Anki cards in a shared Anki deck that were relevant to certain curriculum. This shows that not only is deck creation useful but tagging (categorization) of decks based on curriculum is in need and are problems people are trying to solve. Perhaps an LLM could generate a lot of cards on a given subject and then institutions could simply use an LLM to give them a curated deck based on their curriculum. As we see there are no shortage of possible applications of LLMs and possibly other AI to the Anki system which is what we will explore with this project.