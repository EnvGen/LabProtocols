=========================================================
MiSeq Amplicon Sequencing Sample Prep with Dual Barcoding
=========================================================

**Overview of the workflow:**

The workflow of MiSeq dual indexing library preparation involves the following steps: *Inner PCR*, *Clean-up#1*, *Outer PCR*, *Pre-pooling*, *Clean-up#2*, and *Final pooling*. 

The figure below illustrates the development of the amplicon’s structure in each main step. For the detailed description please see the following pages. 

.. image:: https://cloud.githubusercontent.com/assets/5807710/13554781/55a9442c-e3b1-11e5-8213-df93a6e55958.png
    :width: 360px
    :align: center
    :height: 280px
    :alt: alternate text

**Reagent mentioned in this workflow:**
    * KAPA HiFi HotStart ReadyMix (KAPA Biosystems); 
    * CA beads (Dynabeads® MyOneTM) or AMPure XP beads (Beckman Coulter);
    * EB buffer (Qiagen);
    * Qubit (Invitrogen); 
    * Quant-iT PicoGreen (Thermo Fisher) (Optional);
    * BSA (New England BioLabs) (optional).
 
**1) Inner PCR**

    This step is to amplify your region of interest from the genomic DNA. In order to prepare the amplicon for Illumina sequencing, amplicon primers are attached to Illumina adapters.

    The primers’ structures are:

    .. image:: https://cloud.githubusercontent.com/assets/5807710/13555410/2f26b2f8-e3c0-11e5-9366-f65643a3f67f.png
        :width: 300px
        :align: center
        :height: 50px
        :alt: alternate text

    PCR reaction mixture:

            Optimization of the protocol may be required, but a starting point is 

            10μL of KAPA HiFi HotStart ReadyMix (KAPA Biosystems)

            1μL of each primer (10μM)
    
            1-10ng of template DNA (2ng is suggested)
    
            DNA-free H2O 
    
            to make up a total volume of 20μL (KAPA ReadyMix is used in 2X) 

    Suggestions for 
    
            DNA sample preparation: dilute extracted samples to 1ng/μL. 
    
            PCR inhibition: depending on the type of environment/biome your samples were extracted from, inhibitors may exist and affect PCR performance. 1μL of BSA (10mg/mL) added to the 20μL PCR mixture may help reduce the problem. 

    PCR condition::
        
            Denaturation 	98C° 		2 min
            Denaturation 	98 C°	 	20 s 
            Annealing      	**C°	 	20 s
            Elongation     	72C°    	15 s 
            Final elongation    72C°	 	2 min

    Annealing conditions are primer-dependent but should be similar to those used for the primers without adapters. For elongation time, 15 s/kb should suffice. 20-25 cycles are suggested (maximum 30 cycles); the idea is to gain enough material with as low a cycle number as possible to avoid PCR biases and amplification errors. 2mol of amplicon product should be sufficient for the following procedure.
    
    (**NOTE**: Partial sequences of Illumina adapters from both primers are the same, which means they might anneal and elongate at room temperature, resulting in large amounts of primer dimers during PCR amplification.)    
    
    Approaches to solve this problem:
    
    Option 1: keep master mix of H2O, KAPA, both primers on ice and keep PCR mixture plate on ice block when loading samples.
    
    Option 2: load primers with multi-channel pipette after loading the KAPA mastermix and DNA template. Start PCR amplification within 5 mins.
    
    Here you can also find `16S and 18S rRNA primer sequences <https://github.com/EnvGen/LabProtocols/blob/master/Primer_sequences.rst>`_ and their `targeted phylums <https://github.com/huyue87/hello-world/files/160392/Primer_sequences_matched_RDP_database_Yue_2012Oct09.xlsx>`_ matching to RDP database.
    
    Annealing temperatures for commonly used primer pairs::

        16S 	341F - 805R          54C°
        16S 	341’F - 805R 	    54C°
        16S 	515’F - 805R 	    56C°
        16S 	515’F - 926’R 	    55.5C°
        18S 	574*F - 1132R	    50.4C°     

    **NOTE**:  515’F-926’R also targets the human genome. When studying the microbiota from human samples, it is better to avoid using this primer pairs.  
    
**2)	Clean-up#1**
    
    A cleaning step must be performed to remove loose primers, eventual primer dimers, or low molecular weight unspecific products. This can be achieved by using magnetic beads (e.g. CA beads from Dynabeads® MyOneTM or AMPure beads XP from Beckman Coulter), spin columns (Qiagen DNA purification kit), or gel. If carrying out this procedure in SciLifeLab Stockholm, a CA-cleaning in the MBS is recommended. 
    
    When using the MBS robot with CA beads for cleaning:

    Enter the following parameters to “CA-cleaning program” in the control panel of MBS:

        50uL sample, 20uL CA beads, 10min binding time, 100uL precipitation buffer, 15uL elution buffer. 

    Then follow the instruction from the program to fill in the reagents to a plate as:::

        1st row: 50uL sample (20uL amplicon sample from step1 + 30uL DNA free water)
        2th row: 90uL EB buffer (Qiagen)
        3rd row: 125uL precipitation buffer*
        4nd row: 220uL 80% ethanol (freshly made)
        5th row: 25uL CA beads 

    The precipitation buffer* is composed of PEG in 1.5 M NaCl and the concentration of PEG determines the length of fragments selected. A useful guideline is as follows:

    .. image:: https://cloud.githubusercontent.com/assets/5807710/13556305/cb71026a-e3d6-11e5-9b22-a77ed22f9022.png
        :width: 150px
        :align: center
        :height: 55px
        :alt: alternate text

    (**NOTE**: Only 20uL of CA beads will actually be used in the robot from the loaded 25uL beads. 20uL CA beads are capable to bind 1000ng of DNA. If the DNA you need cleaned exceeds this threshold, please either adjust the input amount of DNA sample to <900ng or increase the CA beads amount.)
    
    When the CA cleaning program in MBS finished, take out the washing plate and place it in a magnetic stand, leaving it undisturbed for at least 3 mins and then transfer the supernatant from the 8th row to a fresh strip/plate.

    (**NOTE**: After the beads clean-up step, all following work that analyzed with Bioanalyzer or Qubit , a magnetic stand is required to be placed beneath DNA sample when loading samples for such analysis, since tiny amount of beads can introduce unexpected result in Bioanalyzer or elevate reading in Qubit.)

**3)	Outer PCR** 

    This step is to barcode the cleaned amplicon product with dual indexes (attach indexes to both ends of the DNA fragment to be able to recognize the samples after sequencing multiple samples at the same time). The indexed PCR primers also contain the Illumina sequencing handles, which allow the barcoded DNA fragments to attach to the Illumina flowcell surface during sequencing. 

    .. image:: https://cloud.githubusercontent.com/assets/5807710/13555801/15f66706-e3ca-11e5-86a1-8dbd8843441f.png
            :width: 300px
            :align: center
            :height: 48px
            :alt: alternate text

    PCR reaction mixture: 

        12 μL of the cleaned PCR product from Clean-up#1 (no more than 5ng of the cleaned amplicon product is suggested)

        14 uL of KAPA ReadyMix (2X)

        1 uL of each primer (10uM).

    PCR condition::

        Denaturation 	 98C°	2 min
        Denaturation 	 98C°	20s
        Annealing 	 62C°	30s 
        Elongation 	 72C° 	30s
        Final elongation 72C°	2 min

    8-10 cycles are suggested for OuterPCR.

**4)	Pre-pooling and Clean-up#2**

    This step can be performed the same way as Clean-up1, which cleaning samples independently. However, since the OuterPCR step, in our experience, has good efficiency and produces fewer primer dimers, it is possible to combine samples prior to cleaning, as will be described below. Pre-pooling barcoded samples before Clean-up#2 does not affect the downstream workflow and effectively reduces the workload of the cleaning procedure. 

    **Pre-pooling:**

    	If you have only one type of amplicon (amplified with the same primer pair in InnerPCR) 
    		- Measure the DNA concentration of samples with Qubit 
    		- Pool barcoded amplicons at equal mass (for instance, pool barcoded amplicons from the same column in the plate at equal amounts)

        If you have more than one type of amplicon (amplified with different primer pairs in InnerPCR), pool each type of amplicon at equal mass.
    
        Suggested amount::
 
            High threshold:

            keep the pre-pooled samples under the threshold of the beads’ capacity in *Clean-up#2*

            Low thereshold: 

            each sample should be at least 5nM when doing pre-pooling, since *clean-up#2* will lose  around 50% of the materials.
        
    **Clean-up#2:**
        	Clean pre-pooled barcoded samples as in *Clean-up#1*. Remember to restrict the amplicon amount within the capacity of beads. This step is mandatory, since Illumina sequencing is rather sensitive to the presence of oligonucleotides, even at concentrations below the detection limit of the bioanalyzer.
    
**5)	Final pooling**

    Measure the concentration of cleaned pre-pooled products from *Clean-up#2* and pool all samples in equal molar amount for the final library for sequencing.


**Supplementary information:**

**1)	Calculating molar concentration::**
 
            Concentration * 10^6 / 656.6*Length
    
        Units of concentration and length: ng/uL and bp 

    For concentration, a fluorometric measurement such as Qubit (Invitrogen) or Quant-iT PicoGreen (Invitrogen) should be preferred over an auto-fluorescence method such as NanoDrop (Thermo Scientific). 
    For length measuring, Measure the DNA fragment length. BioAnalyzer (Agilent) is recommended, but a simple agarose gel may be sufficient.
    
    Sequencing in SciLifeLab, Qubit (dsDNA HS Assay kit) result and Bioanalyzer report are required when handing in library. The library concentration should be > 10nM.

**2)	Index sequences**

    The strategy of barcoding samples with dual indexes enables high-throughput sequencing on multiple samples in one run. Sample-specific combination of dual indexes enables recognizing various samples from the yielded large data set. Our primers in house allow 32*36 = 1152 combinations.  The following are the 32*36 indexes : 
    
    .. image:: https://cloud.githubusercontent.com/assets/5807710/13555999/d14b1dbc-e3cf-11e5-94c1-51401ea839f3.png
                :width: 350px
                :align: center
                :height: 450px
                :alt: alternate text
    
        
You can download the index sequences table in `excel <https://github.com/huyue87/hello-world/files/160388/index_primers_32_36.xlsx>`_  format.

For any issue about the dual index prep protocol, please contact luisa.hugerth@scilifelab.se or yue.hu@scilifelab.se 