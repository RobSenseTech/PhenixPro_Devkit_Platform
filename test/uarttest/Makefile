#set your project name
PRJ_NAME = uarttest.elf

#set your project type : choose one below
CC = arm-linux-gnueabihf-gcc  	#arm-xilinx-linux-gnueabi-gcc
#CC = 
#CC = ar -r 

#set Debug or Release
Compile_Flag = Debug
#Compile_Flag = Release

#set your output path
Output:= ./

#set your source folder
SRC_PATH:= ./

#add the lib you used here
#LIBS := -lLib1 -lLib2 -lLib3
LIBS := #-lpthread 
#LIBPATH := -Lpath1 -Lpath2 -Lpath3
LIBPATH := 
INCLUDEPATH := # INCLUDEPATH := -I/usr/lib/XXX/include

###################################
#DON"T MODIFY THE BELOWS

#list all dirs
SUBDIRS := $(shell find $(SRC_PATH) -type d)
#flags in makefile
DEBUG_FLAG = -g3 -O0 -Wall -c -fmessage-length=0 -D_GNU_SOURCE #wipe off warning of asprintf
RELEASE_FLAG =   -O0 -Wall -c -fmessage-length=0 -D_GNU_SOURCE
RM := rm -rf

#set compile flag
ifeq ($(Compile_Flag),Debug)
CFLAGS := $(DEBUG_FLAG) $(INCLUDEPATH) $(LIBS)
else
CFLAGS := $(RELEASE_FLAG)
endif

#prepare files
#SRCS := $(shell find $(SRC_PATH) -name *.c)
SRCS = uarttest.c
OBJS:=$(SRCS:%.c=./%.o)

#all target
all: $(Output)$(PRJ_NAME)

#tool invocations
$(Output)$(PRJ_NAME):$(OBJS)
	@echo 'Building target: $@'
	@echo 'Invoking:$(CC)'
	@echo 'src:$(SRCS)'
	$(CC) -static -o "$@" $(OBJS) $(LIBS)
	cp $(Output)$(PRJ_NAME) ../filesystem/rootfs/usr/
	../filesystem/mkramfs.sh ../filesystem/rootfs/
	mv  uramdisk.image.gz ../filesystem
	@echo 'Finished building target: $@'
	@echo ' '

#other targets
clean:
	find $(SRC_PATH) -name "*.d" -exec rm -rf {} \;
	find $(SRC_PATH) -name "*.o" -exec rm -rf {} \;
	rm $(Output)$(PRJ_NAME) 

.PHONY:all clean
.SECONDARY:


