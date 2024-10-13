# Dealing with Reality

In a class, the code you write lives in a protected space, isolated from reality. That's helpful as you are learning, because it simplifies the demands.

When you write real applications (programs that many people use), there are a number of differences. Some of the biggest ones are:

- real software is often much larger, with many more lines of code, developed by large teams
- real software changes over time: it's alive!
- real software runs on real users' devices and internet
- real software has real users real data

## Larger projects, developed by teams

The projects you've built in class take a few days or at most a few weeks, built alone or with a few teammates.

Large applications often have codebases with thousands of contributors over years or decades. The programs are much more complicated, with hundreds, thousands, or millions of files. On such a project, no one knows the details of how every line of code works. Instead, each engineer knows roughly how the relevant systems work, and knows a subset of the application where they have responsibility in great detail.

Working in large teams means using tools to collaborate. There are tons of different tools including the normal collaboration tools like Discord, Zoom, Whatsapp, Calendar, and Email. There are also specific software collaboration tools, including version control like Git and Github, design tools like Figma, planning tools like Asana or Trello, as well as common configuration for code editors and tools for pair programming.

## Living Code

In class, you write your code, and then it is finished. There may be multiple parts of the project to tackle, but the requirements are fixed.

Real applications evolve over time, as features are added and removed in response to users' needs. There are tons of implications for this, especially in the tools for managing projects.

As you saw when you deployed your applications, hosting services have tools to redeploy and update the application when you make changes to the _main_ branch on github. They can also create different _preview_ versions of the application, so that teams can test changes internally before releasing them to the world. These are often called the _testing_ or _staging_ environment (as opposed to the _local_ environment on your laptop, or the _production_ environment, which is the live application).

In projects that used the Prisma database, you've seen something called a _migration_, which represents a change to the database schema. Because databases have to change over time, and the changes themselves are complicated and tied to the application's code, it is common for most database schema development to use migrations.

## Real Devices 

In class, your code has to run on your computer. Real applications have to run on the server, and the pages have to work on lots of different users' devices.

Servers may have a different operating system or configuration from your laptop. Working on a team, you may have lots of different devices that need to be able to run the application. There are tools like Docker and Vagrant that simulate a standard environment, so that you can be certain that if your application runs on your computer, it can run on the server or on your teammate's computer.

On the client side, there are no tools like Docker that can standardize exactly the way the client-side code will run. Instead, you have to build web applications so that they work well on different browsers, on different devices.

Designing pages to work well across different screen sizes is called _Responsive Design_. You can use HTML and CSS to shape the content so that it looks 'right' on a monitor, a laptop, or on a phone.

Writing code that works well on different web browsers can also be a challenge. Especially as the web platform changes, some features don't get released to all platforms at the same time. You can browse features and see support across different browsers at [Caniuse](https://caniuse.com/).

## Real internet

Users won't always have a stable internet connection, and they have to pay for data. As a developer it's critical to be aware of what requests your application needs to make and how much data is sent. When possible, design applications _offline first_ so that they can function well, even if there is no data connection.

## Localization and Internationalization

Apps have users from lots of different countries and cultures, who speak lots of different languages. Localization and Internationalization (often abbreviated i18n) are the processes of making applications flexible and adaptive to different languages, cultures, regulations, and markets.

Real applications often make use of libraries to translate key parts of the page (like the text on the buttons or the navigation menu) into different languages, to suit their users. 

## Further Reading: Contending with Reality

Reality is complex. Applications have to negotiate and manage that complexity. If you are curious, read these links to expand your perspective on the world that applications have to contend with.

**[Falsehoods Programmers Believe About Names](https://www.kalzumeus.com/2010/06/17/falsehoods-programmers-believe-about-names/)** explores different assumptions about names that might be designed into an application or database system. Because names are complicated, they are difficult to 'get right', and sometimes it's not even clear what it would mean to get it right! For more lists of falsehoods, you can check out [awesome-falsehoods](https://github.com/kdeldycke/awesome-falsehood).

**[What happens when you load a URL](https://danluu.com/navigate-url/)** is a common interview question and one of the diagrams you've drawn in this course and in the Web Foundations course. The blog post dives much deeper into the topic, and explores things on the hardware and network level. The diagram we've drawn in class leaves out a lot of details! There is a follow-up github repository with a comprehensive answer: [https://github.com/alex/what-happens-when](https://github.com/alex/what-happens-when).

