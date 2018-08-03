# chime5
download URL for the ASR transcripts and the lattices

# Single_Array and Multiple_Array Tasks
Please find the corresponding lattices and transcriptions in each folder.
Single_A: only reference microphone is used
Multiple_A: all Kinects' microphones are used for channel selection.

# Notes
1: In each folder, you will find two dirs for system combination, e.g., 'Single_A/decode_dev_ref_CH2_180' and 'Single_A/decode_dev_ref_ENH_180',
the final ASR score is obtained using MBR combination for these two outputs, and the commands referred to Kaldi script /egs/wsj/local/score_combine.sh

2: some minor changes to /egs/wsj/local/score_combine.sh:

$cmd LMWT=$min_lmwt:$max_lmwt $odir/log/combine_lats.LMWT.log \
       	lattice-combine --inv-acoustic-scale=LMWT ${lats[@]} ark:- \| \
    	lattice-add-penalty --word-ins-penalty=$wip ark:- ark:- \| \
    	lattice-mbr-decode --word-symbol-table=$symtab \
	ark:- ark,t:- \| \
        utils/int2sym.pl -f 2- $symtab \| \
        $hyp_filtering_cmd '>' $odir/scoring_kaldi/penalty_$wip/LMWT.txt || exit 1;


3: we have submitted the final transcriptions of Eval. to chimechallenge@gmail.com 


If any questions, please feel free to contact me: Feifei Xiong @ SPandH, University of Sheffield
f.xiong@sheffield.ac.uk




