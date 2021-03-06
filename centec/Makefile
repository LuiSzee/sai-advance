ifeq ($(targetbase),linux)
include $(MK_DIR)/sys.mk

OBJ_DIR=$(OBJ_BASE_DIR)/sai

LIB = sai
SRCS = $(shell find src/ -name "*.c")
ifeq ($(PLATFORM),ctc)
SRCS += $(shell find platform/mgt -name "*.c")
SRCS += $(shell find platform/driver/macled_handle -name "*.c")
SRCS += $(shell find platform/driver/i2c_handle -name "*.c")
SRCS += $(shell find platform/driver/fiber_handle -name "*.c")
endif
#SRCS = $(shell find dbclient/ -name "*.c")

ifeq ($(findstring goldengate, $(CHIPNAME)),goldengate)
CPPFLAGS += -DGOLDENGATE
endif

ifeq ($(findstring duet2, $(CHIPNAME)),duet2)
CPPFLAGS += -DDUET2
endif

ifeq ($(findstring tsingma, $(CHIPNAME)),tsingma)
CPPFLAGS += -DTSINGMA
endif

ifeq ($(findstring tsingma_mx, $(CHIPNAME)),tsingma_mx)
CPPFLAGS += -DTSINGMA_MX
#for TMMX note
CPPFLAGS += -DSAI_ON_TMMX
endif

CPPFLAGS += -I$(SAI_SDK_DIR)/dal/include
CPPFLAGS += -I$(SAI_SDK_DIR)/sal/include
CPPFLAGS += -I$(SAI_SDK_DIR)/dkits/
CPPFLAGS += -I$(SAI_SDK_DIR)/core/
CPPFLAGS += -I$(SAI_SDK_DIR)/core/app
CPPFLAGS += -I$(SAI_SDK_DIR)/core/init
CPPFLAGS += -I$(SAI_SDK_DIR)/core/common/include
CPPFLAGS += -I$(SAI_SDK_DIR)/core/api/include
CPPFLAGS += -I$(SAI_DIR)/inc
CPPFLAGS += -I$(SAI_DIR)/centec/inc
ifeq ($(PLATFORM),ctc)
CPPFLAGS += -I$(SAI_DIR)/centec/platform/mgt
CPPFLAGS += -I$(SAI_DIR)/centec/platform/inc
CPPFLAGS += -I$(SAI_DIR)/centec/platform/driver/macled_handle
CPPFLAGS += -I$(SAI_DIR)/centec/platform/driver/i2c_handle
CPPFLAGS += -I$(SAI_DIR)/centec/platform/driver/fiber_handle
endif

ifeq ($(ARCH),arm64)
CPPFLAGS += -Wno-unused
endif

CPPFLAGS += -O0 -Wall -Werror -g2 -ggdb

include $(MK_DIR)/lib.mk

CFLAGS += -O -Werror -Wall
endif

ifeq ($(targetbase),vxworks)

OBJ_DIR=$(OBJ_BASE_DIR)/sal

all_targets = src libsal

all: $(all_targets) FORCE
clean: $(addprefix clean_,$(all_targets)) FORCE

src: FORCE
	make -C $(SDK_DIR)/sal/src -f Makefile.vx

clean_src: FORCE
	make -C $(SDK_DIR)/sal/src -f Makefile.vx clean

libsal: FORCE
	make -f Makefile_libsal.vx

clean_libsal: FORCE
	make -f Makefile_libsal.vx clean

.PHONY: FORCE
FORCE:
endif
