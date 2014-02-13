=========================================================
MiSeq Amplicon Sequencing Sample Prep with Dual Barcoding
=========================================================

This protocol can take up to 96 samples, requiring a total of 22 different primers for each sample. A higher degree of multiplexing can be attained by adding additional outer primers.
For target-specific primers, see the primers protocol in this folder.

**1) Product amplification**

	A first PCR is performed using the primer constructs

	Illumina adapter - *forward primer*

		ACACTCTTTCCCTACACGACGCTCTTCCGATCT - *fwd_primer*

	and Illumina adapter - *reverse primer*

		AGACGTGTGCTCTTCCGATCT - *rev_primer*

	Optimization of the protocol may be required, but a starting point is 2.5 μL of each primer (10 μM), 1-10 ng of template DNA, 25 μL of Phusion Mastermix (ThermoScientific) and dH2O to a total volume of 50 μL.

	Cycling conditions are::

		Denaturation	98°C	30”
		Denaturation	98°C	10”	\
		Hybridization	***	30”	|- 20x
		Elongation	72°C	4”	/
		Elongation	72°C	2 min

	Hybridization conditions are primer-dependent, but should be similar to those used for the primers without adapters. Kapa HiFi polymerase (Kapa Biosystems) can be considered with the template is particularly refractory to amplification, following the instructions from the manufacturer.

**2) First Clean-up**

	A cleaning step must be performed to eliminate loose primers and eventual primer dimers or low molecular weight unspecific products. This can be achieved with magnetic beads, a spin column or a gel. If carrying out this procedure in SciLifeLab Stockholm, a CA-cleaning in the MBS is recommended. See “CA purification” protocol”.

**3) Attaching barcodes and adapters**

	A second PCR is conducted for attaching standard Illumina handles and index primers.

	Multiplex_fwd

		AATGATACGGCGACCACCGAGA{TCTACAC}-[F index]-ACACTCTTTCCCTACACGACG

	Multiplex_rev

		CAAGCAGAAGACGGCATACGAGAT-[R index]-GTGACTGGAGTTCAGACGTGTGCTCTTCCGATCT

	The curly brackets denote bases that will not be read in the sequencer. See notes at the bottom for multiplexing indexes combination guidelines.

	Each well should contain 20 μL of the clean PCR product above, 25 μL os Phusion Mastermix and 1.5 μL of each primer (10 μM).

	Cycling conditions are as follows::

		Denaturation	98°C	30”
		Denaturation	98°C	10”	\
		Hybridization	62°C	30”	|- 10x
		Elongation	72°C	****	/
		Elongation	72°C	2 min

Add one second to the elongation time used in the step above. Other, slower polymerases may require longer times, as well as different annealing temperatures.

**4) Second cleaning**

	Repeat step (2), twice if necessary. If using magnetic beads, adapt the bead amount for the larger amount of DNA now present. Beads will interfere with the downstream steps, so remove them first by placing the plate in a magnetic stand, leaving it undisturbed for at least 3 minutes and then transfering the reaction product to a fresh plate.

**5) Quantification**

	Quantify sample concentration and length. For concentration, a fluorometric measurement such as Qubit (Invitrogen) or PicoGreen (Invitrogen) should be preferred over an auto-fluorescence method such as NanoDrop (Thermo Scientific).

**6) Fragment length assessment**

	Measure the average fragment length. BioAnalyzer (Agilent) HS is recommended, but a simple agarose gel may suffice.

**7) Sample pooling**

	Pool all samples together for a total volume of at least 20 μL and a concentration of 2-10 nM / barcoded	template. The molarity of a sample can be calculated using the formula:

				Concentration*10 6 /656.6*Length

**8) Sequencing**

	Samples are now ready to be handled by facility personnel. Adding 5% of random DNA, such as PhiX, is recommended for improving amplicon sequencing in Illumina instruments.


Index Sequences
---------------
The following are the 20 standard Nextera Indexes. All of them can be used as forward or reverse primer, allowing for a 20*20=400 unique combinations. When placed in the in the Multiplex_rev primer, the barcode sequence should be reverse complemented, so that it will be read in the correct sense during sequencing.

+------------+------------+-----------+-----------+
|           i7            |          i5           |
+============+============+===========+===========+
|N701	     |ATTACTCG    |N501       |TATAGCCT   |
+------------+------------+-----------+-----------+
|N702        |TCCGGAGA    |N502       |ATAGAGGC   | 
+------------+------------+-----------+-----------+ 
|N703        |CGCTCATT    |N503       |CCTATCCT   |
+------------+------------+-----------+-----------+ 
|N704        |GAGATTCC    |N504       |GGCTCTGA   |
+------------+------------+-----------+-----------+ 
|N705        |ATTCAGAA    |N505       |AGGCGAAG   |
+------------+------------+-----------+-----------+ 
|N706        |GAATTCGT    |N506       |TAATCTTA   |
+------------+------------+-----------+-----------+ 
|N707        |CTGAAGCT    |N507       |CAGGACGT   |
+------------+------------+-----------+-----------+ 
|N708        |TAATGCGC    |N508       |GTACTGAC   |
+------------+------------+-----------+-----------+ 
|N709        |CGGCTATG    |			  | 
+------------+------------+			  +
|N710        |TCCGCGAA    |			  |
+------------+------------+			  +
|N711        |TCTCGCGC    |			  | 
+------------+------------+			  +
|N712        |AGCGATAG    |                       |
+------------+------------+-----------+-----------+ 

E.g.: 	Combining the following primers:

		F701 AATGATACGGCGACCACCGAGATCTACACTAGATCGCACACTCTTTCCCTACACGACG
		
		R501 CAAGCAGAAGACGGCATACGAGATAGGCTATAGTGACTGGAGTTCAGACGTGTGCTCTTCCGATCT
		
	Will produce Illumina reads with the barcode combination R501-F701, AGGCTATA-ATTACTCG



