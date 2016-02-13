CUR_PATH = $(shell echo $(PWD))
OBJS = $(addprefix objs/,ykushWinCmd.o commandParser.o usbcom.o)
LIBS = -lhidapi-libusb -lusb-1.0 -ludev
LOADPATHS = -L$(CUR_PATH)/linux
PREPROCESSOR_DEFS = -DLINUX
CPP = g++

ykush : $(OBJS)
	$(CPP) $(LOADPATHS) -o ../bin/ykush $(OBJS) $(LIBS)


objs/ykushWinCmd.o : ykushWinCmd.cpp stdafx.h commandParser.h
	$(CPP) $(PREPROCESSOR_DEFS) -c ykushWinCmd.cpp -o objs/ykushWinCmd.o

objs/commandParser.o : commandParser.cpp stdafx.h commandParser.h usbcom.h 
	$(CPP) $(PREPROCESSOR_DEFS) -c commandParser.cpp -o objs/commandParser.o

objs/usbcom.o : usbcom.cpp stdafx.h linux/hidapi.h usbcom.h
	$(CPP) $(PREPROCESSOR_DEFS) -c usbcom.cpp -o objs/usbcom.o

clean :
	rm ../bin/ykush $(OBJS)

