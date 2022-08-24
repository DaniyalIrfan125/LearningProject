Activity Launch Modes:

<b>1.Standard</b><br>
A new instance of activity will be generated in stack everytime.
It is default value of launch mode.There is some difference for different android version: if activity is starting from another application, on androids <= 4.4 it will be placed on same task as starter application, but on >= 5.0 new task will be created.
For Example:
State of Activity Stack before launch B

A -> B -> C -> D

State of Activity Stack after launch B

A -> B -> C -> D -> B

<b>2.Single Top</b><br>
This launch mode is similar to standard mode. Activity with single top launch mode can have many instance in task, but the diffrence is that if activity with single top launch mode is already exist at the top of task(stack) new instance will not be created but onNewIntent() will be called of present instance.
For Example:

State of Activity Stack before launch D

A -> B -> C -> D

State of Activity Stack after launch D activity

A -> B -> C -> D
 (Here old instance gets called and intent data route through onNewIntent() callback)

<b>3.Single Task</b><br>
If the tasks don’t have an existing instance of the Activity, then a new instance is created that is similar to singleTop.
If the tasks have an existing instance of the Activity and it’s at the top of the Activity, then the system will pass the intent data to the onNewIntent function.
If the tasks have an existing instance but not at the top, then it’ll roll back to that Activity and destroy the Activities on top of the SingleTask Activity.

For example
If B has launch mode=SingleTask
State of Activity Stack before launch D

A -> B -> C -> D

State of Activity Stack after launch B activity

A -> B (Here old instance gets called and intent data route through onNewIntent() callback)

Also notice that C and D activities get destroyed here.

<b>4.SingleInstance</b><br>
This is a highly unique start option that is only used in programs with a single activity. It works similarly to Single Task, except that no additional activities are generated in the same task. Any further activity initiated from this point will result in the creation of a new task.

For example
A -> B -> C — Task #1
D — Job #2 (Here, D will be assigned to a separate task)

If you continue like this and add E and D, the stack will look like this: Job #1— A -> B -> C -> E.

For further understaning kindly follow this link
https://inthecheesefactory.com/blog/understand-android-activity-launchmode/en

