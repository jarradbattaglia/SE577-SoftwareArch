# Prompt

```
Modeling software architectures is an essential activity to aligning key stakeholders in most projects.  Many times models are really just pictures, and dont add much value unless the author is available to present their point of view.  Simon Brown is the creator of the C4 model and has some interesting perspectives on effective modeling of software architectures.   One thing Simon claims is that a common set of abtractions are better than a standardized notation. 

WHAT TO HAND IN: After viewing the video below, do you think the abstractions (and the context around the abtractions) in the C4 model is an appropriate way to communicate software architecture information to both technical and non-technical stakeholders?  Please provide one paragraph to support your point of view.

Also, what challenges do you see with the C4 model, if any, when being used on large modern systems that may have thousands of components?

Link to video here:

https://www.youtube.com/watch?v=x2-rSnhpw0g
```

# Answer

I do think it provides an appropriate way to communicate knowledge because it gives context to each type of system, especially Context and Container level.  I think needing to include details and specific sentences helps communicate the intent to the team, where as traditional, quick drawn architectures miss that context and I think people who are trying to keep up or come late may lose the specific information (what does that line to the database mean, is that going to or back, etc).  Also requiring things like sentences and specific visuals (like who the people are, DBs, etc) helps people come back to the diagram later and helps remember key information/intent that maybe you interpret differently after coming back to a worse diagram that has less specifics or more vague.  Overall I think it helps clean up a lot of confusion when getting a high level view of a system.

Now the challenges that may happen as you go deeper and deeper into larger systems is the amount of detail that needs to change.  As he said the code level is useless to write out by yourself as its impossible to keep track of, and I think mapping out every little specific component may be too time (and space) consuming and when something changes or intent changes, needing to rewrite sentences or details on a component becomes too much to update.  So I think in very large systems most people would probably just stop at the container or context level or not include specifics on every component and try to abstract groups of things more.
