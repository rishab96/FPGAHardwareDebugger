NAME=tmp_sub_mtest
PNR=arachne-pnr

DEVICE = 1k
PCF = $(NAME).pcf

QUIET = -q

all: $(NAME).bin

%.bin: %.txt
	icepack $< $@

%.txt: %.blif
	$(PNR) $(QUIET) -d $(DEVICE) --post-place-blif $*.place.blif -o $@ -p $(PCF) $< 

%.blif: %.v
	yosys $(QUIET) -p 'synth_ice40 -top main -blif $@' $< receiver_helper.v transmitter_helper.v

upload: $(NAME).bin
	iceprog $<

explain: $(NAME).txt
	icebox_explain $<

clean:
	rm -f *.bin *.txt *.blif *.rpt


.PRECIOUS: %.bin %.txt %.blif 

.PHONY: all explain install clean
