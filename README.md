# Analysis_Instructions_forShubham
 Go to directory : /afs/cern.ch/work/d/dbhowmik/public/Analysis/MHgg/2017Analysis/CMSSW_9_4_6/src/MonoHiggsToGG/analysis/work/macros

check the path inside myrunAddWeightsAll.sh and run

./myrunAddWeightsAll.sh 41.529(lumi)

./myrunSkimAll.sh

Then go to ../../fits i.e. (analysis/fits) and run

./myformatNtupleForFitting_METcat.sh

cd /afs/cern.ch/work/d/dbhowmik/public/Analysis/MHgg/2017Analysis/Fit_DiPhotonTools/CMSSW_9_4_9/src/diphotons/Analysis/macros

cp -r /afs/cern.ch/work/d/dbhowmik/public/Analysis/MHgg/2017Analysis/CMSSW_9_4_6/src/MonoHiggsToGG/analysis/fits/ntuples4fit_pho_newSig_test_met0_met130 .

./combine_maker_MonoHgg.sh "ntuples4fit_pho_newSig_test_met0_met130" --lumi 41.529 --fit-name cic --mc-file Output_MC.root --fit-background --redo-input 1

./mycombineall_MonoHgg2HDMa.sh {INDIR} --hadd --model 2HDMa -C 0.9 -M AsymptoticLimits --run both

./mylimit_plots_MonoHgg.sh "ntuples4fit_pho_2HDMa_QCD_ma150_met0_met130_cic_default_shapes_lumi_41.529"
