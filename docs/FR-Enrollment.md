At the moment, AutolabJS acts as an open enrollment system. Anyone case register on gitlab, get evaluated on AutolabJS and have their scores listed on the scoreboard. We can have a closed system where only enrolled students are allowed. Different ways in which students can be enrolled into AutolabJS are:

1. Restrict gitlab accounts
    We can manually / programmatically add enrolled students into gitlab and close the registration option of gitlab. Thus only enrolled students can create projects on gitlab. The problem with this choice is that dummy evaluation requests can still be submitted on AutolabJS front end. Of course, these only pollute the scoreboard.

1. Restrict to enrolled users in front end
    Front end can maintain a list of enrolled users in the database.
