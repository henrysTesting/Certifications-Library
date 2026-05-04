Prerequisites 
-----------------
You need to download Obsidian
Obsidian Clipper is highly recommended, but not needed.


CERTIFICATIONS VAULT
====================

An Obsidian vault where Claude maintains a study wiki for professional certifications.
You source the material. Claude does the bookkeeping.


STRUCTURE
---------
raw/            Drop source files here (notes, PDFs, articles). One subfolder per cert.
wiki/           Claude-maintained wiki. One subfolder per cert.
index.md        Catalog of all wiki pages.
log.md          History of every ingest and operation.
CLAUDE.md       Vault schema — tells Claude how everything works.


SLASH COMMANDS
--------------
/ingest <CERT-ID/file.md>   Process a source file into the wiki.
/query <question>           Answer a question using the wiki.
/lint                       Health-check the wiki for broken links and gaps.
/new-cert <CERT-ID>         Scaffold the structure for a new certification.


CURRENT CERTS
-------------
NCA-GENL    NVIDIA Certified Associate: Generative AI LLMs


ADDING A NEW CERT
-----------------
1. Run /new-cert <CERT-ID>
2. Drop your source files into raw/<CERT-ID>/
3. Run /ingest <CERT-ID>/<file>

