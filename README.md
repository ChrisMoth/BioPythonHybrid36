# BioPythonHybrid36
PDB36Parser.py hacks  PDBParser.py to read Hybrid36 PDB files.

MMCIF format is the official format of the RCSB.  However, some argue it is more difficult for human hand-editing.
An alternate solution for residue numbers > 9999 is offered by Hybrid36, which is somewhat supported in the UCSF ChimeraX (and legacy Chimera) applications

http://cci.lbl.gov/hybrid_36/

Hybrid36 is also used by the Modbase Team at UCSF, to handle large residue numbers  (examples include models of Human Gene TTN)

https://modbase.compbio.ucsf.edu/modbase-cgi/index.cgi
