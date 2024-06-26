include .env
build: clean build-sketch compile

clean:
	rm esp32-serial-reverse-proxy.ino

build-sketch:
	@printf "#include <WiFi.h>\n\n" >> esp32-serial-reverse-proxy.ino
	@echo "#define SSID \"${SSID}\"" >> esp32-serial-reverse-proxy.ino
	@echo "#define PASSWORD \"${PASSWORD}\"" >> esp32-serial-reverse-proxy.ino
	@echo "#define TOKEN \"${TOKEN}\"" >> esp32-serial-reverse-proxy.ino
	@echo "#define HOST \"${HOST}\"" >> esp32-serial-reverse-proxy.ino
	@echo "#define PORT ${PORT}" >> esp32-serial-reverse-proxy.ino
	@cat esp32-serial-reverse-proxy-stub >> esp32-serial-reverse-proxy.ino

compile:
	arduino-cli compile

flash:
	arduino-cli upload

forward:
	stty -F /dev/ttyACM0 115200
	socat EXEC:bash /dev/ttyACM0,b115200,echo=0
	#bash < /dev/ttyACM0 > /dev/ttyACM0

install-client:
	cp esp32-serial-proxy.service /etc/systemd/system/
	systemctl enable --now esp32-serial-proxy.service

install-server:
	cp esp32-serial-reverse-proxy.service /etc/systemd/system/
	systemctl enable --now esp32-serial-reverse-proxy.service
