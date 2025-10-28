Polygenic Probability Risk Score (PPRS) SNP Weights

This repository contains the SNP weight files used for constructing polygenic risk scores (PRS) and polygenic probability risk scores (PPRS) for primary open-angle glaucoma (POAG) and related endophenotypes:
	•	Intraocular Pressure (IOP)
	•	Vertical Cup-to-Disc Ratio (VCDR)
	•	Retinal Nerve Fiber Layer Thickness (RNFL)

Two versions of the POAG SNP weights are provided:
	1.	POAG_withUKB — derived including UK Biobank samples.
	2.	POAG_noUKB — derived excluding UK Biobank samples.

Each SNP weight file was compressed and split due to GitHub’s file size limit (<25 MB per file).

⸻

📁 File Organization

Each phenotype’s SNP weights are split into four parts, for example:

POAG_withUKB.txt.zst.partaa
POAG_withUKB.txt.zst.partab
POAG_withUKB.txt.zst.partac
POAG_withUKB.txt.zst.partad

Other phenotypes follow the same naming convention:

POAG_noUKB.txt.zst.partaa ... partad
IOP.txt.zst.partaa ... partad
VCDR.txt.zst.partaa ... partad
RNFL.txt.zst.partaa ... partad

Each .zst file is a Zstandard-compressed flat text file containing three columns:

rsID   Effect_Allele   Weight


⸻

⚙️ How to Recombine and Decompress

1. Combine the split parts

Use the cat command in Linux or macOS to concatenate the parts into a single .zst file:

cat POAG_withUKB.txt.zst.part* > POAG_withUKB.txt.zst

Repeat for other phenotypes as needed (e.g., IOP.txt.zst.part*, VCDR.txt.zst.part*, etc.).

⸻

2. Decompress the .zst file

Use the unzstd command (part of the zstd package) to decompress:

unzstd POAG_withUKB.txt.zst

This will produce a flat text file named:

POAG_withUKB.txt


⸻

3. Verify the output

Each decompressed file should contain approximately 7.3 million SNPs with the following tab-delimited columns:

Column	Description
rsID	dbSNP identifier
Effect_Allele	Allele for which the weight applies
Weight	SNP effect weight used in PRS/PPRS construction


⸻

🧩 Example Workflow

Example (for POAG with UKB sample excluded):

# Combine split parts
cat POAG_noUKB.txt.zst.part* > POAG_noUKB.txt.zst

# Decompress
unzstd POAG_noUKB.txt.zst

# Inspect first few lines
head POAG_noUKB.txt


⸻

🧠 Notes
	•	Files were compressed using Zstandard (zstd) and split using the Linux split command.
	•	To install Zstandard (if not available):

sudo apt install zstd       # Ubuntu/Debian
brew install zstd           # macOS (Homebrew)


	•	To recombine on Windows, use PowerShell:

Get-Content POAG_withUKB.txt.zst.part* -Raw | Set-Content POAG_withUKB.txt.zst -Encoding Byte



⸻

📜 Citation

If you use these SNP weights, please cite the corresponding manuscript:

Gao X. et al. “Multi-Trait Polygenic Probability Risk Score Enhances Glaucoma Prediction Across Ancestries.” under review, 2025.

