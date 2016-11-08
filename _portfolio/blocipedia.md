---
layout: post
title: Blocipedia
feature-img: "img/plum.png"
thumbnail-path: "img/blocipedia.png"
short-description: Broken apps matter.

---
#### When one jumps over the edge, one is bound to land somewhere.

##### Lost Time is Never Found Again
* [Blocipedia In 77 Words](#bottom-line)   
* [TL;DR](#tl-dr)

##### We Have Time to Grow Old
* [A Confession](#confession)
* [What is Blocipedia?](#blocipedia)
* [Highlights](#highlights)
* [Conclusion](#conclusion)
* [New Skills/Concepts](#skills)

## <a name="confession"></a>Out Damn'd Spot

Blocipedia is buggy.  There are certain (not glaring) decificiencies, blemishes that I might otherwise desire to sweep under the rug were it not for a nagging fear of being exposed.  Honesty, then, as pragmatism as opposed to as a testament of moral fiber.

## <a name="blocipedia"></a>It Is Not What You See

Much in the same vein as my other Bloc projects, Blocipedia is a learning tool, not a finished product.  This is as good a answer as any as to why a buggy application is in this portfolio.  The application and the code that can be linked to will tell you little about me or my ablilities. Yet it was during the writing of this application that I experienced my Rails' epiphany.  Ergo if I did not include Blocipedia here, I would have no vehicle with which to express my moment of Rails' clarity.

Before I get too effusive, however, I should perhaps pause, because I fear I may have gotten your hopes up.  After all, what epiphany could a guy with about 2 weeks of Rails' experience really have that would change your world? So all the real excitement is on my end, yet I will push on, recognizing the risk inherent in disappointing prospective employers.

The dull parts: Blocipedia ostensibly is an appication for the creation and indexing of public and private wikis.  It is a Bloc project, but it differs from Bloccit and BlocJams in that the code was not written for me.  I was given explicit instructions as to what features to include and, in some cases, what gems to utilize, but the code is my own.  (This might explain why it is buggy.)

## <a name="highlights"></a>Portrait of the Artist

I moved quickly through the initial building of Blocipedia (almost certainly too quickly for my own learning), but towards the latter stages I ran into a snag that I unltimately realized was a massive red flag indicating that there were fundamental Rails' concepts that I had not grasped yet.

The problem, in a nutshell, was that I was confused as to how to set up associations between Wikis and Users.  The language that Rails uses to describe the associations between models was actually creating my difficulty.  When we put expressions such as `has_many` or `belongs_to` in our model class, there is a strong implication that there is some kind of ownership.  This impression makes sense from a user's point of view.  If, as a user, I create a wiki, then it is my creation.  In that sense I own it. I can have many of them and each one belongs to only me.

Yet one of the points of a wiki is to facilitate collaboration.  The project parameters required private wikis to which the owner could invite other users as collaborators.  This produced a confusion in me because I was thinking of model associations as ownership.  So when I thought about ways to connect collaborators to a wiki, it seemed to me that a wiki would then have multiple owners, because all association was phrased in language that implied possession.  

Possession is just one kind of association and it is not really an accurate way of thinking about how the database tables are set up.  When we stipulate that a user `has_many` wikis, it creates an impression that each user in the users table somehow records the wikis the user 'owns'.  In a simple `has_many`, `belongs_to` relationship, nothing could be further from the truth.  The users table makes no mention of wikis.  In this sense, a "user", a row in a table with all the pertinent information about said user, knows nothing about the wikis it "owns".  The onus for creating the association is actually on the wiki, which has a column in its table to indicate it "belongs" to a specific user.  Then the `.wikis` method that Rails makes available to the Users' class when we stipulate `has_many :wikis` instructs the application to search the wikis table for all rows with the appropriate foreign key associated with the user instance.  

I was trapped by a false interpretation of the language of Rails.  Hours agonizingly lengthened into days as I contemplated the problem.  When the answer finally hit me, I had my moment of clarity:  Rails is all about the database.

Yes, I had understood the database in terms of the architecture of Rails while working previously on Bloccit, but I had failed to comprehend the central importance of the information itself.  Almost every internet interaction is about getting and manipulating information.  How could I have missed it?  Perhaps because it was so ubiquitous, so taken for granted.  Heck, it is right there in the name of the entire industry: Information Technology.  

The database contains the information and the information is stored in tables.  I had been told how to create a migration table and how to run those migrations with `rake db:migrate`, but it suddenly struck me as almost embarrassing how little I had understood of what I was doing.  The numerous many small actions that go into designing an application had obfuscated for me the very basic fact that I was creating simple tables for information to be stored persistently.  

The rest of the architecture, the views, the routing, the controllers, was about facilititating the user's ability to retrieve and manipulate the data stored in those tables.  

I have been at this development business long enough now to come to have an appreciation the enormity of the task in front of me.  Six months in and I look fondly back at my naivete in the days that followed my big epiphany.  I finally had it.  Rails was easy and it was fundamental.  Why would anyone be interested in front end? Front end developers just added the finishing touches to the real meat of an appication: the interaction with the database. 

Now, seduced by the power of data binding and the dark side of the internet, I conceive of applications that Rails alone cannot adequately accomplish, that what I considered then to be the 'mere' facilitation of the user's interaction with the database might actually be not just the harder part, but the more important part.  Users do not come to software applications just to get information.  They are increasingly needful of more powerful, concise, and efficient control of that information.  

That is a story for another day, however.  Its introduction here is a means to the end of stating that there is a pattern emerging here.  The dev universe keeps unfolding before me at an ever increasing rate.  The more I learn, the more avenues for learning open.  I dare say it will be only a few weeks until I am once again chuckling at myself for the notions I hold sacred at this moment.

Yet coming out of Blocipedia, I was Superman.  I had found the key.  Just as "follow the money" will often lead to a clear explanation of non-virtual motivations and events, in Rails my personal mantra is "follow the data" and your way shall be made clear.  If two pieces of data have an association, it needs to be recorded in a table. 

Puffed up with self-congratulatory zeal, I undertook to help a fellow student with Blocipedia a few weeks later, only to discover that I really had not understood Pundit very well.  Even though I had written the application and tested it in the development site, I had not created a test suite.  Further, even though I had added Pundit and written some code in the Pundit files, I was not actually using Pundit for my authorizations.  

Long story short (too late!): I fussed with the code for a little before moving back to other projects.  I believe that this is where I did something that caused the bugs the current incarnation of the app is experiencing.  This is a happy occurence though because it stresses for me the importance of writing that test suite.  If I were adequately testing the models and the authorizations, I would have been able to run the suite after making changes and I would have realized that I broke it.  Now, months later, with no test suite, I am basically up a tree for fixing it without completely rewriting portions of it, something I am unwilling to do because I consider the learning that would come from that to be smaller than the learning from pursuing other work.

I am not even sure, at this point, that I ever had it working correctly in the first place, which is one of the problems associated with doing your testing in the development hosting: it is too easy to miss something that a good test suite would not miss.

## <a name="conclusion"></a> Conclusion

Bleh, I am braindead with this at the moment.  I have not captured the moment of epiphany or what it means, but I think I need some space from it.  I am going to push it so that the people who are giving me feedback can access it.

## <a name="tl-dr"></a>TL;DR

## <a name="skills"></a>New Stuff

* Devise (Users and Sessions)
* Pundit (Authorizations)
* Redcarpet (Markdown)

## <a name="bottom-line"></a>The Bottom Line

Writing, and revisiting, Blocepedia put in perspective the central importance of the database, led me to ~~a deeper~~ an understanding of Rails' migrations and what they represent, and gave me a healthy respect for the value of testing.  Just as Bloccit taught me the structure and much of the "how" of a Rails' application, Blocipedia offered me an opportunity to reflect on the "why" (it's all about the information) and the "what" (it's all about the database).