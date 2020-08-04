### website hacking on Android how to do it?
Well it is Fairley simple there is many many ways to exploit a box/*website* u just have to looking at what u are going at very closely.
Today i will be showing u show how to exploit a website with (blindsql) to gain shell on Android. 
##### NOTICE IT IS VERY IMPORTANT TO DO THIS TOO TARGETS U HAVE PERMISSION TOO

### step (1) finding you're target! 📖
Find you're target now this is not simple and this is not hard.
First u will need dorks if u don't know what a dork is, visit here : *https://www.google.com/amp/s/www.webopedia.com/amp/TERM/G/google-dorking.html*
Alr cool if uk what it is then we can continue 😎, we will do a quick google search like
(*best sqldorks list 2020 pastebin*) the first link that showed up was
*https://w-se.com/latest-carding-dorks-list-for-sql-injection/*
Soo now we pick a google dork that we think would be the most common, and here we go (*Checkout.asp?catid=*)
Now we got a <HuGe> selection of sites soo what do we do now? Well we can pick one for example my target is *https://www.*********.com/item_page.php?Id=78&path=Best%20Sellers&cat_id=

### step (2) finding & exploiting our vuln 🔥
Now we look at our Url we see that there is 3 pram we will test each pram for a error, how do we test for a error?
Well first add a  ' in the pram example : *https://www.********.com/item_page.php?Id=7&path=Best%20Sellers&cat_id='*
As we can see when we submit the url no error and the pages does not change so it is not vuln.
We are skipping path= bc that is LFI a different exploit that is not our topic today.
Soo now we will test Id= so Id=' and lets submit it,
We get this error 
```bash
Warning: mysql_num_rows() expects parameter 1 to be resource, boolean given in /home1/benline/public_html/item_page.php on line 707
```
Now not all the time u will get a error how to see if the page is vuln. If u submit it and the page is still there but the content is blank or text has been removed that can tell u that it is blind based error.

Now what do we do we have a vuln site? How do we get what we are looking for

Well il tell u first download this apk
https://m.facebook.com/M4st3rJ30/posts/1317794145029000
This app will let u exploit sites with attack payloads.

Once downloaded open it now u might be confused if u are new too this stuff

The 2 buttons we are really using are (EXECUTE) & (string based) 

Now paste you're target url in *enter web addresse*
Click the button (execute) to load the page. Click on are pram that is vuln so for me Id=78 remove the ' to get remove the error and click on the button string based u will see alot of payloads the one u need is * Order by *
Click on that and u will have to enter how many columns u want to order so now we are in a poop situation we dont know how many columns the datatables have
How do u find that out? Well easy if we enter 1 and click enter then click execute the page will go back to normal that tells us that there is 1 column now if we type in 10 and the page is the same it will tell us there is 10 columns. Say we put in 12 and the page changes from normal that means theres not 12 columns but if we put in 11 it goes back. Soo we got are number there is a total of 11 columns in the datatable.
Now we got are number 11 we remove the order by text so it looks like Id=78 and we click on *union select* now since we know how many columns there are so we just put 11 and enter
Now u can see the page goes normal but u see numbers where there is a number that means that column is injectable soo now we see that number 2 is injectable like it says on the site so we go to our url where it says 2 we remove the 2 and put : 1,user(),3,4,5,6,7,8,9,10,11
Now click execute and boom we get the database username so we see that 2 is injectable now remove user() and click the button *string based* then click on DIOS by tr0jan! 
Now click execute. Now we can see it dumped alot of tables names so what we are looking for is a admin panel. So do ctrl f and type adminand click enter
That brings use to the table called admin if there is a admin panel so what we need to do is dump this table so in this admin table it says there is 2 tables named username password
So we go back to anonhackbar then we remove all that text in 2 and we click on the button called string based again and click *dump data dios*
Now we type the table name up top so admin then button we type the fields we wanna dump so admin,password.
Now we can see that they don't encode there database so it's in plain text so easy now we have to find the admin panel bc we got the username and password
So go to the url remove it so its like https://******.com/admin we get a 404 well that sucks so we need to look somewhere else so find a image that is hosted on the site click open image location and we look at the dir so we get https://******.com/xadmin/images/ji.jpg we can see that there is a folder called xadmin lets go there so 
https://*****.com/xadmin/ we get a login so lets try the creds that we dumped and uwu we are in YaY but what can we do know?
Well we need a shell go onto a new tab and type batman php shell github download it
Now we go to product and lets edit the product and click image then find you're shell then click save
Then if it says product saved then we did it now too find are shell go to that product then hold them blank images and click open image location now go to that tab it opened and look we got a login to are shell uwu we did it boys now login ro you're php shell and have fun defacing boyz

