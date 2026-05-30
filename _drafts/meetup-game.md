
TItle similar to: AI assisted developement Hackaton Aftermath

At Sourcelabs we usually spend one day per month to explore and learn new topics. This week we focused on a super funny hackaton: we needed to create a game in 6 hours that was following this specs:

#### Specs
inspired by Simon the sourcer, command and conquer, doom, jas jack rabbit, duke nuke.

Beauty of simple old games.

Educational: personal connection
Retro styled game - Stylish
Fun
Music and sound effect usages

#### Tech
Host a game on a web server, playable in a browser. No backend, must use only local storage.
I have only 2 hours to develop this.

This was such a fun experience, and those are the things I've learned by using ai 100% of the time.

Check out what I build first: https://sunnystefi.github.io/grand-hotel/

### Key takeaways
Different prompts:
1. What is required: the problem. I wanted to spend the most tokens on planning, since it's the fondation for a great product. I asked claude 4.8 and used the ultrathink mode with the following prompt:
   `what was required + what are the pillar of the classic games + my impression on the specs, and my personal needs and preferences:`
```
I have only 2 hours to develop and refine this with you.

What are the fundamentals that make those retro games well done and immortal? give me some points and help me explore ideas. From that, do not implement. Explore and ask me many questions and build a doc in docs/ to summarize the implementaion (leave out the technical side first).
```
1. I created a doc and refined the specs.  Ultrathink already used more than 10% of my daily budget so I decided to stop there and downgrade the model
2. Openspec explore the design and further refine the plan.
3. Music generation: trim the design prompt to 3000 lines > Create music with suno. Adjusting the prompt a little and getting a great music in 2 mins.
4. Ask to openspec implement the plan with Sonnet (~27 min).  with openspec new-ff
5. While I wait, I start exploring the game Sonnet generated and I started writing the next prompts with adjutments and features (language support, better sprite, graphic twitches, keyboard preferences) ... changes you see from playing a bit (ans see ai doing thigs).
6. I was keeping a list of prompts to be executed after the change was working as I was expecting
7. Create branches for the changes (openspec). until it works. It was too slow and it was consuming too many tokens.
8. the approch i used was more effective for a quick prototipe: git push if the product is good enough, git stash if the change does not work.

Such a fun experience! Than you for the awesome high level quality training! Learning so much !
