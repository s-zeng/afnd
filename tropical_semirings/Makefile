all: csc_alt_tab_tropical_semirings.pdf noted_csc_alt_tab_tropical_semirings.pdf

csc_alt_tab_tropical_semirings.pdf: csc_alt_tab_tropical_semirings.md title_image.png csc.png graph.dot.svg
	pandoc -t beamer --slide-level 2 -o $@ $<

noted_csc_alt_tab_tropical_semirings.pdf: csc_alt_tab_tropical_semirings.md title_image.png csc.png graph.dot.svg
	pandoc -t beamer --slide-level 2 -H preamble-notes.tex -o $@ $<

graph.dot.svg: graph.dot
	dot -Tsvg -O graph.dot

.PHONY: clean all

clean:
	rm -f csc_alt_tab_tropical_semirings.pdf noted_csc_alt_tab_tropical_semirings.pdf
