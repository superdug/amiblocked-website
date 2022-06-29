---
 title: "I did all of this on my iPad"
 date: 2022-05-25T23:22:35Z
 draft: false
 ---

 So I decided to get myself an iPad Pro 12.9” as a full time machine to replace my need for both an iPad and a MacBook Pro.  This endeavor I should mention was meant to better my life, which doesn’t necessarily mean it was the cheapest or most economical solution, but in the end worked out really well.

 First things first, I need the iPad to do work stuff.  The pandemic and apple just pushing hard on developers has made collaboration software a new mad craze that everyone is starting to support at some level.  Since they’re already developing new software the idea of why not make it for the iPad too has come into play with all of the work software I need for my day to day.

 Now what does that mean exactly?  I mean, my day to day, the parts of my job that I do now virtually that I used to do entirely face to face.  So video meetings, emails, chats, music, documentation, administration, and maybe some advanced stuff to possibly make a laptop entirely for edge cases are all possible.  I use the google suite, office 365, webex, zoom, and slack all successfully and natively in their respective apps on the iPad.  They support mouse and keyboard and all of those video programs support what iPads call “center stage” which takes the front facing camera to center and focuses on your face even if you move around. 

 Which in and of itself is more than enough for what I need it to do really.  As a media communication and consumption device, the iPad wins hands down, right there.  It does it’s job for me, which is media consumption and communication. The iPad has always been a secondary device for me.  While it takes a lot of my attention, as obviously I spend a lot of time in meetings, it was never my primary computing device.

 But the iPad has saved me in the past by just being itself.  I’ve been in the middle of multiple video meetings for work that I was presenting in that failed entirely on my mac that I was able to salvage because my iPad was already on my desk.  The walled garden has a set of strict controls with how you are able to interact with it and software just isn’t allowed to be a bad actor in the iPad ecosystem without a flurry of outrage on your favorite social media outlet calling publishers out.  

 First edge case was the legacy management of my Linux hosts I run.  I have migrated services and have started to embrace the edge and serverless, but still have a need for a full Linux system on the internet.  While all of my new projects utilize AWS services for hosting, I still have legacy operations that I tend to and maintain.  Because of obligations of commitment I can’t just retire the systems, but they work for third parties who’s workflows are important to them.  In the idea of wanting to keep my users happy, if a system “just works” and is not a security risk, I leave it in legacy mode.

 The main idea here is that I need a way to SSH into the systems.  I use public key encryption to identify to my SSH servers which is what I’d consider to be fairly standard.  In testing I found a program called Terminus that is an SSH terminal emulator and SFTP client management system for iOS/iPad OS/Mac OS that manages keys, clients, and profiles in a common application.  Combined with a keyboard and a mouse, the only thing really missing is the ability to copy text directly from the shell into the clipboard.  

 To get around this inconvenience and to support the developer that made this possible, I bought the yearly license to terminus to get the SFTP client.  I would just use a text file as my “copy/paste” bin that I would sync manually between the SSH target and my iPad’s file manager.  It wasn’t the most convenient way to operate, but it got the job done and it made the need to use a laptop for SSH sessions non-existent.  So there was one edge case taken care of.

 Now there was the issue of development.  All of my code lives on GitHub and runs from command line tools that are not mac specific in any way.  There isn’t a command line tool that I use in Mac OS that I haven’t already in the past used in a linux environment first.  Since I already had a linux environment I was using for hosting legacy applications, there was no reason I couldn’t use that environment for development.  So I copied the appropriate SSH keys into my linux environment and headed to the races.

 The first thing I wanted to do was get my project site up and running.  It was bothering me on a lot of levels that the site was up and running and then I ended up killing it entirely and was never able to fully rebuild it.  The site relied entirely on terraform to set up, so I set out to make a terraform development environment.  Wanting to streamline this process as much as possible I tied terraform cloud into github and started to load the terraform code into terraform cloud.  

 Now I’m a big fan of Vim, but let's face it, the mouse won the input war for a reason, it’s just super intuitive to use and it’s always there for you.  The problem is, I want my development editor to work on the iPad.  I’m used to the workflow, the shortcuts, the plugins, etc.  I want that editor on my iPad, but I don’t want a virtual desktop of the software if I can avoid it.  The idea that I turn my iPad into a virtual terminal for a windows or mac back end seems like it would be cheating and also comes with the lag of being non native to begin with.

 Along these lines, I’m not against a google or AWS workspace.  I was always going to fall back on some kind of virtual desktop.  If I needed to branch down this idea, I had begun testing running VS Code for Linux on my Linux environment hosted over SSH via NX.  The native iPad NX client supports key-based auth and the setup compared to a decade ago is an absolute breeze.  Knowing I could easily just upgrade the ram in the box at any moment and still have my native development environment is still on the table as an option.

 Anyways, Microsoft owns GitHub.  They are the creators of my IDE of choice which is Visual Studio Code.  If you change the url for any GitHub.com webpage from .com to .dev you will load that repository up into the web editor.  The web editor is a stripped down version of Visual Studio Code, but in the browser.  It works, and it works really really well.   So now I could push my code commits from my terraform repository up into terraform cloud and get the site rebuilt.

 Since the site uses hugo and an automated git workflow in GitHub to publish, that just means that I need the ability to edit flat files, which I can do from my linux session or from just editing the repository directly with VS Code for the web.  Either way I have managed to replace my laptop with my iPad successfully to date.  It still sits around if I need to access it, but I still haven’t needed to.

 There is all sorts of room for improvement here.  And we’ll start to see that as the ecosystems of Mac OS and iPad OS start to mesh together.  I know that the keeping the ecosystems apart makes some sense to someone somewhere, but not me, and fighting it is just stupid.  People want to interact with a super powerful slate, plain and simple.

 ***UPDDATE** 06-05-2022

 I've since stopped using termius and switched to using [Panic's SSH Client for iOS](https://panic.com/prompt/).  It's made by the same folks that make the playdate gaming system and it includes copy and paste of the terminal screen.  Thus my need for a SCP client was ended and termius was retired.