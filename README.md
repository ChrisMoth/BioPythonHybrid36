# BioPythonHybrid36
PDB36Parser.py hacks PDBParser.py to read Hybrid36 PDB files.

MMCIF format is the official format of the RCSB, and very flexible compared to the rigid old column format of .pdb.  

However, some argue it is more difficult for human hand-editing.
An alternate solution for residue numbers > 9999 is offered by Hybrid36, which is somewhat supported in the UCSF ChimeraX (and legacy Chimera) applications

http://cci.lbl.gov/hybrid_36/

Hybrid36 is also used by the Modbase Team at UCSF, to handle large residue numbers  (examples include models of Human Gene TTN)

https://modbase.compbio.ucsf.edu/modbase-cgi/index.cgi

Here are 2 .py files:

1) hybrid36.py is imported by PDB36Parse.py and reformatted to more current Python3 standards.  It is identical to the deposition at http://cci.lbl.gov/hybrid_36/

2) PDB36Parser.py simply replaces int() conversions on the atom and residue columns to calls to hybrid36.py functions.  As BioPython evolves, you will likely 
want to update PDB36Parser.py.

To use PDB36Parser.py, you must have first installed the Biopython library, and you should test that the included PDBParser() 
module can load, and parse, a structure.

I recommend against replacing your PDBParser() calls.  Rather, fall back PDB36Parser when PDBParser fails.  Here is a sketch:

```from wherever import PDB36Parser
        tryParser36 = False

        try:
            structure = PDBParser().get_structure(structure_id,structure_filename)
        except ValueError:
            tryParser36 = True # We will make a last ditch effort to read as hybrid36 because of alpha in int columns

        if tryParser36: # Try hybrid36 format
            LOGGER.critical("ValueError with traditional parser - how trying hybrid36 parser on %s"%struct_filename)
            modbase_structure = PDB36Parser().get_structure(structure_id,structure_filename)
```



