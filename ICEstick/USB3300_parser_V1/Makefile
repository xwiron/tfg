FNAME := USB3300_parser

all: sim sint

sim: $(FNAME)_tb.vcd

sint: $(FNAME).bin

$(FNAME)_tb.vcd: $(FNAME).v $(FNAME)_tb.v

	iverilog $^ -o $(FNAME)_tb.out

	./$(FNAME)_tb.out

	#gtkwave $@ &

$(FNAME).bin: $(FNAME).v $(FNAME).pcf

	yosys -p "synth_ice40 -blif $(FNAME).blif" $(FNAME).v

	arachne-pnr -d 1k -p $(FNAME).pcf $(FNAME).blif -o $(FNAME).txt

	icepack $(FNAME).txt $(FNAME).bin

prog: sint

	iceprog $(FNAME).bin

clean:
	rm -f *.bin *.txt *.blif *.out *.vcd *~
