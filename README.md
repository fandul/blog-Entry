# Smooth Deliveries with Jenkins


## by Ben Jones, Frederik Alexander Vygg Larsen, and Rihards Pacevics

_Tired of long and tedious operations, flawed code, and way too much off-schedule deliveries? Jenkins is relatively maintenance free and easy to master once you've stepped into the world of build automation tools. You get an easier and automated workflow, and ultimately save time and money._

![](https://github.com/fandul/blog-Entry/blob/master/1.png)

([https://redhatmiddleware.files.wordpress.com/2016/06/image00.png](https://redhatmiddleware.files.wordpress.com/2016/06/image00.png)) 


## The SO last year way of doing things

Before we had tools like Jenkins we had a very hands on approach to deploying our work. Nearly every step involve human intervention, and all the problems that go with it!

We will describe a typical workflow for getting some code pushed, and illustrate just how cumbersome the deployment process can be.



1.  We write some new code, and some tests, which we run locally.
1.  We rebase our code with the master branch and push it to GitHub.
1.  Now we have some new code to deploy, we merge it with the master branch, and create a new release.
1.  The release must then be deployed onto the production server, and the new version is released.

Ok, so that's only four steps, no problem, or so it would seem. But, they all involve a great deal of human interaction. And if things go wrong, which they normally will, we have a tendency to 'look the other way'!

We know that our tests should all pass, but if they don't we can push anyway, and blame some other guy. 

If we rebase our code with the master branch, and there are some conflicts, we need to fix them, but we might not know exactly how the code should have looked, so mistakes can easily be made.

Now we happily merge our code into the master branch, create a release, without running the tests, and hope for the best.

![](https://github.com/fandul/blog-Entry/blob/master/2.jpg)

([http://s2.quickmeme.com/img/46/468394fc32d72c2bdc04abd04834782a2de7fee5834b5df2fa3b9295262db4cb.jpg](http://s2.quickmeme.com/img/46/468394fc32d72c2bdc04abd04834782a2de7fee5834b5df2fa3b9295262db4cb.jpg)) 

Only now do we realise that the code doesn't work. We don't know where or how it happened, and have to start debugging the whole thing, looking for the mistakes. 

Once we are at this stage, everyone in the team is affected. If we can't rely on the master branch being error free, we can't start any new work, so the problem has to be fixed. 

There must be a better way, and there is! 


## "You have no power here!" Human interaction, a thing of the past.

Introducing Jenkins Build Server as it was back three years ago, it comes with a lot of out-of-the-box potential. Its high popularity is due to its ecosystem of more than 1,200 plug-ins thus making it the most compatible open-source cloud build server on the market. It takes care of both continuous integration as well as continuous delivery meaning that not only does it merge code from each involved developer on a project, but it also makes sure that the project stays in a production-ready state, making it possible to deploy at any time. Having naming conventions for each feature branch, and creating roles on the project repository, it is possible to be rid of the one thing that's always certain to happen, human errors.

![](https://github.com/fandul/blog-Entry/blob/master/3.png)

([https://657cea1304d5d92ee105-33ee89321dddef28209b83f19f06774f.ssl.cf1.rackcdn.com/workflow-5d9ad88dcf95d2550662e3c23078e728a349806cd3d36380c8cab001d8676d61.png](https://657cea1304d5d92ee105-33ee89321dddef28209b83f19f06774f.ssl.cf1.rackcdn.com/workflow-5d9ad88dcf95d2550662e3c23078e728a349806cd3d36380c8cab001d8676d61.png)) 

Simply put, we're denying any developer from manually merging any branches, and letting that kind of responsibility to the only suited "person" in the room, Jenkins. By removing human interaction from the process of code merging and deployment, we can have these steps executed faster, more precise, and at a much lower cost, i.e. it takes one devops engineer to set up a build pipeline and maintain it rather than having each developer sitting around waiting for someone to do a code review on their pull request, etc..

At the moment a developer will only have to:



1.  Branch off Master to a feature/ branch.
1.  Write your implementation.
1.  Create a ready/ branch once you're done, and push it to the remote repository.

What happens next is almost magical. Via a webhook, GitHub notifies Jenkins that a new branch using the ready/ naming convention has been created, triggering Jenkins to do a new source code management (scm) checkout. It sees the ready/ branch triggering a new build job. Under the condition that all stages passes, we let Jenkins merge the ready/ branch with Master and ultimately pushing to GitHub. Same process happens again, now notifying Jenkins that Master has been updated. This triggers a different type of build where all source code is compiled and dockerized, eventually doing an automatic deployment on our production server. In any case an error occurs the build exits and the development team gets a notification on their #devops Slack channel, letting them know the outcome of the build and what went wrong. This makes it easier to correct the bug that caused the error in the first place.


## To Sum it All Up

As we have discovered like so many others, we end up saving quite a lot of time by implementing build automation, and by that we potentially save money. Even with a "small" increase in efficiency, it's a large sum of money on a big budget.


![](https://github.com/fandul/blog-Entry/blob/master/4.png)

([http://www.technolava.com/wp-content/uploads/2016/03/jenkins-features.png](http://www.technolava.com/wp-content/uploads/2016/03/jenkins-features.png)) 

Embrace the ideology, embrace the Smooth Deliveries with Jenkins.


## References:



*   [http://www.specialmoves.com/research-and-development/articles/jenkins-and-continuous-integration.html](http://www.specialmoves.com/research-and-development/articles/jenkins-and-continuous-integration.html)
*   [https://martinfowler.com/articles/continuousIntegration.html](https://martinfowler.com/articles/continuousIntegration.html)
*   [https://www.infoworld.com/article/3046038/application-development/why-jenkins-is-becoming-the-engine-of-devops.html](https://www.infoworld.com/article/3046038/application-development/why-jenkins-is-becoming-the-engine-of-devops.html)
