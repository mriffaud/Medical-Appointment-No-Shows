# Medical Appointment No-Shows
![Appointment Banner](https://www.sumoscheduler.com/wp-content/uploads/2014/06/no_show.jpg)

A medical centre offers various services that require customers to book appointments in advance – including medical appointments, small surgery, blood test... 
Most customers attend their appointments on time, but nonetheless about 20% of the patient fail theirs appointments. A no-show is costly to the medical centre as it blocks diary slots for patients that otherwise may attend – and it also implies that the patient that no-shows misses out on an opportunity to look after their health. The medical centre wants to reduce the impact of no-shows by calling or texting in advance patients that are likely to no-show to remind them of the appointment or offer to reschedule.

---
## Table of Content
1. [ Data ](#data)
2. [ Basic Data Information ](#Information)
3. [ Data Cleansing ](#Cleansing)
4. [ Exploratory Data Analysis ](#Analysis)
5. [ Creating a Model for Appointments No Show ](#model)

---
<a name="data"></a>
## 1. Data
The dataset is available on Kaggle: [medical-appointment](https://www.kaggle.com/joniarroba/noshowappointments)

The dataframe is composed of 110,527 medical appointments and 14 features

For more information on the scholarship, please refer to this [Wikipedia page](https://en.wikipedia.org/wiki/Bolsa_Fam%C3%ADlia)

#### Data Dictionary 

* PatientId: patient unique ID
* AppointmentID: appointment unique ID
* Gender: Male or Female
* ScheduledDay: the day someone called or registered the appointment, this is before appointment of course
* AppointmentDay: the day of the actual appointment, when they have to visit the doctor
* Age: How old is the patient
* Neighbourhood: where the appointment takes place
* Scholarship: True of False
* Hipertension: True or False
* Diabetes: True or False
* Alcoholism: True or False
* Handcap: True or False
* SMS_received: True or False
* No-show : True or False

---
<a name="Information"></a>
## 2. Basic Data Information

This section will provide basic informtion about the data.

![describe](https://github.com/mriffaud/Medical-Appointment-No-Shows/blob/master/image/describe.png)

In the table above, the first number, the count, shows how many rows have non-missing values. In this instance, we have no missing values.

The second value is the mean, which is the average. Patients in df are on average 37 years old. Under that, std is the standard deviation, which measures how numerically spread out the values are, in other word it tell how close to the mean the datpoints are.

The column Age has a minimum age of -1 which is erronous data, likewise,the maximum age is 115 years old which seems very high as Brazil's life expectancy for 2020 is 77 years old (please see [here](https://www.worldometers.info/demographics/brazil-demographics/#median-age)). We will deal with these errors in next section.

The column Handcap should be binary (True or False) but it has a max value of 4. This will need to be investigated,

---
<a name="Cleansing"></a>
## 3. Data Cleansing

In this section, we want to amend some columns in df, such as the data type, misspellings and erronous data:
* PatientId is currently a float, it will be converted it into an integer
* ScheduledDay and AppointmentDay are currently objects, it will be converted them into datetime
* AppointmentDay's time will be dropped (as it is set as 00:00:00)
* Misspelled columns are going to be renamed
* Erronous data from the Age column will be deleted

![Patients distribution by Age](https://github.com/mriffaud/Medical-Appointment-No-Shows/blob/master/image/Patients%20distribution%20by%20Age.png)

Also, looking at the distribution of the Age feature, most the patients are between 18 and 55 years old. The patients who are 115 years old are outliars, we will therefore drop these rows as well as the row of the patients aged -1.

---
<a name="Analysis"></a>
## 4. Exploratory Data Analysis

### Overview of No-Show

![PatientId](https://github.com/mriffaud/Medical-Appointment-No-Shows/blob/master/image/PatientId.png)

Missed appointmemts account for 20% of the total appointments in the dataset.

### Finding Duplicates

![Duplicated](https://github.com/mriffaud/Medical-Appointment-No-Shows/blob/master/image/Duplicated.png)

The dataset does not have duplicated appointments but has 48,228 patients that can be considered as returning/known patients.

### Age

![Percentage of Appointments Show/No Show by Age](https://github.com/mriffaud/Medical-Appointment-No-Shows/blob/master/image/Percentage%20of%20Appointments%20Show:No%20Show%20by%20Age.png)

The patients that seems most likely to not show-up for their appointments are between 10 and 35 years old.

### Gender

![Percentage of Appointments Show/No Show by Gender](https://github.com/mriffaud/Medical-Appointment-No-Shows/blob/master/image/Percentage%20of%20Appointments%20Show:No%20Show%20by%20Gender.png)

From the table above, we can clearly see that 'Female' patients usually have more appointments that 'Male' patients, they also have about the double number of missed appointment. However, looking at the percentage of missed appointments by gender shows that it is almost the same rate (about 20%). Therefore, gender does not seem to be an important feature.

### Scheduled Day

#### Looking at the time of the booking

![Patients distribution by Time of the Booking](https://github.com/mriffaud/Medical-Appointment-No-Shows/blob/master/image/Patients%20distribution%20by%20Time%20of%20the%20Booking.png)

The booking are made between 6am and 8pm. There are three bookings that have been taken at 9pm, although these are showed as outliars on the plot above, they will not be dropped as they could be the results of emergencies.

![Percentage of Appointment Show/No Show by Booking Time of the Day](https://github.com/mriffaud/Medical-Appointment-No-Shows/blob/master/image/Percentage%20of%20Appointment%20Show:No%20Show%20by%20Booking%20Time%20of%20the%20Day.png)

Morning bookings seem less likely to be missed than afternoon and evening ones.

#### Looking at the day of booking

![Appointment Show/No Show by Booking Day of the Week](https://github.com/mriffaud/Medical-Appointment-No-Shows/blob/master/image/Appointment%20Show:No%20Show%20by%20Booking%20Day%20of%20the%20Week.png)

![Percentage of Appointment Show/No Show by Booking Day of the Week](https://github.com/mriffaud/Medical-Appointment-No-Shows/blob/master/image/Percentage%20of%20Appointment%20Show:No%20Show%20by%20Booking%20Day%20of%20the%20Week.png)

Most of the bookings are at the beginning of the week, this may be explained because the medical centre seems not to be open over the weekends. Althoug Saturdays have the smallest no show rate, they also represents a too small proportion of the data to be significant. Overall, the days of the week do not seem to be an important feature.

### Appointment Date

![Appointment Show/No Show by Appointment Day of the Week](https://github.com/mriffaud/Medical-Appointment-No-Shows/blob/master/image/Appointment%20Show:No%20Show%20by%20Appointment%20Day%20of%20the%20Week.png)

![Percentage of Appointment Show/No Show by Appointment Day of the Week](https://github.com/mriffaud/Medical-Appointment-No-Shows/blob/master/image/Percentage%20of%20Appointment%20Show:No%20Show%20by%20Appointment%20Day%20of%20the%20Week.png)

The first graph follows the same patterns as section 5.6 "Appointment Show/No Show by Booking Day of the Week" graph. This may be because patient book and have their their appointment on the same day. The percentage of show vs no show dis roughly the same accross the week.

### Waiting Time Between Booking and Medical Appointment

![Patients distribution by Waiting Time](https://github.com/mriffaud/Medical-Appointment-No-Shows/blob/master/image/Patients%20distribution%20by%20Waiting%20Time.png)

Most of the appointments are taken a month in advance. The graph above, highlights erroneous data and outliars. The negative data will be transformed into 'unknown' wating time category while the outliars will be kept as some medical appointment can take up to six months (like small surgeries).

![Percentage of Appointment Show/No Show by Time Between Booking and Appointment](https://github.com/mriffaud/Medical-Appointment-No-Shows/blob/master/image/Percentage%20of%20Appointment%20Show:No%20Show%20by%20Time%20Between%20Booking%20and%20Appointment.png)

The graph above suggests that the longer the waiting time is between booking and the appointmnet the more likely the appointment is to be missed. This feature seems to be an important one as it shows a clear distinction for patients show/ no show depending on the number of days ahead of the appontment patients have booked.

### Neighbourhood

![Appointment Show/No Show by Neighbourhoods](https://github.com/mriffaud/Medical-Appointment-No-Shows/blob/master/image/Appointment%20Show:No%20Show%20by%20Neighbourhoods.png)

![Percentage of Appointment Show/No Show by Neighbourhoods](https://github.com/mriffaud/Medical-Appointment-No-Shows/blob/master/image/Percentage%20of%20Appointment%20Show:No%20Show%20by%20Neighbourhoods.png)

Most of the neighbourhouds have a no show rate of about 20%, the significant drops and peaks are because of the porr representation of a particalar neigbourhood in the dataset rather than because it is significant. Therefre, this feature does not seem to be important for the no show prediction.

### Scholarship

![Appointment Show/No Show by Scholarship](https://github.com/mriffaud/Medical-Appointment-No-Shows/blob/master/image/Appointment%20Show:No%20Show%20by%20Scholarship.png)

![Percentage of Appointment Show/No Show by Scholarship](https://github.com/mriffaud/Medical-Appointment-No-Shows/blob/master/image/Percentage%20of%20Appointment%20Show:No%20Show%20by%20Scholarship.png)

The graphs above shows that 80% of the patients that do not have a scholarship attended their appointent while 75% of the patient with a scholarship attended. This feature could be helpful in dertermining the no show.

### Hypertension

![Appointment Show/No Show by Hypertension](https://github.com/mriffaud/Medical-Appointment-No-Shows/blob/master/image/Appointment%20Show:No%20Show%20by%20Diabetes.png)

![Percentage of Appointment Show/No Show by Hypertension](https://github.com/mriffaud/Medical-Appointment-No-Shows/blob/master/image/Percentage%20of%20Appointment%20Show:No%20Show%20by%20Diabetes.png)

The patients suffering from hypertension tend to attend their appointment more often than those who do not have this condition. However, appointment with hypertension patients represent a small pool in our dataset, just under 20% of the total appointments. This feature could be helpful in dertermining the no show.

### Diabetes

![Appointment Show/No Show by Diabetes](https://github.com/mriffaud/Medical-Appointment-No-Shows/blob/master/image/Appointment%20Show:No%20Show%20by%20Diabetes.png)

![Percentage of Appointment Show/No Show by Diabetes](https://github.com/mriffaud/Medical-Appointment-No-Shows/blob/master/image/Percentage%20of%20Appointment%20Show:No%20Show%20by%20Diabetes.png)

The patients suffering from Diabetes tend to attend their appointment more often than those who do not have this condition. This feature may not be helpful in dertermining the no show.

### Alcoholism

![Appointment Show/No Show by Alcoholism](https://github.com/mriffaud/Medical-Appointment-No-Shows/blob/master/image/Appointment%20Show:No%20Show%20by%20Alcoholism.png)

Patients who suffer from alcoholism represent only 3% of all the appointments.

![Percentage of Appointment Show/No Show by Alcoholism](https://github.com/mriffaud/Medical-Appointment-No-Shows/blob/master/image/Percentage%20of%20Appointment%20Show:No%20Show%20by%20Alcoholism.png)

Looking at the graph above, there does not seem to be a difference between the patient suffering from alcoholism and the rest of the dataset. This feature may not be helpful in dertermining the no show.

### Handicap

![Appointment Show/No Show by Handicap](https://github.com/mriffaud/Medical-Appointment-No-Shows/blob/master/image/Appointment%20Show:No%20Show%20by%20Handicap.png)

Patients suffering from a handicap represent 2% of the total appointments.

![Percentage of Appointment Show/No Show by Handicap](https://github.com/mriffaud/Medical-Appointment-No-Shows/blob/master/image/Percentage%20of%20Appointment%20Show:No%20Show%20by%20Handicap.png)

Looking at the graph above, there does not seem to be a difference between the patient suffering from handicap and the rest of the dataset. This feature may not be helpful in dertermining the no show.

### SMS Received

![Appointment Show/No Show by SMS Received](https://github.com/mriffaud/Medical-Appointment-No-Shows/blob/master/image/Appointment%20Show:No%20Show%20by%20SMS%20Received.png)

![Percentage of Appointment Show/No Show by SMS Received](https://github.com/mriffaud/Medical-Appointment-No-Shows/blob/master/image/Percentage%20of%20Appointment%20Show:No%20Show%20by%20SMS%20Received.png)

The graphs above do not show expected results: 38% appointments for patients that received the sms were missed while 20% of the appointments for patients that did not received a sms. This feature seem to be important in dertermining appointments no show.

---
<a name="model"></a>
## 5. Creating a Model for Appointments No Show

We are using the gradient boosting classifier to predict which customers are going to miss their appointment but first, we created a for loop to test different n-estimators with loss set as ‘deviance’ refering to logistic regression for classification.

![ac_dev_gbc](https://github.com/mriffaud/Medical-Appointment-No-Shows/blob/master/image/ac_dev_gbc.png)

![ac_dev_gbc_plot](https://github.com/mriffaud/Medical-Appointment-No-Shows/blob/master/image/ac_dev_gbc_plot.png)

The best score occurs at n_estimators = 1200, therefore we are choosing it as our parameter.

### Final Model

Once, we identified the optimal n_estimators, we can fit the final model using it.

![Accuracy](https://github.com/mriffaud/Medical-Appointment-No-Shows/blob/master/image/Accuracy.png)

THe model has 80% accuracy.
