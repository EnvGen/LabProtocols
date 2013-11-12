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

		AATGATACGGCGACCACCGAGA{TCTACAC}-[i5 index]-ACACTCTTTCCCTACACGACG

	Multiplex_rev

		CAAGCAGAAGACGGCATACGAGAT-[i7 index]-GTGACTGGAGTTCAGACGTGTGCTCTTCCGATCT

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
The following are the 20 standard Nextera Indexes, which can be combined to form 96 unique combinations. Further multiplexing is possible by adding custom primets.

+------------+------------+-----------+-----------+
|           i7            |          i5           |
+============+============+===========+===========+
|N701	     |TAAGGCGA    |N501       |TAGATCGC   |
+------------+------------+-----------+-----------+
|N702        |CGTACTAG    |N502       |CTCTCTAT   | 
+------------+------------+-----------+-----------+ 
|N703        |AGGCAGAA    |N503       |TATCCTCT   |
+------------+------------+-----------+-----------+ 
|N704        |TCCTGAGC    |N504       |AGAGTAGA   |
+------------+------------+-----------+-----------+ 
|N705        |GGACTCCT    |N505       |GTAAGGAG   |
+------------+------------+-----------+-----------+ 
|N706        |TAGGCATG    |N506       |ACTGCATA   |
+------------+------------+-----------+-----------+ 
|N707        |CTCTCTAC    |N507       |AAGGAGTA   |
+------------+------------+-----------+-----------+ 
|N708        |CAGAGAGG    |N508       |CTAAGCCT   |
+------------+------------+-----------+-----------+ 
|N709        |GCTACGCT    |*NB!* the i7 barcodes  | 
+------------+------------+should be reverse      +
|N710        |CGAGGCTG    |complemented in the    |
+------------+------------+primers you order,     +
|N711        |AAGAGGCA    |to be read correctly   | 
+------------+------------+upon sequencing!       +
|N712        |GTAGAGGA    |                       |
+------------+------------+-----------+-----------+ 


Index Combinations
------------------
If running only a few samples, it is important to make sure that the sequencer detects signal in all channels. To do so, combine indexes as follows:

+------------+--------------------------------------------+---------------------------------+
|Plex        |i7                                          |i5                               |
+============+============================================+=================================+
|1   	     |Any                                         |                                 |
+------------+--------------------------------------------+                                 +
|2           |[option1] N701 + N702                       |                                 |
|            |[option2] N702 + N704                       |                                 |
+------------+--------------------------------------------+                                 +
|3           |[option1] N701 + N702 + N704                |                Any              |
|            |[option2] N703 + N705 + N706                |                                 |
+------------+--------------------------------------------+                                 +
|4-5         |[option1] N701 + N702 + N704 + any other    |                                 |
|            |[option2] N703 + N705 + N706 + any other    |                                 |
+------------+--------------------------------------------+                                 +
|6           |N701 + N702 + N703 + N704 + N705 + N706     |                                 |
+------------+--------------------------------------------+---------------------------------+
|7-12        |[option1] N701 + N702 + N704 + any other    |[option1] N501 + N502            |
|            |[option2] N703 + N705 + N706 + any other    |[option2] N503 + N504            |
|            |                                            |[option3] N505 + N506            | 
+------------+--------------------------------------------+---------------------------------+
|> 12        |N701 + N702 + N703 + N704 + N705 + N706 +   |[option1] N501 + N502 + any other|
|            |any other                                   |[option2] N503 + N504 + any other|
|            |                                            |[option3] N505 + N506 + any other| 
+------------+--------------------------------------------+---------------------------------+

