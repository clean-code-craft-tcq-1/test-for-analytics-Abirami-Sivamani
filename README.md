# Test for Analytics

Design tests for Analytics functionality on a Battery Monitoring System.

## Analysis-functionality to be tested

This section lists the Analysis for which _tests_ must be written.

Battery Telemetrics are collected and stored on a server.
Data for a month is stored in a [csv file](https://en.wikipedia.org/wiki/Comma-separated_values).

Analysis must be done on this csv file to find the following:
- minimum
- maximum
- count of breaches (how many times did it cross the threshold in a month?)
- record trends (date & time when the reading was continuously increasing for 30 minutes)

A PDF report of the analysis must be stored every week.
Notification must be sent when a new report is available.

## Tasks

### List Dependencies

List the dependencies of the Analysis-functionality.

1. Access to the Server containing the telemetrics in a csv file
2. Availability of valid csv file in the Server
3. CSV file should have valid readings

### Mark the System Boundary

What is included in the software unit-test? What is not? Fill this table.

| Item                      | Included?     | Reasoning / Assumption
|---------------------------|---------------|---
Battery Data-accuracy       | No            | We do not test the accuracy of data
Computation of maximum      | Yes           | This is part of the software being developed
Off-the-shelf PDF converter | Yes           | This is part of the software being developed
Counting the breaches       | Yes           | This is part of the software being developed
Detecting trends            | Yes           | This is part of the software being developed
Notification utility        | Yes           | This is part of the software being developed

### List the Test Cases

Write tests in the form of `<expected output or action>` from `<input>` / when `<event>`

Add to these tests:

1. Write minimum and maximum to the PDF from a csv containing positive and negative readings
2. Write "Invalid input" to the PDF when the csv doesn't contain expected data
3. Calculate the count of breaches (exceeds threshold limit) from a csv containing readings
4. Write count of breaches value to the PDF file, if calculated count of breaches has atleast 1 breach.
5. Write "No Breaches Found" to the PDF, if calculated count of breaches value is 0 (No breaches)
6. Find the trends (list of date & time with respective reading) which keeps on increasing for 30 minutes from csv readings data
7. Write the trends to the PDF file, if trends list has data.
8. Write "No Trends Found" to the PDF file, if trends doesn't have any data.
9. Send "New PDF Report Available" Message to the Notification Method, if new PDF report availble


### Recognize Fakes and Reality

Consider the tests for each functionality below.
In those tests, identify inputs and outputs.
Enter one part that's real and another part that's faked/mocked.

| Functionality            | Input        | Output                                              | Faked/mocked part
|--------------------------|--------------|-----------------------------------------------------|----------------------
Read input from server     | csv file     | internal data-structure                             | Fake the server store
Validate input             | csv data     | valid / invalid                                     | None - it's a pure function
Notify report availability | pdf file     | Notification of New Report Available                | Fake the notification call
Report inaccessible server | csv file     | can't access csv file                               | Fake the server store
Find minimum and maximum   | csv data     | Minimum/Maximum                                     | None - it's a pure function
Detect trend               | csv data     | Date & Time, Reading                                | None - it's a pure function
Write to PDF               | csv data     | Minimum, Maximum, Trends, Breach count              | Fake the PDF write
