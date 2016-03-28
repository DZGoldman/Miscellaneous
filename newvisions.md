Form limiter - stops google form from accepting responses after a certain amount of time


onOpen - initialize page, menus items
formLimiterSettings - create actual page (is there html anywhere?)
refreshlimit - take limit into effect if need be (all 3)
checksend_notification - notify if form is reached (all 3)
saveformlimit - all 3
closeform just closes it on html?

helper functions
eval num trigger? uses # and cell
ssetTime trigger uses date
checking time and deleting time are scatterd



Split up into angular directives:
need to:
CRUD limit
check if limit is reached
send notification if it is?


Refresh limit type - instead of having function refresh/recheck, include as part of angular's digest cycle.
Split up by limit type?
-Date time
-responses
-cell value
This makes much more sense logically and fucntionally 
universal functions (like delete limit) go in main application folder



Questions:
Does client side currently use J-Query, or just vanilla-js?
Is there html anywhere, or does gs creat all of it?
Refresh limit type - and form limiter? Do these trigger every n-seconds?
What does close form do?
