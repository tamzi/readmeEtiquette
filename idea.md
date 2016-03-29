
#### Writing a good README

from [the frontier Group article on Writing agood ](http://blog.thefrontiergroup.com.au/2013/05/writing-a-good-readme/)

Posted in Inside TFG, Tips and Tricks


What’s the problem?

As a developer, you’ll work on hundreds of different projects in your career. The biggest pain in the ass when changing projects is having to get started in a new development environment. If you’re moving to a different Rails project you have to install new Rubies and bundle – plus you might need to install Redis, Solr or jam your public key on a server somewhere. Even worse, after bundling you notice this is a Rails 2.3 project not a Rails 3.2 and you haven’t worked with Rails 2.3 for years and can’t remember how to start a server.

Then you have to work out who is in charge of this damn project and bug them to find out why your PostgreSQL is complaining about some “PostGIS” thing you’ve never heard of. Once you get that sorted you run the specs to see what shape the app is in and half your tests fail because you’re missing some `config/some_random_config.yml` file. You talk to the guy in charge of the project and he tells you to scp it from the staging environment. “But dude, how do I even get to the staging environment? What server is it on?”. Turns out it’s on an Amazon server and you need a special permissions file to be able to access it.

Imagine this process happens 12 months after anybody has ever worked on the project and the last girl to hack on the codebase has long since left the company. Your company has just lost months of her gaining knowledge that you now have to re-acquire. Knowledge that should have been documented somewhere so it wasn’t lost.

What’s the solution?

Although I did reveal the solution in the title (because I’m a bad writer, sorry) – the answer to the question is to write and maintain a comprehensive README file.

How do I write a good README?

Writing a good README is easy. You just need to know what information is required for developers to use and understand the application. Here’s some Rails-centric information I include in the READMEs I write for The Frontier Group:

README: General Information

The “General Information” section should give a new developer an idea of what the project is about and who is involved with it.

Information you might want to include is:
•The name of the project
•The name and contact details of the client and any 3rd party vendors
•The names of the developers on the project
•A brief description of the project, you should include the answer to the age-old question “What problem is this project solving?”
•An outline of the technologies in the project. e.g.: Framework (Rails/iOS/Android/Gameboy Colour), programming language, database, ORM.
•Links to any related projects (e.g.: Is this a Rails API that has corresponding iOS and Android clients?)
•Links to online tools related to the application (e.g.: Links to the Basecamp project, a link to the dropbox where all the wireframes are stored, a link to the Pivotal Tracker project)

README: Getting Started

The “Getting Started” section outlines the process of getting the app installed and usable for a developer. I define ‘usable’ in this context as able to login to the application and access all of the functionality available.

Information you might want to include is:
•A detailed spin-up process. This should include: ◦Instructions on installing any software the application is dependent on: e.g.: wkhtmltopdf, PostgreSQL, XQuartz.
◦Instructions on running the app. For rails apps you’ll want to include the rake db:create db:migrate db:seed process here, as well as instructions on starting a server (e.g. are we using pow, or just the default `rails s`)

•A list of credentials that can be used to log in with each user type in the system and ideally the URL that a developer can log in from.
•Any information about subdomains in the app (e.g.: api.myapp.dev/)

When writing instructions pretend you’re writing them for someone who knows next to nothing about developing in the framework/language your application uses.

README: Testing

All you need to include in the “Testing” section is the commands to run any of the test suites you have (e.g.: RSpec, Jasmine, Cucumber, Spinach) and any setup you need to do before-hand (e.g.: rake db:test:prepare). This section will be small but vital.

README: Staging and Production environments

The staging and production environment sections (one section per environment) should provide any information a developer might need to know about these environments.

Information you might want to include is:
•Which server is the application on? Is it on Amazon Sydney? A server in the office? A data-centre down the road?
•How can a developer connect to the server? Do they need particular permissions? Who do they need to talk to to get those permissions?
•Where on the server is the application located
•What is the deploy process for this server
•Are there any other services on the box related to the app a developer will need to know about? Any cron jobs? Some Resque workers?

Maintaining the README

Worst case scenario, you don’t maintain a README. You’ll burn in developer hell, sorry.

Slightly better than that, your changes to the README will be reactive – you’ve had to work out how to install some required software and you’ve put the details of doing that in the README for future developers.

If you’re having to make reactive changes, you’re probably spending 30 minutes that another developer already had to spend working out a solution to the same problem. This equates to 30 completely wasted minutes that could have been spent implementing a feature for your client.

In an ideal world, maintaining the README is proactive and becomes part of your development life-cycle. As an example, your development life-cycle could look like this:
1.Plan feature
2.Write tests
3.Implement functionality
4.Update README if required
5.Get code reviewed and ensure all your tests pass
6.Merge your feature

What am I getting by writing a good README?

With a comprehensive, well-written README any developer should be able to hop on to your project and begin hacking away within 10 minutes. If you consider that over the course of developing an app you’ll likely see multiple developers set up the app multiple times, you’ll cumulatively save hours of developer time with just minutes of work.

Importantly: If you can set yourself up with this fantastic habit early, other developers will love working with you. Documentation is what separates us from the animals, ladies and gentlemen.

I recommend you invest 30 minutes of your week updating the READMEs of the projects you’re working on. You may not see any benefits straight away, but in 12-18 months time whoever has to maintain that code will be thankful you did it. Spoiler alert – that person will probably be you.
