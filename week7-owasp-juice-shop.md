# Week 7: OWASP Juice Shop

OWASP Juice shop is a web application designed to be insecure to mimic an actual exploitable web application and is used to practise exploiting vulnerabilities and teaches the more practical elements of cyber security like SQL Injections, executing Cross Site Scripting [6]. Burp Suite is used as a supporting tool because it acts as an intercepting HTTP proxy between the browser and the server and allows every request or response to be captured, inspected, and modified before it is sent which is important for testing vulnerabilities that cannot be seen from the browser's interface normally , such as manipulating JSON fields in registration requests or removing specific fields  from password change requests [7].

Exercise 1:

Figure 32 - Find Carefully Hidden Scoreboard

![Figure 32 - Find Carefully Hidden Scoreboard](week7-owasp-juice-shop/001_Figure_27_-_Find_Carefully_Hidden_Scoreboard.png)

Step 1: Go on inspect, click on the sources tab, select main.js and type in “path” one of the results should be the score-board

Figure 33- Path Found for Scoreboard

![Figure 33- Path Found for Scoreboard](week7-owasp-juice-shop/002_Figure_28-_Path_Found_for_Scoreboard.png)

Output: When you add “/score-board” to the url, you will be taken to the scoreboard and juice shop will tell you that the challenge has been completed.

Figure 34 - URL Contains "Score-board"

![Figure 34 - URL Contains "Score-board"](week7-owasp-juice-shop/003_Figure_29_-_URL_Contains_Score-board.png)

Figure 35 - Challenge Completed

![Figure 35 - Challenge Completed](week7-owasp-juice-shop/004_Figure_30_-_Challenge_Completed.png)

Challenge 1 CIA Triad Impact

| Confidentiality - Breached | Integrity – Indirect Risk | Availability - Minimal |
| --- | --- | --- |
| Hidden Internal routes are exposed to users who are not logged in | Discovering hidden routes enables further attacks especially if admin routes are found. | Not much risk |

Challenge 2: Create New Admin User

Figure 36 - Create New Admin User Challenge (3 Star)

![Figure 36 - Create New Admin User Challenge (3 Star)](week7-owasp-juice-shop/005_Figure_31_-_Create_New_Admin_User_Challenge_3_Star.png)

Step 1: Create new user on the Register page

Figure 37 - Registering an New User

![Figure 37 - Registering an New User](week7-owasp-juice-shop/006_Figure_32_-_Registering_an_New_User.png)

Step 2: Ensure Burpsuite got the Request for login

Figure 38 - Burpsuite Got the details we Entered

![Figure 38 - Burpsuite Got the details we Entered](week7-owasp-juice-shop/007_Figure_33_-_Burpsuite_Got_the_details_we_Entered.png)

Step 3:

Copy request to repeater, change the email and add a field called “role”. In that role enter admin. The “role” field is used to determine the access level of a user.

Figure 39 - "Role: admin" has been added

![Figure 39 - "Role: admin" has been added](week7-owasp-juice-shop/008_Figure_34_-_Role_admin_has_been_added.png)

Step 4: Once “Repeat” is pressed, your new account should be updated to admin because we changed the role from “customer” to “Admin”

Figure 40 - New User has the role "Admin

![Figure 40 - New User has the role "Admin](week7-owasp-juice-shop/009_Figure_35_-_New_User_has_the_role_Admin.png)

Proof of completion

Figure 41 - Challenge 2 Completed

![Figure 41 - Challenge 2 Completed](week7-owasp-juice-shop/010_Figure_36_-_Challenge_2_Completed.png)

Figure 42 - New Admin User "brianadmin@roehampton.com" has been created

![Figure 42 - New Admin User "brianadmin@roehampton.com" has been created](week7-owasp-juice-shop/011_Figure_37_-_New_Admin_User_brianadminroehampton.com_has_been_created.png)

Challenge 2 CIA Triad Impact

| Confidentiality - Breached | Integrity – Breached | Availability – High Risk |
| --- | --- | --- |
| Gaining admin access exposes registered user emails, hashed passwords and order history. | As an authenticated admin, the attacker can modify user and product data which would erode the trust of available data | An admin account could be used to delete all products or corrupt the database schema |

Challenge 3: Find Admin Page

Figure 43 - Challenge 3: Find Admin Page

![Figure 43 - Challenge 3: Find Admin Page](week7-owasp-juice-shop/012_Figure_38_-_Challenge_3_Find_Admin_Page.png)

Step 1: Go on inspect, click on the sources tab, select main.js and type in “path” one of the results should be “Administration”

Figure 44 - Administration Path Found

![Figure 44 - Administration Path Found](week7-owasp-juice-shop/013_Figure_39_-_Administration_Path_Found.png)

Figure 45 - Acess Admin Challenge Completed

![Figure 45 - Acess Admin Challenge Completed](week7-owasp-juice-shop/014_Figure_40_-_Acess_Admin_Challenge_Completed.png)

Challenge 3 CIA Triad Impact

| Confidentiality - Breached | Integrity – At Risk | Availability – at risk |
| --- | --- | --- |
| Gaining admin access exposes registered user emails, hashed passwords and order history. | As an authenticated admin, the attacker can modify user reviews and product reviews | Administrator controls could be used to lock out customers |

Challenge 4:

Figure 46 - Challenge 4: View Another Users Basket

![Figure 46 - Challenge 4: View Another Users Basket](week7-owasp-juice-shop/015_Figure_41_-_Challenge_4_View_Another_Users_Basket.png)

Step 1: Login to an account, go to the basket page and open up session tab with the inspect tab open.

Figure 47 - Inspect Tab open with the Basket ID

![Figure 47 - Inspect Tab open with the Basket ID](week7-owasp-juice-shop/016_Figure_42_-_Inspect_Tab_open_with_the_Basket_ID.png)

Step 2: Change the Basket ID(bid) to another number like 1 or 2. After that reload the page.

Figure 48 - Basket ID Changed to "2"

![Figure 48 - Basket ID Changed to "2"](week7-owasp-juice-shop/017_Figure_43_-_Basket_ID_Changed_to_2.png)

Output (This shows another customers purchase details which consists of 2 orders of raspberry juice. The limitation of this is that it does not give more details such as the user who ordered it which if it did then a hacker could have made phishing page and send an email to the user explaining that something is wrong with their order.)

Figure 49 - Challenge completed and someone else’s basket is displayed

![Figure 49 - Challenge completed and someone else’s basket is displayed](week7-owasp-juice-shop/018_Figure_44_-_Challenge_completed_and_someone_elses_basket_is_displayed.png)

Output (This shows another customer’s purchase detail with BasketID 5)

Figure 117 - BasketID 5 purchase details from another customer account

![Figure 117 - BasketID 5 purchase details from another customer account](week7-owasp-juice-shop/019_Figure_117_-_BasketID_5_purchase_details_from_another_customer_account.png)

Challenge 4 CIA Triad Impact

| Confidentiality - Breached | Integrity – At Risk | Availability – Minimal |
| --- | --- | --- |
| Another Customers order details are exposed | If its possible to edit the basket, attackers could add or remove items. | The attack does not directly disrupt availability |

Challenge 5:

Figure 50 - Challenge 5: Login As Admin

![Figure 50 - Challenge 5: Login As Admin](week7-owasp-juice-shop/020_Figure_45_-_Challenge_5_Login_As_Admin.png)

Step 1:

Attempt to login as a admin by guessing the email and password once

Figure 51 - Unsuccessful log in using "admin user"

![Figure 51 - Unsuccessful log in using "admin user"](week7-owasp-juice-shop/021_Figure_46_-_Unsuccessful_log_in_using_admin_user.png)

Step 2: Ensure the login request is received by burpsuite and send it to repeater.

Figure 52 - Username and password recorded

![Figure 52 - Username and password recorded](week7-owasp-juice-shop/022_Figure_47_-_Username_and_password_recorded.png)

Step 3: Commit a SQL injection in the email section “adminuser” or 1=1 –"

Figure 53- Sql Injection in the Repeater

![Figure 53- Sql Injection in the Repeater](week7-owasp-juice-shop/023_Figure_48-_Sql_Injection_in_the_Repeater.png)

Output of the sql Injection with a generated authentication token, basket id and email  showing that we have been granted access and Proof of Completion.

Figure 54 - Successful Authentication and Token Recieved

![Figure 54 - Successful Authentication and Token Recieved](week7-owasp-juice-shop/024_Figure_49_-_Successful_Authentication_and_Token_Recieved.png)

Challenge 5 CIA Triad Impact

| Confidentiality - Breached | Integrity – At Risk | Availability - Indirect |
| --- | --- | --- |
| Gaining admin access exposes registered user emails, hashed passwords and order history. | As an authenticated admin, the attacker can modify user and product data which would erode the trust of available data | The attack does not directly disrupt availability but an admin account could be used to delete all products |

Challenge 6:

Figure 55 - Challenge 6: Provoke an Error that is not Handled Gracefully

![Figure 55 - Challenge 6: Provoke an Error that is not Handled Gracefully](week7-owasp-juice-shop/025_Figure_50_-_Challenge_6_Provoke_an_Error_that_is_not_Handled_Gracefully.png)

Step 1:

As a logged in user that you have created, Try and go to the profile page by clicking the profile icon

Figure 56 - Profile Icon

![Figure 56 - Profile Icon](week7-owasp-juice-shop/026_Figure_51_-_Profile_Icon.png)

Step 2: This page should come up showing that the request was not handled gracefully thus completing the challenge

Figure 57 - Unhandled error and it shows the Programming language being used

![Figure 57 - Unhandled error and it shows the Programming language being used](week7-owasp-juice-shop/027_Figure_52_-_Unhandled_error_and_it_shows_the_Programming_language_being_used.png)

Proof of completion

Figure 58 - Challenge Completed

![Figure 58 - Challenge Completed](week7-owasp-juice-shop/028_Figure_53_-_Challenge_Completed.png)

Challenge 6 CIA Triad Impact

| Confidentiality - Breached | Integrity – At Risk | Avaliability - Indirect |
| --- | --- | --- |
| Internal file path, source file name and language used have been exposed | Knowing the framework version could let an attacker look up known vulnerabilities and use payloads | Unhandled execetptions that cause crashes could cause the software to go down. |

Challenge 7:

Figure 59 - Challenge 7: Login Bender

![Figure 59 - Challenge 7: Login Bender](week7-owasp-juice-shop/029_Figure_54_-_Challenge_7_Login_Bender.png)

Step 1: Go to the product page and look through the reviews of all products to find a review left by benders email address.

Figure 60 - A review left by bender on the Banana Juice product

![Figure 60 - A review left by bender on the Banana Juice product](week7-owasp-juice-shop/030_Figure_55_-_A_review_left_by_bender_on_the_Banana_Juice_product.png)

Step 2: Commit SQL Injection in the email section of the login page by typing “- -". You can put any value in the password section.

Figure 61 - Sql Injection

![Figure 61 - Sql Injection](week7-owasp-juice-shop/031_Figure_56_-_Sql_Injection.png)

Proof of completion

Figure 62 - Challenge Completed

![Figure 62 - Challenge Completed](week7-owasp-juice-shop/032_Figure_57_-_Challenge_Completed.png)

Figure 63 - Logged in as Bender

![Figure 63 - Logged in as Bender](week7-owasp-juice-shop/033_Figure_58_-_Logged_in_as_Bender.png)

Challenge 7 CIA Triad Impact

| Confidentiality - Breached | Integrity – Breached | Availability - Risk |
| --- | --- | --- |
| Complete takeover of account allowing access to users personal data. | Attacker could make unauthorised purchases, reviews or change details | Attacker can change users login details and lock them out |

Challenge 8:

Figure 64 - Challenge 8: (Change benders password to slurmCl4ssic)

![Figure 64 - Challenge 8: (Change benders password to slurmCl4ssic)](week7-owasp-juice-shop/034_Figure_59_-_Challenge_8_Change_benders_password_to_slurmCl4ssic.png)

Step 1 Login as bender using a sql injection

Figure 65 - Logged In as Bender

![Figure 65 - Logged In as Bender](week7-owasp-juice-shop/035_Figure_60_-_Logged_In_as_Bender.png)

Step 2: Attempt to change password so you can get the http history in burp suite

Figure 66 - Random Password Entered

![Figure 66 - Random Password Entered](week7-owasp-juice-shop/036_Figure_61_-_Random_Password_Entered.png)

Figure 67 - Login Attempt Caught

![Figure 67 - Login Attempt Caught](week7-owasp-juice-shop/037_Figure_62_-_Login_Attempt_Caught.png)

Step 3: copy the request into the repeater so it can be used again.

Figure 68 - Login attempt is in the Repeater

![Figure 68 - Login attempt is in the Repeater](week7-owasp-juice-shop/038_Figure_63_-_Login_attempt_is_in_the_Repeater.png)

Step 4: remove the field that says “current” which contains the password you entered and send the request

Figure 69 - "Current" Field has been removed

![Figure 69 - "Current" Field has been removed](week7-owasp-juice-shop/039_Figure_64_-_Current_Field_has_been_removed.png)

Proof of completion

Figure 70 - Challenge Completed

![Figure 70 - Challenge Completed](week7-owasp-juice-shop/040_Figure_65_-_Challenge_Completed.png)

Proof password Changed

Figure 71 - Save Password Box shows Updated Password

![Figure 71 - Save Password Box shows Updated Password](week7-owasp-juice-shop/041_Figure_66_-_Save_Password_Box_shows_Updated_Password.png)

Challenge 8 CIA Triad Impact

| Confidentiality - Breached | Integrity – Breached | Availability - Indirect |
| --- | --- | --- |
| Attacker has Permanent access to account until user notices and changes password | Attacker can make purchases and impersonate the user. | Attacker owner is completely locked out and they must contact support to recover their password |

Challenge 9:

Figure 72 – Challenge 9: DOM XSS

![Figure 72 – Challenge 9: DOM XSS](week7-owasp-juice-shop/042_Figure_67_-_Challenge_9_DOM_XSS.png)

Step 1: Copy the “iframe” code

Figure 73 - Iframe Code Copied

![Figure 73 - Iframe Code Copied](week7-owasp-juice-shop/043_Figure_68_-_Iframe_Code_Copied.png)

Step 2: Paste the code into the search bar and then press enter

Figure 74 - Iframe Code Pasted in Search Bar

![Figure 74 - Iframe Code Pasted in Search Bar](week7-owasp-juice-shop/044_Figure_69_-_Iframe_Code_Pasted_in_Search_Bar.png)

Step 3: After you press enter a box saying xss should come up. This tells you the attack was successful

Figure 75 - XSS Attack Output

![Figure 75 - XSS Attack Output](week7-owasp-juice-shop/045_Figure_70_-_XSS_Attack_Output.png)

Notice how the search result is a large empty box

Figure 118 - Empty search result box shown after submitting the payload

![Figure 118 - Empty search result box shown after submitting the payload](week7-owasp-juice-shop/046_Figure_118_-_Empty_search_result_box_shown_after_submitting_the_payload.png)

Proof of completion

Figure 76 - Challenge Completed

![Figure 76 - Challenge Completed](week7-owasp-juice-shop/047_Figure_71_-_Challenge_Completed.png)

Challenge 9 CIA Triad Impact

| Confidentiality - Breached | Integrity – Breached | Availability - Risk |
| --- | --- | --- |
| A real XSS Payload could steal victims session cookie and hijack the account. | Attacker gains the ability to modify content and submit forms. | Could execute denial of service payloads or lure users away from the site |

Challenge 10:

Figure 77 - Challenge 10: Steal User Credentials

![Figure 77 - Challenge 10: Steal User Credentials](week7-owasp-juice-shop/048_Figure_72_-_Challenge_10_Steal_User_Credentials.png)

Step 1: In the search bar, do a union select of the user’s table. The page should give information saying that we don’t have the right number of columns

Figure 78- Union Select SQL Injection

![Figure 78- Union Select SQL Injection](week7-owasp-juice-shop/049_Figure_73-_Union_Select_SQL_Injection.png)

Figure 79- Page Showing the number of columns is incoreect

![Figure 79- Page Showing the number of columns is incoreect](week7-owasp-juice-shop/050_Figure_74-_Page_Showing_the_number_of_columns_is_incoreect.png)

Step 2: Find the correct number of columns by increasing the number of columns you are searching for

Figure 80- Selecting 1 column

![Figure 80- Selecting 1 column](week7-owasp-juice-shop/051_Figure_75-_Selecting_1_column.png)

Figure 81- Error Message Changed

![Figure 81- Error Message Changed](week7-owasp-juice-shop/052_Figure_76-_Error_Message_Changed.png)

Step 3: Once you find the right number of columns, a page page containing all the details of a user should appear.

Figure 82- Selecting 9 Columns is the correct amount of Columns

![Figure 82- Selecting 9 Columns is the correct amount of Columns](week7-owasp-juice-shop/053_Figure_77-_Selecting_9_Columns_is_the_correct_amount_of_Columns.png)

Figure 83 - Page showing user information

![Figure 83 - Page showing user information](week7-owasp-juice-shop/054_Figure_78_-_Page_showing_user_information.png)

Step 4: type a SQL query in the URL that targets id,password and email. This will return a list of user id’s, their emails and passwords

Figure 84- SQL Injection Targeting Email, ID and Password

![Figure 84- SQL Injection Targeting Email, ID and Password](week7-owasp-juice-shop/055_Figure_79-_SQL_Injection_Targeting_Email_ID_and_Password.png)

Figure 85 - Output of the SQL injection

![Figure 85 - Output of the SQL injection](week7-owasp-juice-shop/056_Figure_80_-_Output_of_the_SQL_injection.png)

Proof of completion

Figure 86 - Challenge Completed

![Figure 86 - Challenge Completed](week7-owasp-juice-shop/057_Figure_81_-_Challenge_Completed.png)

Challenge 10 CIA Triad Impact

| Confidentiality - Breached | Integrity – At Risk | Availability – High Risk |
| --- | --- | --- |
| Every users email and password is extracted | High risk of taking over accounts and purchases could be modified. | Forces juice shop to reset all passwords. |

List of all completed challenges

Figure 87 – Completed Challenges

![Figure 87 – Completed Challenges](week7-owasp-juice-shop/058_Figure_82_-_Completed_Challenges.png)

Reflection

Although Juice shop is not an effective tool in protecting user data, it is an effective tool for providing practical exercises on exploiting multiple types of vulnerabilities and teaches how to identify them.  The Most difficult part of the lab was stealing user credentials (Challenge 10) because it required iterative column counts before the final query could be created. The SQL error messages were helpful as the information disclosure provided clues on what the problem was and how to solve it. This demonstrated that information disclosure and SQL Injections are not disconnected but connected problems that increase the severity of each other. BurpSuites repeater was used in some of the challenges and taught how to modify a sent request and observer the servers response without the browser re-validating input forms which mirrors how professional penetration testers operate.

Strengths and Weaknesses

The gamified scoreboard shows instant confirmation when a challenge is completed, and each challenge is categorized based on not just the difficulty rating but the type of vulnerability that is being exploited which allows skills to be built progressively. Juice Shop is very exaggerated in its security design due real world applications not having simultaneous vulnerabilities without being discovered previously.
