#Installation du MQTT broker pour la communication arduino --> Raspberry

1. Installation du MQTT broker sur la raspberry
	sudo apt-get install mosquitto
	
2. Open the config file of MQTT 
	$ sudo nano /etc/mosquitto/mosquitto.conf
	
	We want to use the default settings, to prevent the use of the MQTT by unknonw users, to set it up on port 1883, and to save the passwords on a separate file
	for this, coment the line "include_dir etc/mosquitto/conf.d"
	add : 	
		allow_anonymous false
		password_file /etc/mosquitto/pwfile
		listener 1883
	
	ctrl + x then y to save and close
	
3. set up the MQTT password and username
	$ sudo mosquitto_passwd -c /etc/mosquitto/pwfile "username"
And enter your password

(You can use the -d option to remove a user)

4. Usefull command for the MQTT broker
	$ sudo systemctl status mosquitto   //show the MQTT status
	$ sudo systemctl start mosquitto
	$ sudo systemctl stop mosquitto
	$ sudo systemctl restart mosquitto
	$ sudo systemctl enable mosquitto  //start MQTT at boot
	$ sudo mosquitto //start mosquitto
	
#Publisher setup Arduino

1. Make sure that the wifi emitter is connected
2. load the file arduino_part.ino
3. Check if the library for the sensors are the right ones, if not add them
4. Add in the void loop the code for the sensors
4. Upload the file on the arduino

# Suscriber setup Raspberry

1. sudo pip install paho-mqtt

2. sudo nano get_MQTT_data.py // create a python script to receive the data	
Here we use the file raspberry_part.py

3. $ python raspberry_part.py  //run the script

The taspberry should be receiving datas.
If not check the MQTT ans wifi settings.
