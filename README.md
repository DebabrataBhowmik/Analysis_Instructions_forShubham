# Analysis_Instructions_forShubham

At first copy 2017 nTuples from my eos area to your area(either at eos or wherever you want to keep them): 

cp -r /eos/user/d/dbhowmik/Analysis/nTuple_2017_EOY Location_of_your_area

Either make a new area or do it in your CMSSW_10_6_8 area 

go to CMSSW_10_6_8/src/MonoHiggsToGG/analysis/work/macros

cp /afs/cern.ch/work/d/dbhowmik/public/Analysis/MHgg/2017Analysis/CMSSW_9_4_6/src/MonoHiggsToGG/analysis/work/macros/* . 

cd CMSSW_10_6_8/src/MonoHiggsToGG/analysis/work/scripts

cp /afs/cern.ch/work/d/dbhowmik/public/Analysis/MHgg/2017Analysis/CMSSW_9_4_6/src/MonoHiggsToGG/analysis/work/scripts/* . 

cd CMSSW_10_6_8/src/MonoHiggsToGG/analysis/fits

cp -r /afs/cern.ch/work/d/dbhowmik/public/Analysis/MHgg/2017Analysis/CMSSW_9_4_6/src/MonoHiggsToGG/analysis/fits/2017_2HDMa_EOY/ .

Go to directory : CMSSW_10_6_8/src/MonoHiggsToGG/analysis/work/macros

check the path inside myrunAddWeightsAll_EOY.sh and run

./myrunAddWeightsAll_EOY.sh 41.529(lumi)

hadd nTuple_GJet_EOY.root nTuple_GJet_Pt*.root 

hadd nTuple_QCD_EOY.root nTuple_QCD_Pt*.root 

open myrunSkimAll_2HDMa_testModCuts_EOY.sh;  check input output paths

In Line 16 change skim_testModCuts_combinedMETtest.C to skim_testModCuts.C 

./myrunSkimAll_2HDMa_testModCuts_EOY.sh

Then go to /CMSSW_10_6_8/src/MonoHiggsToGG/analysis/fits/2017_2HDMa_EOY/LowMET  and run

./myformatNtupleForFitting_METcat.sh


Then try to see if this works

cmsrel CMSSW_9_4_9

cd CMSSW_9_4_9/src

cp -r /afs/cern.ch/work/d/dbhowmik/public/Analysis/MHgg/2017Analysis/Fit_DiPhotonTools/CMSSW_9_4_9/src/* .

cmsenv

scram b

cd CMSSW_9_4_9/src/diphotons/Analysis/macros/2017_2HDMa_EOY/LowMET

cp -r CMSSW_10_6_8/src/MonoHiggsToGG/analysis/fits/2017_2HDMa_EOY/LowMET/ntuples4fit_pho_newSig_test_met50_met130 .

./combine_maker_MonoHgg.sh "ntuples4fit_pho_newSig_test_met50_met130" --lumi 41.529 --fit-name cic --mc-file Output_MC.root --fit-background --redo-input 1

./mycombineall_MonoHgg2HDMa.sh "ntuples4fit_pho_newSig_test_met50_met130_cic_default_shapes_lumi_41.529" --hadd --model 2HDMa -C 0.9 -M AsymptoticLimits --run both

./mylimit_plots_MonoHgg.sh "ntuples4fit_pho_newSig_test_met50_met130_cic_default_shapes_lumi_41.529"
