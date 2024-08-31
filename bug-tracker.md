# Bugs

Journal of how I fixed the bugs.

## 3
Bug no. 3 was fixed first.

### Why/How?
After going through the README, I decided to just go through the website and play around with the interface. As I was doing this, I decided to try the first Select not scrolling with screen bug. Saw it was reproducible and moved on. Then while playing with the options, I got an "Oops, broken something: EmployeedId can't be empty" error. It seemed interesting. I checked the console and saw a similar thing. I reproduced the bug and remembered reading about it in the README. It peaked my interest and I decided to dive into the codebase to understand what happened. This led me down the rabbit hole. I mentally worked through the code in each file to picture how they all interact with each other and the problem at hand. Went back to the console and checked error was logged at a particular number, worked backwards and checked the code again. Saw the error was thrown from the `requests.ts`. Deliberately not wanting to tamper with any part of the code until I was sure I understood how it functioned. After analysis, I knew the bug was in the Select calling a function for fetching the transactions by ID but got no idea where or how the bug was still there. Got back to the App.tsx and edited the `onChange` in the `InputSelect`, I got nothing. I was mentally telling myself that I probably wasn't a good developer as I thought I was. 

I got a lucky break when I decided to check one of the files I had overlooked initially during my investigation, `/utils/constants.ts`. I saw the exported constant had an empty ID. WOW! I played around a bit to see how I could make sure that the `requests.ts` could accomodate it, I then thought maybe it should have a definite ID value after all. Doing this didn't make the problem go away tho as we would now have it stuck on loading because the `requests.ts` is filtering based on valid IDs. I decided to add in the `onChange` a check for that custom ID and then load all the transactions we have. 

P.S.: This took over 2 hours :(.


