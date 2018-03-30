![cc 3.0](https://licensebuttons.net/l/by-nc/3.0/br/80x15.png) ([CC-3.0 permissive license](https://tldrlegal.com/license/creative-commons-attribution-(cc)#summary))

# WARNING

Here are my (very simplified) ideias, I don't have intention to make it like a paper or sound as if I were an expert, I'm mostly a game player as many of you. 

# TLDR; My coach (or Driving teacher, professor ...)

Is an **automatic driving coach** that can teach you how/where to improve your skills in a certain track with a certain car (or category of car). 

Let's use **track A** with a **car B**, in the **section 1**, from this track, a coach would tell me that I need to brake earlier to **turn 1** and things like that, such as: **increase your throttle at T2 exit**, **stay in the racing line on S3 (between T1 and T2)**, **brake ealier for T3** and etc.

It might be done by using data observed from the top racers in that same configuration (mostly track and car category).

## Long (or better) explanation

### My assumptions (or the danger of the assumptions)

![racing car timed data](https://image.ibb.co/czsDPn/New_Doc_2018_03_30.jpg)

Let's assume that all the online drivers (players) share a common time (or **timeline**) and that we can gather data such as:

* **steering wheel** (`ste`) position (how much are we steering? measured as an integer value, going from -MIN (left) to MAX (right) )
* **accelaration** (`acc`) force (measured as an integer value, going from 0 to MAX)
* **brake**  (`bra`) force (measured as an integer value, going from 0 to MAX)
* **speed** (`spe`) (measured as an integer value, going from 0 KM/H or MP/H to MAX)
* **location** (`loc`) (measured as an integer value, going from 0 m to MAX m, MAX being the size of the track, this can be a 2D view of the track)

And all these data are in function of time. 

Just to be clear, let's simulate an example here: let's say for a time `t[x]` the **driver1** has the data of `ste=-30, acc=37, bra=0, loc=1280` at the same time `t[x]` the **driver2** in in other location of the track with data of `ste=-1, acc=96, bra=0, loc=2191`.

### A simple driver behavior rating system

We can design a driver behavior rating system (such as [SR on Gran Turismo Sports](https://www.gran-turismo.com/us/gtsport/manual/#!/tips/content02) or [SR on iRacing](https://www.iracing.com/safety-ratings-a-cure-for-the-mayhem-in-online-racing-games/)) using all these data but instead of taking only the incident moment we can observe a wider timeline (that is to say, `t[x-n]` until `t[x]`) and [react correctly to lag](http://community.eu.playstation.com/t5/GT-Sport/Regarding-penalty-judgements/m-p/25604944) or be more fair/accurate such as: 

* don't penalize someone that spin alone (far from other drivers)
* fix (ghost or ignore) abrut changes in speed / acc in short timespan
* decrease the penalty when see observe intentionalyty of avoid crash, such as was the driver, off the throttle? (`acc=0`) did she/he try to avoid the collision? (`ste`)
* and so on and so forth

### A driving teacher system

Once we got all these **data we can use the top drivers** (based on their times on a given combo: track + car category) timing and data and **compare them** to the `pupil` so the `teacher` can tell improvements to be made based on differences among the data:

* You  need to brake earlier to T1
* Increase your throttle at T2 exit
* Stay in the racing line on S3 (between T1 and T2)
* Brake ealier for T3

You see that in reality the top driver, or `master driver`, will be your coach.
