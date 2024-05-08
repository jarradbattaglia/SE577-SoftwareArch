# Prompt 


Please read this paper:  https://github.com/ArchitectingSoftware/SE577-SoftwareArchitecture/blob/main/reading/reflections-on-rest.pdf

This paper is an update on a paper describing the REST Architecture Style after 17 years of practice.

Based on what you learned in this class, your personal experience, and reading this paper, briefly describe why you think this architecture style/patten has stood the test of time.  I would argue its still one of the most popular API architectures in 2022, and very few things have this long of a lifespan in computing.

# Answer 

I think REST has stood the test of time, because as the paper describes it grew at a time when internet growth was expanding into more decentralized networks and needs to scale across series of servers.  From an architecture/technological standpoint REST can scale, it gives developers flexibility by clients and servers being able to negotiate a version of a resource to use (allowing backwards compatibility), and has built in features to manage things like cache and does not need sessions.  From a developer point of view and myself when using it, when modeling how i want data to flow I find it easy to create my REST interfaces based off how I define them in a model.  I have used things like SOAP before and creating something was complex and in my opinion was difficult to align with how i modeled, and things like GraphQL have a high learning curve and complexity (just one endpoint, requiring developer to invest more into learning the data), which i think limits the amount of devs who want to use or work with them.

And as we have described in previous videos and in class, the ability to name resources combined with HTTP methods allows an API to be easily understood by people even new to it.  For instance, doing something like GET /api/v2/users, it is easily understood what that call should be doing (get users resource using v2 of the api) and it gives many options for developers to use (parameters, what type of data to return, etc).  REST seemingly covers most of the things we want from system quality attributes (modular, maintable with older versions and new ones, scalable, evolvable, its easy to test, etc).

Also as the paper describes at the end, it seems REST was thoroughly planned out over a long period of time.  I think the multiple discussions and seemingly feedback the group who developed it took was instrumental in finding out what worked or didnt work from previous design styles and combined those lessons into something that worked for many use cases.