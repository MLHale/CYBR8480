# CYBR8480
This repo contains a digitized version of the course content for IA8470 Secure Mobile/IoT Development at the University of Nebraska at Omaha.

## Overview
Mobile devices are already pervasive fixtures of 21st century culture and increasingly the internet of things (IoT) and wearables are proliferating throughout the world. As this proliferation occurs, numerous vendor-centric and third party mobile, wearable, and internet of things apps are being created by developers and downloaded by end-users with little to no thought about the security and privacy of the information used and collected by the apps. This course examines this issue from a development point of view to a) introduce mobile/wearable/IoT architectures and technologies, b) increase developer application development competencies with these technologies, and c) integrate secure design principles into the ideation, design, and testing phases during development.

### Table of contents
[Online discussion area](#online-discussion-area) | [Location](#location) | [Supplies](#supplies) | [Projects](#projects) | [Labs](#labs) | [Class topics](#class-topics) | [Syllabus](#syllabus) | [License](#license)

## Online Discussion Area
I have setup an online discussion board on slack.com for usage in this class. If you decide to work on a group project, I can create some private channels for you to work on, but I want to be able to participate in your conversations - so please use the space on slack.

Go to [https://drhale8480.slack.com](https://drhale8480.slack.com) and use your unomaha email address to register an account. This will give you access to the course discussion and project collaboration spaces. Use the the general channel or create a new one for your team.

## Location
All classroom activities will take place in PKI room 259 unless otherwise noted ahead of time.

## Supplies

### Hardware/software
* Your laptop - capable of running android studio (Win7+/MacOSX10.10+ 8GB Ram, 2GB disk space, 1280x800 min, 64bit (pref))
* [Metawear](https://mbientlab.com/store/) Any of the R, RPRO, RG, C, or CPRO models will work. If you are just using it in the class, the R version is the cheapest and recommended ($40).
* Android 4.3+ (API level 18+) Bluetooth LE capable phone or tablet
* IoT Device of your choice for your project (something you can select later when you choose a project)

## Labs
- Introduction to the course
  - [Virtualization primer](/modules/virtualization-primer.md)
  - [Github primer](/modules/github-primer.md)
- Hybrid app development in Cordova
  - [Part 1 - Setup and Hello World](modules/hybrid-app-part1/README.md)
  - [Part 2 - Working with Cordova Plugins](modules/hybrid-app-part2/README.md)
  - [Part 3 - Attacking Hybrid apps](modules/hybrid-app-part3/README.md)
- Native App development in Android
  - [Android Lab - Creating your first app and explore Android resources](modules/android.md)
- Wearable Development with Metawear
  - [MetaWear Android Lab](https://mbientlab.com/tutorials/SDKs.html#java)
  - (cordova library no longer open source)[Working with Metawear](modules/metawear-hybrid.md)
  - Javascript example replacing Cordova lab - TBA

## Class Topics
- Getting up to speed
  - Virtualization and Github Labs
- Introduction to Mobile app Ecosystem ([PDF Lecture 1](/lectures/1.pdf))
  - Types of mobile apps
  - Stats: Threat Vectors and vulnerabilities
  - Wearable and IoT Introduction
- Hybrid app Development ([PDF Lecture 2](/lectures/lecture2.pdf))
  - [Lab Part 1](modules/hybrid-app-part1/README.md)
  - [Lab Part 2](modules/hybrid-app-part2/README.md)
  - [Lab Part 3](modules/hybrid-app-part3/README.md)
  - Reading [Reducing Attack Surface on Cordova-based Hybrid Mobile Apps](https://dl.acm.org/citation.cfm?id=2688417)
- Native app Development ([PDF - Credit Xin Yang, UC Santa Barbara](http://lbmedia.ece.ucsb.edu/member/uweb/Teaching/website/PPT/01_Intro_Android_Basics.pdf))
  - Dalvik vs ART architecture [Link to Figure](https://github.com/MLHale/CYBR8480/blob/master/lectures/ART_view.png)
  - Native-level security design features [https://source.android.com/security/overview/kernel-security.html](https://source.android.com/security/overview/kernel-security.html)
- IoT Development primer ([PDF Lecture 4](/lectures/lecture4.pdf))
- Android / IoT Security Readings
  - P. Faruki et al., "Android Security: A Survey of Issues, Malware Penetration, and Defenses," in IEEE Communications Surveys & Tutorials, vol. 17, no. 2, pp. 998-1022, Secondquarter 2015. doi: [https://doi.org/10.1109/COMST.2014.2386139](https://doi.org/10.1109/COMST.2014.2386139)
  - M. M. Hossain, M. Fotouhi and R. Hasan, "Towards an Analysis of Security Issues, Challenges, and Open Problems in the Internet of Things," 2015 IEEE World Congress on Services, New York City, NY, 2015, pp. 21-28. doi: [https://doi.org/10.1109/SERVICES.2015.12](https://doi.org/10.1109/SERVICES.2015.12)
  - M. L. Hale, D. Ellis, R. Gamble, C. Waler and J. Lin, "Secu Wear: An Open Source, Multi-component Hardware/Software Platform for Exploring Wearable Security," 2015 IEEE International Conference on Mobile Services, New York, NY, 2015, pp. 97-104. doi: [https://doi.org/10.1109/MobServ.2015.23](https://doi.org/10.1109/MobServ.2015.23)
  - Farooq, Muhammad Umar, et al. "A critical analysis on the security concerns of internet of things (IoT)." International Journal of Computer Applications 111.7 (2015). [http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.681.4342&rep=rep1&type=pdf](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.681.4342&rep=rep1&type=pdf)
- Open Discussions on student-driven topic areas
- Time to be creative
  - Come up with your own project idea or implement something for a friend/family member or community organization


## Projects
- [Project Milestone 1 rubric](/projects/milestone1.md) : In this project you will define your idea and discuss it with Dr. Hale to get some initial feedback.
- [Project Milestone 2 rubric](/projects/milestone2.md): In this milestone you will work to create an initial basic prototype of your product.
- [Final Milestone rubric](/projects/milestone3.md) : In this milestone you will polish your product and realize your user stories.

2018 Projects
* [BikeSpeedMonitor](https://github.com/oliavd/bikeSpeedMonitor/tree/master/ProjectMileStone1) - Olivier Avande
* [DropTap](https://tap.apt-get-sudo.com/) - Michael Galde
* [SmartThingsWebAPP](https://github.com/woonat01/SmartThingsWebAPP) - Nate Wood
* [Laundry Notification App](https://github.com/SarahLN/Laundry-Notification-App) - Sarah Noles
* [MetaShot](https://github.com/gandersonUNO/MetaShot) - Glenn Anderson and Daniel Lucier

2017 Projects and Final Presentations
* [E-notifier](https://github.com/vingle1/E-Notifier) - Vaibhav Ingle
* [FishBright](https://github.com/Append/fishingapp) - Gib Filter
* [FlyDry](https://github.com/gewethor/FlyDry) - Gabi Wethor
* [KeyboardDetect](https://github.com/JMPercival/8480Project) - James Percival
* [KeyFinder](https://github.com/jnyiok/KeyFinder) - James Nyiok
* [OpenSesame](https://github.com/jeffreysdempsey/OpenSesame) - Jeff Dempsey


## Syllabus
### Date/Time: Wednesday 5:30pm – 8:10pm
### Instructor:  Dr. Hale
### Office:  PKI 174-D, (402) 554-3978
### Office Hours:  By appointment or walk-ins anytime the door is open
### E-mail:  mlhale@unomaha.edu

### Grading Breakdown (due dates are tentative)
- (10%) Participation score (meetings, short tutorial participation, etc)
- (15%) Introduction to Hybrid Apps (Ember/Cordova) (Lab 1 - no rubric)
  - Part 1 - Setup and Hello World (5%)
  - Part 2 - Working with Cordova Plugins (5%)
  - Part 3 - Attacking Hybrid apps (5%)
- (10%) Introduction to Native Apps (Android Studio) (Lab 2 - no rubric)
- (10%) Introduction to Wearables (Metawear) (Lab 3 - no rubric)
- (10%) Topic Centric Discussions (Short reading assignments)
- (15%) Semester Project Milestone 1 - ([Rubric](/projects/milestone1.md))
- (15%) Semester Project Milestone 2 - ([Rubric](/projects/milestone2.md))
- (15%) Semester Project Milestone Final - ([Rubric](/projects/milestone3.md))

Each project milestone will have a specific grading rubric that includes the core requirements for the project (i.e. what the application must do), any required intermediate milestone goals (such as short progress meetings with the instructor), the project due date, and the list of items that must be submitted. Each project will include a presentation component to be presented in class on the project due date. Projects build upon each other. The final Project is considered to be comprehensive. This means that <i>there is no final exam</i>. Final Project presentations will be presented on the day of the Final.

### Attendance
- Class Attendance: You do not have to attend class except on presentation days (see below). Given the course is one day a week, attendance is highly recommended. Missing a single class is equivalent to missing 2-3 classes of a normal course. If you miss class, you are responsible for getting the material – including any assigned project work.
- Presentation Attendance (Mandatory): If you miss class on a presentation day you will receive a 0 on the presentation portion of the project grade unless you have a university-approved excuse or an approved extension (see below).

### Group Work
Students may choose (or be compelled) to work in groups. Group projects will include an individual participation grade worth 40% of the total group points, e.g. a group may make a 100% on a particular project, but an individual with low participation in the group may make a 60%. Participation will be anonymously rated by other group team members and the instructor.

### Team formation
The instructor reserves the right to make a change to any team or any project during the course of the semester for any reason that may or may not be disclosed. Project rescoping will be performed in this event.

### Service Learning / Real World Customers
As part of UNO’s strategic initiatives, individuals or groups may be partnered with community organizations in Omaha for service learning through the center for community engagement. If community partners can be identified, student projects (group or individual) in the class may work towards meeting community needs. In the event of community projects, appropriate scoping will be considered to ensure that community needs can be met within the time constraints of the coursework.

### Project Extensions and Late work
Sometimes unforeseen events occur or development takes longer than expected. In such cases, project extensions will be allowed. To receive a project extension, individuals or groups must request an extension at least 24hours in advance of the project due date. Extension time frames are at the discretion of the instructor, but generally will not be longer than 1 week. Failure to request an extension 24 hours prior to the due date means that the work is due at the specified time. Late work without a requested extension will receive a 5% point reduction per day up to a total of 40%. Late work submitted 2 weeks after an original (or extended) due date will not be accepted.

### Special accommodations for students with disabilities
Students with disabilities requiring special accommodations must contact disability services. Disability services may be reached by phone at (402) 554-2872 or by email at unodisability@unomaha.edu.
### Special accommodations for active duty or reserve military
Students serving in the military requiring special accommodations (e.g. unit deployment) must contact the office of Military and Veteran Services by phone at (402) 554-2349 or by email at unovets@unomaha.edu.

### Plagiarism
The university policies on cheating and plagiarism apply in this course. Except on designated group work, the expectation is that every student will do their own work. Students under suspicion of plagiarism for individual assignment submitted materials will be given an opportunity to defend themselves. If after defense the instructor still believes the work to be plagiarized the department chair will be notified and the grade evaluation for the assignment will be lowered to a value between 50% and 0% at the discretion of the instructor. If a second occurrence of plagiarism occurs, the student will receive an F for the course and the registrar’s office will be notified that the student is not permitted to withdraw from the course. In addition the department chair and dean will be notified.

### Work Retainment
The CS and IS programs in the College of IS&T are accredited through ABET (the Accreditation Board for Engineering and Technology. This organization occasionally requires that we keep samples of student work.

The instructor may retain a copy of your exams (with names and any other identifying information removed) for accreditation or pedagogy purposes, unless you specify otherwise in writing.

In addition, the instructor retains the right to use any code or project artifacts developed in the course for pedagogy, research, or service learning purposes. Student web project code developed in the course may be used in future secure project development courses, by the instructor for research purposes, or by designated stakeholders.

## License
Secure Mobile / IoT Development
Copyright (C) 2016-2017  Dr. Matthew L. Hale

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">CYBER8480 and related works</span> by <a xmlns:cc="http://creativecommons.org/ns#" href="http://faculty.ist.unomaha.edu/mlhale" property="cc:attributionName" rel="cc:attributionURL">Matt Hale</a> are licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.
