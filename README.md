## Setup

Once you are in the cmslpc cluster or lxplus, run the following.
```
export SCRAM_ARCH=el9_amd64_gcc12
cmsrel CMSSW_13_3_1
cd CMSSW_13_3_1/src
cmsenv
```
For the following step you should have a ssh key associated to your GitHub account. For more information, see [connecting-to-github-with-ssh-key.](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
```
git clone -b master git@github.com:ctdax/SpikedRHadronAnalysis.git SpikedRHadronAnalysis
```

## plugins/SpikedRHadronAnalyzer.cc

SpikedRHadronAnalyzer.cc analyzes AOD level root files containing two R-Hadrons per event. It can be run using the command
```
cmsRun test/SpikedRHadronAnalyzer_cfg.py
```

## R-Hadron Gun

test/RHadronGun_cfg.py takes a custom input file for the available R-Hadron processes and outputs an AOD root file with 10 events. It can be run with the following command
```
cmsRun test/RHadronGun_cfg.py inputFiles=<INPUT_FILE> outputFile=<OUTPUT_FILE>
```
Alternatively, plugins/runRHadronGun.sh was built to run the RHadronGun over all process files in data/IndividualRHadronProcesses. If you would like to do this, use the command
```
./plugins/runRHadronGun.sh
```

## Information I found helpful when learning CMSSW

### CMSSW Directory Format

If this is your first time using or seeing a CMSSW directory I highly recommend you checkout [this brief presentation](https://www.hep.ph.ic.ac.uk/~dbauer/cms/tutorial_2011.pdf) and also [this twiki](https://twiki.cern.ch/twiki/bin/view/CMSPublic/WorkBookChapter4#SampleCode), particularly section 4.1.2 'Writing your own EDAnalyzer' of the twiki. Ultimately you should be able to run the analyzer smoothly inside of either directory via the command
```
cmsRun python/config_cfg.py
```

### AOD Contents

The SimCaloHitAnalyzer currently analyzes an AOD gluino root file which is present in config_cfg.py. The contents of the AOD file can either be observed in a TBrowser
```
root -l file:/uscms_data/d2/tadams/hscp/fall22a/CMSSW_10_6_30/src/EXO-RunIISummer20UL18GENSIM-00010-v3.root
TBrowser b("Events")
```
or by using edmDump
```
edmDumpEventContent file:/uscms_data/d2/tadams/hscp/fall22a/CMSSW_10_6_30/src/EXO-RunIISummer20UL18GENSIM-00010-v3.root
```
