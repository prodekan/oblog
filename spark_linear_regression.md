

# Problem statement

   This problem statement is from the Udemy course on pyspark.
   You've been contracted by Hyundai Heavy Industries to help them build a predictive model for some ships. 
Hyundai Heavy Industries is one of the world's largest ship manufacturing companies and builds cruise liners.
You've been flown to their headquarters in Ulsan, South Korea to help them give accurate estimates of how many crew members a ship will require.
They are currently building new ships for some customers and want you to create a model and use it to predict how many crew members the ships will need.
Here is what the data looks like so far:
    Description: Measurements of ship size, capacity, crew, and age for 158 cruise
    ships.

    Variables/Columns
    Ship Name     1-20
    Cruise Line   21-40
    Age (as of 2013)   46-48
    Tonnage (1000s of tons)   50-56
    passengers (100s)   58-64
    Length (100s of feet)  66-72
    Cabins  (100s)   74-80
    Passenger Density   82-88
    Crew  (100s)   90-96

It is saved in a csv file for you called `cruise_ship_info.csv`. Your job is to **create a regression model** that will help predict **how many crew members will be needed for future ships**. 
The client also mentioned that they have found that particular cruise lines will differ in acceptable crew counts, so it is most likely an important feature to include in your analysis! 
Once you've created the model and tested it for a quick check on how well you can expect it to perform, make sure you take a look at why it performs so well!


# Approach for solving

The approach for solving the problem would be the following:

1.  Understand the data
    
        from pyspark.sql import SparkSession
        spark = SparkSession.builder.appName('hyundai').getOrCreate()
        df = spark.read.csv('cruise_ship_info.csv', inferSchema=True, header=True)
        df.show()
    
    Since this sentence *The client also mentioned that they have found that particular cruise lines will differ in acceptable crew counts* it makes sense to look at the cruise lines in more detail.
    
        df.select("Cruise_line").distinct().show()
        +-----------------+
        |      Cruise_line|
        +-----------------+
        |            Costa|
        |              P&O|
        |           Cunard|
        |Regent_Seven_Seas|
        |              MSC|
        |         Carnival|
        |          Crystal|
        |           Orient|
        |         Princess|
        |        Silversea|
        |         Seabourn|
        | Holland_American|
        |         Windstar|
        |           Disney|
        |        Norwegian|
        |          Oceania|
        |          Azamara|
        |        Celebrity|
        |             Star|
        |  Royal_Caribbean|
        +-----------------+
    
    1.  Shape
    2.  Size
    3.  Columns
    4.  Types of colums
    5.  Range of numeric types
    6.  Redundancy
    7.  Relationship between columns
2.  Transform the data to fit the spark linear regression model creation function
3.  Split the data into a training and test set on a ration 70 to 30
4.  Create the model using the training data
5.  Fit the model with test data
6.  Evaluate all necessary metrics to see how good the model is
7.  Test on predicting new values

