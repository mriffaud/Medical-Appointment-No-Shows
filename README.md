# Medical Appointment No-Shows
![Appointment Banner](http://collierycourt.gp.necsu.info/wp-content/uploads/sites/89/2011/02/doctor-appointment-940x198.png)

# Problem Setting
A medical centre offers various services that require customers to book appointments in advance – including medical appointments, small surgery, blood test... 
Most customers attend their appointments on time, but nonetheless about 30% of the patient fail theirs appointments. A no-show is costly to the medical centre as it blocks diary slots for patients that otherwise may attend – and it also implies that the patient that no-shows misses out on an opportunity to look after their health. The medical centre wants to reduce the impact of no-shows by calling or texting in advance patients that are likely to no-show to remind them of the appointment or offer to reschedule.

### Task
As part of the medical centre new initiative, we want to predict wether patients will attend their appointments or not and provide the medical centre with a list of patients to contact.

# Data
The dataset is available on Kaggle: [medical-appointment](https://www.kaggle.com/afflores/medical-appointment)

The datframe is composed of 61K datapoints, from 2017.01.01 to 2017.04.30 and 19 features

### Data Dictionary 
* especialidad : what kind of specialist is going to. Ie dematologist, etc.
* edad: Age
* sexo: sex, 1: Male, 2: Female
* reservamesd : discrete value for the month of the appointment, 1: Jan, 2: Feb…
* reservamesc : continue value for the month of the appointment, the formula is COS(2reservamesdPi/12)
* reservadiad : day of the week for the appointment, 1: Mon… 7: Sun
* reservadiac : continous value for the day of the week, the formula is COS(2reservadiadPi/7)
* reservahorad : discrete value for hour of the appointment
* reservahorac : continous value for the hour of the appointment, the formula is COS(2reservahoradPi/24)
* creacionmesd : discrete value for the month when the appointment was created
* creacionmesc : continous value for the month when the appointment was created, the formula is COS(2creacionmesdPi/12)
* creaciondiad : same as reservadiad, but considering the day when the appointment was created
* creaciondiac : same as reservadiac, but considering the day when the appintment was created
* creacionhorad : hour when the appointment was created
* creacionhorac : continous value for the creacionhourd, the formula is COS(2creacionhoradPi/24)
* latencia : number of days between the appointment and the date when it was created
* canal : channel used for the creation of the apppointment, 1: call center, 2: Personal, 3: Web
* tipo : type of appointment, 1: medical, 2: procedures
* show : 0: no show, 1: show
