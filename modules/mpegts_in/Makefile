include ../../config.mak

vpath %.c $(SRC_PATH)/modules/mpegts_in

CFLAGS= $(OPTFLAGS) -w -I"$(SRC_PATH)/include"


ifeq ($(DEBUGBUILD), yes)
CFLAGS+=-g -DDEBUG
LDFLAGS+=-g
endif

ifeq ($(GPROFBUILD), yes)
CFLAGS+=-pg
LDFLAGS+=-pg
endif

ifeq ($(LINUX_DVB), yes)
CFLAGS+=-DGPAC_HAS_LINUX_DVB
endif

#common obj
OBJS=mpegts_in.o

SRCS := $(OBJS:.o=.c) 

LIB=gm_mpegts_in.$(DYN_LIB_SUFFIX)
ifeq ($(CONFIG_WIN32),yes)
#LDFLAGS+=-export-symbols mpegts_in.def 
endif

all: $(LIB)


$(LIB): $(OBJS)
	$(CC) $(SHFLAGS) $(LDFLAGS) -o ../../bin/gcc/$@ $(OBJS) $(EXTRALIBS) -L../../bin/gcc -lgpac
ifeq ($(STATICBUILD),yes)
	$(CC) $(SHFLAGS) $(LDFLAGS) -o ../../bin/gcc/gm_mpegts_in-static.so $(OBJS) $(EXTRALIBS) -L../../bin/gcc -lgpac_static -lz
endif


%.o: %.c
	$(CC) $(CFLAGS) -c -o $@ $< 


clean: 
	rm -f $(OBJS) ../../bin/gcc/$(LIB)

dep: depend

depend:
	rm -f .depend	
	$(CC) -MM $(CFLAGS) $(SRCS) 1>.depend

distclean: clean
	rm -f Makefile.bak .depend



# include dependency files if they exist
#
ifneq ($(wildcard .depend),)
include .depend
endif
