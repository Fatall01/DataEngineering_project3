# DataEngineering_project3
How did I go from investigating microbial life in oil pipelines to creating my own data engineering pipeline?

As a microbiologist, I used to work alone in my molecular lab, extracting DNA from different microorganisms from oil pipelines and making stories out of it. However, over the years I ended up producing a massive amount of data. I didn't know how to deal with them. Thus, I enrolled in a data science Bootcamp with WBS Coding School in order to efficiently analyze my data.
After spending 7 weeks exploring SQL and Python, diving into dataFrames, and playing with Pandas, I was assigned with the challenging task to help Gans predict their e-scooter movement.

Wait, but who is Gans?
According to my data science instructor, Gans is a startup developing an e-scooter-sharing system, which aspires to operate in the most populous cities all around the world. In each city, there will be hundreds of e-scooters parked in the streets and allows users to rent them by the minute.
What Gans specifically want is to anticipate as much as possible scooter movements. Predictive modeling is certainly on the roadmap, but the first step is to collect more data.
Since data is needed every day, in real-time and accessible by everyone in the company, the challenge is going to be collecting different external data and creating an automated pipeline in the cloud. Here are the steps I followed in order to reach their goal:

-	Collect data from external sources
-	Store the data in a local database (MySQL)
-	Move the database to the cloud (AWS)
-	Automate all the above-mentioned steps
 
1.	Data collection:
 collecting data is the first step of my data engineering plan. To do that, the internet is a great source for all required data and here is my data collection approach:
- Collect flights data, RapidAPI (AeroDataBox’s endpoints) were used to access and collect data about flight arrivals to airports with their ICAO codes.
- API calls to collect free weather data from OpenWeather. Here I used Pyowm library, which is Python wrapper to write requests to the API.
- Web scraping population data of cities where Gans was active. I used python and Beautiful Soup, which enabled me to download and extract the entire HTML codes from the cities of interest and then find the data.
 
2.	Data storage in a local database (MySQL):
 SQLAlchemy (the simplest way) to connect Python to any SQL was used here. After installing it with pip install SQLAlchemy and importing it into the notebook, then define the details to connect to your database. Finally, the method pandas.DataFrame.to_sql() will do the rest by converting a DataFrame into a MySQL table in a single step.

3.	Move pipeline to the cloud (AWS):
 Amazon Web Services (AWS) is a subsidiary of Amazon providing on-demand cloud computing platforms and APIs. These cloud computing web services provide a variety of basic abstract technical infrastructure and distributed computing building blocks and tools such as the RDS, Lambda...
To fill my cloud database with my gathered data I used IAM, RDS and Lambda services from AWS.
Amazon RDS is a managed relational database service that provides you with several familiar database engines to choose from, including MySQL. So basically, I created a database in AWS’s cloud that was able to connect MySQL Workbench through the Lambda function. To give the lambda functions access to the RDS service, I first needed to create a new Role in the AWS Identity and Access Management (IAM).

4.	Automating all the above-mentioned steps:
 the goal here is to schedule a Lambda function that collects data about tomorrow’s weather and flight arrivals on a daily basis. Now that the Lambda function is already created, I just used the AWS’s EventBridge to easily create event triggers that automate the Lamdba functions using Cron expressions.
