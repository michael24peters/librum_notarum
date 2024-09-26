---
tags:
  - permanent
  - analysis
created: 2024-06-17 14:51
date: 2024-06-17
moc:
---
# 202406171451 Getting MC data for η -> μ+ μ- γ

 Here is the path to the MC data through Bookkeeping: 

```path
MC/2018/39112230/Beam6500GeV-2018-MagDown-Nu1.6-25ns-Pythia8/Sim09i/Trig0x617d18a4/Reco18/Turbo05-WithTurcal/Stripping34NoPrescalingFlagged/ALLSTREAMS.DST
```

Which needs to be converted into an XML catalog (according to the [starterkit](https://lhcb.github.io/starterkit-lessons/first-analysis-steps/files-from-grid.html)):

```sh
lb-dirac dirac-bookkeeping-genXMLCatalog --Options=MC_2018_39112230_Beam6500GeV-2018-MagDown-Nu1.6-25ns-Pythia8_Sim09i_Trig0x617d18a4_Reco18_Turbo05-WithTurcal_Stripping34NoPrescalingFlagged_ALLSTREAMS.DST.py --Catalog=myCatalog.xml
```

But it should probably look more like this (if you download this from DIRAC Bookkeeping):

```sh
lb-dirac dirac-bookkeeping-genXMLCatalog --Options=MC_2018_39112230_Beam6500GeV2018MagDownNu1.625nsPythia8_Sim09i_Trig0x617d18a4_Reco18_Turbo05WithTurcal_Stripping34NoPrescalingFlagged_ALLSTREAMS.DST.py --Catalog=myCatalog.xml
```

When I do this (the second one), I get the following error: 

```error
Error getting the list of PFNs: Failed to access some of requested input data
```

This issue is caused by the first two files for η -> μ μ γ being corrupted. 

with this accompanying `summary.xml` file:

```xml
<?xml version="1.0" encoding="UTF-8"?>

<summary xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" version="1.0" xsi:noNamespaceSchemaLocation="$XMLSUMMARYBASEROOT/xml/XMLSummary.xsd">

<success>True</success>

<step>finalize</step>

<usage>

<stat unit="KB" useOf="MemoryMaximum">2177748.0</stat>

</usage>

<input>

<file GUID="925C9E9C-AE06-E811-B99B-001E67792508" name="PFN:00070793_00000001_7.AllStreams.dst" status="part">100</file>

</input>

<output />

<counters>

<counter name="AllStreams_PsAndVsUnpack/# Unpacked FlavourTags">1</counter>

<counter name="AllStreams_PsAndVsUnpack/# Unpacked MuonPIDs">0</counter>

<counter name="AllStreams_PsAndVsUnpack/# Unpacked Particles">573</counter>

<counter name="AllStreams_PsAndVsUnpack/# Unpacked ProtoParticles">3</counter>

<counter name="AllStreams_PsAndVsUnpack/# Unpacked RecVertices">12</counter>

<counter name="AllStreams_PsAndVsUnpack/# Unpacked RichPIDs">0</counter>

<counter name="AllStreams_PsAndVsUnpack/# Unpacked Tracks">3</counter>

<counter name="AllStreams_PsAndVsUnpack/# Unpacked Vertices">216</counter>

<counter name="unpackFittedVeloTracks/# Unpacked Tracks">7010</counter>

<counter name="EcalCovar/#Clusters from 'Rec/Calo/EcalClusters'">9567</counter>

<counter name="ChargedProtoPAddMuon/Rec/Muon/MuonPID ==&gt; Rec/ProtoP/Charged">4598</counter>

<counter name="ChargedProtoPAddRich/Rec/Rich/PIDs ==&gt; Rec/ProtoP/Charged">4598</counter>

<counter name="ChargedProtoPCombDLL/CombineDLL ==&gt; Rec/ProtoP/Charged">4598</counter>

<counter name="UnpackMuonPIDs/# UnPackedData">2958</counter>

<counter name="UnpackTrack/# Unpacked Tracks">14444</counter>

<counter name="UnpackRichPIDs/# UnPackedData">4275</counter>

<counter name="SplitClustersRec/Rec/Calo/EcalClusters=&gt;Rec/Calo/EcalSplitClusters">318</counter>

<counter name="UnpackMuonTracks/# Unpacked Tracks">376</counter>

<counter name="CounterSummarySvc/handled">101</counter>

</counters>

<lumiCounters />

</summary>
```

Once you get the catalog of XML files desired, add this

```python
from Gaudi.Configuration import FileCatalog
FileCatalog().Catalogs = [ "xmlcatalog_file:/path/to/myCatalog.xml" ]
```

to your options file. See the [bookkeeping twiki](https://twiki.cern.ch/twiki/bin/view/LHCb/LHCbDiracBKCLI).

Alternatively, you can just add one of the .dst files:

```sh
lb-dirac dirac-dms-get-file LFN:/lhcb/MC/2018/ALLSTREAMS.DST/00111368/0000/00111368_00000001_7.AllStreams.dst
```

When I do this, I get the following error:

```error
Downloading file to .
Trying to download https://eosctalhcb.cern.ch:8444/eos/ctalhcb/archive/grid/lhcb/archive/lhcb/MC/2018/ALLSTREAMS.DST/00111368/0000/00111368_00000001_7.AllStreams.dst to /afs/cern.ch/user/p/petersm/private/00111368_00000001_7.AllStreams.dst
Trying to download root://x509up_u169732@eosctalhcb.cern.ch//eos/ctalhcb/archive/grid/lhcb/archive/lhcb/MC/2018/ALLSTREAMS.DST/00111368/0000/00111368_00000001_7.AllStreams.dst to /afs/cern.ch/user/p/petersm/private/00111368_00000001_7.AllStreams.dst
Failed : 
    /lhcb/MC/2018/ALLSTREAMS.DST/00111368/0000/00111368_00000001_7.AllStreams.dst : GError('DESTINATION CHECKSUM MISMATCH Source checksum and destination checksum do not match: 0e51213c != 00000001', 5) GError('Failed to stat file (Invalid exchange)', 52)
```

**Solution**: This issue is caused by the first two files for η -> μ μ γ being corrupted. The reason the first two files do not work is unknown.

---
# References


