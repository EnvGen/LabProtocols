=====================================
MiSeq Amplicon Sequencing Sample Prep
=====================================

This protocol can take up to 48 samples, requiring a different primer for each sample.

If preparing many sequences, consider using the dual indexing approach, where 20 primers allow you to prepare up to 96 samples.

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

	Multiplex_1.01

		AATGATACGGCGACCACCGAGATCTACACTCTTTCCCTACACGACGCTCTTCCGATCT

	Multiplex_2.01

		GTGACTGGAGTTCAGACGTGTGCTCTTCCGATCT

	Index_primer

		CAAGCAGAAGACGGCATACGAGAT - X6 - GTGACTGGAGTTC

	Each well should contain 20 μL of the clean PCR product above, 25 μL os Phusion Mastermix, 1 μL of each primer (10 μM) and 2 μL dH2O.

	Cycling conditions are as follows::

		Denaturation	98°C	30”
		Denaturation	98°C	10”	\
		Hybridization	62°C	30”	|- 10x
		Elongation	72°C	5”	/
		Elongation	72°C	2 min

**4) Second cleaning**

	Repeat step (2), twice if necessary. If using magnetic beads, adapt the bead amount for the larger amount of DNA now present. Beads will interfere with the downstream steps, so remove them first by placing the plate in a magnetic stand, leaving it undisturbed for at least 3 minutes and then transfering the reaction product to a fresh plate.

**5) Quantification**

	Quantify sample concentration and length. For concentration, a fluorometric measurement such as Qubit (Invitrogen) or PicoGreen (Invitrogen) should be preferred over an auto-fluorescence method such as NanoDrop (Thermo Scientific).

**6) Fragment length assessment**

	Measure the average fragment length. BioAnalyzer (Agilent) HS is recommended, but a simple agarose gel may suffice.

**7) Sample pooling**

	Pool all samples together for a total volume of at least 20 μL and a concentration of 10 nM / barcoded	template. The molarity of a sample can be calculated using the formula:

				(Concentration*10^6) / (656.6*Length)

**8) Sequencing**

	Samples are now ready to be handled by facility personnel. When using Illumina for amplicon sequencing, it is recommended to spike in 5% of random DNA, such as PhiX.


Index Sequences
---------------
The following are the 48 standard TruSeq Adapter indexes

=======  ========  =======  ========  =======  ========  =======  ========  
Index #  Sequence  Index #  Sequence  Index #  Sequence  Index #  Sequence
=======  ========  =======  ========  =======  ========  =======  ========  
  1      ATCACG      13     AGTCAA      25     ACTGAT      37     CGGAAT
  2      CGATGT      14     AGTTCC      26     ATGAGC      38     CTAGCT
  3      TTAGGC      15     ATGTCA      27     ATTCCT      39     CTATAC
  4   	 TGACCA      16     CCGTCC      28     CAAAAG      40     CTCAGA
  5      ACAGTG      17     GTAGAG      29     CAACTA      41     GACGAC
  6      GCCAAT      18     GTCCGC      30     CACCGG      42     TAATCG
  7      CAGATC      19     GTGAAA      31     CACGAT      43     TACAGC
  8      ACTTGA      20     GTGGCC      32     CACTCA      44     TATAAT
  9      GATCAG      21     GTTTCG      33     CAGGCG      45     TCATTC
 10      TAGCTT      22     CGTACG      34     CATGGC      46     TCCCGA
 11      GGCTAC      23     GAGTGG      35     CATTTT      47     TCGAAG
 12      CTTGTA      24     GGTAGC      36     CCAACA      48     TCGGCA
=======  ========  =======  ========  =======  ========  =======  ========

