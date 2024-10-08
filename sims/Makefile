all : expansion.lineages.mp4 pme_expansion.lineages.mp4

.PRECIOUS : %.trees

%.trees : %.slim
	slim $<

%.lineages.mp4 : %.trees
	lineage_plotting/animate_lineages.py $< -n 5 -p 1 -s 123 -t 1 -x 20

include ../rules.mk
