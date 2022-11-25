all: csc_alt_tab_tropical_semirings.pdf noted_csc_alt_tab_tropical_semirings.pdf

csc_alt_tab_tropical_semirings.pdf: csc_alt_tab_tropical_semirings.md title_image.png csc.png
	pandoc -t beamer -o $@ $<

noted_csc_alt_tab_tropical_semirings.pdf: csc_alt_tab_tropical_semirings.md title_image.png csc.png
	pandoc -t beamer -H preamble-notes.tex -o $@ $<

.PHONY: clean all

clean:
	rm -f csc_alt_tab_tropical_semirings.pdf noted_csc_alt_tab_tropical_semirings.pdf
