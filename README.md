# Border_cross_analysis_dataengineer
@ By Di(Cindy) Xin 02/16/2020
## Dat Challenge Problem:(https://github.com/InsightDataScience/border-crossing-analysis)
The Bureau of Transportation Statistics regularly makes available data on the number of vehicles, 
equipment, passengers and pedestrians crossing into the United States by land.
For this challenge, we want to you to calculate the total number of times vehicles, equipment, 
passengers and pedestrians cross the U.S.-Canadian and U.S.-Mexican borders each month. We also 
want to know the running monthly average of total number of crossings for that type of crossing 
and border.
## Input Dataset
For this challenge, you will be given an input file, Border_Crossing_Entry_Data.csv, that will
reside in the top-most input directory of your repository.
    -Border: Designates what border was crossed
    -Date: Timestamp indicating month and year of crossing
    -Measure: Indicates means, or type, of crossing being measured (e.g., vehicle, equipment, 
              passenger or pedestrian)
    -Value: Number of crossings
## Expected Output:
Using the input file, you must write a program to
Sum the total number of crossings (Value) of each type of vehicle or equipment, or passengers 
or pedestrians, that crossed the border that month, regardless of what port was used.
Calculate the running monthly average of total crossings, rounded to the nearest whole number, 
for that combination of Border and Measure, or means of crossing.   
## Libary & Dependencies 
import csv, sys
from datetime import datetime as dt
import collections
## Solutions:
### Read the input *.csv: read_border()
We created the list of cross borders by reading the csv file and we used the nametuple to transfer the list into tuple, in the tuple we have all the elements ('BorderCross', 'Port_Name, State, Port_Code, Border, Date, Measure, Value, Location')
### Merge the data with the same Border, Measure, Date and count the total value by measures
1. created the list(border_date) which contains the unique combination of Boarder, measure and Date, and iterate each row. For the value which means the count of the crossings, we accumulate it when the same combination accured. And put it in the report.
2. Create the dictionary(border_measure) set the combination of border and meausure as the key and set the date and counts of the crossing as the value. 
We are going to use this to calculate the average number of crossing for a month, thus, this dictionary is the preparation for the avg calculations.
### Sort the report by Date, Value, Measure, and Border by using lambda function as its required in the question 
### Calculate the Average Crossing Numbers Monthly
Based on the second point (dictionary) I mentioned above, we iterate the report,( border_measure)is a dictionary with its keys storing unique string of border and measure. (date , Value ) is the tuple and its the value in here.So we can get all the previous date compared to the current date. So we can extract all the previous months. By looking at the total number of the crossing in the previous month, 
we divied by the length of the month in order to get the average of the total number of crossing.
And the report look like below 
Report(Border='US-Mexico Border', Date=datetime.datetime(2019, 3, 1, 0, 0), Measure='Pedestrians', Value=346158, Average=114486.0),
Report(Border='US-Canada Border', Date=datetime.datetime(2019, 3, 1, 0, 0), Measure='Truck Containers Full', Value=6483, Average=0),
Report(Border='US-Canada Border', Date=datetime.datetime(2019, 3, 1, 0, 0), Measure='Trains', Value=19, Average=0)
### Created a Module to write the report by defining the write Function and implement all the resourses.
## TESTING 
Here are two ways that you can test your code:
1. Firstly, By using Command Line:
The advatage of writing the code in this way is no matter what type of file does the input data looks like, we still can excute this code
In this case, because we are using csv. File --- so we do : Then you will get excatly the same results as the report 
python border_analytics.py       
Border_Crossing_Entry_Data.csv Report.csv
2. Secondly: By putting InputFile in the code :
When you remove the notation, you can get the report like what i showed in the code 
input_file ='Border_Crossing_Entry_Data.csv'

# End :)
