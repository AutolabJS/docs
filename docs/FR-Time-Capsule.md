**Time capsule** allows preservation of student submissions as they exist at a certain time in the past. Thus time capsule gives a hard guarantee to the instructor on the sanctity of the submitted code base.

Time capsule requires collection of student repositories at deadline. The subtle choices involved in implementing this feature are:

1. **User List:** Obtaining the list of users
1. **Trigger event:** for collecting code from gitlab repositories

### User List ###
We can ask the instructor to provide users list for the whole course or for one assignment. Since each AutolabJS instance is tailored to a course, we can assume that each AutolabJS would have enrolled users list. We can store the list of enrolled users in a dedicated DB table. If such a list is available, we must utilize the same. Allowing the instructor to provide the list of users seems to be most generic and most useful. Code written for letting instructor submit a list of users can be utilized in other scenarios as well. We can reuse the list submission code in revaluation, make up, implementing closed system.
    Otherwise, we can proceed with the list of users who already got evaluated once in the chosen lab. Starting with the already evaluated user list seems easier and should be implemented first. For the sake of ease of progress, we must clearly separate the code that obtains the list of users (from DB table / instructor) and the code that takes an array and does the time capsule work.


### Trigger Event ###
We can perform time capsuling work when:

1. User receives highest result evaluation    
    After a user receives highest marks, the score gets stored in the database table. The user repository as exists at that point gets preserved. A fool proof scheme would be replicate the user repository only once. Copying the user repository twice - once into execution node and once into load balancer - gives enough time window for the user to change the repository and create inconsistency in the stored marks and the captured repository.
    Ideally, the load balancer would make a copy of the user repository and forward it to the execution node. If we have a dedicated component for time capsule function, we can have all the other components (load balancer and execution node) interact with time capsule module.

1. User submits evaluation request    
    The replication in time capsule happens after each evaluation request. Given that we already have a git system for user repositories, it does not make much sense in storing each copy of repository; git is already doing it.

1. On evaluation deadline    
    After evaluation deadline is passed, we create copies of all user repositories. This is probably the most sought after usecase in time capsule.

1. On demand    
    Instructor can request for preservation of user code base at a certain point in time. It makes sense to provide option schedule this action as well.

Considering the amount of work the time capsule feature requires, it makes sense to have a dedicated time capsule module which uses gitlab for persistence.
