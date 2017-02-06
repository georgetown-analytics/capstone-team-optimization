# Capstone Team Optimization

**Optimization method to select Capstone teams from the preference survey.**

Georgetown students fill out a project interest survey at the start of Foundations, which we then use to attempt to optimize project teams curation. This serves as an intereting icebreaker to get people talking together about potential projects, but also as a mechanism to show optimization techniques in real life. Though obviously this method is more for demonstration purposes, I think it highlights a few key techniques. 

The optimization works as follows:

1. Assign students into random teams. 
2. Compute the _cost_ of those team assignments across the entire cohort (cost function to follow). 
3. Select a random number of swaps between 10 and 100
4. For each swap, switch two members of teams, if resulting _cost_ is less, continue; otherwise revert to original
5. Repeat steps 2-4 until minimum error or maximum searches

So basically this is a random hill climbing type search (or is intended to be). There are a number of ways to improve this function of course, but it's for demonstration only. 

The cost function is as follows:

1. Start with cost = 0 (perfect teams have no cost)
2. Add the square difference of each team's size with the optimal team size 
3. Add the number of unique OS per team - 1 (e.g. same OS is zero cost) 
4. Add cost of missing roles (e.g. don't have a programmer on the team)
5. Add domain alignment cost (similar domains selected is better)
6. Add dataset alignment cost (similar datasets selected is better) 

Note that this cost function can change and be added to - make sure you review the notebook for the latest version of costs. 

## Getting Started 

The first step is to download a CSV copy of the survey responses and save them to:

    fixtures/cohort#-preferences.csv 

Noting that # should be the cohort number. Run the Jupyter notebook:

    $ jupyter notebook optimize.ipynb 

This should open a browser window with the selection tools. 

In the first cell modify the following constants as needed:

    COHORT = # 
    TEAM_SIZE = 4 

Setting the cohort # to match the one saved in the preferences file. At this point you should be able to hit run all and have the assigned teams print out at the bottom of the notebook. 

**NOTE**: Occassionally I have to munge the CSV file, but it's usually minor and I can never remember what I have to do. 
