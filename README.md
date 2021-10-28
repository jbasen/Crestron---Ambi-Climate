# Crestron---Ambi-Climate

This module provides control of a Ambi Climate from a Crestron 3-Series or 
4-Series Processor.  No true feedback is available.  The outputs are simply
manufactured feedback based on the actions on the inputs to the module. If
the Ambi Climate app is used for control the outputs will become out of synch
with the status of the Ambi Climate

NOTE - THE AMBI CLIMATE API REQUIRES OAUTH AUTHENTICATION.  INITIAL ACCESS
AND REFRESH TOKENS ARE OBTAINED FROM THE AMBI CLIMATE API WEB SITE HERE:
https://api.ambiclimate.com/doc/quickstart.  THE ACCESS TOKEN HAS A LIFESPAN
OF 40 HOURS AND MUST BE REFRESHED USING THE REFRESH TOKEN. THIS CRESTRON
MODULE DOESN'T DETECT AN EXPIRED TOKEN BUT SIMPLY RFRESHES THE TOKEN EVERY
24 HOURS OR ANYTIME THE MODULE IS RESTARTED.  FOR THIS REASON IT IS ADVISABLE
TO OBTAIN YOUR TOKEN RIGHT BEFORE THE MODULE IS FIRST LOADED TO A PROCESSOR

NOTE - THE AMBI CLIMATE API IS LIMITED TO 20 CALLS IN A 10 MINUTE PERIOD.
BECAUSE OF THE RATE LIMIT BE VERY CAREFUL OF POLLING THE SENSOR TEMPERATURE
AND HUMDITY TOO OFTEN.  ALSO, ANALOG INPUTS SHOULDN'T BE DRIVEN BY ANY SYMBOL
THAT USES +/- DIGITAL INPUTS TO SEND A VALUE. INSTEAD THE USER SHOULD BE GIVEN
A SELECTION OF DIFFERENT VALUES TO CHOOSE FROM SO A MINIMUM OF CALLS ARE MADE
TO THE API.

NOTE - THE Diplay_Appliance_State INPUT IS ONLY PROVIDED FOR TESTING.  NONE OF 
THE AMBI CLIMATE API CALLS RETURN FEEDBACK INFORMTATON.  THE Diplay_Appliance_State
CALL INITIATES AN APPLIANCE STATE API CALL AND THE INFORMATION RETURNED BY THIS 
CALL COULD BE PARSED (IT IS DISPLAYED WHEN DEBUG OUTPUT IS SET TO CONSOLE).  
HOWEVER, REQUESTING APPLIANCE STATE INFORMATION AFTER EVERY API CALL WOULD HALVE 
THE NUMBER OF CALLS BEFORE THE RATE LIMIT IS EXCEEDED SO IT ISN'T PARSED OR 
PROVIDED AS MODULE FEEDBACK

Inputs
Initialize                   - Must be pulsed to initilize communications
                               device or the app.
Diplay_Appliance_State       - Displays appliance state info based on Debug_Msg_Output
Get_Sensor_Temperature       - Retrieves the Ambi Climates internal temperature sensor
                               value
Get_Sensor_Humidity          - Retrieves the Ambi Climates internal humidity sensor
                               value
Device_Off                   - Pulse to turn the device controlled by the Sensibo Air
                               off
Comfort_Mode                 - Enables comfort mode
Comfort_Feedback_Too_Hot     - Provides feedback in comfort mode that the room is too
                               hot
Comfort_Feedback_Too_Warm    - Provides feedback in comfort mode that the room is too
                               warm
Comfort_Feedback_Bit_Warm    - Provides feedback in comfort mode that the room is a
                               bit warm
Comfort_Feedback_Comfortable - Provides feedback in comfort mode that the room is 
                               comfortable
Comfort_Feedback_Bit_Cold    - Provides feedback in comfort mode that the room is a
                               bit too cold
Comfort_Feedback_Too_Cold    - Provides feedback in comfort mode that the room is too
                               cold
Comfort_Feedback_Freezing    - Provides feedback in comfort mode that the room is 
                               freezing
Temrature_Model              - Sets the Ambi Climate to Temperature Mode at the specified
                               temprature value
Away_Temperature_Lower       - Sets the Ambi Climate to Away Mode with a low temperture
                               limit 
Away_Temperature_Upper       - Sets the Ambi Climate to Away Mode with a high temperature
                               limit
Away_Humidity_Upper          - Sets the Ambi Climate to Away Mode with a high humidity
                               limit

Outputs
Device_Off_FB                - High if Device_Off input pulsed
Comfort_Mode_FB              - High if Comfort_Mode input is pulsed
Temperature_Mode_FB          - High if Temperature_Mode input is set
Away_Mode_FB                 - High if one of the Away inputs is set
Sensor_Temperature           - Sensor value after Get_Sensor_Temperature is pulsed
Sensor_Humidity              - Sensor value after Get_Sensor_Humidity is pulsed

Parameters
Access_Token                 - OAuth access token obtained from https://api.ambiclimate.com/doc/quickstart
Refresh_Token                - OAuth refresh token obtained from https://api.ambiclimate.com/doc/quickstart
Client_Secret                - Client Secret ID obtained from https://api.ambiclimate.com/doc/quickstart
Location_Name                - Locaion where Ambi Climate is located. Must match app
Room_Name                    - Room where Ambi Climate is located.  Must match app
Debug_Msg_Output             - Where to send debug messages
                               0=None, 1=Console, 2=Error Log, 3=Both 
