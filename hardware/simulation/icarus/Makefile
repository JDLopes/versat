#paths
ROOT_DIR:=../../..
SUBMODULES_DIR:=$(ROOT_DIR)/submodules
MEM_DIR:=$(SUBMODULES_DIR)/mem
RTL_DIR:=$(ROOT_DIR)/hardware
TB_DIR := $(RTL_DIR)/testbench
INC_DIR := $(RTL_DIR)/include



#verilog sources
SRC := $(RTL_DIR)/src/*.v $(MEM_DIR)/tdp_ram/*.v $(MEM_DIR)/sp_ram/*.v $(MEM_DIR)/2p_mem/iob_2p_mem.v

# select testbench file
ifeq ($(CMDGOALS),)
CMDGOALS:=xversat
endif
TB:=$(TB_DIR)/$(CMDGOALS)_tb.v

#headers
INC:=$(INC_DIR)/*.vh

#icarus simulator and flags
VC := iverilog
CFLAGS := -W all -I$(INC_DIR) -g2005-sv -D DEBUG

#
#  VERSAT SIMULATION
#

all: $(SRC) $(INC) $(TB)
	$(VC) $(CFLAGS) $(SRC) $(TB)
	./a.out

#
# SUBMODULE TEST
#

#source files of each submodule test
xaddrgen_src := $(RTL_DIR)/src/xaddrgen.v
xaddrgen2_src := $(xaddrgen_src) $(RTL_DIR)/src/xaddrgen2.v
xalu_src := $(RTL_DIR)/src/xclz.v $(RTL_DIR)/src/xalu.v
xconf_reg_src := $(RTL_DIR)/src/xconf_reg.v
xconf_src := $(xconf_reg_src) $(RTL_DIR)/src/xconf_mem.v $(RTL_DIR)/src/xconf.v $(MEM_DIR)/sp_ram/*.v
xmem_src := $(RTL_DIR)/src/xinmux.v $(xaddrgen2_src) $(MEM_DIR)/tdp_ram/*.v $(RTL_DIR)/src/xmem.v
xdata_eng_src := $(xmem_src) $(xalu_src) $(xmul_pipe_src) $(RTL_DIR)/src/xalulite.v $(RTL_DIR)/src/xmul.v $(RTL_DIR)/src/xmuladd.v $(RTL_DIR)/src/xbs.v $(RTL_DIR)/src/xdata_eng.v

xaddrgen: $(INC)
	$(VC) $(CFLAGS) $($@_src) $(TB_DIR)/$@_tb.v
	./a.out

xaddrgen2: $(INC)
	$(VC) $(CFLAGS) $($@_src) $(TB_DIR)/$@_tb.v
	./a.out

xalu: $(INC)
	$(VC) $(CFLAGS) $(RTL_DIR)/src/xinmux.v $($@_src) $(TB_DIR)/$@_tb.v
	./a.out

xconf_reg: $(INC)
	$(VC) $(CFLAGS) $($@_src) $(TB_DIR)/$@_tb.v
	./a.out

xconf: $(INC)
	$(VC) $(CFLAGS) $($@_src) $(TB_DIR)/$@_tb.v
	./a.out

xmem: $(INC)
	$(VC) $(CFLAGS) $($@_src) $(TB_DIR)/$@_tb.v
	./a.out

xdata_eng: $(INC)
	$(VC) $(CFLAGS) $($@_src) $(TB_DIR)/$@_tb.v
	./a.out

# CLEANUP, ETC
clean:
	@rm -f *~ *# *.vcd a.out *.txt

.PHONY: all clean
