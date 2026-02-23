<h1>Reference Sheet for Data (i.e Data Description)</h1>
"This dataset reflects incidents of crime in the City of Los Angeles dating back to 2020. This data is transcribed from original crime reports that are typed on paper and therefore there may be some inaccuracies within the data. <b>Some location fields with missing data are noted as (0°, 0°)</b>. Address fields are only provided to the nearest hundred block in order to maintain privacy. This data is as accurate as the data in the database. Please note questions or concerns in the comments." 

<h3>Variables</h3>

_Incident Information_ <br>
DR_NO --> Division of Records Number <br>
Date Rptd --> Date Reported <br>
DATE OCC --> Date Occured <br>
TIME OCC --> Time Occured <br>

_Location Information_ <br>
AREA --> Area ID <br>
AREA NAME --> Name for the Area associated with ID. <br>
Rpt Dist No --> Reporting District Number <br>
LOCATION --> Street address or approximate location where the crime occured <br>
Cross Street --> Cross street (if applicable) <br>
LAT --> Latitude of Crime <br>
LON --> Longitude of Crime <br>

_Crime Information_ <br>
Part1-2 --> FBI Crime Classification (Part 1 is serious/violent/property crimes; Part 2 is less serious crimes) <br>
Crm Cd --> Crime Code <br>
Crm Cd Desc --> Short descriptive of what the Crime Code is <br>
Crm Cd 1-4 --> Up to 4 crime codes associated with same incident <br>

_Victim Information_ <br>
Vict Age --> Age of victim (0 if unknown) <br>
Vict Sex --> Gender/sex of the victim <br>
Vict Descent --> Race/ethnicity of the victim <br>

_Premises/Weapon Information_ <br>
Premis Cd --> Premises Code (numeric, type of location) <br>
Premis Desc --> Premises Description (english, type of location) <br>
Weapon Used Cd --> Code for the weapon used <br>
Weapon Desc --> Description of the weapon <br>

_Case Status Information_ <br>
Status --> status code for the case, numeric <br>
Status Desc --> description of the status of the case <br>

_Method of Operation_ <br>
Mocodes --> Meethod of Operation codes, describes how a crime was committed. Typically a string of multiple codes. <br>
