# Stock-Grade-Project-by-Flask-and-Crawler
This is a Stock Grading project made up of crawler, Flask, MongoDB and Boostrap. The skills applied in this project will listed below.<br>
<br>
Crawler: request, pandas<br>
Flask: flask_login (LoginManager, current_user, login_required, login_user, logout_user), Blueprint, flash, redirect, render_template<br>
MongoDB Atlas: flask_mongoengine<br>
*****
To begin with, I aim to use the Profit matrix theory to evaluate stocks in Taiwan by grading them in A1, A2, B1, B2, C1, C2 and D.
<br><br>
![image](https://github.com/BoddyShen/Stock-Grading-Project-by-Flask-and-Crawler/blob/85e44efb85e85aa98c0621b99a5e5458a14942ae/image/stock_grade.png)<br>
Reference: [雷浩斯價值投資網](https://redhouse.statementdog.com/archives/2178#more-2178,https://statementdog.com/explain/earningMatrix.html)<br>

By using annual ROE ('股東權益報酬率') and Free Cash Flow ('營業活動之淨現金流入(出)' - '投資活動之淨現金流入(出)') as references, we can grade the stock and evalute its profitability in a certain period.

See the [demo](https://www.youtube.com/watch?v=bwfWWsZeR0M&ab_channel=BoddyShen).

# Design
![image](https://github.com/BoddyShen/Stock-Grading-Project-by-Flask-and-Crawler/blob/e766be2ab81951a03ab5ec77d2a0630d1aa175b7/image/Stock_Grading.png)

# Frontend
To present this project, we used elements in [Bootstrap](https://getbootstrap.com/docs/4.0/getting-started/introduction/) to build a simple and clean interface for users. With the help of flask-templates engine "jinja2", we can use "if-else" and "for-loop" syntax in the HTML file and have more flexibility to present different content in the same template.

# Backend
The backend of this project was built with the python's framework, flask. Flask provides many useful modules. This project used "blueprint" to build a cleaner and maintainable structure, including "core" and "users". The "core" is only for the landing page, and "users" is for other routes.<br>

In the log-in system, we use flask_login to manage our user's logging status, if users successfully log into the stock page(through password checking in MongoDB or new registration), we will use "login_user()" method to login the user's information from MongoDB. Then we can use "current_user" to present user's data in the frontend and also update and save user's data in the backend.<br>

To use flask_login, our class User  has to build four methods first (is_authenticated, is_active, is_anonymous, get_id()). Fortunately, Flask_login provides a class UserMixin with built-in these four methods, so we can easily inherit UserMixin when building our class User to meet its requirement.Besides, we need to provide a user_loader callback. This callback is used to reload the user object from the user ID stored in the session.
([Ref](https://flask-login.readthedocs.io/en/latest/))<br>

To use the mongoengine, our class User has to inherit the MongoEngine().document when declaring the User. Therefore, we have to inherit both UserMixin and MongoEngine().document at the same time. After declaring the class User,  we can easily use flask_login and mongoengine to help update our user's manipulation. Please see the design figure above.

# Crawler
Our stock's information is crawled in the Stock web ([Goodinfo](https://goodinfo.tw/tw/index.asp)). And the step-by-step crawl method was in the "crawler.ipynb". There are some tips in crawler. <br>
<br>
First, we have to check our request's url in the browser's network instend of the url on the top of the website because this url may direct to its landing page not the page we wanted.<br> 

Second, we may have to put some information when crawling a website ,such as user-agent, because some websites may refute the request without other information.

We can also use "selenium" to automatically manipulate or log into the website to the page we want, the way to crawl the stock page by "selenium" was presented in "selenium_crawler.ipynb".











