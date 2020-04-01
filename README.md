# Medical Appointment No-Shows
![Appointment Banner](http://collierycourt.gp.necsu.info/wp-content/uploads/sites/89/2011/02/doctor-appointment-940x198.png)

# Problem Setting
A medical centre offers various services that require customers to book appointments in advance – including medical appointments, small surgery, blood test... 
Most customers attend their appointments on time, but nonetheless about 20% of the patient fail theirs appointments. A no-show is costly to the medical centre as it blocks diary slots for patients that otherwise may attend – and it also implies that the patient that no-shows misses out on an opportunity to look after their health. The medical centre wants to reduce the impact of no-shows by calling or texting in advance patients that are likely to no-show to remind them of the appointment or offer to reschedule.

### Task
As part of the medical centre new initiative, we want to predict whether patients will attend their appointments or not.

# Data
The dataset is available on Kaggle: [medical-appointment](https://www.kaggle.com/joniarroba/noshowappointments)

The dataframe is composed of 110.527 medical appointments and 14 features

For more information on the scholarship, please refer to this [Wikipedia page](https://en.wikipedia.org/wiki/Bolsa_Fam%C3%ADlia)

### Data Dictionary 

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
