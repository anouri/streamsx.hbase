# Copyright (C) 2013-2014, International Business Machines Corporation  
# All Rights Reserved                                	                 

# NOTE: To compile, you must have HBASE_HOME and HBASE_HOME set in your
# environment.

.PHONY: all clean 

# Fill in HBASE_TOOLKIT location here.
STREAMS_HBASE_TOOLKIT ?= ../../com.ibm.streamsx.hbase

SPLC_FLAGS ?= -a --data-directory data 
SPLC = $(STREAMS_INSTALL)/bin/sc

SPL_CMD_ARGS ?= -t $(STREAMS_HBASE_TOOLKIT)
SPL_MAIN_COMPOSITE_CHECK = com.ibm.streamsx.hbase.sample::CheckAndDelete
SPL_MAIN_COMPOSITE_DELETE = com.ibm.streamsx.hbase.sample::DeleteDemo
SPL_MAIN_COMPOSITE_VERSIONDEL = com.ibm.streamsx.hbase.sample::DeleteAll

all: distributed

data:
	mkdir data


distributed: data
	$(SPLC) $(SPLC_FLAGS) -M $(SPL_MAIN_COMPOSITE_DELETE) $(SPL_CMD_ARGS) --output-dir output_delete
	$(SPLC) $(SPLC_FLAGS) -M $(SPL_MAIN_COMPOSITE_CHECK) $(SPL_CMD_ARGS) --output-dir output_check
	$(SPLC) $(SPLC_FLAGS) -M $(SPL_MAIN_COMPOSITE_VERSIONDEL) $(SPL_CMD_ARGS) --output-dir output_version

clean: 
	$(SPLC) $(SPLC_FLAGS) -C -M $(SPL_MAIN_COMPOSITE_DELETE) --output-dir output_delete
	$(SPLC) $(SPLC_FLAGS) -C -M $(SPL_MAIN_COMPOSITE_CHECK) --output-dir output_check
	$(SPLC) $(SPLC_FLAGS) -C -M $(SPL_MAIN_COMPOSITE_VERSIONDEL) $(SPL_CMD_ARGS) --output-dir output_version
	rm data/*.out

