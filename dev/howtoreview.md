### dev/howtoreview

Code Review is a crucial part of our development workflow.
When performed rigorously along with testing, it allows eliminating most programming mistakes from the source code.
Among other things, it also helps enforcing a clean coding style.
The secondary goal of the review is to improve everyone's programming skills.

##### How to be a good reviewer
Reviewing efficiently is a very hard task: reading and understanding other people's is (by far) way more complicated than writing some.
Here are a few rules to follow when reviewing code:

<u>Always try to understand everything</u><br>
Read the code more than once if needed. If you really don't get something, ask questions: code should always express its intent clearly.

<u>Be critical</u><br>
Read the code carefully and think about what could be improved:
Is there a better way to achieve something ? Could it be easier to read ?
Could it be easier to maintain ? Is it flexible enough ? Can you suggest anything ?
Make yourself a To-Do list of everything you want to check when reviewing.

<u>Show examples</u><br>
Review comments are short messages, and should remain that way.
It is however a good idea to provide concrete examples or links to that illustrate your point.

<u>Be positive</u><br>
Review is not about criticizing people, it is about improving code quality. Make sure your remarks always remain constructive.

<u>Spend enough time on the review</u><br>
Reviews are not expected to be quick: you should spend at least 30 minutes to review a normal-sized patch.
Everyone should dedicate enough time to review one patch everyday.

##### How to be nice to review
<u>Explain your choices</u><br>
When you receive comments, defend your choices and present reasonable arguments. Here too, providing links to documentation can be a good thing.

<u>Be positive</u><br>
This is exactly the same rule as above. Always keep a positive mindset when receiving remarks from reviewers.
Don't try to have the last word at all costs: it's OK to acknowledge when you're wrong.

<u>Reply "Done" on fixes</u><br>
Mistakes that will be fixed in the next patch set should be marked as "Done" using the dedicated button.
It is a good way to inform reviewers that their remarks were taken into account.

<u>Reply to every comment</u><br>
Always make sure to reply to all the comments.
You may disagree with some remarks, or feel like some others are totally irrelevant, however you must reply to them.

<u>Review yourself</u><br>
Looking at the diff view of your own patch can help you find basic errors.
