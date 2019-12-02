# TryHackMe's Holiday Hack Challenge 2019
![Image](https://raw.githubusercontent.com/dscovetta/HolidayHack2019/blob/master/images/hh2.png)

_Background: I'm writing this up to document my own progress through the challenge, and write out how arrived at each answer. Hopefully this will help me and potentially others in future challenges. Although I'm a paying member of TryHackMe, the holiday challenge is open to all._

![Image](https://raw.githubusercontent.com/dscovetta/HolidayHack2019/blob/master/images/hh4.png)

_Luckily, this one can be answered easily enough by inspecting through the browser (web developer tools), as it is passed back from the web server. We can see that it's the cookie is named `authid`._

![Image](https://raw.githubusercontent.com/dscovetta/HolidayHack2019/blob/master/images/hh7e.png)

![Image](https://raw.githubusercontent.com/HolidayHack2019/blob/master/images/hh5.png)

_Allright, this one takes a little more work. Cookies are a key value pair in the form of name:value and used to establish/validate sessions. Session Management refers to how the server keeps track of the actions performed by a client._

![Image](https://raw.githubusercontent.com/HolidayHack2019/blob/master/images/hh10.png)

_So we're able to identify the cookie name/value; but we need to separate the fixed part of the cookie, and de-code it. You can also use Burpsuite to proxy and inspect the traffic between the browser and egress to the web server._

![Image](https://raw.githubusercontent.com/HolidayHack2019/blob/master/images/hh11.png)

_Allright, so - it's encoded at Base64, so let's we'll need to decode. Luckily there's a discord chat server for all this and someone recommended [a neat coder/decoder tool on github](https://gchq.github.io/CyberChef/). We then arrive with the results `usernamev4er9ll1!ss`._

![Image](https://raw.githubusercontent.com/HolidayHack2019/blob/master/images/hh12.png)

_I think I missed a step in separating the username/password in the encoding, and can probably be identified by creating a separate username or password (but not both), and identifying the differences as a seperator._

![Image](https://raw.githubusercontent.com/HolidayHack2019/blob/master/images/hh14.png)

_Yep, so I dug abit deeper and was able to confirm separation:_
- _Email: email@email.com_
- _Name: name_
- _Password: password_
- _Cookie: authid=dXNlcm5hbWV2NGVyOWxsMSFzcw%3D%3D_
- _First part: dXNlcm5hbWV2 - coded, username - uncoded_
- _Second part: NGVyOWxsMSFzcw, v4er9ll1!ss - uncoded_
- _Extra stuff: %3D%3D_

_Allright, so let's take a look at the next one:_

![Image](https://raw.githubusercontent.com/HolidayHack2019/blob/master/images/hh6.png)

_In this exercise I suspect we'll need to re-code with admin credentials and attack the web authentication._
